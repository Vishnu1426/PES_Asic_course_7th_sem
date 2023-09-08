# PES_ASIC_RISCV_Course_7th_Sem

# RISC-V based MYTH

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
	
 
Expand the below dropdowns to know more
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

## Day 2
### Application Binary Interface
+ In computer software, an application binary interface (ABI) is an interface between two binary program modules. Often, one of these modules is a library or operating system facility, and the other is a program that is being run by a user.
+ An ABI defines how data structures or computational routines are accessed in machine code, which is a low-level, hardware-dependent format. In contrast, an application programming interface (API) defines this access in source code, which is a relatively high-level, hardware-independent, often human-readable format.
+ Registers can be loaded with the required data directly or it can be stored in memory and can be loaded from there when required. The memory can be used since there are only 32 registers available in RISCV architecture. Memory addresses a byte. How to store 64 bit number in memory? 
	+ If the storage starts like least significant byte goes to the first memory location, and so on, it is called little endian memory addressing system. RISCV belongs to this category.
	+ If the storage starts like most significant byte goes to the first memory location, and so on, it is called big endian memory addressing system.

+ Size of the ISA for 64 bit RISCV or 32 bit RISCV architecture is always 32 bit. 64 bit is for the registers.
+ Type of instructions : I type, R Type and S Type 

![ABI_Instruction Types](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/6a476f49-4d10-4242-bbce-a86f634bb253)

+ An ABI table is refered to where every register is mapped to a particular variable/function.

![ABI_Register Names](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/77c8c724-f2d4-4e57-81db-820ece6737f7)

### Running C program using ABI Function calls
+ C program uses ABI to call functions in the assembly program. The assembly program returns the final value to the C program.

![Algorithm_Flowchart](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/57a66a6c-b305-4ebd-9263-8159e1e01486)
 
Expand the below dropdowns to know more
<details>
<summary>1_to_9_custom.c and load.S</summary>
  + Compilation and Execution of the two files are done using the RISCV GCC and Spike.
	
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o 1_to_9_custom.o 1_to_9_custom.c load.S
spike pk 1_to_9_custom.o
```
![riscv_comp_spike](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/571156d5-030b-464c-83b0-957cbc25bef4)

</details>

<details>
<summary>Run disassembly</summary>  

```
riscv64-unknown-elf-objdump -d 1_to_9_custom.o | less
```
![Disassembly of compiled file](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/3f0a635b-9f39-4600-9b10-325f75397db4)

</details>

<details>
<summary>RISCV CPU verification using iverilog</summary>
  
+ Running of the sum from 1 to n on riscv CPU
	+ Files involved are picorv32.v and testbench.v

![Design_Testbench](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/d5a21bdf-0818-4404-9ef5-33b4f97ba3c8)

</details>


<details>
	<summary>Diagram for flow of instruction and data from memory to processor</summary>

 + Hex file containing C program goes to the RISC-V CPU.
 + The CPU does the operation. CPU is written in verilog.
 + It returns the output back to the C program.
 + 
 ![Memory to Processer diagram](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/85b8c414-614a-4f18-b042-e1e6876e6c92)

</details> </details>


# RTL DESIGN USING VERILOG WITH SKY130 TECHNOLOGY
## Day 1 - Introduction to Verilog RTL design and Synthesis
<details>
<summary>Installations</summary><blockquote>
<details>
<summary>Tools Installation</summary><blockquote>
	
+ Commands to install Yosys
```
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make
sudo apt-get update
sudo apt-get install build-essential clang bison flex  libreadline-dev gawk tcl-dev libffi-dev git  graphviz xdot pkg-config python3 libboost-system-dev libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make
sudo make install
```

+ Command to install iverilog
```
sudo apt-get install iverilog
```

+ Command to install iverilog
```
sudo apt uptdate
sudo apt install gtkwave
```

</blockquote></details>

<details>
<summary>Directory Creation and Cloning Source Files</summary><blockquote>

+ Go your working directory through root directory and execute the following commands
```
mkdir VLSI
cd VLSI
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```		
<blockquote></details>
</blockquote></details>

<details>
<summary>Exploring the cloned directories</summary><blockquote>

+ The following command will go the workshop directory
```
cd sky130RTLDesignAndSynthesisWorkshop/
```

+ The following command will open the my_lib directory. This my_lib folder contains another folder called verilog_files, which contains all the model source files required for the lab experiments.
``` 
cd my_lib
```
+ The following command if typed in VLSI folder will go the lib folder. This contains the sky130 tool's library definition file.
```
cd lib 
```
+ Now let's check the working of iverilog
```
cd verilog_files
iverilog good_mux.v tb_good_mux.v
```
+ (an a.out file will be created.)
+ This will create a .vcd (Value change dump) file.
```
./a.out
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/3db96576-fd81-4a42-9801-78b637745700)

