# PES_Asic_course_7th_sem
# PES_ASIC_Class

## Day1 
### Instruction Set Architecture
+An Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software. The ISA acts as an interface between the hardware and the software, specifying both what the processor is capable of doing as well as how it gets done.
+ RISC-V[b] (pronounced "risk-five") is an open standard instruction set architecture (ISA) based on established reduced instruction set computer (RISC) principles. Unlike most other ISA designs, RISC-V is provided under royalty-free open-source licenses. A number of companies are offering or have announced RISC-V hardware; open source operating systems with RISC-V support are available, and the instruction set is supported in several popular software toolchains.
### Integer Number Representation
+ Unsigned numbers:- also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.(Range: [0, (2^n)-1 ])
+ Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.(Range : Positive : [0 , 2^(n-1)-1] Negative : [-1 to 2^(n-1)])

### Some RISCV Assemmbly Instructions leartn
+LUI: Load Upper Immediate 
![LUI](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/28ee7cf1-99fd-4fb8-979e-5ddb95b0f8f4)
+ADDI: Add immediate
![addi](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/5ff94dea-4d32-4943-b0ea-441e9196d299)

 
Dropdown
<details>
<summary>Sum of numbers from 1 to n</summary>
  
+ Run sum_1_to_n.c
```
gcc sum_1_to_n.c
./a.out
```
</details>

![sum1ton_c_compilation](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/9fc77570-4ffd-4e7a-a22e-59efdcb7ea79)

<details>
<summary>GCC compile modes and disassemble instruction comparison</summary>

+RISCV GCC compilation with O1 and | less
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



## Day 2
### Application Binary Interface
+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.
+ RISC V architecture being currently used uses Little Endian memory allocation
   + In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
+ Given the 5 bits which are allocated, 2^5 or 32 bits are used for memory allocation.
+ An ABI table is refered to where every register is mapped to a particular variable/function.
<img width="430" alt="ABITable" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/4ca9c3cb-6253-43cd-8bac-a66090687d17">

### Running C program using ABI Function calls
+ In this program, a base(caller) c program calls a function written in assembly-level language. While they are both manipulated using ABI, the function call suceeds.
 <img width="407" alt="ABIFLOW" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/e046f952-d4b3-4239-8379-415eba3ae42e">
 
Dropdown
<details>
<summary>Create cnt1t9.c and load.S</summary>
  
+ create files
```
leafpad cnt1t9.c
leafpad load.S
```
</details>

<details>
<summary>Run and simulate using spike</summary>
  
+ Run c program file and function in assemly language
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o cnt1t9.o cnt1t9.c load.S
spike pk cnt1tn.o
```
<img width="571" alt="D2run2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/09798d44-3a40-42da-a274-99496613d647">


</details>

<details>
<summary>Run disassembly</summary>  

```
riscv64-unknown-elf-objdump -d cnt1tn.o|less
```
![D2disassembly](https://github.com/Srini-web/pes_asic_class/assets/77874288/4c7b2ddb-2880-4551-ae06-a0ee8eb13592)

</details>

<details>
<summary>RISCV CPU verification using iverilog</summary>
  
+ verification of CPU using verilog
   + using vim command
```
vim picorv32.v
```
![D2cpuss2](https://github.com/Srini-web/pes_asic_class/assets/77874288/90b92f7e-b750-4197-8904-1d2052794604)

  + using less command
```
less picorv32.v
```
![D2cpuss](https://github.com/Srini-web/pes_asic_class/assets/77874288/0dae9f41-ebc0-4ab3-9bf1-d99eafc3568d)


</details>
