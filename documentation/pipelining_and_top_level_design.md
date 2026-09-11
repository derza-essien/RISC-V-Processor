# Pipelining and Top Level Design

In this system, there are five distinct stages that all handle different objectives, this allows for the 5-stage pipeline of the risc-v processor.

| Stage | Main Use |
| :-: | - |
| Fetch | Obtain the instruction from the `instruction_memory` and deal with the multiple program counters (for specific branch/jump conditions) |
| Decode | Slice the instruction into relevant register assignments, the type of instruction that is occuring, and sign extention for immediates |
| Execute | Handle the actual computation in the `ALU` and determining whether a branch is taken or not (using branch prediction) |
| Memory | Handles data writes into main memory or cache |
| Writeback | Handles data writes into registers |

In the top module, to decifer between registers, the capital of the name of the stage is used. For example the select bit for the ALU in the execute stage is named ALUControl**E**, compared to ALUControl**D** in the decode stage.