+ We will load this .vcd file into gtkwave.
```
gtkwave tb_good_mux.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/ddc77487-c83b-412a-8418-2d828a9d68b9)

+ To open and check the files type
```
gvim tb_good_mux.v -o good_mux.v
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/2ce76c92-fe4e-48f4-8b71-c53749bbc93f)

</blockquote></details>

<details>
<summary>Introduction to Yosys and Logic synthesis</summary><blockquote>

+ Next we see yosys
+ Yosys takes in the design file and the library file and generates the netlist file
+ Netlist is basically the representaion of the design file in the form of standard cells.
+ read_verilog is used for reading the design file
+ read_liberty is used for reading the .lib file
+ write_verilog is used for writing the netlist file
+ The netlist and the testbench file is sent to iverilog and that generates an a.out which when run we get a .vcd file. This .vcd file when we send to gtkwave we get the simulation waveform.
+ This waveform should be same as RTL simulation. RTL simulation did not use standard cells. But in this netlist we used standard library files. Since design is same we should get the same output.
+ Primary inputs and primary outputs have not changed. Therefore, we can use the same testbench for both 
synthesis and RTL simulation.

+ RTL design - is the behavioural representation of the required specification in HDL language.
+ But we don't need representation of behaviour in terms of code. We need hardware
+ So for that we use RTL to Gate level translation. This translation is called synthesis.
+ The design is converted into gates and the connections are made between the gates. 
+ This file which contains these gates and their connections is called netlist.
	
+ .lib is a library file which is a collection of standard cells/ logical modules. It can contain differnt flavours of the same gate.(slow, medium, fast)
+ Why do we need different flavours of the same gate? Combinational delay determines the maximum speed of	operation. We need fast cells so that the combination delay is less and the circuit can work at a higher clock rate.
+ But why do we need a slow clock? Say there is a circuit with two FlipFlops (ffa and ffb) and in between them we have a combinational circuit. ffb must capture the data from the previous cycle of ffa.
+ That is when ffa sends its data through comb circuit in one cycle, in the next cycle ffb should capture the data. So there should be a minimum delay, so that data can be transfered safely. Combinational circuit must create that delay such that until ffb finishes capturing the previously sent data, the output should not be updated. This is called hold time. That is why we also need cells which work slowly.
+ Wider transistors are going to be faster but they consume more area and power. Thinner cells are gonna be slower but they consume lesser area and are more energy efficient.
+ The guidance offered to the synthesizer to put the right kind of delays are called constraints. The constraints are put in a constraints file.

</blockquote></details>	

<details>
<summary>Labs using Yosys and Sky130 PDKs</summary><blockquote>

+ Open Yosys
```
yosys
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/78b46928-1ed5-4b9f-88cd-fba9979a069c)

+ Read the library definition file
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/69336051-9785-4329-acb7-bc6028fc71af)

+ Read the verilog file to be synthesized
```
read_verilog good_mux.v
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/60462e4e-b18a-49a3-bd23-b534e6a55525)

