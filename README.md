VSD RISC-V INTERNSHIP  / MAKING A GAME CONSOLE USING VSDSQUADRON MINI 
-
-----------------------------------------


# Task-1 : Installing the Oracle Virutal Machine and running Basic C Program 
-
 For installing the oracle virutal machine go through the folling website 
https://www.virtualbox.org/wiki/Downloads

install the virtual machie

 We are creating the Virtual Hard Disk by including the VDI  file
 -
 
Now we are starting compiling with simple c program

Type the following commands

```$ cd 
$ gedit sum1ton.c
```
we will get an interface page to write c program

![Screenshot from 2024-05-24 14-59-13](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/a7189e2e-6635-4e5e-8bab-f8978ce23981)

save the program and compile it 
```
$ gcc sum1ton.c                   
$ ./a.out                          
```

![Screenshot from 2024-05-24 14-58-55](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/f756d24b-6a40-488d-8a84-1352dc12e98f)

we can see the output sum of 6 numbers is 21 

compiling same program with risc-v compiler
-
```
$ cat 1ton.c 
```
that display the total program in the terminal 

![Screenshot from 2024-05-24 16-00-04](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/e5f929ee-ba97-477f-a1a2-d1472797f3ec)


next converting in to .o file 
```
$ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c 
$ ls -ltr sum1ton.o    
```
![Screenshot from 2024-05-24 14-55-13](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/fb1494b4-57b8-4da9-89a7-3a415c79ad64)

Opening the another tab of terminal to get list of instructions \
and type the command \
```
$ risc-v64-unknown-elf-objdump -d sum1ton.o 
```
we will get the set of instructions
![Screenshot from 2024-05-24 14-55-20](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/acbfca4e-4c2b-45b2-88ae-14b8aa464687)

 Now type / main and then type n
 we will get instructions of main There are 11 number of instructions

 ![Screenshot from 2024-05-24 18-33-26](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/d195ebaa-6165-4f36-81fa-651e771ccec0)


now compling with another command 
```
$ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c 
```
here is how it done
![Screenshot from 2024-05-24 18-38-14](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/604e1603-6ccc-47ef-9531-27ad12bb17c0)

and the output we got 11 number of instructions

![Screenshot from 2024-05-24 18-38-27](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/1fda23bb-209b-4609-afb1-e8ede9d689db)

 we can observe that in the both outputs we got 11 istructions......

 #Task 2
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
These Instructions using 3 register inputs - add, xor, 

![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/62d395ba-7f8f-40a8-bdf2-b63b71fc5f2d)

Opcode: 7 bits \
Rd: 5 bits (destination register) \
Funct3: 3 bits \
Rs1: 5 bits (source register 1) \
Rs2: 5 bits (source register 2) \
Funct7: 7 bits

I-type (Immediate): Used for immediate arithmetic, loads, etc.
-
The 12-bit signed immediate is added to the
base address in register rs1 to form the
memory address \
This is very similar to the add-immediate
operation but used to create address, not to
create final result \
• Value loaded from memory is stored in rd

![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/2b29ca68-405e-454a-990b-e7585ebc11e0)

Opcode: 7 bits \
Rd: 5 bits (destination register) \
Funct3: 3 bits \
Rs1: 5 bits (source register) \
Imm: 12 bits (immediate value) 

S-type (Store): Used for store instructions.
-

Store needs to read two registers, rs1 for base memory
address, and rs2 for data to be stored, as well as need
immediate offset! \
• Can’t have both rs2 and immediate in same place as other
instructions! \
• Note: stores don’t write a value to the register file, no rd!
• RISC-V design decision is move low 5 bits of immediate to
where rd field was in other instructions – keep rs1/rs2
fields in same place \
• register names more critical than immediate bits in hardware
design

![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/62f788f6-ae3e-48d5-a42a-afdefb54e8e5)

Opcode: 7 bits \
Imm[4:0]: 5 bits (lower bits of immediate) \
Funct3: 3 bits \
Rs1: 5 bits (source register) \
Rs2: 5 bits (source register 2) \
Imm[11:5]: 7 bits (upper bits of immediate)

B-type (Branch): Used for branch instructions.
-
B-format is mostly same as S-Format, with two
register sources (rs1/rs2) and a 12-bit
immediate \
• But now immediate represents values -212 to
+212-2 in 2-byte increments \
• The 12 immediate bits encode even 13-bit
signed byte offsets (lowest bit of offset is always
zero, so no need to store it) 


![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/88fd3257-892c-475c-9bb5-301984d8faec)

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

![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/98365856-040b-43d4-ab86-9ed69e008a4b)

Has 20-bit immediate in upper 20 bits of
32-bit instruction word \
One destination register, rd \
Used for two instructions \
LUI – Load Upper Immediate \
AUIPC – Add Upper Immediate to PC 

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


![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/1d4c546a-3730-4830-b621-e64a6f3890cb)

Now let's go through some examples.
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

IN this way we are going to format for below RISC-V instructions

ADD r6, r2, r1

SUB r7, r1, r2 

AND r8, r1, r3 

OR r9, r2, r5 

XOR r10, r1, r4 

SLT r11, r2, r4 

ADDI r12, r4, 5 

SW r3, r1, 2 

SRL r16, r14, r2 

BNE r0, r1, 20 

BEQ r0, r0, 15 

LW r13, r1, 2 

SLL r15, r1, r2 

#Task-3
=
 Simulation of RISC-V Core Verilog netlist 
 -

Before going to the work let's learn some key words

