# Priority Arbiter in Verilog (Fixed & Round-Robin, Parameterized for N Masters)

## 📌 Overview

This project implements a **priority-based arbiter system in Verilog**, supporting two arbitration schemes:

- ✅ **Fixed Priority Arbitration**
- 🔄 **Round-Robin Arbitration** (parameterized for any number of masters `N`)

Arbiters are essential in digital systems where **multiple masters compete for access to a shared resource** (like a bus, memory, or communication channel). The arbiter ensures that only one request is granted at a time and that the system operates fairly and efficiently.

---

## 🚀 Use Cases

- 🖥️ Multi-master **bus arbitration** (e.g., AXI/AMBA systems)
- 🧠 **Shared memory** access control between CPU/DMA/GPU
- 📡 **Network-on-Chip (NoC)** routers
- 🎥 **Image/Video processing** with shared buffers

---

## 🛠️ Project Structure

| File                         | Description                                         |
|------------------------------|-----------------------------------------------------|
| `fixed_arbiter.v`           | 4-input fixed-priority arbiter (req[0] is highest)  |
| `round_robin_arbiter.v`     | Round-robin arbiter for 4 masters                   |
| `round_robin_arbiter_n.v`   | Parameterized round-robin arbiter (any `N`)     |
| `test_bench.v`              | Testbench validating correct and fair grant logic   |
| `bus_system.v`              | Top module showing how arbiter connects to bus      |

---

## ⚙️ Arbitration Schemes

### 🔸 1. Fixed Priority Arbiter
- Always grants to the **highest-priority active request**.
- Simple and fast, but **lower-priority masters may starve**.
- Example priority: `req[0] > req[1] > req[2] > req[3]`.

### 🔄 2. Round-Robin Arbiter (4 Masters)
- Rotates priority **cyclically** among requesters.
- Tracks the last granted master using a pointer.
- Ensures **fairness and prevents starvation**.

### 🔁 3. Parameterized Round-Robin Arbiter (N Masters)
- Flexible arbiter that supports **any number of requesters** (`N ≥ 2`).
- Uses modular arithmetic to rotate priority.
- One-hot `grant` output.
- Synthesizable and scalable design.

---

## ✅ Features

- 🧩 Fully synthesizable Verilog RTL
- 🔄 Scalable round-robin arbitration logic
- 🚦 One-hot `grant` output signal
- 🧪 Thorough simulation support
- 🧠 Clean and modular code structure

---
## 🔧 Synthesis Information

- 🛠 Target: Spartan-7  (Vivado tested)
- ⌛ Registers: `log2(N)` bits for tracking pointer
- 🧮 Logic: Combinational priority encoders, AND/OR gates
- 🔐 Output: Safe, one-hot `grant` line for multiplexer/bus control

---


