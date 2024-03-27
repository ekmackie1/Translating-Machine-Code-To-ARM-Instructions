# What is LC2K?
LC2K (or Little Computer 2K) is an extremely useful educational tool meant to simplify assembly languages in order to help beginners better understand the basics of computer architecture, and is used by many educators, students, and hobbyists. By reading machine code, LC2K can convert decimal numbers into instructions to perform in order to make a processor run. For people who plan on eventually learning about much larger subjects such as ARM, LC2K can be a great gateway into the beginner concepts.


# Why Simulate LC2K?
For people with a background in software and are new to hardware, it can be very helpful to ease people in to the subject by teaching it through a programming language such as C. On top of this, simulating LC2K is very modular in that you as a programmer will be granted the freedom of choosing any subset of instructions available, assign any opcode values to them, and organize whether you want your program to read hexadecimal, decimal, and/or binary numbers.


# Opcode And Instructions
In order to get started, you'll need to understand opcodes and instructions. You can begin by choosing any set of instructions you want to use and assigning a number to them to them. While ARM has a massive library of different instructions to choose from, LC2K allows you to simplfy things so there isn't an overwhelming amount of instructions to choose from. 

# Registers
Each instruction will come with 3 other values representing registers, which can be treated as a form of storage for values which will all be defaulted to 0, and an optional comment. a singualr instruction line will generally be in the format: ```INSTR 1 4 7 comment``` the first value is meant to be an instruction (like ADD, SUB, BEQ, etc.) depending on what you want to happen to the following numbers, the following 3 values each play a different role depending on the instruction, but they generally represent field 1, field 2, and field 3 respectively, the comment is optional.

# Memory
Memory is where every instruction will be stored in order. For example, if instruction 1 is ```ADD 4 2 1```, the value ```2228225``` will be stored at index 0 in memory. The explanation for how this was translated will be later explained.

For the sake of simplicity we'll only be using 32-bit instructions and 8 different 3-bit opcodes and give them corresponding binary values. Below I have chosen 8 basic instructions and assigned a binary number (opcode) to each one, and we will be using 8 registers to store values.

<br>Mathematical operation instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;ADD(0b000): ```ADD 2 5 1``` will add the value stored in register 2 to the value stored in register 5 and store the result in register 1
  <br>&nbsp;&nbsp;&nbsp;&nbsp;SUB(0b001): ```SUB 7 0 3``` will subtract the value stored in register 0 to the value stored in register 7 and store the result in register 3
<br>Value transfer instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;LD(0b010): ```LD 1 4 2``` will take the value stored in register 1, add it to the raw value 2, and use it as an index to determine which value in memory will be stored into register 4
  <br>&nbsp;&nbsp;&nbsp;&nbsp;ST(0b011): ```ST 2 1 3``` will take the value stored in register 1, add it to the raw value 3, and use it as an index for memory. The value stored in register 1 will be copied to said index in memory.
<br>Comparison instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;BEQ(0b100): ```BEQ 2 3 4``` will compare the values stored in register 2 and register 3. If they are equal, the program will change the current instruction to the 4th instruction in the input file.
  <br>&nbsp;&nbsp;&nbsp;&nbsp;BNE(0b101): ```BEQ 2 3 4``` will compare the values stored in register 2 and register 3. If they are not equal, the program will change the current instruction to the 4th instruction in the input file.
<br>Niche instrcutions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;NOOP(0b110): ```NOOP``` is a standalone instruction and anything that follows will be treated as a comment. This instruction tells means to do nothing, and is useful in cases where pipelining is used to read multiple instructions at once, in order to stall the program so that updated values can be read when necessary.
  <br>&nbsp;&nbsp;&nbsp;&nbsp;HALT(0b111): ```HALT``` tells the program to stop running. The halt instruction can only be followed by additional raw numbers that will execute no instructions, but will be stored in memory.