* IVERILOG : This is a linux based simulator, Verilog is an implementation of the Verilog hardware description language compiler that generates netlists in the desired format and a simulator

* GTKWAVE : GTKWave is a fully featured GTK+ wave viewer for Unix, Win32, and Mac OSX which reads LXT, LXT2, VZT, FST, and GHW files as well as standard Verilog VCD/EVCD files and allows their viewing

  The above compilers are most important for getting our signal wave forms now we need to install them , we used Icarus Verilog & GTKWave Analyzer V3.3.86 now.

  For istalling we need to use these commands

  $ sudo apt update

  ![Screenshot from 2024-06-01 07-47-12](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/714a977e-36f7-4c1c-8b8b-e226cfe290e6)

  $ sudo apt install iverilog gtkwave

  ![Screenshot from 2024-06-01 07-51-10](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/f6dfff75-640b-4c84-abe9-3f1a369512ce)


Now we installed the compilers in our pc now we need to clone the github repo

$ git clone https://github.com/vinayrayapati/rv32i \
$ cd rv32i

![Screenshot from 2024-06-01 07-55-01](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/3f67e2b3-625d-4433-a1d1-67f8582d54ed)

After cloning the github repo ,now we need to compile the programa and see the output waveforms 
  
we have to create one iiitb_rv32i.vcd dump file to get the output the command as follows

$ iverilog -o iiitb_rv32i iiitb_rv32i.v iiitb_rv32i_tb.v \
$ ./iiitb_rv32i

Now we created the file Lets see the output in the gkt wave vertilog 

use this command in the terminal

$ gtkwave iiitb_rv32i.vcd

![Screenshot from 2024-06-01 07-55-01](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/e8f6e4f1-488d-4c87-9686-84ce4af82d3c)


 Now we get the output in the wave forms 

Below we can see the output wave forms.....

![Screenshot from 2024-06-01 08-11-59](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/26532679-4d42-4522-9593-07fc64faad80)

Pipeline Stages and Signals


Instruction Fetch (IF): 
-
Fetches the instruction from memory. \
Relevant signals: IF_ID_IR[31:0], IF_ID_NPC[31:0].

Instruction Decode (ID): 
-
Decodes the fetched instruction and reads operands from the register file. \
Relevant signals: ID_EX_A[31:0], ID_EX_B[31:0], ID_EX_IMMEDIATE[31:0], ID_EX_NPC[31:0].

Execute (EX): 
-
Performs arithmetic or logical operations. \
Relevant signals: EX_MEM_ALUOUT[31:0], EX_MEM_IR[31:0], BR_EN.

Memory Access (MEM): 
-
Accesses memory for load and store instructions. \
Signals passing to this stage: EX_MEM_ALUOUT[31:0], EX_MEM_IR[31:0].

Write Back (WB): 
-
Writes the result back to the register file. \
Signals passing from the MEM stage to WB are not shown, but EX_MEM_ALUOUT[31:0] often becomes a part of this stage.

-------------------------------------------------------------------------------------------------------------

BR_EN (Branch Enable):
-
This signal indicates whether a branch instruction is enabled. It's used to control the flow of execution based on branch conditions.

![Screenshot from 2024-06-01 08-19-55](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/f7c2617a-3ab1-4032-b250-c706ccde6107)

EX_MEM_ALUOUT[31:0] (Execute/Memory ALU Output):
-
This signal holds the output from the Arithmetic Logic Unit (ALU) during the Execute stage and is passed to the Memory stage. It represents the result of an arithmetic or logical operation.

![Screenshot from 2024-06-01 11-34-04](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/c519e767-1461-482a-8caa-ff840ffd4c74)

EX_MEM_IR[31:0] (Execute/Memory Instruction Register):
-
This signal contains the instruction being processed in the Execute stage and passed to the Memory stage. It helps keep track of which instruction is being executed.

![Screenshot from 2024-06-01 08-21-06](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/33a08f91-6e75-48f7-a568-5976e1d01d21)

ID_EX_A[31:0] (Instruction Decode/Execute Operand A):
-
This signal holds the value of the first operand (source register A) being used in the Execute stage. It's fetched from the register file during the Instruction Decode stage.

ID_EX_B[31:0] (Instruction Decode/Execute Operand B):
-
Similar to ID_EX_A[31:0], this signal holds the value of the second operand (source register B) being used in the Execute stage.

![Screenshot from 2024-06-01 08-21-44](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/5ed5b855-de14-4526-934c-dac0514cf453)

ID_EX_IMMEDIATE[31:0] (Instruction Decode/Execute Immediate):
-
This signal contains the immediate value extracted from the instruction during the Decode stage, which is used in the Execute stage for operations requiring an immediate operand.

![Screenshot from 2024-06-01 11-36-23](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/769e763a-aa4d-46df-b2a4-e8bf78b4c326)

ID_EX_NPC[31:0] (Instruction Decode/Execute Next Program Counter):
-
This signal holds the next program counter value calculated during the Decode stage and used in the Execute stage for branch and jump instructions.

![Screenshot from 2024-06-01 15-10-51](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/34fa85ea-6fd6-4ec5-bcdb-7af01eb3e658)


IF_ID_IR[31:0] (Instruction Fetch/Instruction Decode Instruction Register):
-
This signal contains the instruction fetched from memory during the Instruction Fetch stage and passed to the Instruction Decode stage. It's the current instruction being decoded.

![Screenshot from 2024-06-01 11-36-45](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/25df3ee0-1300-423a-8149-8c8a81481bdd)


