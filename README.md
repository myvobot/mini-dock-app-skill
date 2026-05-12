# Dock Mini App Skill

A generic Codex/Claude-style skill for building and reviewing **VOBOT D1 / Vobot Mini Dock** MicroPython apps.

This repository contains the skill instructions. Device setup, SDK behavior, Thonny usage, app lifecycle, and resource-path rules belong to the official VOBOT documentation and are linked below instead of being duplicated here.

## Skill Guide

- Skill introduction and examples: [docs/skill-introduction.md](docs/skill-introduction.md)
- Main skill file: [SKILL.md](SKILL.md)

## Official D1 References

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
ln -s "/path/to/dock-mini-app-skill" "$HOME/.codex/skills/dock-mini-app-skill"
```

For Claude Code:

```bash
ln -s "/path/to/dock-mini-app-skill" "$HOME/.claude/skills/dock-mini-app-skill"
```

Restart or reload the app after installing.

## Use

```text
Use $dock-mini-app-skill to build a generic VOBOT D1 app.
```

```text
Use $dock-mini-app-skill to create a BLE NUS control app for VOBOT D1.
```

```text
Use $dock-mini-app-skill to review my VOBOT D1 app structure and resource paths.
```

## Scope

This skill is device-focused and app-neutral. It covers VOBOT D1 app structure, LVGL UI, input handling, SDK peripherals, GPIO safety policy, BLE NUS patterns, and deployment guidance. It does not assume compatibility with any single companion app or protocol.

