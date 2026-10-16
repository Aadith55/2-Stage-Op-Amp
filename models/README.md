# Device Model Library

The circuit uses the SPICE model file `models/tsmc018.lib`.

The file contains BSIM3 Level 49 model definitions for the NMOS device `CMOSN` and PMOS device `CMOSP`. Its header identifies the parameter set as `T58F SPICE BSIM3 Version 3.1`, dated October 31, 2005. A comment in the file notes that flicker-noise parameters were added manually from another process.

The custom LTspice symbols in `design/ltspice/sym/` reference the `CMOSN` and `CMOSP` model names and use drain, gate, source, and bulk terminals.