IF_ID_NPC[31:0] (Instruction Fetch/Instruction Decode Next Program Counter):
-
This signal holds the next program counter value calculated during the Instruction Fetch stage and passed to the Instruction Decode stage. It points to the address of the next instruction to be executed.

,![Screenshot from 2024-06-01 15-11-19](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/d63e14c4-8c86-4264-9052-61250256874c)

  
By analyzing these signals in GTKWave, we can observe how instructions progress through each pipeline stage, inspect the values of operands and results of operations, and debug issues like incorrect instruction execution, data hazards, or control hazards. This helps in ensuring that the processor pipeline works as intended and meets design specifications.

---------------------------------------------------------------
## Final_project

#task 4
=

# MAKING A GAME COSOLE USING VSDSQUADRON MINI

![f575878f-6447-4391-aa24-13d8dac9a91f](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/1f3854c4-914c-476d-86c1-c3d3075f5d26)

INTRODUCTION
-


A game console is a device used to connect to a display for playing games. I have developed a game console using the VSDSquadron Mini. We used an OLED display to view the games, making it possible to play games directly on this compact and efficient setup. This application showcases the capabilities of the VSDSquadron Mini.

OVERVIEW
-
This is a smiple model of the game console had 5 push buttons and oled disply to show and a power switch 
we need to connect all the all the components to vsdsquadron mini we have to upload the specific code in to it to get the desired game
The heart of the game console is a RISC-V based microcontroller based vsd mini board  , providing an open-source, highly efficient, and customizable platform for many applications.

------------------------------------------------------------
LIST OF COMPONENTS
-
1. VSDsquadron mini 
2. 5 push buttons
3. zero PCB
4. jumper  wires
5. OLED display
6. Resistors of differnt values

HARDWARE CONNECTIONS
=
---------------------------------------------------------

CIRCUI DIAGRAM
-

![f575878f-6447-4391-aa24-13d8dac9a91f](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/1f3854c4-914c-476d-86c1-c3d3075f5d26)


PINOUT
-
 ![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/90fd5f59-ad37-4515-8948-5095136b599a)

![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/251a0b5a-1739-4686-b5a4-379f28fa29b0)


SOFTWARE REQUIREMENTS
=
I have used the linux to upload the code we need to install the required tools related to the risc-v 
next you need to Install the toolchain (GCC compiler, Python3, and PyUSB):

```sudo apt install build-essential libnewlib-dev gcc-riscv64-unknown-elf
sudo apt install python3 python3-pip
python3 -m pip install pyus
```

 Open a terminal and navigate to the folder with the makefile. Run the following command to compile and upload:
 ```make flash
 ```
If you want to just upload the pre-compiled binary, run the following command instead:

```python3 .tools/rvprog.py -f <firmware>.bin
```

Working code
-





