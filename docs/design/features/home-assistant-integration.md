# Home Assistant integration

Each fixture appears in Home Assistant as a light that takes colour temperature and brightness, plus diagnostic sensors. Home Assistant only sets targets; the loop keeps running without it.

## Entities

| Entity | Type | Purpose |
| --- | --- | --- |
| Fixture light | Light | Colour temperature and brightness; works with Adaptive Lighting |
| Target x, y, Duv | Number | Fine colour control off the white curve |
| Fidelity vs efficiency | Number (slider) | Uses the solver's spare freedom, like Ketra's Vibrancy |
| Measured CCT, Duv, x, y, lux | Sensor | What the fixture is actually producing |
| Board temperature | Sensor | From the TMP117 |
| Per-channel correction gain | Sensor | Aging log; long-term statistics |
| Unmixing residual | Sensor | High value flags room light leaking in or a sensor fault |
| Loop status | Text sensor | Running, blanking, or fault |

## Network and firmware settings

- WiFi is fine; use Ethernet where a cable is easy or signal is poor.
- Set `reboot_timeout: 0s` under both `api:` and `wifi:`, so the lights don't reboot when Home Assistant restarts.
- Set `restore_mode` so lights return to a sensible state after a power cut.

## Automations

- Gate the ambient-light blanking on room occupancy, using existing Aqara sensors.
- Feed circadian colour temperature from Adaptive Lighting or a schedule.

## Open items

- [ ] Decide whether the RadioRA 3 keypads should control these lights through Home Assistant.
- [ ] Pick the occupancy source for each room.
