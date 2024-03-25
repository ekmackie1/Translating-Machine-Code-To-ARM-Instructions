# What is LC2K?
LC2K (or Little Computer 2K) is an extremely useful educational tool meant to simplify assembly languages in order to help beginners better understand the basics of computer architecture, and is used by many educators, students, and hobbyists. By reading machine code, LC2K can convert decimal numbers into instructions to perform in order to make a processor run. For people who plan on eventually learning about much larger subjects such as ARM, LC2K can be a great gateway into the beginner concepts.


# Why Simulate LC2K?
For people with a background in software and are new to hardware, it can be very helpful to ease people in to the subject by teaching it through a programming language such as C. On top of this, simulating LC2K is very modular in that you as a programmer will be granted the freedom of choosing any subset of instructions available, assign any opcode values to them, and organize whether you want your program to read hexadecimal, decimal, and/or binary numbers.


# Opcode And Instructions
In order to get started, you'll need to understand opcodes and instructions. You can begin by choosing any set of instructions you want to use and assigning a number to them to them. While ARM has a massive library of different instructions to choose from, LC2K allows you to simplfy things so there isn't an overwhelming amount of instructions to choose from. Each instruction will come with 3 other values representing registers, which can be treated as a form of storage for values which will all be defaulted to 0, and an optional comment. Instructions will generally be in the format: ```INSTR 1 4 7 comment``` the first value is meant to be an instruction (like ADD, SUB, BEQ, etc.) depending on what you want to happen to the following numbers, the following 3 values each play a different role depending on the instruction, but they generally represent field 1, field 2, and field 3 respectively, the comment is optional.

For the sake of simplicity we'll only be using 8 different 3-bit instructions and give them corresponding binary values. Below I have chosen 8 basic instructions and assigned a binary number (opcode) to each one, and we will be using 8 registers to store values.

Mathematical operation instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;ADD(0b000): This instruction is used for adding the value stored in the register represented by field 1 to the value sotred in the register represented by field 2, and storing the result in the destination register represented by field 3.
  <br>&nbsp;&nbsp;&nbsp;&nbsp;SUB(0b001): This instruction is used for adding the value stored in the register represented by field 1 to the value sotred in the register represented by field 2, and storing the result in the destination register represented by field 3.
Value transfer instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;LD(0b010): this instruction breaks convention in that 
  <br>&nbsp;&nbsp;&nbsp;&nbsp;ST(0b011)
Comparison instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;BEQ(0b100)
  <br>&nbsp;&nbsp;&nbsp;&nbsp;BNE(0b101)
Niche instrcutions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;NOOP(0b110)
  <br>&nbsp;&nbsp;&nbsp;&nbsp;HALT(0b111)
