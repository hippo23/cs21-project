# CS21 Project - Part B
This is a repository for CS21 - Part B

## Opcode Decomposition

| Type | Opcode | Func 3 | 1st Bit Function | 2nd Bit Function | 3rd Bit Function |
| --- | --- | --- | --- | --- | --- |
| A | 00000 | 000 - 011 | 1st bit specifies the ALU Operation | 2nd bit is used for ALUSrcA (ACC or CF:ACC) | 3rd bit is ignored |
| B | 00000 | 100 - 111 | 1st bit specifices RegWrite, ~(1st bit) specifices MemWrite | 2nd bit specifies desired MemAdd | 3rd bit is ignored |
| C | 00001 | 000 - 011 | 1st bit specifies ALUSrcA (Either ACC or CF + ACC) | 2nd bit specifies ALUOp (+ or -) | 3rd bit is ignored (thus far, I haven't debugged this one yet) |

## ALU Modes

1. 0000 is for rotation to the left
2. 0001 is for rotation to the right
   * There should probably be some trigger here so that the overflow bit can be outputted
3. 0010 is for addition
4. 0011 is for subtraction
5. 0100 is for AND
6. 0101 is for OR
7. 0110 is for XOR
8. 0111 is for rotation to the left WITH CF bit
9. 1000 is for rotation to the right WITH CF bit

## ResultSrc Modes

1. 00 is for the ALU output
2. 01 is for data-from-memory output

## AddSrc Modes

1. 0 is for RB:RA
2. 1 is for RD:RC

## ALUSrcA Modes

1. 00 should be for the currently-read register at ACC
2. 01 should be for Mem[MemAdd]
3. 10 should be for CF + ACC (again, precompute this)

## ALUSrcB Modes

1. 00 has no mapping yet, probably an immediate, 01 could be the memory, so on so forth

## CFSrc Modes

This is not implemented, but here's the idea:

1. 00 is for fixed zero
2. 01 is for fixed one.
3. 10 is for output from ALU, and so on and so forth
