# Emulating the RISC-V ISA

## Emulation Background

1. To emulate a processor means to write software which reads the "machine code" of one processor architecture, and re-implement that functionality on a different architecture.
1. Game console emulators and Apple's Rosetta system are common examples.

## Code is Data

1. All RISC-V instructions are represented in one 32-bit integer of machine code. This is called an "instruction word"
1. Therefore, when running on your RISC-V guest, a pointer to a function is really a pointer to a sequence of `uint32_t`. That sequence is the machine code for the function.

## Register Names

1. In RISC-V there are 32 registers, named `x0` to `x31`. The machine code representation uses five bits each to name registers in an instruction word.
1. We have been using the ABI register names, but the assembler translates those into the real names of the registers. e.g. `ra` is `x1` and `a0` is `x10`
1. See the Calling Convention section of the reference card for the full mapping of register names.

## Opcodes

1. There are seven core opcodes (and one extension for `mul`). In the RISC-V spec, see Chapter 24 RV3264G Instruction Set Listings. Opcodes are in bits 0-6 of every RISC-V instruction
    1. R-type instructions (opcode `0b0110011`) are instructions which have two source registers
    1. I-type instructions (opcode `0b0010011`) are instructions which have an 12-bit immediate encoded in the instruction
        1. `ld` instructions have the same format as I-type, but have opcode `0b0000011`
        1. `jalr` (aka `ret`) instructions have the same format as I-type, but have opcode `0b1100111`
    1. S-type instructions (opcode `0b0100011`) are `st` instructions (no `rd`)
    1. SB-type instructions (opcode `0b1100011`) are conditional branch instructions (see also pseudo-instructions)
    1. UJ-type instructions (opcode `0b1101111`) are jump instructions `j` and `jal` (aka `call`)


## Func3 and Func7

1. The three bits from bit 12 to bit 14 are called `func3`. They are used to identify a specific instruction within an opcode family
1. The seven bits from bit 25 to bit 31 are called `func7` and may also be used to identify an instruction
1. The details are in the table on page 130 of the RISC-V spec.

## Pseudo-instructions

1. `li`, `call`, `ret`

## Immediate Values
1. Ranges and assembly using SHIFT and OR
1. All immediate values are signed, and must be sign-extended out to 64 bits using an `int64_t`

## Branch Instructions
1. Branch target calculation
1. Unconditional branch
1. Conditional branch

## Load and Store Instructions

1. `ld` decoding
1. Memory target calculation
1. Casting the target to the correct size