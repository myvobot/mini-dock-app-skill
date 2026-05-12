# App Structure And Deployment

Use this reference for VOBOT D1 / Vobot Mini Dock app layout, lifecycle, upload, restart, and resource-path decisions.

Sources:
- Official getting started: https://dock.myvobot.com/developer/getting_started/
- Official application architecture: https://dock.myvobot.com/developer/guides/application-architecture/
- Official application design: https://dock.myvobot.com/developer/guides/app-design/

## Minimum App Contract

The system scans `/apps`; each subfolder is treated as an app candidate.

Minimum structure:

```text
your_app/
├── __init__.py
└── resources/
```

Publishing-oriented apps may also include `manifest.yml`, `app/`, and `settings/`, but a minimal local app can be just `__init__.py` plus optional resources.

Minimum `__init__.py`:

```python
NAME = "Minimum App"
ICON = ""

async def on_start():
    print("on start")

async def on_stop():
    print("on stop")
```

Useful lifecycle hooks:
- `on_start`: initialize features and UI.
- `on_stop`: deactivate features, stop timers, release SDK peripherals, and clean UI.
- `on_running_foreground`: called while active; the official example describes roughly every 200 ms.
- `on_running_background`: called less often while paused/stopped.
- `on_boot`, `on_create`, `on_pause`, `on_resume`, `on_destroy`: use only when the app needs those phases.

## Resource Paths

The platform can rename the app folder to match `NAME`. Therefore resource references must use the app name, not the local folder.

Correct:

```python
NAME = "Clock Face"
ICON = f"A:apps/{NAME}/resources/icon.png"
BACKGROUND = f"A:apps/{NAME}/resources/background.png"
```

Avoid:
- `resources/icon.png`
- `/Users/.../icon.png`
- `A:apps/local-temp-folder/resources/icon.png`

## Upload

1. Enable Developer Mode on the device.
2. Power-cycle or reconnect power so Developer Mode takes effect.
3. Connect by USB-C data cable.
4. Open Thonny and select the ESP32 port.
5. Open `View > Files`.
6. Upload the complete app folder into device `/apps`.
7. Press `Ctrl+D` after upload or delete.

## Debugging Checklist

- Developer Mode enabled and power-cycled.
- Correct ESP32 port selected in Thonny.
- App folder is under `/apps`, not nested one level too deep.
- Entry file is `__init__.py`.
- `NAME` is defined.
- Asset paths use `A:apps/{NAME}/resources/...`.
- Thonny log is checked for device-side stack traces.
- Large apps respect small device storage limits.

