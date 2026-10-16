# LTspice schematic

Open `2-Stage op-Amp.asc` in LTspice. The project owner confirms that the schematic has been tested locally and the AC performance measurements have been checked against the plots.

## Project files and dependencies

- **Schematic:** `2-Stage op-Amp.asc`
- **Custom symbols:** `sym/cmosp.asy` and `sym/cmosn.asy` are included in this repository.
- **Model library:** the schematic uses the relative include `.include ../../models/tsmc018.lib`. This is the model set used for the project. Public redistribution permission is separate; see [../../models/README.md](../../models/README.md).
- **Symbol model names:** the custom symbols call the models `CMOSP` and `CMOSN` and define D, G, S, B terminals.

## Run transient analysis

The active transient directive is:

```spice
.tran 10m
```

The parameter sweep currently enabled is:

```spice
.step param Rz 1k 20k 1k
```

Run the simulation and plot `Vout`. Use the Step Legend if separate traces are shown for each stepped value.

## Run AC analysis

1. Comment out `.tran 10m`.
2. Enable `.ac dec 100 10 100Meg`.
3. Keep the input source's small-signal AC magnitude set to 1.
4. Run the analysis and plot `Vout` magnitude in dB and phase.
5. Use **View → Step Legend** to identify the `Rz=11k` trace.

For a single run at 11 kΩ, replace the sweep directive with `.param Rz=11k`. Restore the sweep when comparing multiple resistance values.

The supplied report's compensated values are 17.2 MHz unity-gain bandwidth and 78.2° phase margin. The project owner confirms these were checked against the AC plots.
