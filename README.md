# RISC-V Roadshow


The following was done as part of the **RISC-V and VLSI Chip Design Roadshow** held by the Department of Physics, [Sri Sathya Sai Institute of Higher Learning](https://www.sssihl.edu.in/), Prashanti Nilayam Campus. It was hosted by **Kunal Ghosh**, co-founder of [VSD (VLSI System Design)](https://www.vlsisystemdesign.com/), along with **Nahusha K L** and **G R Vighneshwar**.

A brief overview is given below. After every step, a visual is displayed to guide the user.

# Getting Started:
## 1. VirtualBox and Linux OS
You will need a Linux-based operating system for developing on RISC-V. If you're not already using Linux, you can set it up inside a VirtualBox VM on your system.[^1]
## 2. Visual Studio Code with Platformio IDE installed
You can install any code editor, (preferably Visual Studio Code) and install the Platform IDE Extension in the editor.[^2]

# Procedure:
## Writing a Program:
1. Open Ubuntu with the vsdsquadron.vdi SATA mounted.
2. In the terminal (press `ctrl + alt + t`), type the following to install gedit - a text editor for many Linux distributions. 
```
sudo apt install gedit
```
![Installing gedit](./images/1.%20install_gedit.png)
3. Now, type `gedit` to create a new file. A program such as adding the sum of 'n' numbers can be written in this text file. **A small note** - since, the program must run as quickly and efficiently as possible, the code must be written in C language. This file can now be saved as a `.c` file, for example, say, `sum.c`.
4. Now, the code is to be compiled to 0s and 1s using `gcc`. Therefore, type `gcc sum.c`. <br><br>
![Compiling the Program](./images/2.%20gcc.png)
5. Type in `./a.out` to run the `a.out` file in the current directory and render the ouput in the terminal. The program can also be checked here to see if it is programming-consistent.
![Program Output](./images/3.%20sum_output.png)

## Using RISC-V Architecture:   

1. The code `sum.c` is now compiled for a 64-bit RISC-V architecture with the target architecture set to `rv64i`, using the following command. The output will be a file named `sum.o`:
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum.o sum.c
```
![Introducing RISC-V Architecture](./images/4.%20risc-v_architecture.png)
2. The individual machine instructions, as in the RISC-V assembly instructions like `add`, `sub` etc., (in assembly language), along with their memory addresses, from `sum.c` can be seen in the terminal, using:
```
riscv64-unknown-elf-objdump -d sum.o
```
![The RISC-V Instruction Set](./images/5.%20objdump.png)

## Verilog Code to Gates:
1. Change the the working directory to where Openlane-related files are located. So, use
```
cd Desktop/work/tools/openlane_working_dir/openlane
```
![Changing Directory](./images/6.%20change_dir.png)

2. Open docker by typing in `docker` and then type in `./flow.tcl -interactive`. This essentially creates a container to run Openlane tools and opens a `flow.tcl` script. This script is written in tcl (pronounced 'tickle"), a high-level programming language. In interactive mode, Openlane provides an interactive Tcl shell where the user can provide an input.
![Docker](./images/7.%20docker.png)

3. To load the OpenLane package ver. 0.9 so that it can used within the environment, use
```
package require openlane 0.9
```
![Interactive Shell](./images/8.%20tcl_interactive.png)

4. To add a particular design to the chip, the `picorv32a`[^3] design, a CPU core that implements the RISC-V Instruction Set is used. This is done by running `prep -design picorv32a`. The output is shown below:
![Designing Output](./images/9.%20tcl_output.png)

5. Now, synthesis and floorplan can be run using `run_synthesis`. Synthesis translates the RTL (Register Transfer Level) code into a gate-level representation. At the end, it should read that "Synthesis was successful".
![Synthesis Output](./images/10.%20synthesis_output.png)

The above output also mentions the number of wires being used. 
![Synthesis - No. of wires](./images/12.%20synthesis_output2.png)

6. Similarly, `run_floorplan` can be typed in to optimize the physical layout of the design.
![Floorplan Output](./images/14.%20floorplan_output.png)

7. The above line create an output image file that can be viewed using `Eye of Gnome` (Note that `<date>_<time>` refer to the time when the above commands were run):
```
eog designs/picorv32a/runs/<date>_<time>/results/floorplan/picorva32a.floorplan.def.png
```
![Floorplan - Change Dir](./images/13.%20floorplan_code.png) <br><br>
![Floorplan - Output Image](./images/14.%20floorplan_output.png)

8. The design that has been created now has to be "placed", which involves arranging the standard cells (basically, `AND` and `OR` gate) on the chip layout. Placement is crucial for optimizing the design in terms of performance and area before the routing step. So, type in `run_placement`.
![Placement Output](./images/16.%20placement_output.png)

9. Similarly, `run_placement`'s output image can also be viewed using:
```
eog designs/picorv32a/runs/<date>_<time>/results/placement/picorva32a.placement.def.png
```
![Placement - Change Dir](./images/17.%20change_dir_placement.png)
![Placement - Output Image ](./images/18.%20placement.png)

10. Every System we use has an in-built "clock" that times every process precisely. So, `run_cts` runs the Clock Tree Synthesis (CTS), which is responsible for creating the clock tree for the design. It optimizes for skew and latency.
![Clock Tree Synthesis - Skew](./images/19.%20ctr_skew.png)
The output of this line can be seen as below:
![Clock Tree Synthesis - Final Output](./images/20.%20ctr_output.png)

11. The next step: `run_routing` creates connections between the cells. Routing ensures that all the cells are properly connected and that the design meets specified requirements. 
![Routing - Output](./images/21.%20routing_output1.png) 
This step is somewhat of a computational process. So, the system takes time to provide the final output. Therefore, the computation takes place in steps of iterations. From 0th iteration.. 57th Iteration.. so on..
![Routing - 0th Iteration](./images/22.%20Iteration_0.png) <br><br>
![Routing - 1th Iteration](./images/23.%20Iteration_1.png) <br><br>
![Routing - 57th Iteration](./images/24.%20Iteration_57.png) <br><br>

Until, the final output arrives. 
![Routing - Final Output](./images/25.%20routing_done.png)




















































# References:
[^1]: VirtualBox: https://www.virtualbox.org/
[^2]: Platformio IDE: https://platformio.org/platformio-ide
[^3]: Picorv32a Design: https://github.com/YosysHQ/picorv32
