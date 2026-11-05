# Berry scripting and SLZB-OS apps

## Compatibility and lifecycle

SLZB-OS can run Berry scripts locally. Before suggesting a script or app, identify the exact device and hardware revision, installed SLZB-OS and radio firmware, operating mode, radio slot, and integration. Ask for missing details when they affect compatibility. Check each module, function, and app against the [module reference](https://github.com/smlight-tech/slzb-os-scripts#module-reference) and [app catalog documentation](https://github.com/smlight-tech/slzb-os-apps): firmware floors, development builds, hardware and mode requirements differ. For example, `ZB` base functions are documented from v2.8.0, `ZHB` from v2.9.6, and Berry `MQTT` from v3.2.4; specific functions can require later versions.

Apps require supported ESP32-S3 hardware according to the app repository. An absent or empty `models` field does not prove support on a non-U device: check platform, installed firmware and mode as well as the manifest. Do not infer capability from a different model.

The [getting-started guide](https://github.com/smlight-tech/slzb-os-scripts/blob/main/docs/getting-started.md) describes script metadata and event execution. `#META {"start":1}` requests autostart, while `start:0` is manual. Prefer a manual test before enabling autostart. Keep callbacks short: blocking or slow handlers can interfere with other work and Zigbee connections. Do not place delays or infinite loops in callbacks. A `ZB.on_pkt` return value of `true` can suppress forwarding on supported CC2652x radios; check radio and firmware-specific documentation. Direct radio access and socket suspension can disrupt traffic. An accepted script or app is not evidence that its automation works.

## Apps and permissions

Inspect the app source, manifest, firmware floor, compatible models, permissions, and recovery procedure before recommending installation. In the [app manifest](https://github.com/smlight-tech/slzb-os-apps#metajson), `events` grants access to coordinator SSE events, `api` grants raw API access, `fs.system` allows system-wide filesystem access, `bytecode` permits unvalidated compiled Berry code, and `thread.cli` allows Thread CLI control including access to the network key. These require trust; do not treat the sandbox as an absolute security guarantee. Check app-specific lifecycle and data deletion behavior before removal; apps can start at boot or restart after failure.

Explain the destination, effect, outage, backup, and recovery; obtain explicit confirmation before installing, running, enabling autostart, restarting, or removing scripts or apps. Preserve secrets and avoid logging network keys or credentials. Check execution state and relevant logs after authorized changes. Do not use repeated reboot as a default fix.

## Berry MQTT

The [Berry MQTT module](https://github.com/smlight-tech/slzb-os-scripts/blob/main/docs/modules/mqtt.md) is a scripting interface, distinct from the general SLZB-OS MQTT API, Zigbee Hub MQTT API, and Zigbee2MQTT topics. Its `publish` and `subscribe` use the configured base topic; `publishCustom` and `subscribeCustom` use the supplied topic without that prefix. On broker reconnection, subscriptions may need to be registered again. Check firmware support: the documented `getState` and `on_state_change` functions are available from v3.4.3.dev2, not necessarily on older versions. Do not assume subscription persistence or callback availability.

## Documentation and uncertainty

Use the [Berry scripting repository](https://github.com/smlight-tech/slzb-os-scripts) for module signatures and [examples](https://github.com/smlight-tech/slzb-os-scripts/tree/main/examples); check the documentation for the installed firmware rather than assuming `main` matches it. If an example and the API reference disagree, surface the conflict and confirm the signature for that version before suggesting code. Do not present documentation-only examples as device-tested.
