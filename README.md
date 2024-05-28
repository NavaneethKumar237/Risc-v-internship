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

Now let's discuss about in detail 
-
ADD
-
This instruction allows add two registers together and save the result in the third one.\ For example: ADD x3, x1, x2. It means add together x1 and x2 and save the result in x3. \As each instruction consists of 32 bits.

The ADD instruction is an R-type (Register) instruction, which has the following format:
![image](https://github.com/NavaneethKumar237/Risc-v-internship/assets/167600626/c9b0647c-5bed-4931-ab5a-cf73677b748f)

32-bit Instruction Code  \
Now, let's put these fields together: \

funct7: 0000000  \
rs2: 00001     \
rs1: 00010     \
funct3: 000    \
rd: 00110      \
opcode: 0110011  \
Putting it all together:  \

31-25	24-20	19-15	14-12	11-7	6-0    \
0000000	00001	00010	000	00110	0110011   \
In binary: 0000000 00001 00010 000 00110 0110011  \

Convert this to hexadecimal for a more compact representation: \

0000000 is 0x00    \ 
00001 is 0x01 \
00010 is 0x02\
000 is 0x00\
00110 is 0x06\
0110011 is 0x33\
Thus, the 32-bit binary instruction can be written as: 0x00200633












