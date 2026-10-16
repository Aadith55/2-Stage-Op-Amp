# Device model library

The schematic includes:

```text
models/tsmc018.lib
```

This file is currently present in the public repository. Before sharing the repository further, confirm that the file's source and licence permit redistribution. A `.gitignore` entry does not remove files that are already tracked by Git.

## Provenance and suitability

The file is named `tsmc018.lib`, but its header identifies the parameter set as `T58F SPICE BSIM3`. It also contains a comment that flicker-noise parameters were manually added from another process. The filename alone is not evidence that it is an official or suitable TSMC 180 nm model. Confirm the provenance and compatibility with the intended design before describing it as such.

If redistribution is not explicitly permitted, remove the model file from the public repository and retain an authorized local copy for running the schematic. Do not commit proprietary foundry models or PDK files without permission.

The custom LTspice symbols are under `design/ltspice/sym/`. They reference the model names `CMOSP` and `CMOSN` with D, G, S, B terminals; confirm compatibility if LTspice produces netlist or model errors.
