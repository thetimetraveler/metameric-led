# Ketra patent RE49246 — LED forward-voltage and photodetector calibration

Source: https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/RE49246
Captured: 2026-10-09 (text summary of roughly the first 70% of the document, not the original PDF)

## Bibliographic
- Reissue of U.S. Pat. No. 9,510,416 (issued Nov. 29, 2016; Application Ser. No. 14/471,081, filed Aug. 28, 2014)
- Title, assignee, inventors and abstract were not in the captured text; see the front page of the PDF.

## Claims (summary)
- **Claim 1 (method):** Drive several emission LEDs continuously, switch them off briefly at intervals, and measure each LED's forward voltage one at a time. Look up expected wavelength and intensity by interpolating a stored calibration table relating wavelength and intensity to drive current at several temperatures.
- **Claim 16 (device):** Emission LEDs, storage holding the calibration table, a driver/receiver circuit that makes the forward-voltage measurements, and a control circuit that does the interpolation.
- **Claim 32 (method):** Determine each LED's expected wavelength, measure the photodetector's photocurrent and forward voltage, and calculate the photodetector's responsivity from stored coefficients.
- **Dependent claims:** linear and piece-wise linear interpolation; choosing interpolation by LED color; radiance or luminance values; adjusting drive current to reach an adjusted luminous flux.

## Description (summary)
- **Per-color photodetector measurement:** Detector responsivity is characterized for each emitter color as a function of emitter wavelength and detector forward voltage, using a first-order model (slope, offset, temperature-shift term). Phosphor-converted white LEDs can use separate detectors for the phosphor and blue-pump portions.
- **Forward voltage as temperature:** Measured with a small non-operative current (~0.3–3 mA for emitters, ~100–300 µA for a single photodetector) so the resistive drop, which grows with age, has little effect. Forward voltage serves as a junction-temperature indicator.
- **Calibration tables:** Wavelength, intensity and forward voltage recorded across drive currents at two temperatures, typically ~25 °C and ~70 °C. Linear emitters (red) need fewer stored points than non-linear ones (green, blue), which may use more points or polynomial coefficients.
- **Color point control:** Color shifts with temperature and aging, especially in multi-color devices; adjusting drive current to hold flux also moves chromaticity. Example target: (0.437, 0.404) for 3000K white. The captured text ends before the full control method.
