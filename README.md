# Single-Cycle RISC-V Processor (Logisim-Evolution)

A fully functional **32-bit single-cycle RISC-V processor** implemented in [Logisim-Evolution v4.1.0](https://github.com/logisim-evolution/). Built as a computer architecture project to demonstrate the complete datapath of a single-cycle CPU.

---

## 📐 Supported Instructions

| Type | Instructions |
|------|-------------|
| R-Type | `add`, `sub`, `and`, `or` |
| I-Type | `addi`, `lw`, `jalr` |
| S-Type | `sw` |
| B-Type | `beq`, `bne` |
| U-Type | `lui`, `auipc` |
| J-Type | `jal` |

---

## 🗂️ Files

| File | Description |
|------|-------------|
| `riscv_single_cycle.circ` | Main Logisim-Evolution circuit file |
| `testbench.txt` | Assembly test program with expected outputs |

---

## 🧪 Testbench

The `testbench.txt` contains a 16-instruction test program loaded into the ROM. Each clock tick executes one instruction.

### Test Program (Assembly)

```text
0x00 | lui  x1,  0x12345       → x1 = 0x12345000
0x04 | auipc x2, 0x10          → x2 = PC + 0x10000 = 0x00010004
0x08 | addi x3, x0, 15         → x3 = 0x0000000F
0x0C | addi x4, x0, 10         → x4 = 0x0000000A
0x10 | sub  x5, x3, x4         → x5 = 0x00000005
0x14 | and  x6, x3, x4         → x6 = 0x0000000A
0x18 | or   x7, x3, x4         → x7 = 0x0000000F
0x1C | addi x8, x0, 64         → x8 = 0x00000040
0x20 | sw   x7, 0(x8)          → RAM[0x40] = 0x0000000F
0x24 | beq  x5, x4, 8          → not taken (5 ≠ 10)
0x28 | bne  x5, x4, 8          → taken → PC = 0x30
0x2C | addi x9, x0, 999        → skipped
0x30 | jal  x10, 12            → x10 = 0x34, PC → 0x3C
0x34 | addi x11, x0, 888       → x11 = 0x00000378
0x38 | jal  x0, 0              → infinite loop (skipped by jalr)
0x3C | jalr x0, x10, 0         → PC → 0x34
```

### Expected Final Register State
| Register | Value |
|----------|-------|
| x1 | `0x12345000` |
| x2 | `0x00010004` |
| x5 | `0x00000005` |
| x9 | `0x00000000` |
| x10 | `0x00000034` |
| x11 | `0x00000378` |
| RAM[0x40] | `0x0000000F` |

---

## 🚀 How to Run

1. Download and install [Logisim-Evolution v4.1.0](https://github.com/logisim-evolution/releases)
2. Open `riscv_single_cycle.circ` in Logisim-Evolution
3. The ROM is pre-loaded with the test program from `testbench.txt`
4. Use **Manual Clock Tick** (Ctrl+T) to step through each instruction
5. Observe register file and RAM values updating each tick

---

## 🏗️ Architecture Overview

- **Datapath**: Single-cycle (one instruction per clock cycle)
- **ISA**: RISC-V RV32I (subset)
- **Word size**: 32-bit
- **Register file**: 32 registers (x0–x31), x0 hardwired to 0
- **Memory**: Separate instruction memory (ROM) and data memory (RAM)
- **PC**: 32-bit program counter with support for branch and jump targets

---

## 🛠️ Tools Used

- [Logisim-Evolution v4.1.0](https://github.com/logisim-evolution/)

---

## 📜 License

This project was created for educational purposes as part of a Computer Architecture course.