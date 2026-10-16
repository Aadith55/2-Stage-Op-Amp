# LTspice schematic

Open `2-Stage op-Amp.asc` in LTspice. The schematic currently has transient analysis enabled, AC analysis commented out, and an `Rz` parameter sweep enabled.

## Project files and dependencies

- **Schematic:** `2-Stage op-Amp.asc`
- **Custom symbols:** `sym/cmosp.asy` and `sym/cmosn.asy` are included in this repository.
- **Model library:** the schematic uses the relative include `.include ../../models/tsmc018.lib`. The model file currently exists in the repository; see [../../models/README.md](../../models/README.md) for the provenance and redistribution note.
- **Symbol model names:** the custom symbols call the models `CMOSP` and `CMOSN` and define D, G, S, B terminals. Confirm these match the active model library and pin order if LTspice produces a netlist error.

If LTspice cannot resolve the symbols from the schematic's `sym/` directory, configure that folder in the local symbol search path. Keep the repository copies as the project source of truth.

## Run transient analysis

The active transient directive is:

```spice
.tran 10m
```

The parameter sweep currently enabled is:

```spice
.step param Rz 1k 20k 1k
```

Run the simulation and plot `Vout`. Use the Step Legend if there are separate traces for the stepped values.

## Run AC analysis

1. Comment out `.tran 10m`.
2. Enable `.ac dec 100 10 100Meg`.
3. Keep the input source's small-signal AC magnitude set to 1.
4. Run the analysis and plot `Vout` magnitude in dB and phase.
5. Use **View → Step Legend** to identify the `Rz=11k` trace.

For a single run at 11 kΩ, replace the sweep directive with `.param Rz=11k`. Restore the sweep when comparing multiple resistance values.

The supplied report's compensated targets are 17.2 MHz unity-gain bandwidth and 78.2° phase margin. Report actual measurements from the current LTspice run rather than assuming the targets were reproduced.
