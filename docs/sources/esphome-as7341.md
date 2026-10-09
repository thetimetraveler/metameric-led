# ESPHome — AS7341 Spectral Color Sensor

Source: https://esphome.io/components/sensor/as7341/
Captured: 2026-10-09 (text summary of the page, not the original HTML)

## What it is
The `as7341` sensor platform connects the AS7341 spectral color sensor to ESPHome. Requires the I²C bus to be configured.

## Channels (all optional, each takes standard sensor options)
- `f1`–`f8`: spectral channels at ~415, 445, 480, 515, 555, 590, 630, 680 nm
- `clear`: clear channel
- `nir`: near-infrared channel

## Other options
- `gain`: X0.5, X1, X2, X4, X8 (default), X16, X32, X64, X128, X256, X512. Higher gain suits low light.
- `astep`: number of integration steps. Default 599, range 0–65534.
- `atime`: integration time per step, in 2.78 µs increments. Default 29, range 0–255.
- Standard I²C device options also apply.

## Integration time
Total = (ATIME + 1) × (ASTEP + 1) × 2.78 µs
Defaults: (29 + 1) × (599 + 1) × 2.78 µs ≈ 50 ms

## Minimal example
```yaml
sensor:
  - platform: as7341
    f1:
      name: "415nm"
    f4:
      name: "515nm"
    clear:
      name: "Clear"
    nir:
      name: "NIR"
```
