# RISC-V RV32I Assembler & Linker

A two-pass assembler and a linking loader for a subset of the **RISC-V RV32I** instruction set. Both tools are written in Python with Tkinter GUIs. The linked program runs on the **PicoRV32** soft-core in Verilog simulation and on a Tang Nano 9K FPGA.

> Team project (4 students) for the *System Programming* course (BIL302), Sakarya University of Applied Sciences. The course report is included as a PDF.

## Features

### Assembler (`Pico_Assembler_SUBU`)
- **Two-pass assembly.** Pass 1 builds the symbol table (SYMTAB); pass 2 encodes the instructions.
- **Standard RV32I machine-code encoding** for 13 instructions:
  - R-type: `ADD`, `SUB`, `AND`, `OR`, `XOR`
  - I-type: `ADDI`, `ANDI`, `ORI`, `LW`
  - S-type: `SW`
  - B-type: `BEQ`, `BNE`
  - J-type: `JAL`
- **Directives:** `START`, `END`, `CSECT`, `EXTDEF`, `EXTREF`, `WORD`, `RESW`, `.TEXT`, `.DATA`, `.WORD`, `.SPACE`.
- **Separate modules.** Exported (`EXTDEF`) and external (`EXTREF`) symbols, with relocation records for the linker.
- **Error detection:** undefined or duplicate labels, invalid mnemonics and operands, address overflow and malformed directives.
- **Tkinter GUI:** a code editor, file mode, and a listing and SYMTAB view.

### Linker (`Pico_Linker_SUBU`)
- **Two-pass linking loader.** It builds the external symbol table (ESTAB), resolves external references and applies relocations.
- **Multiple modules.** It links several `.obj` modules into one memory image.
- **Outputs:** `ESTAB.txt`, `output.mem` (for Verilog `$readmemh`) and `output.hex`.

### FPGA (`Pico_Linker_SUBU/FPGA`)
- `top.v` loads `output.mem` into BRAM and runs it on PicoRV32. A memory-mapped store drives the on-board LEDs.
- `tb_top.v` is the testbench for waveform simulation (27 MHz clock, as on the Tang Nano 9K).
- `tangnano9k.cst` holds the pin constraints for the Tang Nano 9K.

## Screenshots

![Assembler error handling](Pico_Assembler_SUBU/test_g%C3%B6r%C3%BCnt%C3%BCleri/NegatifAdres%20-%20Kopya.png)

<!-- Add a GUI screenshot or GTKWave capture here. -->

## Getting started

Requirements: Python 3.10+ (Tkinter is included with the standard installer). For simulation you also need a Verilog simulator and GTKWave; for the board you need the Gowin IDE.

```bash
git clone https://github.com/charafeddine99/riscv-assembler-linker.git
cd riscv-assembler-linker

# 1. Assemble each module (.asm → .obj)
python Pico_Assembler_SUBU/launcher.py

# 2. Link the object files (.obj → output.mem / output.hex)
python Pico_Linker_SUBU/launcher.py
```

Example of a multi-module source (from `Pico_Assembler_SUBU/kullandimiz assembler kaynak kodu.txt`):

```asm
MAIN   CSECT
       EXTDEF RE1
       EXTREF GET42
BASLA  JAL x1, GET42
LOGIC  CSECT
       EXTDEF GET42
GET42  ADDI x10, x0, 42
```

## Project structure

```text
├── Pico_Assembler_SUBU/
│   ├── launcher.py          # Tkinter GUI
│   └── src/                 # parser, encoder, assembler core, error handling
├── Pico_Linker_SUBU/
│   ├── launcher.py          # Tkinter GUI
│   ├── src/                 # object-file parser, linker core
│   └── FPGA/                # top.v, tb_top.v, picorv32.v, tangnano9k.cst
├── README.txt               # original project notes (Turkish)
└── BIL302_PROJE2_*.pdf      # course report
```

## Related

[Pico-Assembler-Linker-Loader-FPGA](https://github.com/charafeddine99/Pico-Assembler-Linker-Loader-FPGA) is the follow-up project. It adds a UART loader, so programs can be sent to the FPGA at run time without re-synthesis.

## Credits

The PicoRV32 core (`picorv32.v`) is by Claire Xenia Wolf ([YosysHQ/picorv32](https://github.com/YosysHQ/picorv32)), under the ISC license.

## License

[MIT](LICENSE). This covers the project's own code.
