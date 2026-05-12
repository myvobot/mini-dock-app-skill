# Hardware And Peripherals

Use this reference for built-in hardware, SDK peripherals, connector/pin caution, and raw GPIO decisions.

Sources:
- Official peripherals reference: https://dock.myvobot.com/developer/reference/peripherals/
- Official device reference: https://dock.myvobot.com/developer/reference/system/
- Official settings reference: https://dock.myvobot.com/developer/reference/settings/
- Official product intro/spec: https://dock.myvobot.com/

## Device Facts

Publicly documented hardware facts:
- device family: VOBOT D1 / Vobot Mini Dock
- screen: 2 inch, 320x240, 16M colors
- ports include USB-C, USB 3.0, HDMI, and Ethernet
- Python app development is supported through the Mini Dock SDK and MicroPython/LVGL

Use `device` when available:

```python
import device

dev_id = device.id
dev_model = device.model
hardware_version = device.version.hardware
firmware_version = device.version.firmware
nightstand = device.in_nightstand_mode()
```

Use `settings` for system preferences:

```python
import settings

use_celsius = settings.temp_unit() == 1
use_24h = settings.hour24()
```

## Built-In Peripherals

Prefer SDK modules over raw pins for built-in hardware.

### Screen

```python
import peripherals

resolution = peripherals.screen.screen_resolution
brightness = peripherals.screen.brightness()
peripherals.screen.brightness(50)
```

### Buzzer

```python
import peripherals

if peripherals.buzzer.acquire():
    peripherals.buzzer.set_freq(400)
    peripherals.buzzer.set_volume(50)
    peripherals.buzzer.set_volume(0)
    peripherals.buzzer.release()
```

Frequency range from official reference: 100 to 8000. Volume range: 0 to 100.

### LED Clock

```python
import peripherals

if peripherals.led_clock.acquire():
    peripherals.led_clock.set_display(1, 0x7F)
    peripherals.led_clock.brightness(80)
    peripherals.led_clock.release()
```

Groups 1-4 are digit segments, group 5 covers weekdays/PM, and group 6 covers symbols.

### Ambient Light

```python
import peripherals

if peripherals.ambient_light.acquire():
    count = peripherals.ambient_light.count
    peripherals.ambient_light.set_color([(255, 0, 0)], True)
    peripherals.ambient_light.brightness(80)
    peripherals.ambient_light.release()
```

## Physical Pins And Raw GPIO

Do not assume VOBOT D1 has the same pin mapping as unrelated boards named "D1 Mini" or ESP8266 dev boards.

Skill policy:
- If the user asks for "pin definitions", first distinguish built-in peripheral APIs, external connector pins, and raw MCU GPIO.
- For built-in functions, use SDK modules above.
- For physical connector wiring, ask for or inspect the exact hardware revision, schematic, board photo, or vendor documentation.
- For raw GPIO code, generate a diagnostic REPL script rather than claiming a fixed pinout.
- Avoid assigning GPIOs used by display, buttons, USB, flash, boot straps, or internal peripherals unless verified.

Diagnostic pattern:

```python
from machine import Pin
import time

PIN = 0  # replace only after hardware verification
p = Pin(PIN, Pin.IN, Pin.PULL_UP)

while True:
    print(PIN, p.value())
    time.sleep_ms(200)
```

When producing code that uses raw GPIO, label the mapping as "user-provided" or "needs device verification" unless it comes from a trusted source for the exact VOBOT D1 hardware revision.

