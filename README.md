# SMLIGHT Skill

A reusable agent skill for configuring, operating, integrating, and troubleshooting SMLIGHT devices and SLZB-OS. Capabilities vary by model, firmware, and operating mode; consult the applicable official documentation.

## Installation

Copy `SKILL.md` and the `reference/` directory together into a directory named `smlight` in the client's skills location. Check whether the destination already exists and preserve local changes. Consult the client's version-specific documentation to confirm the supported location and whether reloading is needed.

| Client | Typical user-level directory |
| --- | --- |
| OpenCode | `~/.config/opencode/skills/smlight` |
| Claude Code | `~/.claude/skills/smlight` |
| Codex | `~/.agents/skills/smlight` |

## Usage

For example, ask the agent: “Use the smlight skill to troubleshoot my SLZB coordinator without changing its configuration.” Provide the model, version, mode, and integration when available. Confirm that the client loaded the skill; availability does not guarantee automatic invocation.

## Updating

Installed copies are independent. Compare `SKILL.md` and `reference/` with the installed copy before updating, and preserve local modifications. Copying files does not remove obsolete references.

## Sources

- [SMLIGHT manuals](https://smlight.tech/support/manuals/)
- [Zigbee Hub manual](https://smlight.tech/support/manuals/books/slzb-os/chapter/zigbee-hub)
- [SLZB-OS MQTT API](https://smlight.tech/support/manuals/books/slzb-os/page/mqtt-api)
- [SMLIGHT ESPHome](https://github.com/smlight-tech/slzb-esphome)
