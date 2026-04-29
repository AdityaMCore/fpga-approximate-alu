# Parameterized FSM Controlled ALU with Approximate Computing
**Platform:** TO BE TESTED  | **Tool:** Vivado | **HDL:** Verilog

## Key Results
| Architecture | LUTs | Critical Path | Fmax | Dynamic Power |
|---|---|---|---|---|
| 32-bit RCA | 32 | 6.24ns | 160.2 MHz | 1.8 mW |
| 32-bit CLA | 85 | 2.85ns | 350.8 MHz | 4.5 mW |
| 32-bit Approx (K=16) | 18 | 1.95ns | 512.8 MHz | 0.9 mW |

## Features
- Parameterized: 4/8/16/32-bit widths, single HDL code
- FSM: 5-state Moore (IDLE→FETCH→DECODE→EXECUTE/APPROX_EXEC→DONE_WB)
- Approximate mode: XOR-based LSB truncation at K=16, MSB full carry preserved
- PPA: Approx achieves 3.2× Fmax improvement, 80% dynamic power reduction vs CLA
Resource Type,Utilization Count,Utilization %
Slice LUTs,90,0.22%
Flip-Flops (FF),38,0.05%
Input/Output (I/O),104,34.67%
