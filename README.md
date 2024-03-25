# What is LC2K?
LC2K (or Little Computer 2K) is an extremely useful educational tool meant to simplify assembly languages in order to help beginners better understand the basics of computer architecture, and is used by many educators, students, and hobbyists. By reading machine code, LC2K can convert decimal numbers into instructions to perform in order to make a processor run. For people who plan on eventually learning about much larger subjects such as ARM, LC2K can be a great gateway into the beginner concepts.


# Why Simulate LC2K?
For people with a background in software and are new to hardware, it can be very helpful to ease people in to the subject by teaching it through a programming language such as C. On top of this, simulating LC2K is very modular in that you as a programmer will be granted the freedom of choosing any subset of instructions available, assign any opcode values to them, and organize whether you want your program to read hexadecimal, decimal, and/or binary numbers.


# Opcode And Instructions
In order to get started, you'll need to understand opcodes and instructions. You can begin by choosing any set of instructions you want to use and assigning a number to them to them. While ARM has a massive library of different instructions to choose from, for the sake of simplicity we'll only be using 8 different 3-bit instructions and give them corresponding binary values. Below I have chosen 8 basic instructions and assigned a binary number (opcode) to each one. Each instruction will come with 3 other values and an optional comment. Instructions will generally be in the format:
<br>```INSTR 1 4 7 comment


Mathematical operation instructions:
  ADD(0b000): 
  SUB(0b001)
Value transfer instrcutions:
  LD(0b010)
  ST(0b011)
Comparison instructions:
  BEQ(0b100)
  BNE(0b101)
Niche instrcutions:
  NOOP(0b110)
  HALT(0b111)
