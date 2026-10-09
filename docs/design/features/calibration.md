# Calibration

Each fixture gets its own calibration table, built once in a dark jig with a spectrometer and checked against a Ketra A20. Full reasoning is in the [Q&A log](../qa-log.md).

## Instrument

Not decided. A used i1Pro 2 with ArgyllCMS is the best value; a new Sekonic C-800 or UPRtek MK350D is the premium option.

| Option | Approx. cost | Notes |
| --- | --- | --- |
| Used i1Pro 2 + ArgyllCMS | A few hundred dollars (unverified) | Real spectrometer; scriptable; about ±0.002 xy repeatability; weak in low light |
| Used ColorMunki Photo / i1Studio | Less | Reported nearly as good for LEDs |
| Hopoo HPCS-330P | $599 | Handheld; untested accuracy; Windows-only software |
| Sekonic C-800 / UPRtek MK350D | About $1,900 | Best accuracy; MK350D has an SDK |
| Opple Light Master | $40–60 | White light only; spot checks |

## Ketra A20 reference

- **Decided:** buy an A20.
- **Open:** how to control it. Ketra needs HomeWorks, Athena or myRoom XC, and RadioRA 3 likely can't control it. Ask the lighting rep at Lightopia.
- **Uses:** a side-by-side visual match on a divided white card, and a check that your meter reads it near its set colour.
- **Limits:** its spectrum differs from the strip, so sensor corrections don't transfer exactly. Warm both lights 30 minutes before comparing.

## Jig

- **Bench box:** about 60 × 30 × 30 cm, black-lined. Holds a 30–50 cm sample of channel and diffuser on printed V-blocks, with the meter on a 2020 rail at fixed 10 cm and 30 cm stops. An E26 socket plate puts the A20 at the same distance.
- **Clamp-on hood:** a printed black shroud that clips over 30 cm of an installed channel near its sensor, with the same meter cradle. Used at night with the room dark.
- **Validation:** 5 readings untouched, then 5 after re-seating. Spread must stay within about ±0.001 xy.

## Procedure

1. Warm up the meter and take a dark reading.
2. Cold sweep: each channel alone at 8 levels, plus about 20 white check points. A Python script sets levels through ESPHome's API, triggers the meter, and logs meter, AS7343 and TMP117 readings to CSV.
3. Run full white for 45–60 minutes with the box closed, then repeat the sweep warm.
4. Fit each channel's colour and output against level and temperature; record the AS7343 fingerprints.
5. Measure the white check points and apply a small correction to cancel remaining per-channel error.
6. Store the table on the fixture's controller.

## Open items

- [ ] Choose the instrument.
- [ ] Confirm how the A20 will be controlled.
- [ ] Decide on the reference standard: match Ketra, or absolute CIE values.
- [ ] Design and print the V-blocks, cradle and hood.