```

#include <driver.h>           // TinyJoypad conversion driver
#include <spritebank.h>       // grafix

// ===================================================================================
// Global Variables
// ===================================================================================
uint8_t Live = 0;
uint8_t ShieldRemoved = 0;
uint8_t MONSTERrest = 0;
uint8_t LEVELS = 0;
uint8_t SpeedShootMonster = 0;
uint8_t ShipDead = 0;
uint8_t ShipPos = 56;

#define SHOOTS 2

// ===================================================================================
// Function Prototypes
// ===================================================================================
void LoadMonstersLevels(int8_t Levels, SPACE *space);
void SnD(int8_t Sp_, uint8_t SN);
void SpeedControle(SPACE *space);
void GRIDMonsterFloorY(SPACE *space);
uint8_t LivePrint(uint8_t x, uint8_t y);
void Tiny_Flip(uint8_t render0_picture1, SPACE *space);
uint8_t UFOWrite(uint8_t x, uint8_t y, SPACE *space);
void UFOUpdate(SPACE *space);
void ShipDestroyByMonster(SPACE *space);
void MonsterShootupdate(SPACE *space);
void MonsterShootGenerate(SPACE *space);
uint8_t MonsterShoot(uint8_t x, uint8_t y, SPACE *space);
uint8_t ShieldDestroy(uint8_t Origine, uint8_t VarX, uint8_t VarY, SPACE *space);
void ShieldDestroyWrite(uint8_t BOOLWRITE, uint8_t line, SPACE *space, uint8_t Origine);
uint8_t MyShield(uint8_t x, uint8_t y, SPACE *space);
uint8_t ShieldBlitz(uint8_t Part, uint8_t LineSH);
uint8_t BOOLREAD(uint8_t SHnum, uint8_t LineSH, SPACE *space);
void RemoveExplodOnMonsterGrid(SPACE *space);
uint8_t background(uint8_t x, uint8_t y, SPACE *space);
uint8_t Vesso(uint8_t x, uint8_t y, SPACE *space);
void UFO_Attack_Check(uint8_t x, SPACE *space);
uint8_t MyShoot(uint8_t x, uint8_t y, SPACE *space);
void Monster_Attack_Check(SPACE *space);
int8_t OuDansLaGrilleMonster(uint8_t x, uint8_t y, SPACE *space);
uint8_t SplitSpriteDecalageY(uint8_t Input, uint8_t UPorDOWN, SPACE *space);
uint8_t Murge_Split_UP_DOWN(uint8_t x, SPACE *space);
uint8_t WriteMonster14(uint8_t x);
uint8_t Monster(uint8_t x, uint8_t y, SPACE *space);
uint8_t MonsterRefreshMove(SPACE *space);
void VarResetNewLevel(SPACE *space);

// ===================================================================================
// Main Function
// ===================================================================================
int main(void) {
  // Setup
  JOY_init();

  // Loop
  while(1) {
    uint8_t Decompte = 0;
    uint8_t VarPot;
    uint8_t MyShootReady = SHOOTS;
    SPACE space;

  NEWGAME:
    Live = 3;
    LEVELS = 0;
    Tiny_Flip(1, &space);
    while(1) {
      if(JOY_act_pressed()) {
        JOY_sound(100, 125); JOY_sound(50, 125);
        goto BYPASS2;
      }
    }

  NEWLEVEL:
    JOY_DLY_ms(1000);

  BYPASS2:
    VarResetNewLevel(&space);
    SpeedControle(&space);
    VarPot = 54;
    ShipPos = 56;
    space.ScrBackV=(ShipPos / 14) + 52;
    goto Bypass;

  RestartLevel:
    if(Live > 0) Live--;
    else goto NEWGAME;

  Bypass:
    ShipDead = 0;
    Decompte = 0;
    Tiny_Flip(0, &space);
    JOY_DLY_ms(1000);
    while(1) {
      if(MONSTERrest == 0) { 
        JOY_sound(110, 255); JOY_DLY_ms(40); JOY_sound(130, 255); JOY_DLY_ms(40);
        JOY_sound(100, 255); JOY_DLY_ms(40); JOY_sound(1, 155);   JOY_DLY_ms(20);
        JOY_sound(60, 255);  JOY_sound(60, 255);
        if(LEVELS < 9) LEVELS++;
        goto NEWLEVEL;
      }
      if((((space.MonsterGroupeYpos) + (space.MonsterFloorMax + 1)) == 7) && (Decompte == 0)) ShipDead = 1;
      if(SpeedShootMonster <= 9 - LEVELS) SpeedShootMonster++;
      else {SpeedShootMonster = 0; MonsterShootGenerate(&space);}
      space.ScrBackV = (ShipPos / 14) + 52;
      Tiny_Flip(0, &space);
      space.oneFrame = !space.oneFrame;
      RemoveExplodOnMonsterGrid(&space);
      MonsterShootupdate(&space);
      UFOUpdate(&space);
      if(((space.MonsterGroupeXpos >= 26) && (space.MonsterGroupeXpos <= 28))
        && (space.MonsterGroupeYpos == 2) && (space.DecalageY8 == 4)) space.UFOxPos = 127;
      if(VarPot > (ShipPos + 2)) ShipPos = ShipPos + ((VarPot - ShipPos) / 3);
      if(VarPot < (ShipPos - 2)) ShipPos = ShipPos - ((ShipPos - VarPot) / 3);
      if(ShipDead != 1) {
        if(space.frame < space.frameMax) space.frame++;
        else {
          GRIDMonsterFloorY(&space);
          space.anim = !space.anim;
          if(space.anim == 0) SnD(space.UFOxPos, 200);
          else SnD(space.UFOxPos, 100);
          MonsterRefreshMove(&space);
          space.frame = 0;
        }

        if(JOY_left_pressed()) {
          if(VarPot > 5) VarPot = VarPot - 6;
        }
        if(JOY_right_pressed()) {
          if(VarPot < 108) VarPot = VarPot + 6;
        }
        if((JOY_act_pressed()) && (MyShootReady == SHOOTS)) {
          JOY_sound(200, 4); MyShootReady = 0; space.MyShootBall = 6; space.MyShootBallxpos = ShipPos + 6;
        }
      }
      else {
        JOY_sound(80, 1); JOY_sound(100, 1); 
        Decompte++;
        if(Decompte >= 30) {
          JOY_DLY_ms(600);
          if(((space.MonsterGroupeYpos) + (space.MonsterFloorMax + 1)) == 7) goto NEWGAME;
          else goto RestartLevel;
        }
      }
      if(space.MyShootBall == -1) {
        if(MyShootReady<SHOOTS) MyShootReady++;
      }
    JOY_SLOWDOWN();
    }
  }
}

// ===================================================================================
// Functions
// ===================================================================================
void LoadMonstersLevels(int8_t Levels, SPACE *space) {
  uint8_t x, y;
  for(y=0; y<5; y++) {
    for(x=0; x<6; x++) {
      if(y!=4) space->MonsterGrid[y][x] = MonstersLevels[(Levels * 24) + (y * 6) + x];
      else     space->MonsterGrid[y][x] = -1;
    }
  }
}

void SnD(int8_t Sp_, uint8_t SN) {
  if(Sp_ != -120) {JOY_sound(220, 8); JOY_sound(200, 4);}
  else JOY_sound(SN, 1);
}

void SpeedControle(SPACE *space) {
  uint8_t xx, yy;
  MONSTERrest = 0;
  for(yy=0; yy<4; yy++) {
    for(xx=0; xx<6; xx++) {
      if((space->MonsterGrid[yy][xx] != -1) && ((space->MonsterGrid[yy][xx] <=5 ))) MONSTERrest++;
    }
  }
  space->frameMax = (MONSTERrest >> 3);
}

// Thanks to Sven Bruns for informing me of an error in this function!
void GRIDMonsterFloorY(SPACE *space) {
  uint8_t y,x;
  space->MonsterFloorMax = 3;
  for(y=0; y<4; y++) {
    for(x=0; x<6; x++) {
      if(space->MonsterGrid[3-y][x] != -1) return;
    }
    space->MonsterFloorMax = space->MonsterFloorMax - 1;
  }
}

uint8_t LivePrint(uint8_t x, uint8_t y) {
  #define XLIVEWIDE ((5 * Live) - 1)
  if((0 >= (x - XLIVEWIDE)) && (y == 7)) {
    return LIVE[x];
  }
  return 0x00;
}

void Tiny_Flip(uint8_t render0_picture1, SPACE *space) {
  uint8_t y, x; 
  uint8_t MYSHIELD = 0x00;
  for(y=0; y<8; y++) {
    JOY_OLED_data_start(y);
    for(x=0; x<128; x++) {
      if(render0_picture1 == 0) {
        if(ShieldRemoved == 0) MYSHIELD = MyShield(x, y, space);
        else MYSHIELD = 0x00;
        JOY_OLED_send( background(x, y, space)
                       | LivePrint(x, y) 
                       | Vesso(x, y, space)
                       | UFOWrite(x, y, space)
                       | Monster(x, y, space)
                       | MyShoot(x, y, space)
                       | MonsterShoot(x, y, space)
                       | MYSHIELD);
      }
      else JOY_OLED_send(intro[x + (y * 128)]);
    }
    if(render0_picture1 == 0) {
      if(ShieldRemoved == 0) ShieldDestroy(0, space->MyShootBallxpos, space->MyShootBall, space);
    }
    JOY_OLED_end();
  }
  if(render0_picture1 == 0) {
    if(!(space->MonsterGroupeYpos < (2 + (4 - (space->MonsterFloorMax + 1))))) {
      if(ShieldRemoved != 1) {
        space->Shield[0] = 0x00;
        space->Shield[1] = 0x00;
        space->Shield[2] = 0x00;
        space->Shield[3] = 0x00;
        space->Shield[4] = 0x00;
        space->Shield[5] = 0x00;
        ShieldRemoved = 1;
      }
    }
  }
}

uint8_t UFOWrite(uint8_t x, uint8_t y, SPACE *space) {
  if((space->UFOxPos != -120) && (y == 0) && (space->UFOxPos <= x) && (space->UFOxPos >= (x - 14)))
    return Monsters[(x - space->UFOxPos) + (6 * 14) + (space->oneFrame * 14)];
  return 0x00;
}

void UFOUpdate(SPACE *space) {
  if(space->UFOxPos != -120) {
    space->UFOxPos = space->UFOxPos - 2;
    SnD(space->UFOxPos, 0);
    if(space->UFOxPos <= -20) space->UFOxPos = -120;
  }
}

void ShipDestroyByMonster(SPACE *space) {
  if((space->MonsterShoot[1] >= 14) && (space->MonsterShoot[1] <= 15) 
  && (space->MonsterShoot[0] >= ShipPos) && (space->MonsterShoot[0] <= ShipPos+14))
    ShipDead=1;
}

void MonsterShootupdate(SPACE *space) {
  if(space->MonsterShoot[1] != 16) {
    ShipDestroyByMonster(space);
    if(ShieldDestroy(1, space->MonsterShoot[0], space->MonsterShoot[1] >> 1, space))
      space->MonsterShoot[1] = 16;
    else
      space->MonsterShoot[1] = space->MonsterShoot[1] + 1;
  }
}

void MonsterShootGenerate(SPACE *space) {
  uint8_t a = JOY_random() % 3; 
  uint8_t b = JOY_random() % 6; 
  if(b >= 5) b = 5;
  if(space->MonsterShoot[1] == 16) {
    if(space->MonsterGrid[a][b] != -1) {
      space->MonsterShoot[0] = (space->MonsterGroupeXpos + 7) + (b * 14);
      space->MonsterShoot[1] = ((space->MonsterGroupeYpos + a) * 2) + 1;
    }
  }
}

uint8_t MonsterShoot(uint8_t x, uint8_t y, SPACE *space) {
  if(((space->MonsterShoot[1] >> 1) == y) && (space->MonsterShoot[0] == x)) {
    if((space->MonsterShoot[1] & 1) == 0) return 0b00001111;
    else return 0b11110000;
  }
  return 0x00;
}

uint8_t ShieldDestroy(uint8_t Origine, uint8_t VarX, uint8_t VarY, SPACE *space) {
  #define OFFSETXSHIELD -1
  if(VarY == 6) {
    if((VarX >= 20 + OFFSETXSHIELD) && (VarX <= 27 + OFFSETXSHIELD)) {
      if(BOOLREAD(0, VarX - (20 + OFFSETXSHIELD), space)) {
        ShieldDestroyWrite(0, VarX - (20 + OFFSETXSHIELD), space, Origine);
        return 1;
      }
    }
    if((VarX >= 28 + OFFSETXSHIELD) && (VarX <= 35 + OFFSETXSHIELD)) {
      if(BOOLREAD(1, VarX - (28 + OFFSETXSHIELD), space)) {
        ShieldDestroyWrite(1, VarX - (28 + OFFSETXSHIELD), space, Origine);
        return 1;
      }
    }
    if((VarX >= 55 + OFFSETXSHIELD) && (VarX <= 62 + OFFSETXSHIELD)) {
      if(BOOLREAD(2, VarX - (55 + OFFSETXSHIELD), space)) {
        ShieldDestroyWrite(2, VarX - (55 + OFFSETXSHIELD), space, Origine);
        return 1;
      }
    }
    if((VarX >= 63 + OFFSETXSHIELD) && (VarX <= 70 + OFFSETXSHIELD)) {
      if(BOOLREAD(3, VarX - (63 + OFFSETXSHIELD), space)) {
        ShieldDestroyWrite(3, VarX - (63 + OFFSETXSHIELD), space, Origine);
        return 1;
      }
    }
    if((VarX >= 90 + OFFSETXSHIELD) && (VarX <= 97 + OFFSETXSHIELD)) {
      if(BOOLREAD(4, VarX - (90 + OFFSETXSHIELD), space)) {
        ShieldDestroyWrite(4, VarX - (90 + OFFSETXSHIELD), space, Origine);
        return 1;
      }
    }
    if((VarX >= 98 + OFFSETXSHIELD) && (VarX <= 105 + OFFSETXSHIELD)) {
      if(BOOLREAD(5, VarX - (98 + OFFSETXSHIELD), space)) {
        ShieldDestroyWrite(5, VarX - (98 + OFFSETXSHIELD), space, Origine);
        return 1;
      }
    }
  }
  return 0;
}

void ShieldDestroyWrite(uint8_t BOOLWRITE, uint8_t line, SPACE *space, uint8_t Origine) {
  switch(line) {
    case 0:
      space->Shield[BOOLWRITE] = space->Shield[BOOLWRITE] - 128;
      if(Origine == 0) space->MyShootBall = -1;
      break;
    case 1:
      space->Shield[BOOLWRITE] = space->Shield[BOOLWRITE] - 64;
      if(Origine == 0) space->MyShootBall = -1;
      break;
    case 2:
      space->Shield[BOOLWRITE] = space->Shield[BOOLWRITE] - 32;
      if(Origine == 0) space->MyShootBall = -1;
      break;
    case 3:
      space->Shield[BOOLWRITE] = space->Shield[BOOLWRITE] - 16;
      if(Origine == 0) space->MyShootBall = -1;
      break;
    case 4:
      space->Shield[BOOLWRITE] = space->Shield[BOOLWRITE] - 8;
      if(Origine == 0) space->MyShootBall = -1;
      break;
    case 5:
      space->Shield[BOOLWRITE] = space->Shield[BOOLWRITE] - 4;
      if(Origine == 0) space->MyShootBall = -1;
      break;
    case 6:
      space->Shield[BOOLWRITE] = space->Shield[BOOLWRITE] - 2;
      if(Origine == 0) space->MyShootBall = -1;
      break;
    case 7:
      space->Shield[BOOLWRITE] = space->Shield[BOOLWRITE] - 1;
      if(Origine == 0) space->MyShootBall = -1;
      break;
    default:
      break;
  }
}

uint8_t MyShield(uint8_t x, uint8_t y, SPACE *space) {
  #define OFFSETXSHIELD -1
  if(y != 6) return 0x00;
  if((x >= 20 + OFFSETXSHIELD) && (x <= 27 + OFFSETXSHIELD)) {
    if(BOOLREAD(0, x - (20 + OFFSETXSHIELD), space)) return ShieldBlitz(0, x - (20 + OFFSETXSHIELD));
    else return 0x00;
  }
  if((x >= 28 + OFFSETXSHIELD) && (x <= 35 + OFFSETXSHIELD)) {
    if(BOOLREAD(1, x - (28 + OFFSETXSHIELD), space)) return ShieldBlitz(1, x - (28 + OFFSETXSHIELD));
    else return 0x00;
  }
  if((x >= 55 + OFFSETXSHIELD) && (x <= 62 + OFFSETXSHIELD)) {
    if(BOOLREAD(2, x - (55 + OFFSETXSHIELD), space)) return ShieldBlitz(0, x - (55 + OFFSETXSHIELD));
    else return 0x00;
  }
  if((x >= 63 + OFFSETXSHIELD) && (x <= 70 + OFFSETXSHIELD)) {
    if(BOOLREAD(3, x - (63 + OFFSETXSHIELD), space)) return ShieldBlitz(1, x - (63 + OFFSETXSHIELD));
    else return 0x00;
  }
  if((x >= 90 + OFFSETXSHIELD) && (x <= 97 + OFFSETXSHIELD)) {
    if(BOOLREAD(4, x - (90 + OFFSETXSHIELD), space)) return ShieldBlitz(0, x - (90 + OFFSETXSHIELD));
    else return 0x00;
  }
  if((x >= 98 + OFFSETXSHIELD) && (x <= 105 + OFFSETXSHIELD)) {
    if(BOOLREAD(5, x - (98 + OFFSETXSHIELD), space)) return ShieldBlitz(1, x - (98 + OFFSETXSHIELD));
    else return 0x00;
  }
  return 0x00;
}

uint8_t ShieldBlitz(uint8_t Part, uint8_t LineSH) {
  uint8_t Var0 = 0;
  switch(LineSH) {
    case 0: if(Part == 0) Var0 = 0b11110000; else Var0 = 0b00001111; break;
    case 1: if(Part == 0) Var0 = 0b11111100; else Var0 = 0b00001111; break;
    case 2:
    case 3:
    case 4:
    case 5: Var0 = 0b00001111; break;
    case 6: if(Part == 1) Var0 = 0b11111100; else Var0 = 0b00001111; break;
    case 7: if(Part == 1) Var0 = 0b11110000; else Var0 = 0b00001111; break;
    default: Var0 = 0b00000000; break;
  }
  return Var0;
}

uint8_t BOOLREAD(uint8_t SHnum, uint8_t LineSH, SPACE *space) {
  uint8_t Var0 = 0b10000000 >> LineSH;
  return((space->Shield[SHnum] & Var0) != 0);
}

void RemoveExplodOnMonsterGrid(SPACE *space) {
  uint8_t x, y;
  for(y=0; y<=3; y++) {
    for(x=0; x<=5; x++) {
      if(space->MonsterGrid[y][x] >= 11) space->MonsterGrid[y][x] = -1; 
      if(space->MonsterGrid[y][x] >= 8)  space->MonsterGrid[y][x] = space->MonsterGrid[y][x] + 1;
    }
  }
}

uint8_t background(uint8_t x, uint8_t y, SPACE *space) {
  uint8_t scr = space->ScrBackV + x;
  if(scr > 127) scr = space->ScrBackV + x - 128;
  return(0xff - back[y * 128 + scr]);
}

uint8_t Vesso(uint8_t x, uint8_t y, SPACE *space) {
  if((x - ShipPos >= 0) && (x - ShipPos < 13) && (y==7)) {
    if(ShipDead == 0) return vesso[x - ShipPos];
    else return vesso[x - ShipPos + (12 * space->oneFrame)];
  }
  return 0;
}

void UFO_Attack_Check(uint8_t x, SPACE *space) {
  if(space->MyShootBall == 0) {
    if((space->MyShootBallxpos >= space->UFOxPos) && (space->MyShootBallxpos <= space->UFOxPos + 14)) {
      for(x=1; x<100; x++) JOY_sound(x, 1);
      if(Live < 3) Live++;
      space->UFOxPos =- 120;
    }
  }
}

uint8_t MyShoot(uint8_t x, uint8_t y, SPACE *space) {
  if((space->MyShootBallxpos == x) && (y == space->MyShootBall)) {
    if(space->MyShootBall > -1) space->MyShootBallFrame = !space->MyShootBallFrame;
    else return 0x00;
    if(space->MyShootBallFrame == 1) space->MyShootBall--;
    Monster_Attack_Check(space);
    UFO_Attack_Check(x, space);
    return SHOOT[space->MyShootBallFrame];
  }
  return 0x00;
}

void Monster_Attack_Check(SPACE *space) {
  int8_t Varx = 0, Vary = 0;
  #define Xmouin   (space->MonsterGroupeXpos) 
  #define Ymouin   (space->MonsterGroupeYpos << 3) //-space->DecalageY8
  #define XPlus    (Xmouin + 84)
  #define YPlus    (Ymouin + (4*8))
  #define MYSHOOTX (space->MyShootBallxpos)
  #define MYSHOOTY ((space->MyShootBall << 3) + ((space->MyShootBallFrame + 1) << 2))
  if((MYSHOOTX >= Xmouin) && (MYSHOOTX <= XPlus) && (MYSHOOTY >= Ymouin) && (MYSHOOTY <= YPlus)) {
    //enter in the monster zone
    Vary = (MYSHOOTY - Ymouin + 4) >> 3;
    Varx = (MYSHOOTX - Xmouin + 7) / 14;
    if(Varx < 0) Varx = 0;
    if(Vary < 0) Vary = 0;
    if(Varx > 5) return;
    if(Vary > 3) return;
    if((space->MonsterGrid[Vary][Varx] > -1) && (space->MonsterGrid[Vary][Varx] < 6)) {
      JOY_sound(50, 10);
      space->MonsterGrid[Vary][Varx] = 8;
      space->MyShootBall = -1;
      SpeedControle(space);
    }
    //fin monster zone
  }
}

int8_t OuDansLaGrilleMonster(uint8_t x, uint8_t y, SPACE *space) {
  if(x < space->MonsterGroupeXpos) return -1;
  if(y < space->MonsterGroupeYpos) return -1;
  space->PositionDansGrilleMonsterX = (x - space->MonsterGroupeXpos) / 14;
  space->PositionDansGrilleMonsterY = (y - space->MonsterGroupeYpos);
  if(space->PositionDansGrilleMonsterX > 5) return -1;
  if(space->PositionDansGrilleMonsterY > 4) return -1;
  return 0;
}

uint8_t SplitSpriteDecalageY(uint8_t Input, uint8_t UPorDOWN, SPACE *space) {
  if(UPorDOWN) return(Input << space->DecalageY8);
  else return(Input >> (8 - space->DecalageY8));
}

uint8_t Murge_Split_UP_DOWN(uint8_t x, SPACE *space) {
  int8_t SpriteType = -1;
  int8_t ANIMs = -1;
  uint8_t Murge1 = 0;
  uint8_t Murge2 = 0;
  if(space->DecalageY8 == 0) {
    SpriteType = space->MonsterGrid[space->PositionDansGrilleMonsterY][space->PositionDansGrilleMonsterX];
    if(SpriteType < 8) ANIMs = space->anim * 14;
    else ANIMs = 0;
    if(SpriteType == -1) return 0x00;
    return Monsters[(WriteMonster14(x - space->MonsterGroupeXpos) + SpriteType * 14) + ANIMs];
  }
  else {
    //debut
    if(space->PositionDansGrilleMonsterY == 0) {
      SpriteType = space->MonsterGrid[space->PositionDansGrilleMonsterY][space->PositionDansGrilleMonsterX];
      if(SpriteType < 8) ANIMs = space->anim * 14;
      else ANIMs = 0;
      if(SpriteType != -1) Murge2 = SplitSpriteDecalageY(Monsters[(WriteMonster14(x - space->MonsterGroupeXpos) + SpriteType * 14) + ANIMs], 1, space);
      else Murge2 = 0x00;
      return Murge2;
    }
    else {
      SpriteType = space->MonsterGrid[space->PositionDansGrilleMonsterY - 1][space->PositionDansGrilleMonsterX];
      if(SpriteType < 8) ANIMs = space->anim * 14;
      else ANIMs = 0;
      if(SpriteType != -1) Murge1 = SplitSpriteDecalageY(Monsters[(WriteMonster14(x - space->MonsterGroupeXpos) + SpriteType * 14) + ANIMs], 0, space);
      else Murge1 = 0x00;
      SpriteType = space->MonsterGrid[space->PositionDansGrilleMonsterY][space->PositionDansGrilleMonsterX];
      if(SpriteType < 8) ANIMs = space->anim * 14;
      else ANIMs = 0;
      if(SpriteType != -1) Murge2 = SplitSpriteDecalageY(Monsters[(WriteMonster14(x - space->MonsterGroupeXpos) + SpriteType * 14) + ANIMs], 1, space);
      else Murge2 = 0x00;
      return(Murge1 | Murge2);
    }  
  } //fin
}

uint8_t WriteMonster14(uint8_t x) {
  while(x >= 14) x -= 14;
  return x;
}

uint8_t Monster(uint8_t x, uint8_t y, SPACE *space) {
  if(OuDansLaGrilleMonster(x, y, space) != -1) return  Murge_Split_UP_DOWN(x, space);
  return 0x00;
}

uint8_t MonsterRefreshMove(SPACE *space) {
  if(space->Direction == 1) {
    if(space->MonsterGroupeXpos < space->MonsterOffsetDroite) {
      space->MonsterGroupeXpos = space->MonsterGroupeXpos + 2;
      return 0;
    }
    else {
      if(space->DecalageY8 < 7) {
        space->DecalageY8 = space->DecalageY8 + 4;
        if(space->DecalageY8 > 7) space->DecalageY8 = 7; 
      }
      else {
        space->MonsterGroupeYpos++;
        space->DecalageY8 = 0;
      }
      space->Direction = 0;
      return 0;
    }
  }
  else {
    if(space->MonsterGroupeXpos > space->MonsterOffsetGauche) {
      space->MonsterGroupeXpos = space->MonsterGroupeXpos - 2;
      return 0;
    }
    else {
      if(space->DecalageY8 < 7) {
        space->DecalageY8 = space->DecalageY8 + 4;
        if(space->DecalageY8 > 7) space->DecalageY8 = 7;
      }
      else {
        space->MonsterGroupeYpos++;
        space->DecalageY8 = 0;
      }
      space->Direction = 1;
      return 0;
    }
  }
}

void VarResetNewLevel(SPACE *space) {
  ShieldRemoved = 0;
  SpeedShootMonster = 0;
  MONSTERrest = 24;
  LoadMonstersLevels(LEVELS, space);
  space->Shield[0] = 255;
  space->Shield[1] = 255;
  space->Shield[2] = 255;
  space->Shield[3] = 255;
  space->Shield[4] = 255;
  space->Shield[5] = 255;
  space->MonsterShoot[0] = 16;
  space->MonsterShoot[1] = 16;
  space->UFOxPos = -120;

  space->MyShootBall = -1;
  space->MyShootBallxpos = 0;
  space->MyShootBallFrame = 0;
  space->anim = 0;
  space->frame = 0;
  space->PositionDansGrilleMonsterX = 0;
  space->PositionDansGrilleMonsterY = 0;
  space->MonsterFloorMax = 3;
  space->MonsterOffsetGauche = 0;
  space->MonsterOffsetDroite = 44;
  space->MonsterGroupeXpos = 20;
  if(LEVELS > 3) space->MonsterGroupeYpos = 1;
  else space->MonsterGroupeYpos = 0;
  space->DecalageY8 = 0;
  space->frameMax = 8;
  space->Direction = 1; //1 right 0 gauche
  space->oneFrame = 0;
}
```



