# What is LC2K?
LC2K (or Little Computer 2K) is an extremely useful educational tool meant to simplify assembly languages in order to help beginners better understand the basics of computer architecture, and is used by many educators, students, and hobbyists. By reading machine code, LC2K can convert decimal numbers into instructions to perform in order to make a processor run. For people who plan on eventually learning about much larger subjects such as ARM, LC2K can be a great gateway into the beginner concepts.+

# Why Simulate LC2K?
For people with a background in software and are new to hardware, it can be very helpful to ease people in to the subject by teaching it through a programming language such as C. On top of this, simulating LC2K is very modular in that you as a programmer will be granted the freedom of choosing any subset of instructions available, assign any opcode values to them, and organize whether you want your program to read hexadecimal, decimal, and/or binary numbers.


# Reading Binary
Binary is an alternate way to represent any number in 0s and 1s. The way you read it is by startinf from the right-most value, and incrementing an exponent starting with base 2. So if I had a binary value ```0b | 1 | 1 | 1 | 1```, this can be rewritten as ```2^3 | 2^2 | 2^1 | 2^0```. You will then add these numbers up to get your decimal value ```2^3 + 2^2 + 2^1 + 2^0 = 8 + 4 + 2 + 1 = 15``` so ```0b1111 = 15```. When you throw 0s into the mix, these can act as an off switch for its respective value. So if I change the binary to 0b1010, we then have ```2^3 + 0 + 2^1 + 0 = 8 + 0 + 2 + 0 = 10``` so ```0b1010 = 10```.

# Manipulating Binary
Bianry shifting is another relevant and useful for manipulating instructions translated to integers. In order to shift bianry values, you can take an example variable like ```n = 0b010``` and apply ```n = n << 1``` to set ```n = 0b0100```, this happened because the binary value was shifted one position to the left. Using this example, all cases of this can be set up as such: ```[value] = [value] [operator] [spaces to shift]``` where ```[value]``` is the value to be shifted, ```[operator]``` is either << or >> for left and right shift respectively, and ```[spaces to shift]``` represented the amound of times to shift in the specified direction. Note that these values will be limited by how many bit they can hold, so a 4 bit int being shifted left, will cause the greatest bit to be lost and defaulted to 0. 


# Opcode And Instructions
In order to get started, you'll need to understand opcodes and instructions. You can begin by choosing any set of instructions you want to use and assigning a number to them to them. While ARM has a massive library of different instructions to choose from, LC2K allows you to simplfy things so there isn't an overwhelming amount of instructions to choose from.


# Translating instructions
You can translate instructions to machine code values using binary. Using a 32-bit format, we can reserve bits for certain fields and opcodes. bits 0-15 will be reserved for field 3, bits 16-18 will be reserved for field 2, bits 19-21 will be reserved for field 1, and bits 22-24 will be reserved for the opcode. Bits 25-31 will remain empty. We will translate ```ADD 4 2 1``` as an example. Under "Instructions We Will Be Using", you can find that ADD has the associated binary 0b000 and has 3 reserved bits, 4 has a binary value of 0b100 and has 3 reserved bits, 2 has a binary value of 0b010 and has 3 reserved bits, and 1 has a value of 0b001 and has 16 reserved bits. When we line these values up, we get ```000 100 010 001 0000000000000001```, this leaves us with a final binary value of ```0b0001000100010000000000000001``` which translates to a decimal value of ```2228225```.


# Registers
Each instruction will come with 3 other values representing registers, which can be treated as a form of storage for values which will all be defaulted to 0, and an optional comment. a singualr instruction line will generally be in the format: ```INSTR 1 4 7 comment``` the first value is meant to be an instruction (like ADD, SUB, BEQ, etc.) depending on what you want to happen to the following numbers, the following 3 values each play a different role depending on the instruction, but they generally represent field 1, field 2, and field 3 respectively, the comment is optional.


# Memory
Memory is where every instruction will be stored in order. For example, if instruction 1 is ```ADD 4 2 1```, the value ```2228225``` will be stored at index 0 in memory.

For the sake of simplicity we'll only be using 32-bit instructions and 8 different 3-bit opcodes and give them corresponding binary values. Below I have chosen 8 basic instructions and assigned a binary number (opcode) to each one, and we will be using 8 registers to store values. The associated numbers are chosen at random for example purposes.


# Instructions We Will Be Using
Mathematical operation instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;ADD(0b000): ```ADD 2 5 1``` will add the value stored in register 2 to the value stored in register 5 and store the result in register 1
  <br>&nbsp;&nbsp;&nbsp;&nbsp;SUB(0b001): ```SUB 7 0 3``` will subtract the value stored in register 0 to the value stored in register 7 and store the result in register 3
