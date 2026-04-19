[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fartogahr%2Fsmarter-motion-light%2Fblob%2Fmain%2Fsmarter_motion_light.yaml)

# smarter-motion-light

A Home Assistant motion light blueprint that won't turn lights on when the room is already bright.

## Why

The stock motion light blueprint fires on any motion, even at noon with sunlight pouring through the window. This one adds two optional gates:

- **Illuminance** — skip turning on if a lux sensor says the room is already bright enough.
- **Sun position** — during dusk, night, and dawn, ignore the lux check and always turn on.

It also supports smooth fade-on / fade-off transitions instead of snapping lights on and off.

Both gates are independent toggles. Pick whichever combo fits your room.

## Recommended setups

- **Window + lux sensor:** both gates on. Start with a 60 lux threshold and tune.
- **No window / weird exposure:** sun off, lux on.
- **No lux sensor:** both off. Plain motion light with a sane 10s default wait time.

## Inputs

| Input | Notes |
|---|---|
| Motion Sensor | Motion or occupancy binary sensor. |
| Light | Light or group to control. |
| Use sun gating | Bypass lux check during dusk/night/dawn. |
| Sunrise / sunset offset | Minutes to shrink the "daytime" window. Default 60. Bump higher at high latitudes. |
| Use illuminance gating | Only turn on if lux is below threshold. |
| Illuminance Sensor | Required only if lux gating is on. |
| Illuminance Threshold | Default 60 lx. |
| Use smooth transitions | Fade on/off instead of snapping. |
| Turn-on transition | Seconds to fade on. Default 2. |
| Turn-off transition | Seconds to fade off. Default 5. |
| Wait time | Seconds to keep the light on after motion clears. Default 10. |

## Tuning the lux threshold

Depends entirely on sensor placement. A corner-mounted sensor reads much lower than one by the window. Rough guide:

- Below 50 lx: dim, most people want lights
- 50–150 lx: borderline
- 150+ lx: bright enough to read

Watch your sensor for a few days and pick a number that matches when you'd reach for the switch. For reference: an overcast afternoon in my Prague living room reads around 37 lx with the sensor in the corner.

## License

See [LICENSE](LICENSE).