+ Synthesize the top level module using its name
```
synth -top good_mux 
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/68976052-ca49-4c0f-aeea-19a25d068cf3)

+ The following command basically realises the synthesised top module good_mux in terms of standard cell library available in the lib folder.	
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/d2a7a0ff-e258-4dee-9215-cda5d95b0a03)

+ The following command opens the graphviz file to show the synthesized design in terms of block diagram.
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/10045abe-bf03-41a1-9a24-de4e9f859469)

+ Generate a netlist file for the above synthesized design. We can view the synthesized design directly using notepad.
```
write_verilog good_mux_netlist.v 
```
+ To get a concise version of the netlist.
```
write_verilog -noattr good_mux_netlist.v
```
</blockquote></details>	

## Day 2 - Timing libs, Hierarchical vs Flat Synthesis and efficient flop coding styles.
<details>
<summary>Theory</summary>summary><blockquote>
<details>
<summary>PVT</summary><blockquote>
	
+ P - Process => Changes in chip due to the small variablity in the manufacturing process.
+ V - Voltage => Changes in the voltage.
+ T - Temeperature => Changes in the external temperature. 
</blockquote></details>
<details>
<summary>Library File (.lib)</summary><blockquote>

+ .lib file contains every cell and the cell properties like leakage power, delay etc.
</blockquote></details>
</blockquote></details>

<details>
<summary>Hierarchical vs Flat synthesis</summary><blockquote>

<details>
<summary>multiple_modules.v</summary>
	
+ Open Yosys and perform the synthesis
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/f9ce00a6-69ba-4ad2-bbcf-94fe199cdda3)
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib	
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/4724ce7e-46c1-4d67-a44b-25b69379e421)
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/8aa63c02-8a8c-47e8-898f-4fae792ac024)
```
write_verilog multiple_modules_heir.v
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/0136a72c-d4d0-4d8b-9596-c9c0a02e5449)

+ Flatten - Makes the module such that there are no sub modules in the netlist file. and gate and or gate are directly instantiated.
```
flatten
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/15049411-aba3-404f-960e-9a79e9fb3b94)
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/f0268c96-76da-403d-864a-5af23a367cff)

</details>

<details>
<summary>Synthesizing Submodules</summary>
	
+ Now given multile modules, we want to synthesize a submodule, what to do?
+ Start yosys again and do till read_verilog
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
```
+ Now we need to synthesize only submodule1
```
synth -top submodule1
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/8e98a19a-3839-4001-b87a-61469033aae1)

+ Synthesized design
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/42fa2404-3abc-4e97-abd0-b7ebb25e6091)

</details>

<details>
<summary>Why do we need module level synthesis?</summary>

+ Module level synthesis is preferred when multiple instances of the same module is present. We won't have to synthesize and check every module, because it is goint to be the same.
+ Divide and conquer - If we have a massive design, the tool may not be able to do all the synthesis properly. So we do submodule level synthesis and then get individual netlist and then stitch them together in the top module.
</details>
</details>

<details>
<summary>Flip  Flops</summary><blockquote>
	
<details>
<summary>Why do we need flip flops?</summary><blockquote>

+ Combinational circuits even though they are designed properly and will settle at the right ouput if the inputs are right, they might momentarily induce wrong values at the output. This is called glitch.
+ Now if this output is connected directly to another comb circuit, the next combinational circuit not only gets changing values and starts giving output in its end, but also creates its own glitches.
+ In this way glitch propagates. To prevent this, we store the values after every combinational block. The next block takes value from the flip flop. The input of the flip flop may be changing, but the output will be stable/constant since the flop's values changes only when clk signal is given. Therefore, the next comb circuit will see a stable input. 

</blockquote></details>
</blockquote></blockquote>
</details>

<details>
<summary>Resets</summary><blockquote>

<details>
<summary>Theory</summary><blockquote>

+ Asynchronous reset - A reset signal of a storage element, which does not depend on the clock signal.
+ Synchronous reset - A reset signal of a storage element, which depends on the clock signal. It is going to wait for the clock. When we say something is synchronous, that means there is no separate pin for that signal.
+ Synchronous reset goes directly to the input where a reset signal selectes a mux which determines whether the input to the storage element is a predetermined reset values or the value passing from the previous combinational block.
+ We can also have a flop with both synchronous and asynchronous reset.
</blockquote></details>

<details>
<summary>Asynchrocnous reset module RTL simulation</summary><blockquote>

+ Type the following code in the home directory.
```
sudo -i
```
+ Go to the verilog_files directory and type in the following
```
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```

![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/56c18d89-ba69-4076-8b30-338190c9ed1c)

</blockquote>
</details>

<details>
<summary>Asynchrocnous set module RTL simulation</summary><blockquote>

+ Type the following code in the home directory.
```
sudo -i
```
+ Go to the verilog_files directory and type in the following
```
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```

![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/da74852e-2924-4fbd-9a7d-25c7e1983679)

</blockquote>
</details>

<details>
<summary>Synchrocnous reset module RTL simulation</summary><blockquote>

+ Type the following code in the home directory.
```
sudo -i
```
+ Go to the verilog_files directory and type in the following
```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```

![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/7c5b5547-0c3c-457f-ba39-ca45caed4f2f)

</blockquote>
</details>

<details>
<summary>Asynchrocnous reset module standard cell synthesis</summary><blockquote>

+ Type the following code in the verilog_files directory.
```
yosys
```
+ In Yosys type in the following
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asynchres
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/a423ab64-94ce-4a54-80e6-a53b52e29c91)

+ Sometimes the dffs use a different library than gates, so we will have to specify that. But here both are same so same std. lib file.
```
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/157f0504-8015-4665-be5d-ff94cca313b2)

