# Decision log

Two decisions are made so far: the controller and the Ketra A20. Everything marked Proposed comes from research and needs your call. New decisions go at the top.

| Date | Decision | Status | Why | Doc |
| --- | --- | --- | --- | --- |
| Oct 9, 2026 | Personal build only, not for sale | Decided | Ketra patents are a concern only for a product | [System design](system-design.md) |
| Oct 9, 2026 | PWM at about 4.9 kHz (14-bit) plus 2-bit temporal dithering | Proposed | About 16-bit effective resolution for warm dimming, still above flicker-risk frequencies | [Colour mixing](features/colour-mixing.md) |
| Oct 9, 2026 | Optional INA226 current/voltage monitor per channel | Proposed | Closest stand-in for forward-voltage sensing; also catches supply voltage sag | [Temperature compensation](features/temperature-compensation.md) |
| Oct 9, 2026 | TCA9548A I²C multiplexer only if a second 0x39 sensor shares a controller | Proposed | One spectral sensor per controller has no conflict; ESPHome supports the mux natively | [Optical feedback](features/optical-feedback.md) |
| Oct 9, 2026 | Use a QuinLED An-Penta-Plus as the controller | Decided | 5 PWM channels, ESP32, optional Ethernet, ESPHome support | [System design](system-design.md) |
| Oct 9, 2026 | Buy a Ketra A20 as a colour reference | Decided | Side-by-side visual target and meter sanity check | [Calibration](features/calibration.md) |
| Oct 9, 2026 | Firmware: ESPHome custom external component, not WLED | Proposed | The solver and correction loop must run on the device; WLED can't host them | [Colour mixing](features/colour-mixing.md) |
| Oct 9, 2026 | Optical sensor: ams AS7343 inside the fixture | Proposed | 11 visible bands are enough to separate 5 channels from one reading | [Optical feedback](features/optical-feedback.md) |
| Oct 9, 2026 | Temperature sensor: TMP117 on the aluminium channel | Proposed | ±0.1 °C accuracy, I²C, four addresses per bus | [Temperature compensation](features/temperature-compensation.md) |
| Oct 9, 2026 | Strip: Yuji CRI-MAX 5-in-1 RGBWW, 24 V | Proposed | CRI 95+ whites do the fidelity work; RGB only trims colour | [Parts and tools](parts-and-tools.md) |
| Oct 9, 2026 | Network: WiFi is fine; Ethernet where easy | Proposed | The loop runs locally; the network carries only setpoints and logs | [Home Assistant integration](features/home-assistant-integration.md) |
| Oct 9, 2026 | No per-LED addressing; split long runs into zones | Proposed | Addressable chips are 8-bit or poorly supported; one sensor can't see pixels | [Fixture matching and aging](features/fixture-matching-and-aging.md) |
| Oct 9, 2026 | Calibration instrument | Open | Used i1Pro 2 + ArgyllCMS vs Sekonic C-800 / UPRtek MK350D | [Calibration](features/calibration.md) |
| Oct 9, 2026 | Reference standard: match Ketra or absolute CIE | Open | Decides whether the A20 or a spectrometer leads calibration | [Calibration](features/calibration.md) |
