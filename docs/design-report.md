# Two-Stage CMOS Operational Amplifier: Design Summary

This document describes the two-stage CMOS op-amp, its transistor dimensions, and the AC and transient simulation results.

## Objective and architecture

The circuit is designed for a 10 pF capacitive load. It uses a 3 pF Miller compensation capacitor and a series nulling resistor to improve phase margin.

## Design specifications and results

| Parameter | Value |
|---|---:|
| Process target | 180 nm |
| Supply voltage | 1.8 V / 0 V |
| Input common-mode voltage | 0.9 V |
| Load capacitance | 10 pF |
| Open-loop DC gain | 80 dB |
| Uncompensated unity-gain bandwidth | 9.25 MHz |
| Uncompensated phase margin | 16.6° |
| Compensated unity-gain bandwidth | 17.2 MHz |
| Compensated phase margin | 78.2° |
| Miller compensation capacitor | 3 pF |
| Selected series nulling resistor | 11 kΩ |

The uncompensated Miller architecture shows poor phase margin. The feed-forward path through the Miller capacitor contributes a right-half-plane zero, adding phase lag. The uncompensated response has a reported unity-gain bandwidth of 9.25 MHz and phase margin of 16.6°.

A parametric SPICE sweep was used to evaluate the series nulling resistor. The selected value is 11 kΩ. The compensated response shows a unity-gain bandwidth of 17.2 MHz and phase margin of 78.2°. Simulation plots are available in [results/figures/](../results/figures/).

## Transistor dimensions

The following width and length values are used in the LTspice schematic:

| Devices | Width (W) | Length (L) |
|---|---:|---:|
| M1, M2 | 20 µm | 0.5 µm |
| M3 | 40 µm | 0.5 µm |
| M4, M5 | 10 µm | 0.5 µm |
| M6, M7 | 5 µm | 0.5 µm |
| M8 | 5 µm | 0.5 µm |

M8 is set to 5 µm in the simulated circuit. A separate note describes the second-stage bias device as approximately 3×, but the circuit and simulation use the 5 µm width listed here.

## Model file

The circuit uses `models/tsmc018.lib`, which contains BSIM3 Level 49 model definitions for `CMOSN` and `CMOSP`. The file header identifies the parameter set as T58F SPICE BSIM3 Version 3.1. See [models/README.md](../models/README.md) for the model details.
