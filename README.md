# metameric-led

A DIY controller that keeps a multi-channel LED strip looking the same color as its temperature, brightness and age change.

A five-channel strip can't copy a reference lamp's spectrum exactly, but it can match how that lamp *looks*: a metamer. This project works out how to hold that match steady as the LEDs warm up and age, using a [QuinLED An-Penta-Plus](https://quinled.info/) driver, an AS7341 spectral sensor read through ESPHome, and Home Assistant for setpoints and logging.

This is a personal, non-commercial build, and it is not affiliated with or endorsed by Lutron.

**Status:** early research. The reference notes and patents are here; the design document is being moved over.

## What's here

| Path | Contents |
| --- | --- |
| [`docs/sources/`](docs/sources/) | Reference notes captured from outside sources |
| [`docs/patents/`](docs/patents/) | Full-text PDFs of the reference patents |

### Reference notes

- [ESPHome AS7341 sensor](docs/sources/esphome-as7341.md): channels, gain and integration-time options
- [Patent RE49246](docs/sources/patent-RE49246.md): forward-voltage and photodetector calibration ([PDF](docs/patents/RE49246.pdf))
- [Patent 12,052,807](docs/sources/patent-12052807.md): calibration over temperature, drive current and time ([PDF](docs/patents/12052807.pdf))

The patent notes are summaries of roughly the first 70–75% of each document, not complete readings. Check the PDFs for anything that matters.
