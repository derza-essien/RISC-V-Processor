# Control Unit

The control unit consits of 3 inputs, the `opcode`, the `funct3` signal and `funct7` signal. These signals allow us to know what type of instruction we have based on the table below (this is in accordance to the instruction set manual):

| Instruction Type | opcode (7 bit binary number) | 
| :-: | :-: |
| Load | 000 0011 |
| Store | 010 0011 |
| R (register write) | 011 0011 |
| I (immediate instruction) | 001 0011 |
| Branch instruction | 110 0011 |
| Jump instruction | 110 0111 |

With more complex instructions (those being the I and R instructions), `funct3` and `funct7` would be used to differentiate between the specific type of instruction (e.g. an add, subtract, shift etc.).

Depending on these input values, our signals, mostly acting as select signals for muxes in the execute stage, would be varied for the correct behaviour in later stages.
