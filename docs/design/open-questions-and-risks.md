# Open questions and risks

The biggest open question is the reference standard: matching Ketra or hitting absolute CIE values. It decides which instrument to buy and how calibration runs.

## Open questions

- [ ] Reference standard: match a Ketra A20, or absolute CIE accuracy?
- [ ] Can RadioRA 3 control a Ketra A20? If not, what does an unpaired A20 do at power-on? (Ask the lighting rep at Lightopia.)
- [ ] Calibration instrument: used i1Pro 2, or Sekonic C-800 / UPRtek MK350D?
- [ ] How many fixtures, in which rooms, and how long is each run?
- [ ] Whites only, or saturated colours too?
- [ ] Should RadioRA 3 keypads control these lights through Home Assistant?
- [ ] Accept the proposed firmware, sensor, temperature sensor and strip choices? (See [Decision log](decision-log.md).)

## Risks

| Risk | Effect | Mitigation |
| --- | --- | --- |
| Sensor reads PWM flicker as noise | Unstable corrections at low duty | Integrate over a whole number of PWM periods, at least 50; average readings |
| Visible blink during ambient blanking | Annoying flash at high brightness | Blank only when the room is empty |
| Room light leaks into the sensor | Loop "corrects" toward daylight | Sensor inside the sealed channel with baffles; alarm on high unmixing residual |
| Sensor drifts with heat and age | Loop tracks a drifting sensor | Golden reference strip and yearly spectrometer checks |
| White channels hard to tell apart | Unstable warm/cool correction | Correct overall colour only; keep the warm/cool split open-loop |
| Coarse PWM steps at low brightness | Colour jumps when dimmed | Lower PWM frequency for more bits; temporal dithering |
| Cheap meter error on narrow R/G/B peaks | Wrong channel table | Correct against measured whites; check against the A20 |
| Electrical code | Safety and inspection | Class 2 supply; mains wiring in a proper box; electrician where required |
| Ketra patents | Legal exposure if sold | Decided: personal build, not for sale |
