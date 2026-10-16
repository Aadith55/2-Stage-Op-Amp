# Two-Stage CMOS Operational Amplifier

A two-stage CMOS op-amp design targeting the TSMC 180 nm process, captured in LTspice. The project focuses on open-loop gain and frequency compensation for a 10 pF capacitive load.

> **Simulation status:** the schematic has been organized for this repository, but it has not been re-run here. Reproduction still depends on the TSMC 180 nm model library and the custom LTspice symbols used by the original design. The performance figures below are reported in the supplied project report.

## Reported specifications

| Parameter | Reported value |
|---|---:|
| Process | TSMC 180 nm |
| Supply | 1.8 V / 0 V |
| Input common-mode voltage | 0.9 V |
| Load capacitance | 10 pF |
| Open-loop DC gain | 80 dB |
| Compensated unity-gain bandwidth | 17.2 MHz |
| Compensated phase margin | 78.2° |
| Miller capacitor | 3 pF |
| Series nulling resistor | 11 kΩ |

The supplied report gives the uncompensated response as **9.25 MHz unity-gain bandwidth** and **16.6° phase margin**. It attributes the poor phase margin to a right-half-plane zero associated with the Miller capacitor. A series nulling resistor was swept to improve stability; the report identifies 11 kΩ as the selected value.

## Repository layout

```text
.
├── README.md
├── .gitignore
├── design/
│   └── ltspice/
│       ├── 2-stage-opamp.asc
│       └── README.md
├── docs/
│   └── design-report.md
├── models/
│   └── README.md
└── results/
    ├── README.md
    └── figures/
        └── README.md
```

## Getting started

1. Install LTspice.
2. Add the TSMC 180 nm model library locally as `models/tsmc018.lib`. See [models/README.md](models/README.md); do not commit foundry models unless their license explicitly permits redistribution.
3. Make sure the custom symbol files referenced by the schematic (`cmosp` and `cmosn`) are available in your LTspice symbol library. See [design/ltspice/README.md](design/ltspice/README.md).
4. Open `design/ltspice/2-stage-opamp.asc` in LTspice and run the AC sweep. The schematic sweeps `Rz` from 1 kΩ to 20 kΩ in 1 kΩ steps.
5. Save the Bode plot and transient response screenshots under `results/figures/`, with the test setup and the selected `Rz` value recorded.

For a transient run, switch the active analysis directive from `.ac dec 100 10 100Meg` to `.tran 10m`, then run the simulation again.

## Transistor dimensions in the supplied schematic

| Devices | Schematic dimensions (W/L) | Reported function |
|---|---:|---|
| M1, M2 | 20 µm / 0.5 µm | PMOS active loads |
| M3 | 40 µm / 0.5 µm | Second-stage PMOS amplifier |
| M4, M5 | 10 µm / 0.5 µm | NMOS differential input pair |
| M6, M7 | 5 µm / 0.5 µm | Tail-current mirror |
| M8 | 5 µm / 0.5 µm | Second-stage bias |

**Sizing note:** the report's transistor-sizing table leaves dimensions blank and describes M8 as approximately 3× for second-stage bias. The attached schematic instead sets M8 to 5 µm, the same width as M6 and M7. Confirm the intended sizing before treating the table above as final.

## Important limitations

- The original schematic referenced a TSMC model library at a machine-specific Windows path. That path has been changed to a repository-relative include, `../../models/tsmc018.lib`; the library itself is not included.
- The custom `cmosp` and `cmosn` symbol definitions were not among the supplied files.
- The report's simulation values are transcribed as reported, not independently verified in this environment.
- Result screenshots and simulation logs still need to be added under `results/`.

See [docs/design-report.md](docs/design-report.md) for the report-derived design summary and comparison of uncompensated versus compensated results.
