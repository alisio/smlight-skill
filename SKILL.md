---
name: smlight
description: Use when working with SMLIGHT SLZB devices, SLZB-OS, Zigbee or Thread coordinators, Home Assistant, ZHA or Zigbee2MQTT integration, configuration, troubleshooting, or firmware.
---

# SMLIGHT

Use the official documentation for the exact model, hardware, firmware, and installed version. Features, interfaces, and procedures differ across products and versions; do not assume every SMLIGHT device runs SLZB-OS.

## Workflow

1. Identify the model and hardware revision, system and radio firmware, operating mode, connection, and integration. Ask for missing details when they change the answer.
2. Read the relevant reference and confirm details in the official documentation for the installed version. Distinguish the SLZB-OS integrated Zigbee Hub from a radio managed by external Zigbee2MQTT or ZHA; identify where the network state and backups are stored.
3. Diagnose by layer: power and network, SLZB-OS, radio, Zigbee or Thread controller, MQTT, and Home Assistant. Prefer read-only checks and protect passwords, tokens, network keys, and backups.
4. Before changing settings, restarting, migrating, updating, or restoring, explain the target, impact, possible outage, backup, and recovery plan; obtain explicit confirmation. Verify the result afterward. Do not assume firmware downgrade or network migration is supported.

| Task | Reference |
| --- | --- |
| Models, radios, modes, Zigbee, Thread, and Home Assistant | [Devices and integrations](reference/devices.md) |
| Web interface, MQTT, automation, and Ansible | [Management and automation](reference/management.md) |
| Troubleshooting, backups, recovery, and firmware | [Operations and troubleshooting](reference/operations.md) |

## Safety notes

- Do not let multiple clients control the same radio at the same time; confirm the topology before connecting another controller.
- Network, radio, channel, or Zigbee identity changes can interrupt access or require migration; verify the procedure for the exact scenario.
- Distinguish SLZB-OS firmware, radio firmware, and ESPHome; updating one does not update the others.
- Do not invent endpoints or parameters, or treat the web interface's internal API as a stable contract. If the installed version has no documented method, state the limitation.

Sources: [SMLIGHT manuals](https://smlight.tech/support/manuals/), [Zigbee Hub manual](https://smlight.tech/support/manuals/books/slzb-os/chapter/zigbee-hub), [MQTT API](https://smlight.tech/support/manuals/books/slzb-os/page/mqtt-api), and [SMLIGHT ESPHome](https://github.com/smlight-tech/slzb-esphome).
