# 5-Stage Pipelined MIPS Processor

This repository is a showcase for a 32-bit MIPS processor I designed and built from scratch in Verilog. This was a 5th-semester (3rd-year) computer architecture project.

The core Verilog code is kept in a **private repository** to maintain academic integrity, as the project is currently under academic assessment. I am happy to provide a full code walkthrough during a technical interview.

---

## Core Architectural Features

The primary goal was to correctly implement a pipelined datapath capable of handling all data hazards without unnecessary stalls.

* **Full 5-Stage Pipeline:** Complete implementation of the **IF, ID, EX, MEM,** and **WB** stages.

* **Hazard Detection Unit:** A dedicated control unit in the ID stage that detects `lw-addi` (load-use) data hazards. When detected, it correctly stalls the pipeline for one cycle by flushing the ID/EX register.

* **Complete Forwarding Unit:** A full data forwarding (bypassing) unit to resolve all other data hazards and maximize performance. This logic is fully combinational and handles all paths:
    * **WB-to-EX Forwarding:** Forwards the final `lw` data or R-type result from the WB stage directly to the ALU in the EX stage. This path was critical for solving the `lw-addi` hazard.
    * **MEM-to-EX Forwarding:** Forwards R-type ALU results from the MEM stage.

* **Combinational Write-Back Stage:** The `wb_stage` was built as combinational logic. This was a key design decision to fix a race condition where the forwarding unit would get the write-enable signal one cycle too late.

* **Robust Reset Logic:** Full asynchronous reset logic is implemented for every pipeline register, the PC, and the Register File to ensure a clean, `0`-state start and prevent `X` propagation.

---

## Datapath Architecture

Below is a high-level block diagram of the 5-stage datapath, including the forwarding paths.

*(Note: You should create your own simple diagram showing the 5 stages and forwarding paths and upload it here.)*
