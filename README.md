MiniMIPS CPU
Custom MATLAB Processor

1. Introduction
MiniMIPS is a fully simulated CPU implemented entirely in MATLAB/Simulink. It follows a classic 5-stage pipeline architecture and supports a custom instruction set, complete data path, control logic, and cycle-accurate execution. The goal of the project was to create a functioning processor model capable of running real assembly programs and reflecting hardware-accurate behavior, including stalls, forwarding, and branch flow.

2. Architecture Overview
Pipeline Stages
MiniMIPS implements the traditional 5 hardware pipeline stages:

Instruction Fetch (IF): program counter logic, instruction memory, PC update
Instruction Decode (ID): full decoder, immediate generation, register file reads
Execute (EX): ALU for arithmetic/logical operations (add, sub, xor, slt, shifts)
Memory Access (MEM): load/store operations on a simulated memory
Writeback (WB): writing ALU or memory results into the register file
3. Instruction Set Architecture (ISA)
The project includes a complete ISA inspired by MIPS, with:

Arithmetic and logical instructions
Load/store instructions
Branch and jump operations
Pseudo-instructions for easier testing
Binary encoding formats defined and decoded in ID stage
All instructions were assembled using small MATLAB scripts that served as a lightweight assembler.

4. Control Logic, Hazards, & Pipeline Behavior
Hazard Detection
A detection unit identifies read-after-write (RAW) hazards and triggers stalls where needed.

Forwarding Unit
Forwarding paths bypass ALU results to upcoming instructions to avoid unnecessary stalls.

Branch Handling
The processor includes a simple branch prediction and branch resolution system to minimize pipeline flushes.

FSM-Based Control Unit
A MATLAB-modeled finite state machine generates control signals for every instruction type.

5. ALU & Data Path Components
ALU
Supports:

Addition
Subtraction
Comparisons (slt)
Bitwise ops (xor)
Logical and arithmetic shifting
Arithmetic operations were optimized by reorganizing internal logic to reduce simulated cycle latency.

Register File
32 registers with dual-read and single-write capability, updated precisely at the WB stage.

Memory Subsystem
Simulated byte-addressable memory with separate I-MEM and D-MEM modules.

6. Simulation & Validation
Cycle-Accurate Logging
The simulator records:

PC at every cycle
Register writebacks
Memory reads/writes
Stall cycles and pipeline bubble insertions
Assembly Program Testing
Over 100 assembly programs were executed to verify correctness, including:

Fibonacci
Factorial
Array operations
Sorting routines
Matrix multiplication
Branch-heavy loops
Memory-intensive workloads
These validated the pipeline, control flow, and hazard logic under a wide range of behaviors.

7. Overall Project Focus
MiniMIPS focuses on building a realistic, functioning CPU model within MATLAB—capturing how instructions move through a pipeline, how hazards are resolved, and how control/memory subsystems interact during execution. The result is a full processor capable of running non-trivial programs at cycle-accurate granularity.
