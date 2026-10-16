# Device Model Library

The circuit uses the model file:

```text
models/tsmc018.lib
```

The file's header identifies the parameter set as `T58F SPICE BSIM3`. It also includes a comment that flicker-noise parameters were manually added from another process. The filename alone does not establish the foundry or process provenance, so keep the model description aligned with the source documentation that came with the file.

## Redistribution

This repository is public. Check that the source and licence permit redistribution of the model file before sharing it publicly. A `.gitignore` rule does not remove files already tracked by Git. If redistribution is not allowed, remove the model file from the public repository and keep an authorized local copy for running the schematic.

The custom LTspice symbols are stored in `design/ltspice/sym/`. They reference `CMOSP` and `CMOSN` model names with D, G, S, B terminals.
