# Design summary and reported results

This page summarizes the supplied report, *Two-Stage CMOS Operational Amplifier Design in 180nm Technology*, and records the transistor dimensions encoded in the uploaded LTspice schematic. The performance figures below are transcribed from the report; related screenshots are stored in [results/figures/](../results/figures/).

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

## Compensation narrative from the report

The report states that the uncompensated Miller architecture exhibits poor phase margin, attributing the behavior to a right-half-plane zero associated with the capacitor's feed-forward path. It reports initial unity-gain bandwidth of 9.25 MHz and phase margin of 16.6°.

The report then describes a parametric SPICE sweep of a series nulling resistor and identifies 11 kΩ as the selected value. It reports compensated unity-gain bandwidth of 17.2 MHz and phase margin of 78.2°.

The figures are source-reported values and have not been independently re-simulated as part of this repository update. The uploaded plots can be inspected in [results/figures/](../results/figures/). Confirm the measurements from LTspice before describing the figures as independently reproduced.

## Transistor dimensions used in the simulation

The dimensions encoded in the uploaded schematic and confirmed by the project owner are:

| Devices | Width (W) | Length (L) |
|---|---:|---:|
| M1, M2 | 20 µm | 0.5 µm |
| M3 | 40 µm | 0.5 µm |
| M4, M5 | 10 µm | 0.5 µm |
| M6, M7 | 5 µm | 0.5 µm |
| M8 | 5 µm | 0.5 µm |

**M8 is documented as 5 µm wide**, matching the value used in the simulation. The supplied report's prose separately describes M8 as approximately 3× for second-stage bias, but the table leaves the transistor dimensions blank. This repository records the as-simulated width and does not alter it to match that ambiguous statement.

## Model provenance

The model file in the repository is named `tsmc018.lib`, but its header identifies the model set as `T58F SPICE BSIM3` and contains a note that flicker-noise parameters were manually added from another process. Confirm its source and suitability for this circuit before presenting it as a verified TSMC 180 nm model. Also confirm that the file's licence allows public redistribution.
