# Temperature compensation

A TMP117 on the aluminium channel feeds a per-channel model of how output changes with heat, and the solver re-runs every few seconds. Ketra measures each LED's own temperature through its forward voltage; the An-Penta can't, so board temperature stands in.

## Design

- **Sensor:** TMP117 bonded to the channel with thermal epoxy or pad, 5–10 cm from the strip's input end, shielded from the LED light.
- **Calibration points:** measure each channel cold (first 30 seconds after power-on) and warmed up (60 minutes at full output).
- **Model:** linear for white, green and blue. Red likely needs a curve; the patents flag red and amber as the most temperature-sensitive.
- **Self-heating:** LED temperature runs above board temperature in proportion to drive level. Model it as board temperature plus a per-channel factor times that channel's level, fitted from the data.
- **Update rate:** read every 1–5 seconds and re-solve the channel levels.
- **Wiring note:** don't use a DS18B20; the An-Penta's free pins are input-only and can't run 1-Wire.

## Optional upgrade: per-channel current monitoring

An INA226 on each channel is the closest DIY stand-in for Ketra's forward-voltage sensing. Try it only if the TMP117 model misses the drift target.

- **Why it works:** on a constant-voltage strip, each segment is LEDs in series with a resistor. As the LEDs heat, their forward voltage drops, so channel current rises slightly. That rise tracks the LEDs' own temperature, per colour.
- **Supply sag:** the INA226 also reads bus voltage. Supply changes move LED current and output directly, so this corrects them too.
- **Wiring:** a small shunt in each channel wire between the strip and the An-Penta output. Size it so the highest channel current gives about 60–80 mV across it.
- **PWM:** the INA226 reports average current. Divide by the known duty to get the on-current, and only trust readings above about 10% duty; below that, fall back to the TMP117 model.
- **Bus:** INA226 has 16 selectable addresses, so five or six share the I²C bus with the other sensors.

## Done when

Colour drift from cold start to fully warm stays under Δu′v′ 0.002.

## Open items

- [ ] Confirm TMP117 mounting method and location on the channel.
- [ ] Decide whether a heat mat is needed for an intermediate calibration temperature.
