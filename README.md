## Assembly to Object Code Assembler and Simulator

This project consists of an assembler and a simulator for a custom Instruction Set Architecture (ISA). The assembler converts human-readable assembly code into machine-readable object code, and the simulator executes the object code, simulating a simple CPU. The ISA supports basic arithmetic and logical operations, label-based jumps, and variable storage.

### Features
- Handles all supported instructions.
- Manages labels and variables.
- Generates distinct readable errors for illegal instructions.
- Produces a binary file as output if the assembly code is error-free.
- Simulates the execution of the binary code and outputs the state of the program counter and registers after each instruction.

### Supported Instructions
- Arithmetic operations: `ADD`, `SUB`.
- Logical operations: `AND`, `OR`.
- Data transfer: `MOV`.
- Control flow: `JMP`.

### Usage

#### Assembler
1. **Input**: A text file containing the assembly code.
2. **Output**: A text file with the corresponding binary object code.
3. **Errors**: Reports syntax errors, typos, use of undefined variables or labels, illegal register or immediate values, and incorrect use of `hlt`.

#### Simulator
1. **Input**: A binary file generated by the assembler.
2. **Output**: 
   - The state of the program counter and registers after each instruction execution.
   - A memory dump of the whole memory after the program halts.

### File Structure

1. `assembler.py`: Converts assembly code to binary object code.
2. `simulator.py`: Executes the binary object code.
