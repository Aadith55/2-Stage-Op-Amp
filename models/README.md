# Device model library

The schematic includes:

```text
models/tsmc018.lib
```

This is the model file used for the project simulation, as confirmed by the project owner.

## Model details and redistribution

The file is named `tsmc018.lib`, but its header identifies the parameter set as `T58F SPICE BSIM3`. It also contains a comment that flicker-noise parameters were manually added from another process. This describes the file's contents; it does not change the fact that it is the model set used for the reported simulation.

The repository is public, so confirm that the file's source and licence permit redistribution. A `.gitignore` entry does not remove a file that is already tracked by Git. If redistribution is not permitted, remove the model file from the public repository and retain an authorized local copy for running the schematic.

The custom LTspice symbols are under `design/ltspice/sym/`. They reference model names `CMOSP` and `CMOSN` with D, G, S, B terminals.
