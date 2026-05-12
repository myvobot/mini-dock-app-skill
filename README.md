# mini dock skill

A generic Codex/Claude-style skill for building and reviewing **mini dock** MicroPython apps.

This repository contains the skill instructions. Device setup, SDK behavior, Thonny usage, app lifecycle, and resource-path rules belong to the official VOBOT documentation and are linked below instead of being duplicated here.

## Skill Guide

- Skill introduction and examples: [docs/skill-introduction.md](docs/skill-introduction.md)
- Main skill file: [SKILL.md](SKILL.md)
- Test prompts: [tests/prompts.md](tests/prompts.md)

## Repository Structure

```text
mini_dock/
|-- SKILL.md
|-- README.md
|-- agents/
|   `-- openai.yaml
|-- docs/
|   `-- skill-introduction.md
|-- references/
|   |-- app-structure-and-deployment.md
|   |-- ble-nus.md
|   |-- hardware-and-peripherals.md
|   `-- ui-and-input.md
`-- tests/
    `-- prompts.md
```

## Official mini dock References

- VOBOT developer getting started: https://dock.myvobot.com/developer/getting_started/
- Important resource path configuration: https://dock.myvobot.com/developer/getting_started/#important-resource-file-path-configuration
- Thonny download: https://thonny.org/
- Application architecture: https://dock.myvobot.com/developer/guides/application-architecture/
- Button events: https://dock.myvobot.com/developer/guides/button-event/
- Interface guide: https://dock.myvobot.com/developer/guides/app-interface-guide/
- Peripherals reference: https://dock.myvobot.com/developer/reference/peripherals/

## Install

For Codex:

```bash
ln -s "/path/to/mini_dock" "$HOME/.codex/skills/mini-dock"
```

For Claude Code:

```bash
ln -s "/path/to/mini_dock" "$HOME/.claude/skills/mini-dock"
```

PowerShell example:

```powershell
New-Item -ItemType Junction -Path "$env:USERPROFILE\.codex\skills\mini-dock" -Target "C:\path\to\mini_dock"
```

Restart or reload the app after installing.

## Use

```text
Use $mini-dock to build a generic mini dock app.
```

```text
Use $mini-dock to create a BLE NUS control app for mini dock.
```

```text
Use $mini-dock to review my mini dock app structure and resource paths.
```

## Scope

This skill is device-focused and app-neutral. It covers mini dock app structure, LVGL UI, input handling, SDK peripherals, GPIO safety policy, BLE NUS patterns, and deployment guidance. It does not assume compatibility with any single companion app or protocol.
