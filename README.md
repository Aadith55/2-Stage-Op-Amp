# Two-Stage CMOS Operational Amplifier

An LTspice project for a two-stage CMOS operational amplifier intended for a 10 pF capacitive load. The repository contains the circuit schematic, custom LTspice symbols, the model file used in the project, and simulation screenshots.

> **Validation status:** the project owner has opened and tested the schematic in LTspice and checked the AC performance measurements against the plots. The performance figures below are taken from the supplied report and checked by the owner; they were not re-simulated independently as part of this documentation edit.

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

The report attributes the poor uncompensated phase margin to a right-half-plane zero associated with the Miller capacitor and describes adding a series nulling resistor to improve stability. The numeric values above are report-derived and were checked by the project owner against their simulation plots.

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
3. The schematic includes `../../models/tsmc018.lib`, relative to the schematic directory. See [models/README.md](models/README.md) for the model provenance and redistribution note.
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

The supplied report's prose separately describes M8 as approximately 3×, but its transistor-sizing table leaves W/L blank. This repository documents **M8 = 5 µm**, the value used in the simulation, rather than changing it to match the ambiguous prose.

## Included results

- [AC analysis at 11 kΩ](results/figures/AC%20Analysis%20at%2011kOhm.png)
- [Uncompensated AC analysis](results/figures/AC%20analysis%20Uncompensated.png)
- [Transient output waveform](results/figures/Transient%20Analysis.png)

## Model-file note

The file committed as `models/tsmc018.lib` is the model set used for this project. Its header identifies the parameter set as **T58F SPICE BSIM3** and includes a note that flicker-noise parameters were manually added from another process. Confirm that the file may be redistributed publicly before sharing or reusing it outside the permissions under which you obtained it. See [models/README.md](models/README.md).
