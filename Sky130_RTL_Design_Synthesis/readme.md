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
```
./a.out
```
+ This will create a .vcd file and this we load it into gtkwave.
```
gtkwave tb_good_mux.vcd
```
+ To open and check the files type
```
gvim tb_good_mux.v -o good_mux.v
```
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
+ Wider transistors are gonna be faster but they consume more area and power. Thinner cells are gonna be slower but they consume lesser area and are more energy efficient.
+ The guidance offered to the synthesizer to put the right kind of delays are called constraints. The constraints are put in a constraints file.

</blockquote></details>	

<details>
<summary>Labs using Yosys and Sky130 PDKs</summary><blockquote>

+ Open Yosys
```
yosys
```
+ Read the library definition file
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
+ Read the verilog file to be synthesized
```
read_verilog good_mux.v
```
+ Synthesize the top level module using its name
```
synth -top good_mux 
```
+ The following command basically realises the synthesised top module good_mux in terms of standard cell library available in the lib folder.	
```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
+ The following command opens the graphviz file to show the synthesized design in terms of block diagram.
```
show
```
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
</details>

<details>
<summary>Why do we need module level synthesis?</summary>

+ Module level synthesis is preferred when multiple instances of the same module is present. We won't have to synthesize and check every module, because it is goint to be the same.
+ Divide and conquer - If we have a massive design, the tool may not be able to do all the synthesis properly. So we do submodule level synthesis and then get individual netlist and then stitch them together in the top module.
</details>




synth -top mul2 output
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/44efda31-08fa-456a-89b7-1eaa9514bb1f)
No of cells in the synthesis output is 0

show (mul2)
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/b77faa6b-8a65-4cf4-a61d-a3e6b13f7840)

write_verilog -noattr mult_2_net.v
!gvim mult_2_net.v
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e4fdaf35-e8bd-4d9c-82f3-807224ccdcd7)

read_verilog mult_8.v
synth -top mult8
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/0196bee8-7cdf-4b3c-a99a-44b068971326)
No of cells in the synthesis output is 0
show
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e5b0a3f9-1fd6-4332-a9cc-bcb53b1ad686)
write_verilog -noattr mult8_net.v
!gvim mult8_net.v
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/ac2d334f-ef75-4876-9435-25d0aaba97ee)






yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check.v
synth -top opt_check
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/22d07c7f-9a8f-4c0a-9f8d-1618de38b333)
opt_clean -purge
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/05e0e289-3f50-48a4-ba02-d7c229d21937)
 abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 ![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/5bad624d-4670-4f84-bc04-97938bae335f)
show
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/1416eb1b-ca9d-424f-abe8-62ac849dc17f)

read_verilog opt_check2.v	
synth -top opt_check2
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/88762908-92b5-4edb-ae86-adce8f06879d)
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib	
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/6e8ca5c4-c379-4581-9d14-f8f22d0967c4)
show
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/228ef8e4-ba69-4052-a532-3c9010323a7b)


read_verilog opt_check3.v
synth -top opt_check3
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/0885eb7e-1633-400e-b9bf-c4c0cc1c677f)
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/432b099a-f463-4fd5-8d50-0020dd18f76d)
show
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/e254c37f-e328-44c8-b744-816eb7cce7e4)



iverilog dff_const1.v tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/262685d9-0c40-4416-8fee-b7f6ae465f66)
iverilog dff_const2.v tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/966ad2a5-8324-44f3-bfe3-13e948048cc3)


yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/bb00ab0b-5e76-4d62-bd13-9d7058b5878b)
This synthesis infers a flop

dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/d31dd76b-c8de-4134-bb05-273f86b4c238)
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/14dea5ac-0d89-43d7-a92e-8dec15fd48e1)
show
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/06f36d91-ecac-4f64-8306-92b3da435cb9)


yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const2.v
synth -top dff_const2
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/24b86bf4-72fa-4c57-8d8a-64a0883377f3)
This design does not infer flop

Since there are dffs
dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/6a79119a-0320-451d-b174-9bc0d56ffc9c)
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/f8acce45-ca08-4e80-a2ae-570ba6617a98)

iverilog dff_const3.v tb_dff_const3.v
./a.out
gtkwave tb_dff_const3.vcd
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/85f08ceb-bcc9-430c-9222-0ee93dafbc09)

read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const3.v
synth -top dff_const3
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/7fe6a41d-0ff9-45a8-8035-5739b09c17dc)
It can be seen that both the flip flops are there in the synthesized design.
dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/a9804fb4-1fb0-4cd1-9d32-07e01e8fbe4c)
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/8b86aa8c-9cc3-450d-b44f-444183c03832)
show
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/ea2ba0b6-85f6-4bc7-9f64-1361c2fe983e)



yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/8f0d4aa5-e84f-426e-bcf0-d045efa684fb)
dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/0763e414-4c7a-4a06-98a8-a82e231d6b28)
show
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/fd8baa0a-6648-4899-a5a2-09294d333e53)

Experimenting with the counter_opt.v
Using all three bits of the counter
![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/5f0e5277-a35d-4d83-b0c4-bcedcaae82d6)
yosys
	read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	read_verilog counter_opt2.v
	synth -top counter_opt
 ![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/ad37c007-ecff-413c-b661-2a350ced30e1)
	Since there are dffs
	dfflibmap ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
	show
 ![image](https://github.com/Vishnu1426/PES_Asic_course_7th_sem/assets/79538653/1a5c80f5-dfe2-49a9-9e0b-5969f3aa4e42)
