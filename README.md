# CSARCH2-S20-Group7-CaseStudy2

## 8-bit INC/DEC CPU

### I. Instruction Set Architecture

This CPU supports four 8-bit instructions for incrementing and decrementing Registers A and B.

| Instruction | Opcode (Hex) | Binary Opcode | Action |
| :--- | :---: | :---: | :--- |
| **INC\_A** | **00** | `0000 0000` | Register A ← A + 1 |
| **DEC\_A** | **01** | `0000 0001` | Register A ← A - 1 |
| **INC\_B** | **02** | `0000 0010` | Register B ← B + 1 |
| **DEC\_B** | **03** | `0000 0011` | Register B ← B - 1 |

### II. Testing Procedure in Logisim

Testing requires a **two-step cycle** for every instruction: 1) Load the Opcode into the Instruction Register (IR), and 2) Execute the instruction. The **Poke Tool** (the pointing hand icon) is used for all manual inputs.

# CPU Instruction Testing Guide

## Phase A: Load Value into Register A

Use this phase to manually load a value (e.g., **5**) into **Register A**.

1. **Set Manual Input Mode:** Set the `data_in` pin to **1** (manual input enabled).
2. **Select Register A:** Set `select_a` to **1**.
3. **Set Input Value:** Enter the desired value on `d_in`  
   Example: `00000101` (decimal 5).
4. **Execute Load:** Click the **Clock**.
6. **Verification:** The **A register output** should now show **5**.

## Phase B: Load Opcode (Example: `INC_A`)

This phase loads an instruction opcode into the instruction register (IR).

1. **Prepare Opcode:** Set `data_in` = **0**.
2. **Input Opcode:** Enter `00000000` (INC_A) on `d_in`.  
3. **Clock IR:** Click the **Clock**.  

## Phase C: Load Value into Register B

Use this phase to manually load a value (e.g., **0**) into **Register B**.

1. **Set Manual Input Mode:** Set the `data_in` pin to **1**.
2. **Select Register B:** Set `select_b` to **1** and `select_a` to **0**.
3. **Set Input Value:** Enter the value on `d_in`  
   Example: `00000000` (decimal 0).
4. **Execute Load:** Click the **Clock**.
6. **Verification:** The **B register output** should now show **0**.

## Phase D: Load Opcode (Example: `DEC_B`)

1. **Prepare Opcode:** Set `data_in` = **0**.
2. **Input Opcode:** Enter `00000011` (DEC_B) on `d_in`.
3. **Clock IR:** Click the **Clock**.

