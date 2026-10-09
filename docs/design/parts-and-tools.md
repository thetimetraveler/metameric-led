# Parts and tools

Parts are per fixture (a 2–3 m run) unless noted; prices are approximate as of October 2026. Set the Status column as you buy.

## Parts

| Part | Example | Approx. price | Where | Status |
| --- | --- | --- | --- | --- |
| Controller | QuinLED An-Penta-Plus | from $40 | quinled.shop (US via DrZzs) | — |
| LED strip | Yuji CRI-MAX 5-in-1 RGBWW, 24 V, 60 LEDs/m | about $218 per 5 m | Yuji store | — |
| Power supply | 24 V UL-listed Class 2 LED supply, ≥125% of load (60 W+ per 5 m) | $25–60 | Mouser, Digi-Key | — |
| Spectral sensor | Adafruit AS7343 (#6477) | $19.95 | Adafruit, SparkFun | — |
| Temperature sensor | Adafruit TMP117 (#4821) | $11.50 | Adafruit, Digi-Key | — |
| XYZ sensor (optional) | DFRobot TCS3430 (SEN0403) | $14.90 | DFRobot | — |
| I²C multiplexer (if two 0x39 sensors) | TCA9548A breakout | under $10 | Adafruit | — |
| I²C extender (runs over 1 m) | PCA9615 differential pair | $10–20 | SparkFun | — |
| Qwiic / Stemma QT cables | 100–500 mm set | about $10 | Adafruit, SparkFun | — |
| Aluminium channel + opal diffuser + end caps | Deep channel, 15 mm+ | $15–40 per 2 m | Klus, Amazon | — |
| Wire | 18 AWG 6-conductor for runs; 22–24 AWG for I²C | about $20 | Amazon | — |
| Connectors | 6-pin 12 mm RGBCCT connectors, Wago 221, fork crimps | about $15 | Amazon | — |
| Inline fuse | Sized to wire gauge | about $5 | Digi-Key | — |
| Baffling and thermal | Black foam tape, thermal epoxy or pads | about $15 | Amazon | — |
| Reference lamp | Ketra A20 | about $100 | Lightopia | — |

## Tools

| Tool | Use | Status |
| --- | --- | --- |
| Temperature-controlled soldering iron (e.g. Pinecil), solder, flux | Strip and sensor connections | — |
| Ferrule crimper and fork/ring crimper | Controller screw terminals | — |
| Multimeter (true-RMS if possible) | Wiring checks, channel current | — |
| Spectrometer (choice open, see [Calibration](features/calibration.md)) | Per-channel calibration | — |
| 3D printer | Sensor end caps, V-blocks, meter cradle, hood | — |
| Hacksaw and mitre box | Cutting channel | — |
| Jig materials: black foam board or plywood, flocking paper, 2020 rail, E26 socket and cord | Calibration jig | — |
| Heat mat + Inkbird thermostat (optional) | Intermediate calibration temperature | — |
| Software: ESPHome, Home Assistant, Python with NumPy/SciPy and colour-science, ArgyllCMS | Firmware, fitting and measurement | — |
