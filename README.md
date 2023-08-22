# PES_ASIC_RISCV_Course_7th_Sem

## Day 1 
### Instruction Set Architecture
+ An Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software. The ISA acts as an interface between the hardware and the software, specifying both what the processor is capable of doing as well as how it gets done.
+ RISC-V[b] (pronounced "risk-five") is an open standard instruction set architecture (ISA) based on established reduced instruction set computer (RISC) principles. Unlike most other ISA designs, RISC-V is provided under royalty-free open-source licenses. A number of companies are offering or have announced RISC-V hardware; open source operating systems with RISC-V support are available, and the instruction set is supported in several popular software toolchains.
### Integer Number Representation
+ Unsigned numbers:- also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.(Range: [0, (2^n)-1 ])
+ Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.(Range : Positive : [0 , 2^(n-1)-1] Negative : [-1 to 2^(n-1)])

### Some RISCV Assemmbly Instructions leartn
+ lui: Load Upper Immediate 

![LUI](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/28ee7cf1-99fd-4fb8-979e-5ddb95b0f8f4)

+ addi: Add immediate

![addi](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/5ff94dea-4d32-4943-b0ea-441e9196d299)

### Some basic commands and brief explanation
+ RISCV GCC compilation
~~~
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o <filename.o> <filename.c>
~~~
 + O1 -> will do normal compilation
 + Ofast -> will do compilation in such a way that the number of lines in the assembly code is reduced

```
riscv64-unknown-elf-objdump -d <filename.o>
riscv64-unknown-elf-objdump -d <filename.o> | less
```
 + /main -> will give you the main function's assembly code

+ Spike simulation
```
spike pk <filename.o>
```
 + This will give the output same as that obtained when ./<filename.o> is run

+ Spike Debugger
```
spilke -d pk <filename.o>
```
 + This will open debugger,  which can be used to perform debugging which includes execution of assembly code lines manually
```
: until pc 0 100b0
```
 + This will run the assembly codes from 0 to 100b0 locations
 + From 100b0 onwards it will enable us to run manually
```
: reg 0 a2
```
 + This will show the contents of the register a2. 0 means core 0
 + Press enter to run the next instruction
	
 
Dropdown
<details>
<summary>Sum of numbers from 1 to n</summary>
  
+ Run sum_1_to_n.c
```
gcc sum_1_to_n.c
./a.out
```
![sum1ton_c_compilation](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/9fc77570-4ffd-4e7a-a22e-59efdcb7ea79)
</details>

<details>
<summary>GCC compile modes and disassemble instruction comparison</summary>

+ RISCV GCC compilation with O1 and | less
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum_1_to_n.o sum_1_to_n.c
riscv64-unknown-elf-objdump -d sum_1_to_n.o | less
```
![sum1ton_riscv_less_O1](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/0e82b3dd-8877-48fd-8238-2add78b885b2)

+RISCV GCC compilation with O1 main function

![sum1ton_riscv_main_O1](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/aed450c1-53ac-4b83-9b75-6050ea1f0657)

+RISCV GCC compilation with Ofast and | less
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum_1_to_n.o sum_1_to_n.c
riscv64-unknown-elf-objdump -d sum_1_to_n.o | less
```
![sum1ton_riscv_less_Ofast](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/c79a4bb2-f93b-467e-b916-733dbd9e1ddf)

+RISCV GCC compilation with Ofast main function

![sum1ton_riscv_main_Ofast](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/962086e0-0f05-4e02-8898-f80a4e1a9845)

</details>
<details>
<summary> Spike simulation of sum of numbers from 1 to n</summary>
  
+ Spike simulation of the RISC V compiled program

![sum1ton_spike](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/d3990f4b-453d-495d-bfdb-7540eea1f9e3)

+ Spike debugger

![sum1ton_spike_debug](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/96e686fb-0be8-4e31-bf15-2a3e7ee160a4)
  
</details>
<details>
<summary>Finding the maximum and minimum values of a long long unsigned integer</summary>
  
+ Finding the maximum and minimum values of a long long unsigned integer

![unsigned](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e150f2ac-1b6f-4dba-afbf-673412eee5be)

</details>
<details>
<summary>Finding the maximum and minimum values of a long long signed integer</summary>
  
+ Finding the maximum and minimum values of a long long signed integer

![signed](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/3e57b1ac-a916-4819-92b5-9b7c1c27e5a3)

</details>
