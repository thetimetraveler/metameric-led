# Q&A log: follow-up questions

*Oct 9, 2026*

WiFi is fine, the Ketra A20 is most useful as a side-by-side visual reference, a used i1Pro 2 is the cheapest instrument worth trusting, and per-LED addressing is not worth copying. This page answers five follow-up questions on this build with the QuinLED An-Penta-Plus.

| Question | Short answer |
| --- | --- |
| 1. Ethernet or WiFi? | WiFi is fine; the correction loop runs on the ESP32. Set ESPHome `reboot_timeout: 0s`. |
| 2. Ketra A20 as a reference? | Yes, if it can be controlled. RadioRA 3 likely can't control Ketra, so confirm first. |
| 3. Cheaper instruments? | Used i1Pro 2 or i1Studio with ArgyllCMS. Skip the Opple and unbranded clones. |
| 4. Calibration jig? | A bench box for each strip reel plus a clamp-on hood for installed fixtures. |
| 5. Copy Ketra's per-LED addressing? | No. Ketra addresses per lamp and per colour channel, which the An-Penta already does. |

## 1. Ethernet or WiFi?

WiFi is fine. The whole correction loop runs on the ESP32: sensor reads, temperature compensation and the colour math. The network only carries setpoints from Home Assistant and data going back to it.

Use Ethernet when any of these apply:

- A cable is easy to run to the controller.
- You'll have several controllers.
- The controller sits somewhere with poor signal, such as a ceiling cavity or metal enclosure.
- You want the most reliable streaming during calibration runs.

The real gotcha is firmware, not the network type. By default ESPHome reboots the device after 15 minutes without WiFi or a Home Assistant connection. That makes the lights blink off when HA restarts or the router hiccups.

- Set `reboot_timeout: 0s` under both `api:` and `wifi:`.
- Set `restore_mode` so the lights return to a sensible state after a power cut.

## 2. Using a Ketra A20 as a reference

