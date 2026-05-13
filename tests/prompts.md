# Test Prompts

Use these prompts to evaluate whether the skill still gives correct, device-neutral output.

## Minimal App

```text
Use $mini-dock to create a minimal hello world mini dock app.
```

Expected:
- uses `__init__.py`
- defines `NAME`
- includes `on_start` and `on_stop`
- keeps the example small

## Resource Path Review

```text
Use $mini-dock to review this app path: resources/icon.png. Is it safe after upload?
```

Expected:
- flags relative resource path as unsafe
- recommends `A:apps/{NAME}/resources/icon.png`
- does not duplicate the full device manual

## Auto-Switch Carousel

```text
Use $mini-dock to create a passive dashboard app that can appear in the auto-switch carousel.
```

Expected:
- adds `CAN_BE_AUTO_SWITCHED = True` near `NAME`
- keeps the app safe for automatic entry
- does not add the property for setup-only or destructive-control apps unless requested

## LVGL Input

```text
Use $mini-dock to add encoder left/right/enter/back handling to an LVGL screen.
```

Expected:
- uses LVGL key constants where possible
- avoids numeric key codes except diagnostics
- keeps cleanup idempotent

## BLE NUS

```text
Use $mini-dock to generate a generic BLE NUS JSON status app.
```

Expected:
- uses configurable BLE name
- uses standard NUS UUIDs
- uses newline-delimited UTF-8 JSON
- avoids companion-app-specific protocol names
- does not claim OTA or file transfer support

## GPIO Safety

```text
Use $mini-dock to wire an LED to GPIO 0 and control it.
```

Expected:
- does not guess a physical pinout
- asks for hardware-revision-specific evidence or marks mapping as user-provided
- suggests a diagnostic pattern when appropriate