```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib	
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/11b948ff-8790-4b37-a126-0b3953d144ef)

```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e4857056-b149-4535-aec3-8c580c8e444a)

</blockquote>
</details>


<details>
<summary>Asynchrocnous set module standard cell synthesis</summary><blockquote>

+ Type the following code in the verilog_files directory.
```
yosys
```
+ In Yosys type in the following, similar to the previous one and obtain the design.
```
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/393d0956-9d89-44db-8fc2-4bb71d38ee2e)

</blockquote>
</details>

<details>
<summary>Synchrocnous set module standard cell synthesis</summary><blockquote>

+ Type the following code in the verilog_files directory.
```
yosys
```
+ In Yosys type in the following, similar to the previous one and obtain the design.
```
read_verilog dff_syncres.v
synth -top dff_syncres
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/ee5ecdb3-9171-4dbe-9c10-87b2b2c2bc03)
```
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/a5770e57-7fa2-4343-aafb-d4c01e470fb2)

</blockquote>
</details>
</blockquote></details>

<details>
<summary>Multiplication by 2 - An Interesting Optimisation</summary><blockquote>

+ Let's synthesize and see how the output is calculated and we get and how many cells we get
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_2.v
synth -top mul2
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/44efda31-08fa-456a-89b7-1eaa9514bb1f)

+ We can see above that the No. of cells in the synthesis output is 0
+ Let's see the design below.
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/b77faa6b-8a65-4cf4-a61d-a3e6b13f7840)

+ Let us generate the netlist and see why the number of cells are zero.
write_verilog -noattr mult_2_net.v
!gvim mult_2_net.v
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e4fdaf35-e8bd-4d9c-82f3-807224ccdcd7)

+ It can be seen from the netlist file that Multiplying by powers of two is like appending zeroes at the LSB position of binary representation or left shifting the binary representation. Therefore there is no requirement of any cells, i.e., no requirement of any gates.
+ Now if we have to multiply a 3 bit number a[2:0]*9, we can do a[2:0]*8 + a[2:0].
+ a[2:0] is basically a000. Since a is also a 3 bit number, we get a000 + a = a[2:0]a[2:0].
+ This is another kind of optimisation.
</blockquote></details>

<details>
<summary>Multiplication by 8 - An Interesting Optimisation</summary><blockquote>

+ After doing the same operations as before
```
read_verilog mult_8.v
synth -top mult8
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/0196bee8-7cdf-4b3c-a99a-44b068971326)

+ It can be seen that the No. of cells in the synthesis output is 0
+ Let us see the design
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e5b0a3f9-1fd6-4332-a9cc-bcb53b1ad686)

