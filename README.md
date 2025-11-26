# CSARCH2-S20-Group7-CaseStudy2

## 8-bit INC/DEC CPU

### I. Instruction Set Architecture

This CPU supports four 8-bit instructions for incrementing and decrementing Registers A and B.

| Instruction | Opcode (Hex) | Binary Opcode | Action |
| :--- | :---: | :---: | :--- |
| **INC\_A** | **01** | `0000 0001` | Register A ← A + 1 |
| **DEC\_A** | **02** | `0000 0010` | Register A ← A - 1 |
| **INC\_B** | **03** | `0000 0011` | Register B ← B + 1 |
| **DEC\_B** | **04** | `0000 0100` | Register B ← B - 1 |


### II. Testing Procedure in Logisim

Testing requires a **two-step cycle** for every instruction: 1) Load the Opcode into the Instruction Register (IR), and 2) Execute the instruction. The **Poke Tool** (the pointing hand icon) is used for all manual inputs.

#### Phase A: Pre-Load Operands (Setup)

Use this phase to set initial data in the registers (e.g., loading **5** into Register A).

1.  **Set Input Value:** Click the **`external_data_in`** pin and set a test value (e.g., **5**).
2.  **Enable External Load:** Click the manual pin **`LOAD_BUS_EXT`** to **HIGH (1)**.
    * *(Action: This forces the Bus Mux to select the external data).*
3.  **Enable Register Load:** Click the **`LD_A`** pin (or `LD_B`) to **HIGH (1)**.
4.  **Execute Load:** **Poke the Clock once.**
5.  **Clean Up:** Set `LOAD_BUS_EXT` and `LD_A` **LOW (0)**.
6.  **Verification:** The `Q_A_OUT` pin must now show **5**.

#### Phase B: Execute $\text{INC\_A}$ (Opcode 01)

This verifies the instruction execution cycle and control logic.

| Step | Action | Required Control Signals | Verification Check (Main Bus) |
| :---: | :--- | :---: | :--- |
| **1. Load Opcode** | Set `external_data_in` = **1**. | `LOAD_BUS_EXT` = **1**, `LD_IR` = **1** | (Bus shows 1) |
| **2. Clock IR** | **Poke the Clock once.** | (IR now holds 1) | |
| **3. Clean Up** | Set `LOAD_BUS_EXT` and `LD_IR` **LOW (0)**. | `LOAD_BUS_EXT` = **0** | (Bus Mux now selects ALU Result) |
| **4. Execute** | **Poke the Clock once.** | `LD_A` = **1** (Asserted by Decoder) | (Bus shows $5+1=\mathbf{6}$) |

**Final Result:** The **`Q_A_OUT`** pin must show **6**.

#### Phase C: Repeat for DEC\_B (Example)

1.  **Setup Register B:** Use **Phase A** to load Register B with a test value (e.g., **10**). Clean up.
2.  **Load Opcode:** Use **Steps 1-3 of Phase B** to load Opcode **04** (`DEC_B`) into the IR. Clean up.
3.  **Execute:** Set `LOAD_BUS_EXT` = **0**. **Poke the Clock once.**
    * *Verification Check:* The Bus should show $10-1=\mathbf{9}$.
4.  **Final Result:** The **`Q_B_OUT`** pin must show **9**.