<br><br>Value transfer instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;LD(0b010): ```LD 1 4 2``` will take the value stored in register 1, add it to the raw value 2, and use it as an index to determine which value in memory will be stored into register 4
  <br>&nbsp;&nbsp;&nbsp;&nbsp;ST(0b011): ```ST 2 1 3``` will take the value stored in register 1, add it to the raw value 3, and use it as an index for memory. The value stored in register 1 will be copied to said index in memory.
<br><br>Comparison instructions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;BEQ(0b100): ```BEQ 2 3 4``` will compare the values stored in register 2 and register 3. If they are equal, the program will change the current instruction to the 4th instruction in the input file.
  <br>&nbsp;&nbsp;&nbsp;&nbsp;BNE(0b101): ```BEQ 2 3 4``` will compare the values stored in register 2 and register 3. If they are not equal, the program will change the current instruction to the 4th instruction in the input file.
<br><br>Niche instrcutions:
  <br>&nbsp;&nbsp;&nbsp;&nbsp;NOOP(0b110): ```NOOP``` is a standalone instruction and anything that follows will be treated as a comment. This instruction tells means to do nothing, and is useful in cases where pipelining is used to read multiple instructions at once, in order to stall the program so that updated values can be read when necessary.
  <br>&nbsp;&nbsp;&nbsp;&nbsp;HALT(0b111): ```HALT``` tells the program to stop running. The halt instruction can only be followed by additional raw numbers that will execute no instructions, but will be stored in memory.


# Reading in a file line by line
Below is a C program that will read in every line in a txt file, and store them all in order in an array. Each string is then printed out on it's own individual line. You will want to implement this in order to separate your txt file into separate instructions to execute. This will help you
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main() {
    //An array that can hold up to 1000 strings. Each of which can be up to 1000 characters long.
    char lines[1000][1000];
    FILE *file;
    int numLines = 0;

    //Opens the file "input.txt". Cuts off the program early if the file cannot be read.
    file = fopen("input.txt", "r");
    if (file == NULL) {
        perror("Can't read input file");
        return 1;
    }

    //Read the input file line by line.
    char line[1000];
    while (fgets(line, sizeof(line), file) != NULL && numLines < 1000) {
        // Remove newline character if present
        if (line[strlen(line) - 1] == '\n')
            line[strlen(line) - 1] = '\0';
        
        //Copy and paste the current line to the next open slot in lines.
        strcpy(lines[numLines], line);
        numLines++;
    }

    //Closes the file.
    fclose(file);

    //Prints out the file's contents line by line
    printf("Contents of the file:\n");
    for (int i = 0; i < numLines; i++) {
        printf("%s\n", lines[i]);
    }
    return 0;
}
```


# Parsing a string by using whitespace as a delimiter
Below is a C program that takes in a string (in C a char array), and splits it into separate strings using whitespace as the delimiter for separation. Note that although the strings "pointless" and "comment" will be put into the array, they will be ignored when we run the actual program. For this example ```ADD 1 2 4 pointless comment``` is used.
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to separate a string by whitespace and store substrings in an array
int separateByWhitespace(const char *str, char substrings[1000][1000], int *numSubstrings) {
    int count = 0;
    *numSubstrings = 0;
    char *token;

    //Copy the input string to avoid changing the original
    char *strCopy = strdup(str);
    if (strCopy == NULL) {
        perror("Error copying string");
        return 0;
    }

    // Tokenize the string using whitespace as delimiters
    token = strtok(strCopy, " \t\n");
    while (token != NULL && count < 1000) {
        strcpy(substrings[count], token);
        count++;
        token = strtok(NULL, " \t\n");
    }

    //Assign the number of substrings
    *numSubstrings = count;
    //Free up memory
    free(strCopy);

    return 1;
}

int main() {
    char str[] = "ADD 1 2 4 pointless comment";
    char substrings[1000][1000];
    int numSubstrings;

    if (separateByWhitespace(str, substrings, &numSubstrings)) {
        printf("Number of substrings: %d\n", numSubstrings);
        for (int i = 0; i < numSubstrings; i++) {
            printf("%s\n", substrings[i]);
        }
    } else {
        printf("Cannot separate string");
    }
    return 0;
}
```


# Implementing ADD and SUB
Below is a function that executes instructions ```ADD 1 2 4 pointless comment``` and ```SUB 7 6 5 pointless comment``` after they've been parsed and placed into its own array.
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void executeAddSub(char* instr[], int registers[]) {
    //if the instr is ADD, add the contents of the register in field1 to the contents of the register in field2 and store the result in reg3
    if (strcmp(instr[0], "ADD") == 0) {
        registers[atoi(instr[3])] = registers[atoi(instr[1])] + registers[atoi(instr[2])];
    }
    //if the instr is SUB, subtract the contents of the register in field2 from the contents of the register in field1 and store the result in reg3
    else if (strcmp(instr[0], "SUB") == 0) {
        registers[atoi(instr[3])] = registers[atoi(instr[1])] - registers[atoi(instr[2])];
    }
}

