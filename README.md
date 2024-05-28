vsd risc-v internship
-

Task 1 : installing the oracle virutal machine and running basic c program 
-
For installing the oracle virutal machine go through the folling website 
https://www.virtualbox.org/wiki/Downloads

install the virtual machie

 we are creating the virtual hard disk by including the VDI  file
 -
 
Now we are starting compiling with simple c program

Type the following commands

$ cd \
$ gedit sum1ton.c

we will get an interface page to write c program

![Screenshot from 2024-05-24 14-59-13](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/a7189e2e-6635-4e5e-8bab-f8978ce23981)

save the program and compile it \
$ gcc sum1ton.c                    (compiles the program) \
$ ./a.out                          (gives output)

![Screenshot from 2024-05-24 14-58-55](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/f756d24b-6a40-488d-8a84-1352dc12e98f)

we can see the output sum of 6 numbers is 21 

compiling same program with risc-v compiler
-
$ cat 1ton.c \
that display the total program in the terminal 

![Screenshot from 2024-05-24 16-00-04](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/e5f929ee-ba97-477f-a1a2-d1472797f3ec)


next converting in to .o file \
$ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c \
$ ls -ltr sum1ton.o    (file is created)

![Screenshot from 2024-05-24 14-55-13](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/fb1494b4-57b8-4da9-89a7-3a415c79ad64)

Opening the another tab of terminal to get list of instructions \
and type the command \
$ risc-v64-unknown-elf-objdump -d sum1ton.o \
we will get the set of instructions
![Screenshot from 2024-05-24 14-55-20](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/acbfca4e-4c2b-45b2-88ae-14b8aa464687)

 Now type / main and then type n
 we will get instructions of main There are 11 number of instructions

 ![Screenshot from 2024-05-24 18-33-26](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/d195ebaa-6165-4f36-81fa-651e771ccec0)


now compling with another command \
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c \
here is how it done
![Screenshot from 2024-05-24 18-38-14](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/604e1603-6ccc-47ef-9531-27ad12bb17c0)

and the output we got 11 number of instructions

![Screenshot from 2024-05-24 18-38-27](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/1fda23bb-209b-4609-afb1-e8ede9d689db)

 we can observe that in the both outputs we got 11 istructions......

 Task 2
 =
 Lets get in to Risc-v chip, and learn about different types of RISC-V Instruction types R,I,S,B,U,J.
 -

![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/255a9251-0bbb-47e2-adb8-4bcc0abfca1b)

The above shown the base instructions formates 

RISC-V Instruction Types and Formats
=
RISC-V defines several instruction formats, including:

R-type (Register): Used for arithmetic and logical operations.
-
Opcode: 7 bits \
Rd: 5 bits (destination register) \
Funct3: 3 bits \
Rs1: 5 bits (source register 1) \
Rs2: 5 bits (source register 2) \
Funct7: 7 bits

I-type (Immediate): Used for immediate arithmetic, loads, etc.
-
Opcode: 7 bits \
Rd: 5 bits (destination register) \
Funct3: 3 bits \
Rs1: 5 bits (source register) \
Imm: 12 bits (immediate value) 

S-type (Store): Used for store instructions.
-
Opcode: 7 bits \
Imm[4:0]: 5 bits (lower bits of immediate) \
Funct3: 3 bits \
Rs1: 5 bits (source register) \
Rs2: 5 bits (source register 2) \
Imm[11:5]: 7 bits (upper bits of immediate)

B-type (Branch): Used for branch instructions.
-
Opcode: 7 bits \
Imm[11]: 1 bit (most significant bit of immediate) \
Imm[4:1]: 4 bits (lower bits of immediate) \
Funct3: 3 bits \
Rs1: 5 bits (source register 1) \
Rs2: 5 bits (source register 2) \
Imm[10:5]: 6 bits (upper bits of immediate) \
Imm[12]: 1 bit (most significant bit of immediate) 

U-type (Upper immediate): Used for instructions with a 20-bit immediate.
-
Opcode: 7 bits \
Rd: 5 bits (destination register) \
Imm: 20 bits (immediate value)

J-type (Jump): Used for jump instructions.
-
Opcode: 7 bits \
Rd: 5 bits (destination register) \
Imm[19:12]: 8 bits (upper immediate) \
Imm[11]: 1 bit (immediate bit 11) \
Imm[10:1]: 10 bits (middle bits of immediate) \
Imm[20]: 1 bit (most significant bit of immediate)

