# Device models

The schematic expects a TSMC 180 nm SPICE model library at:

```text
models/tsmc018.lib
```

The attached schematic originally referenced a library under a personal Windows directory. The project copy uses a relative include so the repository is not tied to that computer.

The model library was not included with the supplied files. Obtain it from an authorized source and add it locally if its license allows redistribution. Do **not** commit proprietary foundry models or PDK files unless you have explicit permission.

The schematic also uses custom LTspice symbols named `cmosp` and `cmosn`. These symbols were not supplied. Install them locally in LTspice or adapt the schematic to compatible symbols and model names. Record any local-only setup here once confirmed.
