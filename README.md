# Two-Stage CMOS Operational Amplifier

An LTspice project for a two-stage CMOS operational amplifier intended for a 10 pF capacitive load. The repository contains the circuit schematic, its custom LTspice symbols, a SPICE model file, and the uploaded simulation screenshots.

> **Reproducibility note:** the repository contents have been organized, but the current circuit has not been independently re-simulated as part of this documentation update. Treat numerical performance values as reported by the supplied report or shown in the uploaded plots, as identified below.

## Reported specifications

| Parameter | Value in supplied report |
|---|---:|
| Technology target | 180 nm |
| Supply | 1.8 V / 0 V |
| Input common-mode voltage | 0.9 V |
| Load capacitance | 10 pF |
| Open-loop DC gain | 80 dB |
| Uncompensated unity-gain bandwidth | 9.25 MHz |
| Uncompensated phase margin | 16.6° |
| Compensated unity-gain bandwidth | 17.2 MHz |
| Compensated phase margin | 78.2° |
| Miller capacitor | 3 pF |
| Series nulling resistor selected in the report | 11 kΩ |

The report attributes the poor uncompensated phase margin to a right-half-plane zero associated with the Miller capacitor and describes adding a series nulling resistor to improve stability. The figures in the table above are transcribed from the supplied report; verify measurements against the current LTspice plots before presenting them as independently reproduced results.

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
3. The schematic includes `../../models/tsmc018.lib`, relative to the schematic directory. Read [models/README.md](models/README.md) for the model-file provenance and redistribution caveat.
4. The custom transistor symbols `cmosp` and `cmosn` are stored in `design/ltspice/sym/`. If your LTspice installation does not resolve these relative symbol references, configure that directory in its symbol search path.
5. The schematic currently has transient analysis enabled and AC analysis commented out. To run AC analysis, comment out `.tran 10m` and enable `.ac dec 100 10 100Meg`.
6. The directive `.step param Rz 1k 20k 1k` sweeps the compensation resistance. Use **View → Step Legend** in the waveform viewer to identify the trace for `Rz=11k`. For a single 11 kΩ run, replace the sweep directive with `.param Rz=11k`.

## Transistor dimensions used in the simulation

The following dimensions are encoded in the uploaded schematic and reflect the values used in the simulation, as confirmed by the project owner.

| Devices | Width (W) | Length (L) | Function |
|---|---:|---:|---|
| M1, M2 | 20 µm | 0.5 µm | PMOS active loads |
| M3 | 40 µm | 0.5 µm | Second-stage PMOS amplifier |
| M4, M5 | 10 µm | 0.5 µm | NMOS differential input pair |
| M6, M7 | 5 µm | 0.5 µm | Tail-current mirror |
| M8 | 5 µm | 0.5 µm | Second-stage bias |

The supplied report's prose separately describes M8 as approximately 3×, but its transistor-sizing table leaves W/L blank. This repository documents **M8 = 5 µm**, which is the value used in the simulation, rather than changing it to match the ambiguous prose.

## Included results

- [AC analysis at 11 kΩ](results/figures/AC%20Analysis%20at%2011kOhm.png)
- [Uncompensated AC analysis](results/figures/AC%20analysis%20Uncompensated.png)
- [Transient output waveform](results/figures/Transient%20Analysis.png)

Keep the plots as direct LTspice exports and include legible axes, trace legends, and cursor measurements wherever they support a reported value.

## Model-file note

The file committed as `models/tsmc018.lib` has a header identifying the model set as **T58F SPICE BSIM3** and includes a note that flicker-noise parameters were manually added from another process. Confirm the file's provenance, suitability for this design, and permission to redistribute it publicly before describing it as an official TSMC 180 nm model or sharing the repository further. See [models/README.md](models/README.md).
