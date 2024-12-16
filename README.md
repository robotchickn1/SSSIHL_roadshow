# RISC-V Roadshow


The following was done as part of the **RISC-V and VLSI Chip Design Roadshow** held by the Department of Physics, Sri Sathya Sai Institute of Higher Learning, Prashanti Nilayam Campus. It was hosted by **Kunal Ghosh**, co-founder of VSD (VLSI System Design), along with **Nahusha K L** and **G R Vighneshwar**.

A brief overview of what is to be done is given below.

# Prerequisites:
## VirtualBox and Linux OS
You will need a Linux-based operating system for developing on RISC-V. If you're not already using Linux, you can set it up inside a VirtualBox VM on your current system.[^1]
## Visual Studio Code with Platformio IDE installed
You can install any code editor, (preferably Visual Studio Code) and install the Platform IDE Extension in the editor. 

# Procedure:
## Part 1:
1. Open Ubuntu with the vsdsquadron.vdi SATA.
2. Open the terminal (by pressing `ctrl + alt + t` and type the following to install gedit - a text editor for many Linux distributions.
   ```
   sudo apt install gedit
   ```
4. Now, type `gedit` to create a new file. A program such as adding the sum of 'n' numbers can be written in this text file. **A small note** - since, the program must run as quickly and efficiently as possible, the code must be written in C language. This file can now be saved as a `.c` file, for example, say, `sum.c`.
5. Now, the code can be compiled to 0s and 1s using `gcc`. So, type `gcc sum.c` to do so.
6. Type in `./a.out` to run the `a.out` file in the current directory and render the ouput in the terminal. The program can also be checked here to see if it is consistent.

## Using RISC-V Architecture

1. The code `sum.c` is now compiled for a 64-bit RISC-V architecture with the target architecture set to `rv64i`, using the following command. The output will be a file named `sum.o`:
   ```bash
   riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum.o sum.c

2. The individual machine instructions, as in the RISC-V assembly instructions like `add`, `sub` etc., (in assembly language), along with their memory addresses, from `sum.c` can be seen in the terminal, using:
   ```bash
   riscv64-unknown-elf-objdump -d sum.o


## Verilog Code to Gates:
1. Change the the working directory to where OpenLane-related files are located. So,
   ```bash
   cd Desktop/work/tools/openlane_working_dir/openlane
2. Open docker by typing in `docker` and then type in `./flow.tcl -interactive`. This essentially creates a container to run Openlane tools and opens a `flow.tcl` script. This script is written in tcl (pronounced 'tickle"), a high-level programming language. In interactive mode, OpenLane provides an interactive Tcl shell where the user can provide inputs.
3. To load the OpenLane package ver. 0.9 so that it can used within the environment, type in `package require openlane 0.9`.
4. To add a particular design to the chip, the `picorv32a`[^2] design, a CPU core that implements the RISC-V Instruction Set is used. This is done by running `prep -design picorv32a`.
5. The design that has been created now has to be "placed", which involves arranging the standard cells (basically, `AND` and `OR` gate) on the chip layout. Placement is crucial for optimizing the design in terms of performance and area before the routing step. So, type in `run_placement`.
5. Similarly, synthesis and floorplan can also be run using `run_synthesis` and `run_floorplan` respectively. Synthesis translates the RTL (Register Transfer Level) code into a gate-level representation and `floorplan` optimizes the physical layout of the design. 
6. The above lines create an output image file that can be viewed using `Eye of Gnome`: `eog designs/picorv32a/runs/<date>_<time>/results/floorplan/picorva32a.floorplan.def.png`. Note that `<date>_<time>` refer to the time when the above commands were run. 
7. Now "placement" can be done to refine or adjust the initial placement after some changes or the above optimizations. So, type `run_placement`, whose output image can be viewed using `eog designs/picorv32a/runs/<date>_<time>/results/placement/picorva32a.placement.def.png`, where `<date>_<time>` have the above meaning.
8. Every System we use has an in-built "clock" that times every process precisely. So, `run_cts` runs the Clock Tree Synthesis (CTS), which is responsible for creating the clock tree for the design. It optimizes for skew and latency.
9. The next step: `run_routing` creates connections between the cells. Routing ensures that all the cells are properly connected and that the design meets specified requirements. 























































# References:
[^1]: VirtualBox: https://www.virtualbox.org/
[^2]: Picorv32a Design: https://github.com/YosysHQ/picorv32
