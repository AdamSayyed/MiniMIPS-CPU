# MiniMIPS CPU — Custom MATLAB/Simulink Processor

MiniMIPS is a fully simulated 32-bit CPU implemented entirely in **MATLAB** and **Simulink**, featuring a classic **5-stage pipeline**, custom instruction set, cycle-accurate execution, and full data-path/control-path design.  
The processor executes real assembly programs and models hardware-accurate behavior including hazards, forwarding, branch handling, and stalls.

---

## 1. Introduction

MiniMIPS was built to demonstrate core computer architecture concepts using MATLAB/Simulink.  
The CPU features:

- A functioning 5-stage pipeline  
- A MIPS-inspired instruction set  
- Hazard detection + forwarding  
- Custom assembler  
- Logging of cycle-by-cycle state  

The processor runs real assembly programs and produces cycle-accurate execution traces.

---

## 2. Architecture Overview

MiniMIPS implements the standard **5 hardware pipeline stages**:

### **Instruction Fetch (IF)**
- Program Counter (PC) logic  
- Instruction Memory (I-MEM)  
- PC update and sequential flow  

### **Instruction Decode (ID)**
- Full instruction decoder  
- Immediate generation  
- Register File reads  

### **Execute (EX)**
- ALU operations  
- Branch evaluation  
- Effective address calculations  

### **Memory Access (MEM)**
- Loads and stores on a simulated byte-addressable D-MEM  

### **Writeback (WB)**
- Writing results back to the register file  

---

## 3. Instruction Set Architecture (ISA)

The MiniMIPS ISA is inspired by classic MIPS and includes:

### **Arithmetic & Logic**
- `add`, `sub`, `xor`, `slt`, `sll`, `srl`, `sra`

### **Memory Access**
- `lw`, `sw`

### **Control Flow**
- `beq`, `bne`, `j`, `jr`, `jal`

### **Pseudo-Instructions**
Used primarily for testing and assembly convenience.

Binary encodings are defined manually, and a MATLAB-based assembler converts `.asm` files into executable machine code.

---

## 4. Control Logic, Hazards & Pipeline Behavior

### **Hazard Detection Unit**
- Detects RAW hazards  
- Inserts pipeline stalls when required  

### **Forwarding Unit**
- Forwards ALU and MEM results to dependent instructions  
- Reduces unnecessary stalls  

### **Branch Handling**
- Branch resolution in EX stage  
- Simple prediction strategy  
- Pipeline flush logic implemented  

### **Control Unit (FSM-Based)**
The FSM generates all necessary control signals:

- ALU operation codes  
- RegWrite, MemRead, MemWrite  
- Branch and jump signals  
- Forwarding/stall signals  

---

## 5. Data Path Components

### **ALU**
Supports:
- Addition and subtraction  
- Bitwise logic  
- Set-on-less-than  
- Logical/arithmetic shifts  

ALU logic is optimized to reduce simulated cycle latency.

### **Register File**
- 32 registers  
- Dual read ports  
- Single synchronous write port (WB stage)

### **Memory System**
- Separate instruction (I-MEM) and data memory (D-MEM)  
- Byte-addressable  
- Word-aligned access for loads/stores  

---

## 6. Simulation & Validation

### **Cycle-Accurate Logging**
MiniMIPS logs the following for every cycle:

- PC value  
- Pipeline register values  
- Register writebacks  
- Memory reads/writes  
- Stall cycles and pipeline bubbles  

### **Assembly Program Tests**
More than **100** assembly programs were used for validation:

- Fibonacci  
- Factorial  
- Sorting  
- Array operations  
- Matrix multiplication  
- Branch-heavy loops  
- Memory-intensive workloads  

These tests validated both correctness and full pipeline behavior.

---

## 7. Project Goals

MiniMIPS was designed to:

- Provide a complete, realistic CPU pipeline model in MATLAB  
- Accurately demonstrate hazard detection & forwarding  
- Show interactions between control logic, datapath, and memory  
- Run non-trivial assembly programs with cycle accuracy  
- Serve as an educational and research tool for CPU architecture  

---