GAMES
=
There are many games but i got stucked with the tiny invaders that was my childhood favourate game 
-

Tiny Invaders
-



![WhatsApp Image 2024-06-08 at 8 35 32 AM](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/7e566995-a99a-48a3-8065-f27c93e4a7bb)


![WhatsApp Image 2024-06-08 at 8 35 31 AM](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/bfb99085-bcf5-486a-9394-edf84c9d7ce0)






Tiny Lander
-




![WhatsApp Image 2024-06-08 at 8 35 34 AM (1)](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/9feb1697-4776-49e3-aba9-a433682249bb)

![WhatsApp Image 2024-06-08 at 8 35 33 AM](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/12f81480-3cce-4443-8764-c86790ab85a3)





Tiny Arkanoid
-




![WhatsApp Image 2024-06-08 at 8 35 33 AM](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/88d73dbe-6949-4473-849d-52e55d2cc14f)

![WhatsApp Image 2024-06-08 at 8 35 32 AM](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/257629a9-6e16-4929-bf1c-3b9eaad5bec8)




Tiny Pacman
-


![WhatsApp Image 2024-06-08 at 8 35 30 AM](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/c98669b0-b33d-46a9-952d-9fad5877b09f)

--------------------------------------------------------------

OUTPUT VIDEO
=


https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/2f5b777e-b68f-4eff-8fa0-3c57443e0724


https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/8b3b07a9-b928-444d-8940-2c808f9fe0eb







----------------------------------------------------------
# Acknowledgement


I am B. Navaneeth Kumar, and I am deeply thankful to my mentor, Kunal Ghosh, for his marvelous training in RISC-V and VLSI using VSDsquadron mini. I am grateful for the great opportunity to work with him and am always ready to collaborate with Mr. Kunal Ghosh, the founder & CEO of VLSI System Design.






