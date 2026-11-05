# SMLIGHT Skill

A reusable agent skill for configuring, operating, integrating, and troubleshooting SMLIGHT SLZB devices, their radios, and SLZB-OS, including Berry scripts and SLZB-OS apps. Capabilities vary by model, firmware, and operating mode; consult the applicable official documentation.

## Installation

Copy `SKILL.md` and the `reference/` directory together into a directory named `smlight` in the client's skills location. Check whether the destination already exists and preserve local changes. Consult the client's version-specific documentation to confirm the supported location and whether reloading is needed.

| Client | Typical user-level directory |
| --- | --- |
| OpenCode | `~/.config/opencode/skills/smlight` |
| Claude Code | `~/.claude/skills/smlight` |
| Codex | `~/.agents/skills/smlight` |

## Usage

In OpenCode, invoke the skill explicitly by mentioning `@smlight`, then describe the task and provide the model, firmware version, mode, and integration when available. For example:

> `@smlight` Explain how to troubleshoot my SLZB coordinator without changing its configuration.

To confirm it loaded, check the conversation for a `skill` tool call with the ID `smlight` and the skill instructions added to the context. A skill appearing as available does not mean its full instructions have been loaded. Other clients may use different invocation and confirmation steps; consult their documentation.

## Updating

Installed copies are independent. Compare `SKILL.md` and `reference/` with the installed copy before updating, and preserve local modifications. Copying files does not remove obsolete references.

## Sources

- [SMLIGHT manuals](https://smlight.tech/support/manuals/)
- [Zigbee Hub manual](https://smlight.tech/support/manuals/books/slzb-os/chapter/zigbee-hub)
- [SLZB-OS MQTT API](https://smlight.tech/support/manuals/books/slzb-os/page/mqtt-api)
- [SMLIGHT ESPHome](https://github.com/smlight-tech/slzb-esphome)
- [SLZB-OS Berry scripting](https://github.com/smlight-tech/slzb-os-scripts)
- [SLZB-OS apps](https://github.com/smlight-tech/slzb-os-apps)
- [Zigbee Hub devices](https://github.com/smlight-tech/slzb-os-zigbee-hub)
- [pysmlight](https://github.com/smlight-tech/pysmlight)
- [SMLIGHT CC flasher](https://github.com/smlight-tech/smlight-cc-flasher) and [CC web tools](https://github.com/smlight-tech/smlight-cc-web-tools)
