# Simulation results

The project owner has run the schematic in LTspice, checked the AC measurements against the Bode plots, and reviewed the transient result. These plots are included below. The headline performance values are the values reported in the supplied design report.

## Included plots

- [AC analysis at 11 kΩ](figures/AC%20Analysis%20at%2011kOhm.png)
- [Uncompensated AC analysis](figures/AC%20analysis%20Uncompensated.png)
- [Transient output waveform](figures/Transient%20Analysis.png)

The report lists 9.25 MHz unity-gain bandwidth and 16.6° phase margin for the uncompensated case, and 17.2 MHz and 78.2° for the compensated case. For any future rerun, preserve the LTspice version, model-file version/source, supply, input common-mode voltage, input AC magnitude, load capacitance, analysis settings, selected `Rz`, and the method used to read each measurement. State whether results are simulated or measured on hardware.
