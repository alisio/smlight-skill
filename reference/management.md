# Management and automation

## Choosing an interface

Check the version-specific manual for supported options, such as the web interface, MQTT, metrics, events, or other documented interfaces. The Zigbee Hub MQTT API and the general SLZB-OS MQTT API are not interchangeable; confirm the version, mode, topics, and authentication before use. The supplied documentation places the general MQTT API at version 3.2.4 and later, but specific features may require newer versions.

The web interface's internal API is not a stable public contract. If an operation has no documented interface for the installed version, state that and suggest an available official procedure; do not guess endpoints, parameters, or return semantics.

Restrict management access to a trusted network and protect credentials and keys. Confirm that the version supports TLS before transmitting secrets; if it does not, consider an appropriate secure tunnel instead of exposing the interface directly to the internet.

Check whether the web interface password is enabled and enable it when it is missing. Browser sign-in and API authentication can be separate flows: a client that authenticates successfully against the API may still land on the login page in a browser, and the form may require both a user name and a password. Confirm both for the installed version instead of assuming one covers the other. Enabling or changing the password is itself a security change; see [operations and troubleshooting](operations.md) for its effect on the controller link.

## Reverse-engineered web interface (observation, not a contract)

The following was observed on an SLZB-06p7U running SLZB-OS 3.4.5.dev0. It comes from inspecting the web interface, not from manufacturer documentation, and it is not a stable public contract. Re-verify it on the installed firmware before relying on it; treat a mismatch as a reason to stop and re-read the interface, not to adjust values by trial.

- Reads come from `GET /api2?action=0&page=<pageId>`. The configuration is returned in the `respValuesArr` response header as JSON, not in the page body. Servers send the name in camel case, but HTTP clients may normalize header names to lower case; match it case-insensitively.
- Writes go to `POST /settings/saveParams` as `application/x-www-form-urlencoded`, carrying `pageId` plus the form fields of that page. An unchecked checkbox is sent as `off`, not omitted. A request without `pageId` returns HTTP 500. The response lists the fields that changed and whether a reboot is required; it does not prove the value was applied, so read the page again.
- Whether a field left out of the write is preserved or cleared was not verified. Send the whole form for the page, filling every field that other settings depend on with the value just read, so a write that changes one field cannot silently reset another. Treat omission as untested behavior, not as "leave it as is". The same applies to credential fields the automation is not meant to handle: keeping them out of the write is reasonable, but say that the field is then unverified rather than claiming it is untouched.
- Some select fields invert key and value in the read: the serial baud rate appears as `"115200": true` with no `baud` field. Those values cannot be compared, so resend them whenever the page is written.
- `/ha_info` is the documented identification endpoint and reports model, system firmware, hardware revision, radio type, and radio firmware. Confirm model and firmware version there before writing anything, and refuse to write on a version the mapping was not verified against.

Pages observed: 1 radio mode and Wi-Fi bridge, 2 Ethernet and Wi-Fi networking, 3 serial port, 4 security and access point, 6 telemetry, 7 automatic update, 8 LEDs and night mode, 9 NTP, 10 remote syslog, 24 SLZB-OS MQTT. Page identifiers belong to the firmware, not to the model, and may shift between versions.

- Commands go to `GET /api2?action=4&cmd=<n>` (`action=4` is `API_CMD`). Numbers taken from the pysmlight library (`pysmlight/const.py`, `class Commands`; sent by `CmdWrapper.set_cmd` in `pysmlight/web.py`): `0` router reconnect, `1` radio restart, `2` radio bootloader, `3` full device reset (ESP reboot). An optional `idx:<n>` parameter selects the radio. `cmd=3` reboots the device exactly like the web Reboot control: confirm with the operator first and keep it out of automated sequences.
- `GET /api2?action=5` returns the recent device log as plain text; useful for reading boot, network, and socket events without the web interface. Device logs may include network and configuration details: inspect them without disclosing secrets, and confirm whether this endpoint requires authentication on the installed version.
- Page 10 is the remote syslog page: `syslogEn` (checkbox, sent as `on`/`off`), `syslogIp`, and the port field. Enabling it is not enough. In one observation on the firmware above, the syslog client started at boot only: after a successful write (page read back `syslogEn=true`), the device emitted nothing for over 20 minutes while its own log showed activity, and messages began arriving right after `action=4&cmd=3`. Treat a reboot as part of the change and confirm it with the operator first. Point `syslogIp` only at a trusted, protected destination; the device sends these lines in clear text.
- In the same observation, the reboot's effect on an external Zigbee2MQTT controller was: the TCP link to the coordinator port dropped (`ECONNRESET`), Zigbee2MQTT reconnected on its own within a few seconds without re-pairing, and `/ha_info` answered again after about 6 s. The link returned on a new local port, so comparing the socket before and after is not a valid check of a clean recovery. The reconnection behavior itself is described in [operations and troubleshooting](operations.md).
- In that session, syslog lines left with the SLZB-OS local time but were stamped as if UTC; read the timestamp as device-local time.
- Page 7 is the automatic-update page. The update channel is the `fw_ch` field: `0` any, `1` release, `2` dev — the same mapping the pysmlight library encodes in `SEL_FW_CHANNEL` (`pysmlight/const.py`), whose `set_fw_channel` posts `pageId=7` with `fw_ch` plus an extra `ha` flag that the page form did not require. The channel chooses which builds an update check offers; it neither changes nor describes the installed build, so a device can run a development build while its channel is `any`. Selecting release on such a device changes nothing at first, but makes a stable build the candidate — possibly older than the installed one — so read the offered version before applying an update, because that would be a downgrade. The page also holds the scheduled-check fields (`enabled`, `chkHour`, `chkInterval`); send them back as read so a channel change does not alter the schedule.

## Python

[pysmlight](https://github.com/smlight-tech/pysmlight) describes itself as a Python library for SLZB-06 network coordinators; its code includes authentication, reads, commands, settings, and firmware actions. Check model compatibility, the installed library and firmware versions, and their supported operations before use; do not assume support for other models. Its use of web interfaces does not make those interfaces stable public contracts. Prefer reads, protect credentials and transport, obtain explicit confirmation for changes, and verify the resulting state without assuming idempotency.

For Berry MQTT scripts and reconnection behavior, see [scripting and apps](scripting.md).

## Ansible automation

Ansible is one automation option, not a requirement. First identify the documented management method and where the modules will run; do not assume SSH access to the device. Compare actual and desired state when the interface allows it, store secrets with an appropriate mechanism, and keep them out of logs. Explicitly state any idempotency, check-mode, and recovery limitations that cannot be verified.

Obtain confirmation before applying changes and test first in an isolated environment or on an authorized device. After applying a change, read the state again when possible; an accepted request does not prove that the change worked.

Without a reliable state read, do not claim idempotency or post-change verification. Ansible check mode alone does not guarantee that an API has no side effects.

When model support, the interface, or a state read is still unconfirmed, collect the missing data before writing a playbook or a custom module. Do not fill unknown values with plausible-looking placeholders and present the result as complete. If a sketch helps the conversation, mark it non-executable, keep unknown values visibly unresolved, and do not ship insecure defaults such as credentials over unencrypted HTTP.

Read-only discovery comes first: confirm reachability, the management port, and the identification data the unit reports for the installed firmware, then decide whether the remaining operations are documented. Identification data alone does not prove that a library or module supports the model.

Source: [Manufacturer MQTT API](https://smlight.tech/support/manuals/books/slzb-os/page/mqtt-api) and the official documentation for the installed version.
