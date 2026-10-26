# COMP 311 — Lab 3: RISC-V ALU

Build a 32-bit ALU in Digital. This repository contains unfinished circuits with named pins and local tests. You supply the logic and wiring.

**Due:** November 6, 2026, at 11:59 p.m.

[Read the lab handout](https://www.cs.unc.edu/~kakiryan/teaching/311-fa26/labs/lab3.html).

## Getting started

1. Open `boolean-unit.dig` in Digital.
2. Complete and test the sub-units in the order below.
3. Open `alu.dig` and connect your completed sub-units using **Components → Custom**.
4. Keep all five circuit files in this folder so custom components can be found.

You may move the supplied pins, but preserve their names and widths. The starter circuits intentionally have no logic or wiring; tests will not pass until you complete them.

## Circuit interfaces

| File | Inputs | Outputs |
|---|---|---|
| `boolean-unit.dig` | `A` (32), `B` (32), `Bool` (2) | `Out` (32) |
| `bidirectional-shifter.dig` | `A` (32), `B` (32), `ShiftOp` (2) | `Out` (32) |
| `add-sub-unit.dig` | `A` (32), `B` (32), `Sub` (1) | `Out` (32), `Sign` (1), `Overflow` (1) |
| `slt-unit.dig` | `Sign` (1), `Overflow` (1) | `Out` (1) |
| `alu.dig` | `A` (32), `B` (32), `ALUOp` (4) | `Result` (32), `FlagZ` (1) |

Parentheses give bit widths. The sub-unit controls use these encodings:

- `Bool`: `00` AND, `01` OR, `10` XOR.
- `ShiftOp`: `00` SLL, `01` SRL, `10` SRA.
- `Sub`: `0` ADD, `1` SUB.

Unused `Bool` and `ShiftOp` values are not tested. For shifts, **A is the value and B[4:0] is the shift amount**. SLT compares signed two's-complement operands using the sign and overflow of **A − B**.

## Final ALU operations

| ALUOp (binary) | Operation |
|---|---|
| `0000` | AND |
| `0001` | OR |
| `0010` | ADD |
| `0011` | XOR |
| `0100` | SLL |
| `0101` | SRL |
| `0110` | SUB |
| `0111` | SLT |
| `1000` | SRA |

`FlagZ` is 1 exactly when the selected `Result` is zero. SLT produces a 32-bit result of 0 or 1. All arithmetic results are truncated to 32 bits.

## Local tests

Each circuit includes a green Test block. Use Digital's test-case runner to run that circuit's tests after wiring it. The same cases are provided as readable text in `tests/`; those files use Digital test-case syntax and can be pasted into a Test block if needed.

| Circuit | Cases |
|---|---:|
| Boolean unit | 81 |
| Shifter | 105 |
| Add/sub unit | 54 |
| SLT unit | 4 |
| Full ALU | 262 |

Keep the supplied expected outputs unchanged. You may add additional tests. These are practice checks, not an exhaustive test of all possible inputs.

Optional command-line testing, if Java and Digital are installed:

```sh
java -cp /path/to/Digital.jar CLI test -circ alu.dig
```

Replace `/path/to/Digital.jar` with your installation's path. Substitute another circuit filename to test a sub-unit.

## Submission

Commit and push your completed circuits, and submit through the course's Lab 3 assignment on Gradescope following the posted submission instructions. Include all five `.dig` files and any additional custom circuit dependencies. Keep your working ALU for Lab 4.
