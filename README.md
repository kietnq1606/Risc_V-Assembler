# RISC-V Assembler

## Project Overview

A Python-based assembler that translates RISC-V assembly instructions into 32-bit machine code using the RISC-V Instruction Set Architecture (ISA).

**RISC-V Assembly → Assembler → 32-bit Machine Code**

## System Architecture

The assembler uses a **Two-Pass Architecture** with **Table-Driven Encoding**.

| Stage | Operation | Output |
|---|---|---|
| First Pass | Identify labels and calculate addresses | Symbol Table |
| Second Pass | Parse instructions and resolve operands | Instruction Fields |
| Encoding | Map and combine binary fields | Machine Code |

### Core Components

| Component | Function |
|---|---|
| Parser | Extract mnemonics and operands |
| Symbol Table | Map labels to addresses |
| Lookup Tables | Map instructions and registers to binary values |
| Encoder | Arrange bit fields into machine instructions |

## Instruction Encoding

### Instruction Formats

| Format | Description | Binary Structure (MSB → LSB) |
|---|---|---|
| R-Type | Register | funct7 · rs2 · rs1 · funct3 · rd · opcode |
| I-Type | Immediate | imm[11:0] · rs1 · funct3 · rd · opcode |
| S-Type | Store | imm[11:5] · rs2 · rs1 · funct3 · imm[4:0] · opcode |
| B-Type | Branch | imm[12,10:5] · rs2 · rs1 · funct3 · imm[4:1,11] · opcode |
| U-Type | Upper Immediate | imm[31:12] · rd · opcode |
| J-Type | Jump | imm[20,10:1,11,19:12] · rd · opcode |

### Encoding Process

| Assembly Element | Conversion |
|---|---|
| Mnemonic | 7-bit opcode |
| Register | 5-bit register index |
| Function | 3-bit funct3 / 7-bit funct7 |
| Immediate | Binary value |
| Label | PC-relative offset for branches and jumps |

All fields are combined according to the corresponding instruction format to generate the final **32-bit machine code**.
