# Patent notes

Ketra's colour-hold system is an accurate per-channel model plus infrequent optical correction, not mainly a sensor trick. These notes come from the published Lutron/Ketra patents, not the two patent PDFs ([RE49246](../patents/RE49246.pdf) and [12,052,807](../patents/12052807.pdf)), which the research session couldn't open. For notes on those two PDFs, see [RE49246](../sources/patent-RE49246.md) and [12,052,807](../sources/patent-12052807.md).

## How Ketra's colour-hold system works

| Mechanism | What the patents describe | Key patents |
| --- | --- | --- |
| Factory calibration per channel | Each LED chain measured at 3+ drive currents and 2 temperatures; output, colour and forward voltage stored in the fixture | [US9651632B1](https://patents.google.com/patent/US9651632B1/en), [US9392660B2](https://patents.google.com/patent/US9392660B2/en) |
| Temperature from forward voltage | LEDs briefly blanked; a small current reveals each LED's forward voltage as a temperature proxy | [US9578724B1](https://patents.google.com/patent/US9578724B1/en) |
| Colour-specific behaviour | Red and amber output change sharply and non-linearly with heat; white, green and blue change little | [US9578724B1](https://patents.google.com/patent/US9578724B1/en) |
| LEDs as sensors | An LED detects other LEDs' light while it is off; later designs use a small red/orange detector LED | [US20100327764A1](https://patents.google.com/patent/US20100327764A1/en), [US9769899B2](https://patents.google.com/patent/US9769899B2/en) |
| Aging correction | One emitter lit at a time; its output measured by a detector run at low current so the detector itself doesn't age | [USRE49246E1](https://patents.google.com/patent/USRE49246E1/en) |
| Hidden measurements | Off-slots synced to mains; drive raised 1–10% while on to keep average brightness | [US9578724B1](https://patents.google.com/patent/US9578724B1/en) |
| Multi-lamp interference | Measurement slots offset between lamps; ambient checked before measuring | [US9247605B1](https://patents.google.com/patent/US9247605B1/en), [US9155155B1](https://patents.google.com/patent/US9155155B1/en) |
| Colour mixing | 16-bit brightness, x, y and a "white mix" input; scaled to the most light possible at that colour | [US9237623B1](https://patents.google.com/patent/US9237623B1/en) |

## What a DIY build can replicate

| Element | Feasible here? | How |
| --- | --- | --- |
| Per-channel calibration table | Yes | Spectrometer, per fixture |
| Colour target solved over 4+ channels | Yes | Bounded least squares on the ESP32 |
| Temperature compensation | Partly | Board temperature from a TMP117, not per-LED forward voltage |
| Optical feedback | Yes, differently | One AS7343 per fixture with spectral unmixing |
| Invisible measurement slots | Limited | Blank only when the room is empty |
| Aging compensation | Yes, slowly | Correction gains plus a golden reference strip |
| One-step MacAdam matching | Unlikely | Expect 2–3 steps |
