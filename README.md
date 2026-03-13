# Arithmetic Logic Unit &nbsp; <img src="https://github.com/user-attachments/assets/52a60221-cf09-4f87-b8fd-c5ce991e7918" width="40" height="40" align="top" />

An ALU architecture designed to perform various operations on two 8-bit inputs according to an opcode
 
## Details 
- The full Quartus project is in `Quartus Project/`, while the indiviudal VHDL components are in `Components/`.
- This project was created in `Quartus II 13.0sp1` using mainly VHDL, and implemented into an FPGA board *(Cyclone- II EP2C35F672C6 FPGA)*
- Each component was individually designed with VHDL, then the full architecture was connected together using block diagrams


## Architecture 

This design is comprised of several key components:

- Two **8-bit D-latches** (for storing inputs)
- A **4:16 decoder**
- A **Finite State Machine** (FSM)
- The **Arithmetic Logic Unit** (ALU)
- Two **seven-segment display drivers**

## Truth Tables and Block Diagrams 

Listed below are the truth tables and block diagrams of every component in this design:

---
### 8bit D-Latch

<div style="display:flex; justify-content:center; align-items:center; gap:30px;">
  
| Clock | D   | Q       |
| ----- | --- | ------- |
| 1     | 1   | 1       |
| 1     | 0   | 0       |
| 0     | 1   | `Qpast` |
| 0     | 0   | `Qpast` |

<img width="300" alt="d latch" src="https://github.com/user-attachments/assets/d656db7f-6d45-4c5a-8389-6bfec4f41809" />

</div>

---
### 4:16 Decoder

<div style="display:flex; justify-content:center; align-items:center; gap:30px;">
  
| Enable | w₃w₂w₁w₀ | Y₁₅Y₁₄Y₁₃Y₁₂Y₁₁Y₁₀Y₉Y₈Y₇Y₆Y₅Y₄Y₃Y₂Y₁Y₀ |
| ------ | -------- | -------------------------------------- |
| 1      | 0000     | 0000000000000001                       |
| 1      | 0001     | 0000000000000010                       |
| 1      | 0010     | 0000000000000100                       |
| 1      | 0011     | 0000000000001000                       |
| 1      | 0100     | 0000000000010000                       |
| 1      | 0101     | 0000000000100000                       |
| 1      | 0110     | 0000000001000000                       |
| 1      | 0111     | 0000000010000000                       |
| 1      | 1000     | 0000000100000000                       |
| 1      | 1001     | 0000001000000000                       |
| 1      | 1010     | 0000010000000000                       |
| 1      | 1011     | 0000100000000000                       |
| 1      | 1100     | 0001000000000000                       |
| 1      | 1101     | 0010000000000000                       |
| 1      | 1110     | 0100000000000000                       |
| 1      | 1111     | 1000000000000000                       |
| 0      | dddd     | 0000000000000000                       |

<img width="400" alt="d latch" src="https://github.com/user-attachments/assets/1252ddaf-5b21-4353-829e-a02d123298ec" />

</div>

---
### Finite State Machine

<div style="display:flex; justify-content:center; align-items:center; gap:30px;">
  
| Current State (y₃y₂y₁y₀) | Next State W=0 (Y₃Y₂Y₁Y₀) | Next State W=1 (Y₃Y₂Y₁Y₀) | Output (Z₃Z₂Z₁Z₀) |
| ------------------------ | ------------------------- | ------------------------- | ----------------- |
| 0000                     | 0000                      | 0001                      | 0000 (0)          |
| 0001                     | 0001                      | 0010                      | 0001 (1)          |
| 0010                     | 0010                      | 0011                      | 0010 (2)          |
| 0011                     | 0011                      | 0100                      | 0101 (5)          |
| 0100                     | 0100                      | 0101                      | 0111 (7)          |
| 0101                     | 0101                      | 0110                      | 0100 (4)          |
| 0110                     | 0110                      | 0111                      | 0010 (2)          |
| 0111                     | 0111                      | 0000                      | 0100 (4)          |
| 1ddd                     | XXXX                      | XXXX                      | XXXX              |


<img width="400" alt="fsm" src="https://github.com/user-attachments/assets/6d4defd7-1f44-465b-abf5-497710c3f948" />

</div>



---
### Arithmetic Logic Unit

<div style="display:flex; justify-content:center; align-items:center; gap:30px;">
  
| Function Number | Opcode            | Function     |
| --------------- | ----------------- | ------------ |
| #1              | 00000000 00000001 | A + B        |
| #2              | 00000000 00000010 | A − B        |
| #3              | 00000000 00000100 | ¬A           |
| #4              | 00000000 00001000 | A ⊼ B (NAND) |
| #5              | 00000000 00010000 | A ⊽ B (NOR)  |
| #6              | 00000000 00100000 | A ∧ B (AND)  |
| #7              | 00000000 01000000 | A ⊕ B (XOR)  |
| #8              | 00000000 10000000 | A ∨ B (OR)   |

<img width="300" alt="alu" src="https://github.com/user-attachments/assets/fdaea61b-157f-4245-ae0a-4b790923b41a" />

</div>



## Entire Block Diagram

<p align="center">
  <img width="1000" alt="block-diagram" src="https://github.com/user-attachments/assets/af8d4d80-52f7-4447-8d0f-0bb8f27100db"/>
</p>

---
_thanks for reading_


