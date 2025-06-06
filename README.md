# CS21 Project - Part B
This is a repository for CS21 - Part B

## Opcode Decomposition

| Type | Opcode | Func 3 | 1st Bit Function | 2nd Bit Function | 3rd Bit Function | Exception Details |
| --- | --- | --- | --- | --- | --- |  --- |
| Rotation Operations | 00000 | 000 - 011 | 1st bit specifies the ALU Operation | 2nd bit is used for ALUSrcA (ACC or CF:ACC) | 3rd bit is ignored | --- | 
| ACC to \ from Mem | 00000 | 100 - 111 | 1st bit specifices RegWrite, ~(1st bit) specifices MemWrite | 2nd bit specifies desired MemAdd | 3rd bit is ignored | --- |
| ACC from Mem +- ACC and Mem +- ACC + CF   | 00001 | 000 - 011 | 1st bit specifies ALUSrcA (Either ACC or CF + ACC) | 2nd bit specifies ALUOp (+ or -) | 3rd bit is ignored (thus far, I haven't debugged this one yet) | --- |
| Basic Mem INC and DEC | 00001 | 100 - 111 | 1st bit specifies the operation | 2nd bit specifies the MemAdd | --- | --- |
| General Purpose Register INC and DEC | 0001X | --- |  --- | --- | --- | Refer to CS21 docs for function |
| Bitwise Operations | 00011 | (010 - 00) OR (101 - 111) | --- | --- | --- | The value of the last three bits are used directly to determine operation and destination |
| ACC to \ from General Purpose Registers | 0010X | --- | --- | --- | --- | Refer to CS21 docs for function | 
| Clear and set CF | 00101 | 010 - 011 | 1st bit is used to determine if we are adding 0 or 1 | --- | --- | --- |
| 12 bits of PC to temp, temp to 0 | 00101 | 110 | --- | --- | --- | Only one func3, so we can hardcode what happens |

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
10. 1011 is for nonzero arg2 check
11. 1100 is for zero arg2 check
12. 1101 is for zero CF check
13. 1110 is for nonzero CF check
14. 1111 is for bitwise nonzero check

## ResultSrc Modes

1. 00 is for the ALU output
2. 01 is for data-from-memory output
3. 10 is for the currently-read general purpose register

## AddSrc Modes

1. 0 is for RB:RA
2. 1 is for RD:RC

## ALUSrcA Modes

1. 00 should be for the currently-read register at ACC
2. 01 should be for Mem[MemAdd]
3. 10 should be for CF + ACC (again, precompute this)
4. 11 is for the currently-read general purpose register

## ALUSrcB Modes

1. 00 is for Mem[MemAdd]
2. 01 is for the immediate that is entered
3. 10 is for the general purpose register used in branching
4. 11 is for constant 1

## CFSrc Modes

1. 00 is for fixed zero
2. 01 is for fixed one.
3. 10 is for the overflow / underflow bit from an ALU operation
4. 11 is for the NBit that happens during a rotate ALU operation

## PCSrc Modes
1. 00 is for PC + 2
2. 01 is for last 12 bits = TEMP
3. 10 is for last 11 bits = imm
4. 11 is for last 12 bits = imm

## TempSrc Modes
1. 00 is for PC + 2
2. 01 is for constant zero

## MemSrc Modes
1. 00 is for ALU output
2. 01 is for ACC output
