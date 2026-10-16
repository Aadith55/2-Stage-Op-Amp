# LTspice schematic

Open `2-stage-opamp.asc` in LTspice. The schematic currently has a transient analysis directive enabled and an AC sweep directive commented out.

## Local dependencies

- **TSMC 180 nm model library:** place a licensed copy at `models/tsmc018.lib` at the repository root. The schematic uses the relative include `.include ../../models/tsmc018.lib`.
- **Custom transistor symbols:** the schematic uses `sym\cmosp` and `sym\cmosn`. Their symbol definitions were not among the supplied attachments. Add the required symbol files to your LTspice symbol library, or change the schematic to use symbols supported by your own model setup.
- **Model names and pin order:** confirm the custom symbols' netlist model names and pin mapping match the provided TSMC library. These details cannot be inferred from the supplied schematic alone.

## Run transient analysis

The default active directive is `.tran 10m`, with `.step param Rz 1k 20k 1k` to sweep the series nulling resistor from 1 kΩ through 20 kΩ. Run the simulation and inspect the output waveform for each step.

## Run AC analysis

1. Edit the schematic's analysis directives: comment out `.tran 10m` and uncomment `.ac dec 100 10 100Meg`.
2. Keep the input source's small-signal AC value set to 1.
3. Run AC analysis and plot `Vout` magnitude and phase.
4. Read unity-gain bandwidth and phase margin from the Bode response, using the correct stepped `Rz` trace.

The supplied report identifies 11 kΩ as the selected compensation resistance. Confirm that value in the AC results before reporting the final compensated performance.