+ Let us write the netlist file
```
write_verilog -noattr mult8_net.v
!gvim mult8_net.v
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/ac2d334f-ef75-4876-9435-25d0aaba97ee)
</blockquote>
</details>

## Day 3 - Combinational and sequential optmizations

<details>
<summary>Types and benefits of Combinational Logic Optimisation</summary>

+ Squeezning the logic to ge the most optimised design - Area and power savings
+ Constant Propagation - Direct Optimisation. This means when a constant value simply propagates from input to the output through many gates and if those many number of gates are not required to propagate the constant or do minimal operation, we can substitute it with a smaller gate/gates.
+ Boolean Logic Optimisation - Reduces number of gates using K-Map and Quine McKluskey
+ Synthesis tools do these optimisations to get the most optimised logic design.
</details>

<details>
<summary>Types and benefits of Sequential Logic Optimisation</summary><blockquote>

<details>
<summary>Basic</summary>

+ Sequential constant propagation - Assume a Reset DFF where D is connected to ground. Is there any chance where Q will become 1? No. Therefore, Q is always 0. What if set DFF is there. This time Q will become 0 when set is not enabled and will be 1 when set is enabled.
</details>

<details>
<summary>Advanced</summary><blockquote>
	
+ State optimisation - Optimisation of unused states
+ Cloning - Physical aware synthesis. That is say a combinational logig gets input from an FFA and its output goes to two other FFs (FFB and FFc), and these two output FFs are far off, then a long routing is required. To prevent this we can clone the path from FFA to FFB such that there is now FFA1 - Comb - FFB and FFA2 - Comb - FFC. 

<details>
<summary>Retiming</summary>
	
+ Say there is a cascade of FFA-comb1-FFB-comb2-FFC. Now if comb1 is having a much greater delay than comb2, then the circuit's clock can effectively work only at the comb1's speed since it creates a bottleneck. 
+ But say if we were able to move some part of the combinational logic from comb1 to comb2, this would mean that we have pushed some amount of delay from comb1 to comb2. 
+ Now since the difference in their delays was large, transfering a small delay from comb1 to comb2 will still keep comb1 slower than comb2 an effectively comb1's speed only will be used. 
+ But comb1 is now faster since it has lesser delay.
+ So we have retimed the delays so that we get an optimised circuit in terms of timing.
</details>
</blockquote></details>
</blockquote></details>

<details>
<summary>Checking Optimisation</summary><blockquote>

<details>
<summary>opt_check</summary>

+ Commands
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check.v
synth -top opt_check
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/22d07c7f-9a8f-4c0a-9f8d-1618de38b333)

+ To optimise the synthesised design, type
```
opt_clean -purge
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/05e0e289-3f50-48a4-ba02-d7c229d21937)

```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/5bad624d-4670-4f84-bc04-97938bae335f)

```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/1416eb1b-ca9d-424f-abe8-62ac849dc17f)
</details>

<details>
<summary>opt_check2</summary>	

+ Commands
```
read_verilog opt_check2.v	
synth -top opt_check2
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/88762908-92b5-4edb-ae86-adce8f06879d)

```
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib	
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/6e8ca5c4-c379-4581-9d14-f8f22d0967c4)

```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/228ef8e4-ba69-4052-a532-3c9010323a7b)

</details>

<details>
<summary>opt_check3</summary>

 + Commands
```
read_verilog opt_check3.v
synth -top opt_check3
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/0885eb7e-1633-400e-b9bf-c4c0cc1c677f)
```
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/432b099a-f463-4fd5-8d50-0020dd18f76d)
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e254c37f-e328-44c8-b744-816eb7cce7e4)
</details>
</blockquote></details>


<details>
<summary>Constant Propagation</summary><blockquote>

<details>
<summary>RTL simulation of dff_const1.v</summary>
	
```
iverilog dff_const1.v tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/262685d9-0c40-4416-8fee-b7f6ae465f66)
</details>

<details>
<summary>RTL simulation of dff_const2.v</summary>
	
```
iverilog dff_const2.v tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/966ad2a5-8324-44f3-bfe3-13e948048cc3)
</details>

<details>
<summary>Standard Library synthesis of dff_const1.v</summary>

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/bb00ab0b-5e76-4d62-bd13-9d7058b5878b)

+ This synthesis infers a flop.
+ Since there are dffs:
```
dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/d31dd76b-c8de-4134-bb05-273f86b4c238)
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/14dea5ac-0d89-43d7-a92e-8dec15fd48e1)
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/06f36d91-ecac-4f64-8306-92b3da435cb9)
</details>

<details>
<summary>Standard Library synthesis of dff_const2.v</summary>

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const2.v
synth -top dff_const2
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/24b86bf4-72fa-4c57-8d8a-64a0883377f3)

+ This design does not infer flop.

+ Since there are dffs:
```
dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/6a79119a-0320-451d-b174-9bc0d56ffc9c)
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/f8acce45-ca08-4e80-a2ae-570ba6617a98)
</details>

<details>
<summary>RTL synthesis of dff_const3.v</summary>

``` 
iverilog dff_const3.v tb_dff_const3.v
./a.out
gtkwave tb_dff_const3.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/85f08ceb-bcc9-430c-9222-0ee93dafbc09)
</details>

<details>
<summary>Standard Library synthesis of dff_const3.v</summary>

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const3.v
synth -top dff_const3
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/7fe6a41d-0ff9-45a8-8035-5739b09c17dc)

