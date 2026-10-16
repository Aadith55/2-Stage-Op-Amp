# Two-Stage CMOS Operational Amplifier

This project covers the design and LTspice simulation of a two-stage CMOS operational amplifier for a 10 pF capacitive load. It includes the circuit schematic, custom transistor symbols, the SPICE model file used for the simulation, and AC and transient analysis plots.

## Design specifications

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

The uncompensated circuit has poor phase margin due to a right-half-plane zero associated with the Miller capacitor. A series nulling resistor was swept in LTspice to improve stability. With (R_z = 11\,\text{k}\Omega), the recorded AC response shows improved phase margin and higher unity-gain bandwidth.

## Repository layout

```text
.
├── README.md
├── .gitignore
├── design/
│   └── ltspice/
│       ├── 2-Stage op-Amp.asc
│       ├── README.md
│       └── sym/
│           ├── cmosn.asy
│           ├── cmosp.asy
│           └── README.md
├── docs/
│   └── design-report.md
├── models/
│   ├── README.md
│   └── tsmc018.lib
└── results/
    ├── README.md
    └── figures/
        ├── AC Analysis at 11kOhm.png
        ├── AC analysis Uncompensated.png
        ├── Transient Analysis.png
        └── README.md
```

## Getting started

1. Install LTspice.
2. Open `design/ltspice/2-Stage op-Amp.asc`.
3. The schematic includes `../../models/tsmc018.lib`, relative to the schematic directory. See [models/README.md](models/README.md) for model details.
4. The custom symbols `cmosp` and `cmosn` are in `design/ltspice/sym/`. If LTspice does not resolve these relative symbol references, add that directory to its symbol search path.
5. The schematic has transient analysis enabled and AC analysis commented out. To run AC analysis, comment out `.tran 10m` and enable `.ac dec 100 10 100Meg`.
6. The directive `.step param Rz 1k 20k 1k` sweeps the compensation resistance from 1 kΩ to 20 kΩ. Use **View → Step Legend** to identify the `Rz=11k` trace. To simulate only that value, replace the sweep directive with `.param Rz=11k`.

## Transistor dimensions

The following dimensions are used in the circuit:

| Devices | Width (W) | Length (L) | Function |
|---|---:|---:|---|
| M1, M2 | 20 µm | 0.5 µm | PMOS active loads |
| M3 | 40 µm | 0.5 µm | Second-stage PMOS amplifier |
| M4, M5 | 10 µm | 0.5 µm | NMOS differential input pair |
| M6, M7 | 5 µm | 0.5 µm | Tail-current mirror |
| M8 | 5 µm | 0.5 µm | Second-stage bias |

M8 is set to 5 µm in the simulated circuit. A separate design note describes the second-stage bias device as approximately 3×, but the schematic and simulation use the 5 µm value shown above.

## Simulation results

- [AC analysis at 11 kΩ](results/figures/AC%20Analysis%20at%2011kOhm.png)
- [Uncompensated AC analysis](results/figures/AC%20analysis%20Uncompensated.png)
- [Transient output waveform](results/figures/Transient%20Analysis.png)

## Model file

The circuit uses `models/tsmc018.lib`, which contains the BSIM3 Level 49 definitions used by the custom `CMOSN` and `CMOSP` symbols. Its header identifies the parameter set as T58F SPICE BSIM3 Version 3.1. See [models/README.md](models/README.md) for details.
