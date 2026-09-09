# RISC-V-Processor

> **Note on this repository:** the coursework mandates that the source repository is kept private for academic-integrity reasons, thus no source code is hosted here. This repository documents the sections I personally designed and the reasoning behind them. The linked documents below describe each component in more detail.


## What the processor does

This processor is a 5-stage (IF/ID/EX/MEM/WB) pipelined RV32I core which includes extensions such as hazard detection, forwarding, and branch prediction. Using the [RISC-V instruction set manual](https://courses.grainger.illinois.edu/ece391/sp2025/docs/unpriv-isa-20240411.pdf), the bits are passed through the system producing accurate results shown via test-benching in verilator and waveform analysis via gtawave.

## My Contributions

| Area | Documentation |
| - | - |
| Branch Prediction | [branch prediction] |
| Control Unit | [control unit] |
| Hazard Detection & Forwarding | [hazard detection & forwarding] |
| Pipelining & Top-Level Design | [pipelining & top-level design] |
| Verification | [verification] |
