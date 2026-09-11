# Hazard Detection and Forwarding

The hazard unit is used to handle data and control hazards. 

### Data Hazards

A data hazard occurs when an instruction calls for a read of a register/address in memory whilst a later stage in the pipeline (i.e. the memory and write back stages) is writing data into that entry. This is essentialy a read-after-write hazard which typically occurs with BRAM/URAM in FPGAs, and the issue with this is that given a write takes a clock cycle to be processed, the reading instruction would have not recieved this context, hence there is a potential for this instruction to read invalid data (causing the instruction to be invalid).

To solve these data hazards, forwarding had been implemented. This is a technique which compares the registers called in each stage to see if there is a match, determines if a read-after-write error would occur in that case, and if so, a `Forward1E/2E` signal is sent which is used as a 2-bit select input for a mux. In this mux, depending on the value of the select bits, forwarded data from memory, forwarded data from the register, or ALU calculated data will be written into the register at the execute stage.

### Contorl Hazards

Contorl Hazards occur when there is a branch or jump instruction that is taken. The RISC-V processor reads instructions in the instruction memory in sequential 4-byte words, this means that in the example below, when the branch occurs in the execute stage, there are still instructions which exist in the decode and fetch stages which are now invalid as the jump skips those instructions.

```
// assuming a0 = 2, a1 = 3, the bne branch will be taken
// hence the next two instructions are invalid

0x0004  bne a0, a1, [EXIT_LOOP]
0x0008  add a2, a2, a3
0x000C  addi a5, a6, 3
...
...

0x0020  sub a2, a3, a4              [EXIT_LOOP]
```

To solve this issue, a technique called flushing is used. `flush` signals are asserted in the hazard unit which means that all internal registers in the decode and fetch stages are asserted to zero, so that the garbage data is removed from the system.