Now let's discuss about in detail 
-
ADD
-
This instruction allows add two registers together and save the result in the third one.\ For example: ADD x3, x1, x2. It means add together x1 and x2 and save the result in x3. \As each instruction consists of 32 bits.

The ADD instruction is an R-type (Register) instruction, which has the following format:
![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/c9b0647c-5bed-4931-ab5a-cf73677b748f)

32-bit Instruction Code  \
Now, let's put these fields together: 

funct7: 0000000  \
rs2: 00001     \
rs1: 00010     \
funct3: 000    \
rd: 00110      \
opcode: 0110011  \
Putting it all together:  

31-25	24-20	19-15	14-12	11-7	6-0    \
0000000	00001	00010	000	00110	0110011   \
In binary: 0000000 00001 00010 000 00110 0110011  

Convert this to hexadecimal for a more compact representation: 

0000000 is 0x00 \ 
00001 is 0x01 \
00010 is 0x02 \
000 is 0x00 \
00110 is 0x06 \
0110011 is 0x33 \
Thus, the 32-bit binary instruction can be written as: 0x00200633

The 32-bit instruction code for the RISC-V instruction ADD r6, r2, r1 is 0x00200633 in hexadecimal, corresponding to the R-type format as follows: 
![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/ec1a18b2-5719-458e-91d2-04d3b60489cb)

SUB
-
The R-type format in RISC-V is structured as follows:
![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/309efc6b-f279-4392-bd32-7ed631917c17)
opcode: The opcode for R-type arithmetic instructions is 0110011. \
funct7: For the SUB instruction, funct7 is 0100000. \
funct3: For the SUB instruction, funct3 is 000. \ 
rd (destination register): r7 corresponds to 00011 in binary.\
rs1 (source register 1): r1 corresponds to 00001 in binary. \
rs2 (source register 2): r2 corresponds to 00010 in binary 

Now, we combine all these fields into the 32-bit instruction format:

![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/b571312d-5ba5-4b71-9619-a751735d5dc3)

Converting each field to its binary representation:

funct7: 0100000 (7 bits) \
rs2: 00010 (5 bits) \ 
rs1: 00001 (5 bits) \ 
funct3: 000 (3 bits) \
rd: 00111 (5 bits)  \
opcode: 0110011 (7 bits) 

Concatenating all these binary fields: 

0100000 00010 00001 000 00111 0110011 

Finally, converting this binary string to hexadecimal: 

Binary: 0100000 00010 00001 000 00111 0110011 
Hex: 0x400108B3 

The exact 32-bit instruction code for the SUB r7, r1, r2 instruction is: 0x400108B3

This hexadecimal value represents the encoded instruction in RISC-V machine language according to the R-type format.


AND
-

The RISC-V instruction set architecture (ISA) includes various instruction types, each defined by its own format. For your specific instruction, "AND r8, r1, r3," the format is R-type. Below, I'll break down the instruction and explain how to encode it in its 32-bit instruction code format.

R-Type Instruction Format \
R-type instructions are used for register-register operations and have the following fields:

![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/05be8b21-27cc-4e4c-b271-97135eb24681)

opcode: The opcode for R-type instructions (for AND) is 0110011. \
rd: Destination register, r8 which corresponds to 01000.    \
funct3: The function code for AND is 111.    \
rs1: First source register, r1 which corresponds to 00001.  \
rs2: Second source register, r3 which corresponds to 00011.  \
funct7: The function code (7 bits) for AND is 0000000.  

Encoding "AND r8, r1, r3" into 32-bit Instruction Code \
Let's put the fields together:

opcode: 0110011 (bit positions 0-6) \
rd: 01000 (bit positions 7-11) \
funct3: 111 (bit positions 12-14) \
rs1: 00001 (bit positions 15-19) \
rs2: 00011 (bit positions 20-24) \
funct7: 0000000 (bit positions 25-31) 

Concatenating these binary strings together gives us the 32-bit instruction:

0000000 00011 00001 111 01000 0110011

When you concatenate these fields, you get:

0000000 00011 00001 111 01000 0110011

Converting to Hexadecimal \
To make it easier to read and use, let's convert this binary instruction to hexadecimal.

Split into 4-bit segments: 0000 0000 0011 0000 0111 1010 0001 1001 \
Convert each segment to hex:
0000 -> 0 \
0000 -> 0 \
0011 -> 3 \
0000 -> 0 \
0111 -> 7 \
1010 -> A \
0001 -> 1 \
1001 -> 9 \
So, the hexadecimal representation of the 32-bit instruction is:0x00307A19.







