# Fixture matching and aging

Fixtures match each other because every one is calibrated with the same meter, in the same jig, against the same target. Aging is tracked through each fixture's correction gains and checked against a sealed reference strip.

## Design

- **Same batch:** buy all strip for a room from one reel or bin order.
- **Same session:** calibrate every fixture with the same meter, jig and geometry, ideally in one session.
- **Shared target:** every fixture solves for the same x, y and brightness using its own table.
- **Golden reference:** keep a 30 cm offcut from the same reel sealed in the dark. Once or twice a year, measure it in the jig. If its reading has moved, the sensor drifted, not the LEDs, so rescale the sensor fingerprints instead of the LED gains.
- **Aging log:** send each channel's correction gain to Home Assistant long-term statistics. A steadily rising gain is that channel's lumen loss.
- **Annual check:** spot-check a few colours per fixture with the spectrometer each year.
- **Long runs:** split runs longer than about 3 m into separately driven zones, each with its own sensor and calibration. No per-LED addressing.

## Done when

All fixtures in a room measure within 2–3 MacAdam steps of each other at 2700, 3500 and 5000 K.

## Open items

- [ ] Count fixtures and run lengths per room to size zones and controllers.
- [ ] Decide where the golden reference is stored.