The A20 is a good reference only if you can control it, and RadioRA 3 probably can't. Lutron's [A20 spec sheet](https://assets.lutron.com/a/documents/a20_specification_sheet.pdf) says colour and intensity control need a compatible system. Its [A20 product page](https://www.lutron.com/us/en/lighting/lamps-track-lights/a20-lamp?sku=A20) lists HomeWorks, Athena and myRoom XC. The [Ketra FAQ](https://www.lutron.com/us/en/lighting/ketra/faq) says Ketra doesn't integrate directly with RadioRA 2. A [forum post](https://cocoontech.com/members/tleffing.10401/recent-content) claims RA3 has no Ketra support, but that isn't an official source.

- [ ] Ask the Lightopia rep whether RA3 can control an A20.
- [ ] Ask what the A20 does when powered with no controller. If it only comes on at one fixed white, it's a reference for that single point.

**If you can control it, use it two ways:**

1. **Side-by-side visual match.** Light one half of a matte white card with the A20 and the other half with your fixture, with a divider between them. Adjust your fixture until the edge between the halves disappears. Record what your fixture's sensor reads at that point and use it as your target. This gets you "matches Ketra" without trusting any meter.
2. **Meter check.** Ketra rates the A20 as holding its colour within a one-step MacAdam ellipse over its life. That is a consistency claim, not an absolute-accuracy guarantee, but it's a good sanity check. If your meter reads the A20 at 2700 K well off the curve, suspect the meter.

**Limits:**

- The A20 uses a different 4-channel light engine than your 5-in-1 strip, so their spectra differ. Sensor corrections derived from the A20 won't transfer exactly to the strip, especially for RGB- or XYZ-filter sensors.
- Two lights with different spectra can match for one person and not another. Check the final match with a second viewer.
- Warm up both lights for about 30 minutes before comparing.

## 3. Cheaper calibration instruments

A used X-Rite i1Pro 2 with the free ArgyllCMS software is the best value. It is a real spectrometer, and ArgyllCMS can script its readings for the jig.

| Option | Approx. cost | Verdict |
| --- | --- | --- |
| [i1Pro 2](https://chromapure.com/products-i1pro.asp) / i1Pro, used, + [ArgyllCMS](https://argyllcms.com/doc/spotread.html) | A few hundred dollars used (unverified) | **Best value.** 10 nm optical resolution; chromaticity repeatability within about ±0.002 xy. Weak in low light, so measure close. |
| ColorMunki Photo / i1Studio, used | Cheaper | Lighting hobbyists [report](https://budgetlightforum.com/comment/1467289) it's nearly as good for LED measurement. |
| [Hopoo HPCS-330P](https://plastiquealaloupe.fondationtaraocean.org/products/hpcs-330p-spectrometer-ppfd-meter-par-quantum-meter-wireless/211699738/) | $599 | Handheld; 4 nm FWHM and ±1 nm wavelength accuracy listed. No independent accuracy test found, and Windows-only software is harder to automate. |
| Unbranded clones (e.g. [GOYOJO HP330](https://www.accio.ai/find-product/spectrum-analyser-accessories-price-philippines)) | ~$268 | Unknown accuracy. Skip. |
| Opple Light Master | ~$40–60 | White light only. Fine for spot checks, useless for the R/G/B channels. |

**Accuracy verdict.** For matching your fixtures to each other with the same meter, these are good enough: averaged readings around ±0.002 xy support the 2–3-step target. For absolute CIE accuracy, cheap units are weakest on the narrow red, green and blue peaks.

Two things lower the stakes:

- After the first fit, measure a few target whites directly and apply a small correction. That cancels most per-channel error.
- If the A20 is controllable, matching to it covers the absolute side.

## 4. Calibration jig plan

Build two pieces: a bench box for characterizing each strip reel, and a clamp-on hood for calibrating installed fixtures.

### A. Bench box (strip characterization and A20 comparison)

- **Enclosure:** about 60 × 30 × 30 cm, plywood or black foam board, lined with black flocking paper. Baffle the cable entry against light leaks.
- **Sample mount:** 3D-printed V-blocks holding a 30–50 cm piece of the same aluminium channel and diffuser you'll install. Mount the AS7343 and TMP117 exactly as in the real fixtures.
- **Meter mount:** a printed cradle on a 2020 aluminium extrusion rail, with fixed stops at 10 cm and 30 cm. The i1Pro needs the closer stop.
- **A20 bay:** a swappable plate with an E26 socket that puts the bulb at the same distance as the strip sample. Add a divided white card for the side-by-side match.
- **Temperature points:**
  - **Cold:** readings in the first 30 seconds after a cold start.
  - **Hot:** close the box and run full white for 45–60 minutes.
  - **Optional:** a reptile heat mat with an Inkbird thermostat holds an intermediate temperature.

### B. Clamp-on hood (each installed fixture)

- A printed black shroud that clips over a 30 cm section of the installed channel, near the sensor end.
- It carries the same meter cradle at the same fixed distance.
- Run it at night with the room dark. This calibrates each fixture's own sensor without uninstalling anything.

### Automation

- A Python script on a laptop sets channel levels through ESPHome's native API (`aioesphomeapi`) and triggers ArgyllCMS `spotread`.
- It logs the meter reading, the AS7343 channels and the TMP117 temperature to a CSV.
- Each run covers every channel alone at 8 levels plus about 20 white check points, roughly 100 points in all. With 2–5 seconds of settling per point, that's about 15 minutes per temperature.

### Prove the jig before trusting it

1. Take 5 repeat readings without touching anything.
2. Remove and re-seat the sample 5 times, measuring each time.
3. If the re-seated spread is worse than about ±0.001 xy, tighten the mounting before collecting data.

### Jig parts

- [ ] Foam board or plywood
- [ ] Black flocking paper
- [ ] 2020 extrusion rail
- [ ] 3D-printed cradles and V-blocks
- [ ] E26 socket and cord
- [ ] Spare channel and diffuser offcuts
- [ ] Heat mat and Inkbird thermostat (optional)

## 5. Does Ketra address individual LEDs?

No, not in the pixel sense, and you shouldn't either. Each Ketra lamp has one multi-die emitter with its colours driven as separate channels, and each lamp is individually addressable. The patents' one-emitter-at-a-time measurements are per colour channel, not per position along a strip. One An-Penta driving one fixture is the same arrangement: each fixture is one "Ketra lamp" with 5 channels instead of 4.

**Why not go addressable:**

- **Too coarse.** The common 5-channel addressable chip, the [WS2805](https://wmsc.lcsc.com/wmsc/upload/file/pdf/v2/lcsc/2306301035_Worldsemi-WS2805_C5446697.pdf), has 256 dimming levels per channel at 4 kHz. That is far coarser than the An-Penta's 4,096+ levels, and precise warm-dim colour needs fine low-end control.
- **Hard to calibrate per pixel.** One sensor sees the blended light of many pixels, so per-pixel calibration means scanning each pixel with the meter.
- **Worse colour quality.** Addressable RGB+CCT strips rarely match the Yuji CRI-MAX strip's colour rendering.

**If you still want it:**

| Part | Notes |
| --- | --- |
| [SM16825E](https://wiki.adom.inc/kyle/sm16825e) strip | 16-bit dimming per channel, 5 channels, per-channel current adjustment. WLED support was only [requested](https://wled.discourse.group/t/sm16825-chip-support/11140) as of 2024; check before buying. |
| WS2805 strip | [Supported in WLED 0.15](https://wled.discourse.group/t/wled-and-cct/12853), but 8-bit. Not suitable for this build. |
| QuinLED Dig-Uno or Dig-Quad | Digital controller to drive either strip. |

**Better fix for long runs:** split runs longer than about 3 m into separately driven zones, each with its own sensor and calibration. That costs more An-Pentas, but each stays a simple, accurate controller.

## Sources

- [Lutron Ketra A20 specification sheet](https://assets.lutron.com/a/documents/a20_specification_sheet.pdf)
- [Lutron Ketra A20 product page](https://www.lutron.com/us/en/lighting/lamps-track-lights/a20-lamp?sku=A20)
- [Lutron Ketra FAQ](https://www.lutron.com/us/en/lighting/ketra/faq)
- [Cocoontech forum post on RA3 and Ketra](https://cocoontech.com/members/tleffing.10401/recent-content)
- [ChromaPure i1Pro 2 product page](https://chromapure.com/products-i1pro.asp)
- [ArgyllCMS spotread documentation](https://argyllcms.com/doc/spotread.html)
- [BudgetLightForum i1Pro / ArgyllCMS thread](https://budgetlightforum.com/comment/1467289)
- [Hopoo HPCS-330P listing](https://plastiquealaloupe.fondationtaraocean.org/products/hpcs-330p-spectrometer-ppfd-meter-par-quantum-meter-wireless/211699738/)
- [GOYOJO HP330 listing](https://www.accio.ai/find-product/spectrum-analyser-accessories-price-philippines)
- [Worldsemi WS2805 datasheet](https://wmsc.lcsc.com/wmsc/upload/file/pdf/v2/lcsc/2306301035_Worldsemi-WS2805_C5446697.pdf)
- [SM16825E summary](https://wiki.adom.inc/kyle/sm16825e)
- [WLED forum: SM16825 support request](https://wled.discourse.group/t/sm16825-chip-support/11140)
- [WLED forum: WS2805 support](https://wled.discourse.group/t/wled-and-cct/12853)
