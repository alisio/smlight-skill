# Devices and integrations

Identify the exact model and hardware revision in the manufacturer's documentation before advising on power, network features, radios, or firmware. The catalog and capabilities change; do not extrapolate from one model to another.

- The SLZB-06 family includes models with one Zigbee/Thread radio; MR models have two radios and can operate separate networks simultaneously. Confirm the actual hardware and firmware combination.
- U-series models add features on supported hardware; USB host, OTBR, and Bluetooth depend on the model and firmware. SLZB-07 is a USB product line: do not assume it has a web interface or runs SLZB-OS.
- Zigbee and Thread on one radio with multiprotocol firmware is not the same as two networks on separate radios; check current Home Assistant and manufacturer recommendations.
- In external coordinator mode, Zigbee2MQTT or ZHA manages the network through the radio. In integrated Zigbee Hub mode, the stack runs on SLZB-OS and can integrate through MQTT. These architectures have different backup and migration procedures.
- For Thread, distinguish RCP with an external OTBR from OTBR running on the device. Confirm support, version, and network requirements before configuration.
- For ZHA or Zigbee2MQTT, consult the integration documentation and the device configuration generator when available. Use the interface, port, protocol, and driver that match the radio and firmware; avoid simultaneous clients on the same radio.
- For the integrated Zigbee Hub, check its [supported-device list](https://github.com/smlight-tech/slzb-os-zigbee-hub/tree/main/devices_support) and [Berry ZCN converter manual](https://smlight.tech/support/manuals/books/slzb-os/page/berry-zcn-system-manual) for the exact device and installed version. Zigbee2MQTT support does not establish Hub support, or vice versa.
- For ESPHome on SLZB hardware, identify the exact model and hardware revision before selecting the corresponding configuration in the [SMLIGHT ESPHome repository](https://github.com/smlight-tech/slzb-esphome). ESPHome, SLZB-OS, and radio firmware are separate; verify features and recovery for the installed combination.

Sources: [SMLIGHT manuals](https://smlight.tech/support/manuals/), [Zigbee Hub](https://smlight.tech/support/manuals/books/slzb-os/chapter/zigbee-hub), [Zigbee2MQTT](https://www.zigbee2mqtt.io/), and [Home Assistant](https://www.home-assistant.io/integrations/zha/).
