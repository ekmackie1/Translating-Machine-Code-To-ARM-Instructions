# What is ARM?
ARM is an extremely powerful tool used to send instructions to processors that can be found in a variety of smartphones, tablets, computers, and more. Adopting the use of ARM processors has become a common practice for many of the largest tech companies delivering these devices, and will continue to be used in big tech. Because of its impact on the industry, ARM has become a cornerstone for the development of these devices.

# Opcode And Instructions
In order to get started, you'll need to understand the instructions involved. While ARM has a massive library of different instructions to choose from, for the sake of simplicity we'll only go over 14 basic 4-bit instructions represented in binary.

NOOP(0b0000): NOOP is short for "no operation", and is used to stall in order to prevent any further instructions from being immediately executed. This can be useful in cases where pipelining is used. Pipelining is used to expidite the instruction reading process by beginning the deciphering of new instructions before the previous one has finished executing. But because the previous instruction hasn't finished executing, the current one may need new values that will later be produced by said previous instruction. To prevent this issue, we would use NOOP in order to stall the instruction and let the previous one move far along enough to produce updated values to be used.

LD(0b0001): LD is an abbreviation for "load"