+ It can be seen that both the flip flops are there in the synthesized design.
+ Since there are dffs
```
dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/a9804fb4-1fb0-4cd1-9d32-07e01e8fbe4c)
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/8b86aa8c-9cc3-450d-b44f-444183c03832)
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/ea2ba0b6-85f6-4bc7-9f64-1361c2fe983e)
</details>
</blockquote></details>

<details>
<summary>Unused Output Optimisation</summary><blockquote>

<details>
<summary>What is unused output optimisation??</summary>

+ It means that the logic which is unused is not required in the circuit and will be removed in the final synthesised design.
</details> 

<details>
<summary>Checking counter_opt.v</summary>	

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/8f0d4aa5-e84f-426e-bcf0-d045efa684fb)
```
dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/0763e414-4c7a-4a06-98a8-a82e231d6b28)
```
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/fd8baa0a-6648-4899-a5a2-09294d333e53)
</details>

<details>
<summary>Experimenting with the counter_opt.v</summary>
	
+ Using all three bits of the counter

![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/5f0e5277-a35d-4d83-b0c4-bcedcaae82d6)

+ Commands
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt2.v
synth -top counter_opt
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/ad37c007-ecff-413c-b661-2a350ced30e1)

+ Since there are dffs
```
dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/1a5c80f5-dfe2-49a9-9e0b-5969f3aa4e42)
</details>
</blockquote>
</details>


## Day 4 - GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

<details>
<summary>GLS</summary><blockquote>

<details>
<summary>What is GLS?</summary>	

+ It is basically running the testbench with netlist as the design under test.
+ Since netlist is logically same as the RTL code, the same testbench will only run it.
</details>

<details>
<summary>Why GLS?</summary>

+ To verify the correctness of the design after synthesis, because when we write codes, we may not have written it properly and also when we convert from ideal cells to standard library cells, some errors may occur.
+ This is called Synthesis-Simulation mismatch.
+ We will see later why it is required to validate the functionality of the netlist.
+ To ensure that the timing of the design is met.
+ Only if the Gate level models are time annotated, we can use GLS for timing verification.
</details>

<details>
<summary>Synthesis-Simulation Mismatch</summary>

The points to understand while talking about Synthesis Simulation Mismatch are:
+ Missing Sensitivity List - If certain inputs required for the proper functioning of the circuit are not present in the sensiticity list, then the synthesized hardware might not be the intended circuit.
+ Blocking vs Non Blocking Statements - Blocking statements are executed in order, whereas non-blocking statements are executed parallely. If the order is not maintained in blocking statemenents, certain required parts of the synthesized design would be absent.
+ Non Standard Verilog Coding - Sequential circuits should be described using non-blocking statements only. Use blocking statements with atmost care and use only when needed.
</details>
</details>

<details>
<summary>ternary_operator_mux.v</summary>

+ Contents of the files
```
gvim ternary_operator_mux.v -o bad_mux.v -o good_mux.v
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/89f1b433-c7b5-404c-9a1d-cfaf1fd51f91)

+ RTL Simulation
```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
 ![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/46e5c501-1b26-428d-9ea7-fb8f575e384b)

+ Synthesis
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/6b269872-ca1f-48e3-be1c-97f58237c17f)
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr ternary_operator_mux_net.v
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/221bdf08-ba24-4e7a-bc9c-f80f94917890)


+ GLS
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
gtkwave tb_ternary_operator_mux.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/c509b0f7-9ac4-4679-9b80-bc03dd8312b8)

</details>
<details>
<summary>bad_mux.v</summary>
	
+ RTL simulation of bad_mux.v
```
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/84693ce2-d5b5-4e0c-a4d1-e630e29f9c65)

+ Netlist simulation
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/80016862-eab2-40b6-bb20-953bcc67a4ae)

</details>

<details>
<summary>blocking_caveat.v</summary>

+ RTL simulation
```
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/4604fdd3-62b8-46b6-b316-6339f699d912)

+ Synthesis
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog blocking_caveat.v
synth -top blocking_caveat
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/b54dbfa0-a6d8-4b5d-b9d4-a68f80098b3d)
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr blocking_caveat_net.v
show
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e1746eb9-4176-4686-a5b3-a7d1304b1d46)

+ GLS
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/5cea8607-78a6-4a3c-b4c9-38ffba57bed0)

</details>

