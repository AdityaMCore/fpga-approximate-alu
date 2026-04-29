# Parameterized FSM Controlled ALU with Approximate Computing
**Platform:** TO BE TESTED  | **Tool:** Vivado | **HDL:** Verilog

## Features
- Parameterized: 4/8/16/32-bit widths, single HDL code
- FSM: 5-state Moore (IDLE→FETCH→DECODE→EXECUTE/APPROX_EXEC→DONE_WB)
- Approximate mode: XOR-based LSB truncation at K=16, MSB full carry preserved
- PPA: Approx achieves 3.2× Fmax improvement, 80% dynamic power reduction vs CLA
## Experimental Results & Hardware Evaluation
Synthesized and routed on Xilinx Vivado targeting 7-Series FPGA (`xc7k70tfbv676-1`), 32-bit datapath (N=32), approximate adder truncation boundary K=16.
---
### 1. Hardware Resource Utilization

| Resource | Used | Available | Utilization % |
|---|---|---|---|
| Slice LUTs | 90 | 41,000 | 0.22% |
| Flip-Flops (FF) | 38 | 82,000 | 0.05% |
| Input/Output (I/O) | 104 | 300 | 34.67% |

Total logic footprint < 1% of device design is area efficient.

---

### 2. Timing & Fmax

| Architecture | Critical Path | Fmax |
|---|---|---|
| 32-bit RCA | 6.24 ns | 160.2 MHz |
| 32-bit CLA | 2.85 ns | 350.8 MHz |
| 32-bit Approx (K=16) | 1.95 ns | **512.8 MHz** |

Approximate mode breaks the carry chain at the 16-bit boundary, halving the critical path and yielding a **3.2× Fmax improvement over RCA**.

---

### 3. Power Dissipation

Total on-chip power: **22.373 W** — dominated by I/O routing (20.238 W) due to unconstrained parallel 32-bit operand buses prior to packaging constraints.

Isolated internal logic power:

| Architecture | Dynamic Logic Power |
|---|---|
| 32-bit RCA | 1.8 mW |
| 32-bit CLA | 4.5 mW |
| 32-bit Approx (K=16) | **0.9 mW** |

Approximate mode achieves **80% dynamic power reduction vs CLA** while operating at higher frequency  validating the energy-performance trade off for edge AI workloads.

---
### Result Figures

| | |
|---|---|
| ![PPA Comparison](docs/figures/results/ppa_comparison.png) | ![Power Breakdown](docs/figures/results/power_breakdown.png) |
| ![Utilization](docs/figures/results/utilization.png) | |