int main() {
    int registers[8] = {0, 1, 2, 3, 4, 5, 6, 7};
    char* instr1[] = {"ADD", "1", "2", "4", "pointless", "comment"};
    char* instr2[] = {"SUB", "7", "6", "5", "pointless", "comment"};
    executeAddSub(instr1, registers);  //changed register 4 from 4 -> 3
    executeAddSub(instr2, registers);  //changed register 5 from 5 -> 1

    //should print "0, 1, 2, 3, 3, 1, 6, 7"
    for (int i = 0; i < 8; i++) {
        printf("REGISTER %d: %d\n", i, registers[i]);
    }

    return 0;
}
```


# Implementing LD and ST
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>


void executeLdSt(char* instr[], int* registers, int* memory) {
    //get an index for what position in memory will be used by adding the contents of reg1 to the raw value in field3
    int memoryIndex = registers[atoi(instr[1])] + atoi(instr[3]);
    //load the designated memory value into the register specified in field2
    if (strcmp("LD", instr[0]) == 0) {
        registers[atoi(instr[2])] = memory[memoryIndex];
    }
    //take the value stored in the register indicated in field2 and store it into the designated memory index
    else if (strcmp("ST", instr[0]) == 0) {
         memory[memoryIndex] = registers[atoi(instr[2])];
    }
}

int main() {
    int registers[8] = {0, 0, 0, 0, 0, 0, 0, 0};
    int memory[] = {2, 37, 44490, 2261, 4444440};
    char* instr1[] = {"LD", "1", "2", "4", "pointless", "comment"};  //puts 4444440 into register 2
    char* instr2[] = {"LD", "1", "3", "0", "pointless", "comment"};  //puts 2 into register 3
    char* instr3[] = {"ST", "3", "2", "1", "pointless", "comment"};  //replaces memory value 2261 with 4444440
    executeLdSt(instr1, registers, memory);
    executeLdSt(instr2, registers, memory);
    executeLdSt(instr3, registers, memory);
    printf("REGISTERS: ");
    for (int i = 0; i < 8; i++) {
        printf("%d, ", registers[i]);
    }
    printf("\n");
    printf("MEMORY: ");
    for (int i = 0; i < 5; i++) {
        printf("%d, ", memory[i]);
    }
}
```


# Implementing BEQ and BNE
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void executeBeqBne(int* reg, char* instr[], int *n) {
    if (strcmp(instr[0], "BEQ") == 0) {
        //if the contents in the registers of field1 and field2 are equal, change n to the raw value in field3
        if ((reg[atoi(instr[1])]) == (reg[atoi(instr[2])])) {
            *n = atoi(instr[3]);
        }
    }
    else if (strcmp(instr[0], "BNE") == 0) {
        //if the contents in the registers of field1 and field2 are not equal, change n to the raw value in field3
        if ((reg[atoi(instr[1])]) != (reg[atoi(instr[2])])) {
            *n = atoi(instr[3]);
        }
    }
}

int main() {
    int registers[8] = {0, 0, 1, 1, 2, 2, 3, 3};
    int n = 0;
    char* instr1[] = {"BEQ", "0", "2", "4", "pointless", "comment"};  //reg0 = 0 and reg2 = 1 so n does not change to 4
    executeBeqBne(registers, instr1, &n);
    printf("%d\n", n);
    char* instr2[] = {"BEQ", "0", "1", "4", "pointless", "comment"};  //reg0 = 0 and reg1 = 0 so n does change to 4
    executeBeqBne(registers, instr2, &n);
    printf("%d\n", n);
    char* instr3[] = {"BNE", "0", "1", "8", "pointless", "comment"};  //reg0 = 0 and reg1 = 0 so n does not change to 8
    executeBeqBne(registers, instr3, &n);
    printf("%d\n", n);
    char* instr4[] = {"BNE", "0", "7", "8", "pointless", "comment"};  //reg0 = 0 and reg7 = 3 so n does change to 8
    executeBeqBne(registers, instr4, &n);
    printf("%d\n", n);
}
```


# Implementing NOOP and HALT
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void executeNoopHalt(char** instr, int* noopCount) {
    if (strcmp(instr[0], "NOOP") == 0) {
        *noopCount += 1;
    }
    if (strcmp(instr[0], "HALT") == 0) {
        printf("%s\n", "HALTED");
        printf("NOOP COUNT: %d\n", *noopCount);
        exit(0);
    }
}

int main() {
    int noopCount = 0;
    char* instr1[] = {"NOOP", "comment", "1"};
    char* instr2[] = {"NOOP", "comment", "2"};
    char* instr3[] = {"HALT", "comment", "3"};
    executeNoopHalt(instr1, &noopCount);
    executeNoopHalt(instr2, &noopCount);
    executeNoopHalt(instr3, &noopCount);
    printf("PROGRAM DID NOT HALT");
    return 1;
}
```

<br>You can apply these templates to create any oher examples you want with any conditions, allowing you to even make instructions that don't actually exist.
