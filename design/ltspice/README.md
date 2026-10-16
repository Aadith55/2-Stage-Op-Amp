# LTspice Schematic

Open `2-Stage op-Amp.asc` in LTspice. The schematic has transient analysis enabled, AC analysis commented out, and an `Rz` parameter sweep configured.

## Files and dependencies

- **Schematic:** `2-Stage op-Amp.asc`
- **Custom symbols:** `sym/cmosp.asy` and `sym/cmosn.asy`
- **Model file:** `../../models/tsmc018.lib`, referenced relative to the schematic directory

The custom symbols reference the models `CMOSP` and `CMOSN` and define drain, gate, source, and bulk terminals. If LTspice reports unresolved symbols or model errors, check the symbol search path, model names, and terminal mapping.

## Transient analysis

The active directive is:

```spice
.tran 10m
```

The resistor sweep is:

```spice
.step param Rz 1k 20k 1k
```

Run the simulation and plot `Vout`. Use the Step Legend to identify traces for each value of `Rz`.

## AC analysis

1. Comment out `.tran 10m`.
2. Enable `.ac dec 100 10 100Meg`.
3. Keep the input source's small-signal AC magnitude set to 1.
4. Run the analysis and plot `Vout` magnitude in dB and phase.
5. Use **View → Step Legend** to identify the trace for `Rz=11k`.

To run only the 11 kΩ case, replace the sweep directive with `.param Rz=11k`. Restore the sweep when comparing multiple resistance values.

The compensated response has a recorded unity-gain bandwidth of 17.2 MHz and phase margin of 78.2°.
