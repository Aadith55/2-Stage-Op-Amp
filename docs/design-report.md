# Design summary and simulation results

This page summarizes the supplied report, *Two-Stage CMOS Operational Amplifier Design in 180nm Technology*, and records the transistor dimensions encoded in the uploaded LTspice schematic. The project owner has run the schematic in LTspice and checked the AC performance measurements against the result plots.

## Objective and architecture

The design is a two-stage CMOS operational amplifier intended for a 10 pF capacitive load. The report discusses a 3 pF Miller compensation capacitor and a series nulling resistor used to improve phase margin.

## Reported specifications

| Parameter | Value in supplied report |
|---|---:|
| Technology target | 180 nm |
| Supply | 1.8 V / 0 V |
| Common-mode input | 0.9 V |
| Load capacitance | 10 pF |
| Open-loop DC gain | 80 dB |
| Uncompensated unity-gain bandwidth | 9.25 MHz |
| Uncompensated phase margin | 16.6° |
| Compensated unity-gain bandwidth | 17.2 MHz |
| Compensated phase margin | 78.2° |
| Miller capacitor | 3 pF |
| Selected series nulling resistor | 11 kΩ |

The report states that the uncompensated Miller architecture exhibits poor phase margin, attributing the behavior to a right-half-plane zero associated with the capacitor's feed-forward path. It reports initial unity-gain bandwidth of 9.25 MHz and phase margin of 16.6°.

The report then describes a parametric SPICE sweep of a series nulling resistor and identifies 11 kΩ as the selected value. It reports compensated unity-gain bandwidth of 17.2 MHz and phase margin of 78.2°. The project owner confirms that the schematic has been run and these measurements have been checked against the AC plots. The screenshots are stored in [results/figures/](../results/figures/).

## Transistor dimensions used in the simulation

The dimensions encoded in the uploaded schematic and confirmed by the project owner are:

| Devices | Width (W) | Length (L) |
|---|---:|---:|
| M1, M2 | 20 µm | 0.5 µm |
| M3 | 40 µm | 0.5 µm |
| M4, M5 | 10 µm | 0.5 µm |
| M6, M7 | 5 µm | 0.5 µm |
| M8 | 5 µm | 0.5 µm |

**M8 is 5 µm wide**, matching the value used in the simulation. The supplied report's prose separately describes M8 as approximately 3× for second-stage bias, but its transistor-sizing table leaves the W/L cells blank. This repository records the as-simulated value and does not change it to match that ambiguous statement.

## Model-file note

The `models/tsmc018.lib` file is the model set the project owner used for the simulation. Its header identifies the parameter set as `T58F SPICE BSIM3` and contains a note that flicker-noise parameters were manually added from another process. Public redistribution permission remains a separate licensing question; see [models/README.md](../models/README.md).
