# Colour mixing

The solver turns a target colour (x, y) and brightness into five channel levels using the fixture's own calibration table. It runs on the An-Penta inside an ESPHome external component.

## Design

- **Inputs:** target x, y (or colour temperature plus Duv) and brightness Y.
- **Method:** bounded least squares over the five channels' measured colour vectors, with each level between 0 and 1.
- **Spare freedom:** five channels and three colour equations leave two free dimensions. Spend them on colour fidelity (Rf) or efficiency, like Ketra's Vibrancy control.
- **Speed:** precompute a lookup table along the white curve (about 2000–6500 K) plus Duv offsets, so the ESP32 interpolates instead of optimizing live.
- **Brightness cap:** at each colour, scale to the most light all channels can make together.
- **Low-end resolution:** run PWM at about 4.9 kHz for 14-bit levels, add 2-bit temporal dithering for about 16-bit effective, and measure the lowest duty levels directly during calibration because very short pulses aren't linear.
- **RGB use:** keep red, green and blue as small trims near the white curve. Leaning on them lowers colour rendering.

## Done when

A spectrometer confirms 2700, 3500 and 5000 K targets within Δu′v′ 0.003.

## Open items

- [ ] Pick the objective for the two free dimensions: fidelity, efficiency, or a user slider.
- [ ] Choose PWM frequency and bit depth after checking for visible flicker on camera.
- [ ] Decide whether saturated colours are in scope or whites only.
