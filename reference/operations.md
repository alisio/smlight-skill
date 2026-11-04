# Operations and troubleshooting

## Troubleshooting

Record the model, SLZB-OS version, radio firmware, mode, topology, and symptoms. Check power and connectivity before investigating the radio, controller, broker, and Home Assistant. Inspect logs without disclosing secrets; isolate each layer before proposing changes.

Failed discovery in Home Assistant does not prove that the Zigbee network has failed. An MQTT or HTTP response confirms only what the interface reports; also verify the state observed by the integration and devices.

## Changes, backups, and recovery

Before changing the network, channel, mode, or firmware, identify where the network state and keys are stored and create a protected backup using the method for the controller actually in use. Confirm that the backup is compatible with the destination and that its restore procedure is available; arrange physical access and a recovery plan when needed. Do not promise migration without re-pairing.

For a migration, confirm that the destination can import the network state and identity; preserving the network does not guarantee preservation of names, groups, or integrations. Do not operate two coordinators with the same identity at the same time. Keep the source controller and data until the destination is validated, and define when to stop or roll back.

Distinguish a system update from a radio firmware update. Before requesting authorization, check the source and target release notes, model, power, maintenance window, outage, and recovery plan. Do not automatically delete older backups: some versions may change formats or require a special procedure. After updating, verify the version, connectivity, controller, and device operation.

When possible, verify the backup's integrity and test restoration before making the change. Identify affected services and completion or abort criteria; allow time for sleeping devices to communicate again.

If manuals give conflicting guidance across versions, state the uncertainty and check the exact version before acting. Channel, key, and firmware changes can affect sleeping devices or require physical intervention.

Sources: [SMLIGHT manuals](https://smlight.tech/support/manuals/), release notes for the installed version, and documentation for the controller actually in use.
