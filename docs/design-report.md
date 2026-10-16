# Design summary and reported results

This page transcribes the key information from the supplied project report, *Two-Stage CMOS Operational Amplifier Design in 180nm Technology*. Figures below are reported by that document and have not been independently reproduced as part of preparing this repository.

## Objective and architecture

The design is a two-stage CMOS operational amplifier intended for a 10 pF capacitive load. The report discusses a 3 pF Miller compensation capacitor and a series nulling resistor used to improve phase margin.

## Reported specification table

| Parameter | Value in supplied report |
|---|---:|
| Technology | TSMC 180 nm |
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

These are source-reported figures. Add a new set of verified Bode plots and simulation settings under [results/](../results/) when the design is rerun using the correct model library.

## Schematic sizing values and a discrepancy to resolve

The attached LTspice schematic encodes the following dimensions:

| Devices | Width | Length |
|---|---:|---:|
| M1, M2 | 20 µm | 0.5 µm |
| M3 | 40 µm | 0.5 µm |
| M4, M5 | 10 µm | 0.5 µm |
| M6, M7 | 5 µm | 0.5 µm |
| M8 | 5 µm | 0.5 µm |

The report's transistor-sizing table leaves the width and length cells blank. Its text labels M8 as a second-stage bias device of approximately 3×, while the schematic gives M8 the same width as M6 and M7. Resolve the intended ratio and update the schematic and report together before presenting the dimensions as finalized.
