Priority Arbiter (Fixed & Round-Robin, Parameterized for N Masters)

**Overview:**
This project implements a priority-based arbiter system in Verilog. It supports two arbitration schemes:
  Fixed Priority Arbitration
  Round-Robin Arbitration (parameterized for N masters)

Arbiters are used when multiple masters request access to a shared resource, such as a system bus, memory, or communication channel. The arbiter ensures that only one request is granted at a time and that the system operates without conflict.

**Use Cases:**
  Bus arbitration in multi-master systems
  Shared memory access between CPU, DMA, and GPU
  Router ports in Network-on-Chip (NoC) architecture
  Video/image processing pipelines accessing common buffers

**Files Included:**
  fixed_priority_arbiter.v — A 4-input fixed priority arbiter (req[0] has highest priority)
  round_robin_arbiter.v — A round-robin arbiter for 4 requesters
  round_robin_arbiter_n.v — A fully parameterized round-robin arbiter for N requesters
  bus_system - A bus_system which selects the master's data lines based on access. 
  test_bench.v — Testbench for simulating and verifying the arbitration logic

**Arbitration Strategies:**
  
  **Fixed Priority Arbiter:**
    Always grants to the highest-priority request  
    For example: req[0] > req[1] > req[2] > req[3]
    Simple but can cause starvation for lower-priority requesters

  **Round-Robin Arbiter (4 Masters):**
    Fairly rotates priority among the 4 requesters
    Uses a state pointer to remember the last granted master
    Prevents starvation

  **Parameterized Round-Robin Arbiter (N Masters):**  
    Can handle any number of requesters (N ≥ 2)
    Uses modular arithmetic to rotate the priority
    The grant signal is always one-hot (only one bit high)
    Synthesizable and efficient

**Features:**
  Fully synthesizable RTL Verilog
  Supports both fairness (round-robin) and efficiency (fixed priority)
  One-hot grant output to control access cleanly
  Works for N = 4, 8, 16, etc.
  Suitable for FPGA or ASIC design

**How It Works (Internally):**
  A register last_grant stores the last granted master index
  On every clock, the arbiter searches the next requester based on a circular (rotating) priority
  Once a valid request is found, it updates the last_grant and issues a one-hot grant
  Grant generation is purely combinational and follows the current priority pointer

**Synthesis Information:**
  Target Device: Spartan-7 or any FPGA (Vivado tested)
  Registers: log2(N) bits for the state pointer
  Logic: AND/OR gates, priority selectors, modulus operators
  Output: One-hot encoded grant signal

Open for improvements, contributions, and testing!
