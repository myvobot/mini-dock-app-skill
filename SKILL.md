---
name: dock-mini-app-skill
description: Use this skill when building, modifying, reviewing, or debugging generic VOBOT D1 / Vobot Mini Dock MicroPython apps, LVGL user interfaces, device input handling, resource paths, Thonny deployment, hardware peripheral use, GPIO/pin-safety decisions, or BLE Nordic UART Service workflows. This skill is device-focused and should not assume compatibility with any single companion app.
---

# Dock Mini App Skill

## Purpose

Build VOBOT D1 / Vobot Mini Dock apps that are portable across use cases. Prefer verified device and SDK behavior, keep app-specific protocols configurable, and call out anything that is inferred or unverified.

## Default Workflow

1. Identify the target: UI app, hardware/peripheral app, BLE app, diagnostic, or existing-app repair.
2. Confirm only the missing critical inputs: app name, required hardware features, whether BLE/networking is needed, and whether assets are required.
3. Generate a copyable app folder using `__init__.py` as the entrypoint.
4. Use lifecycle hooks (`on_start`, `on_stop`, and optional foreground/background hooks) for setup, periodic work, and cleanup.
5. Keep resource paths derived from `NAME`, never from the local folder name.
6. Include concise deployment and debugging steps unless the user asks for code only.

## App Rules

- Entry file: `__init__.py`.
- Required app property: `NAME = "App Name"`.
- Optional icon: `ICON = f"A:apps/{NAME}/resources/icon.png"` when an icon exists.
- Put bundled files under `resources/`.
- Build resource paths as `f"A:apps/{NAME}/resources/..."`.
- Keep installed app size in mind; the official architecture reference notes small app storage limits.
- Do not generate `main.py` as the D1 app entrypoint.
- Do not delete the device `/apps` directory when uninstalling; delete only the target app folder.

## UI And Input

Use LVGL for screens. For simple UI, create one `lv.obj()` screen, attach labels or controls, then `lv.scr_load(scr)`.

When user input matters, use LVGL key events and symbolic constants (`lv.KEY.LEFT`, `lv.KEY.RIGHT`, `lv.KEY.ENTER`, `lv.KEY.ESC`) rather than hard-coding numeric key codes unless diagnosing low-level behavior.

Read `references/ui-and-input.md` when building layouts, fonts, button/encoder flows, approval screens, menus, or screen-size adaptive UI.

## Hardware And Pins

Prefer the official `peripherals` SDK modules for built-in hardware: screen brightness/resolution, buzzer, LED clock, and ambient light. Acquire and release controllable peripherals when the SDK requires it.

For raw GPIO or physical pin work, do not invent a VOBOT D1 pinout. Treat physical pin mappings as hardware-revision-specific unless the user provides a schematic, board photo, or tested REPL output. Generate a diagnostic script when needed.

Read `references/hardware-and-peripherals.md` before using built-in peripherals, raw GPIO, physical connectors, or pin definitions.

## BLE NUS

BLE support is generic Nordic UART Service guidance for VOBOT D1 MicroPython apps. Do not bake in a companion app name, product identity, or approval protocol unless the user requests it.

Default BLE principles:
- Use configurable device name and protocol fields.
- Use standard NUS UUIDs unless the user asks for a custom service.
- Prefer newline-delimited UTF-8 JSON for interoperable command/response flows.
- Keep advertising payloads small; let centrals discover services through GATT after connecting.
- Avoid claiming BLE OTA, file upload, retransmission, or throughput results unless separately verified.

Read `references/ble-nus.md` before generating BLE advertising, GATT service registration, RX/TX, JSON protocol, or BLE debugging code.

## Deployment

Default handoff order:
1. Directory tree.
2. File contents or patch summary.
3. Upload path: copy the app folder into device `/apps`.
4. Restart: press `Ctrl+D` in Thonny after upload/delete.
5. Debugging: inspect Thonny logs and device-side errors.

Read `references/app-structure-and-deployment.md` for the full deployment checklist, lifecycle details, and resource-path rules.

## Errors To Avoid

- Tying generic BLE output to a specific app such as "Claude D1 Buddy" unless requested.
- Treating observed numeric key codes as the public API when LVGL symbolic constants are available.
- Re-registering BLE GATT services repeatedly during app re-entry.
- Calling `ble.active(False)` in normal app stop without considering re-entry behavior.
- Using desktop paths or temporary folder names for assets.
- Guessing physical GPIO mappings from unrelated D1 Mini / ESP8266 boards.

