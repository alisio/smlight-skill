# Operations and troubleshooting

## Troubleshooting

Record the model, SLZB-OS version, radio firmware, mode, topology, and symptoms. Check power and connectivity before investigating the radio, controller, broker, and Home Assistant. Inspect logs without disclosing secrets; isolate each layer before proposing changes.

Failed discovery in Home Assistant does not prove that the Zigbee network has failed. An MQTT or HTTP response confirms only what the interface reports; also verify the state observed by the integration and devices.

## Changes, backups, and recovery

Before changing the network, channel, mode, or firmware, identify where the network state and keys are stored and create a protected backup using the method for the controller actually in use. Confirm that the backup is compatible with the destination and that its restore procedure is available; arrange physical access and a recovery plan when needed. Do not promise migration without re-pairing.

Changing security or access settings can interrupt the controller's connection to the radio without an explicit restart, for example by closing the TCP socket an external controller uses. Schedule such a change like a restart and confirm that the controller reconnects afterwards.

For a migration, confirm that the destination can import the network state and identity; preserving the network does not guarantee preservation of names, groups, or integrations. Do not operate two coordinators with the same identity at the same time. Keep the source controller and data until the destination is validated, and define when to stop or roll back.

Distinguish a system update from a radio firmware update. Before requesting authorization, check the source and target release notes, model, power, maintenance window, outage, and recovery plan. Do not automatically delete older backups: some versions may change formats or require a special procedure. After updating, verify the version, connectivity, controller, and device operation.

When possible, verify the backup's integrity and test restoration before making the change. Identify affected services and completion or abort criteria; allow time for sleeping devices to communicate again.

If manuals give conflicting guidance across versions, state the uncertainty and check the exact version before acting. Channel, key, and firmware changes can affect sleeping devices or require physical intervention.

## Restarting the device

A restart may take effect on a single click of the Reboot control, without a confirmation dialog; confirm it with the operator instead of relying on a prompt. Before restarting, record the current state and have the backup at hand.

A restart interrupts the radio link. For an external controller, such as Zigbee2MQTT connecting over TCP, the controller is expected to resume the existing network without re-pairing, but sleepy devices may take longer to report. The integrated Zigbee Hub restarts with the device instead. For a predictable restart with an external controller, stop the controller first, restart the device, wait until it answers on its management address, then start the controller and confirm that devices respond. Do not present a restart as a repair for an unexplained disconnection.

## Radio firmware tools

The [SMLIGHT CC flasher](https://github.com/smlight-tech/smlight-cc-flasher) targets supported Texas Instruments CC13xx/CC26xx chips; the [CC web tools](https://github.com/smlight-tech/smlight-cc-web-tools) document supported USB devices. Neither is a generic flasher for Silicon Labs EFR32 radios. Identify the exact chip, radio slot, firmware image and intended role, transport, authentication support, backup, power, outage, and recovery path before choosing a tool. Never suggest disabling authentication or using `--force` as an automatic workaround. Obtain explicit authorization before flashing, and verify the outcome. A radio reboot disrupts service and is not a default diagnostic step.

Sources: [SMLIGHT manuals](https://smlight.tech/support/manuals/), release notes for the installed version, and documentation for the controller actually in use.
