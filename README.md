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
   ```bash
   sudo apt install gedit
3. Now, type `gedit` to create a new file. A program such as adding the sum of 'n' numbers can be written in this text file. **A small note** - since, the program must run as quickly and efficiently as possible, the code must be written in C language. This file can now be saved as a `.c` file, for ex. `sum.c`.
4. Now, the code can be compiled to 0s and 1s using `gcc`. So, type `gcc sum.c` to do so.
5. Type in `./a.out` to run the `a.out` file in the current directory and render the ouput in the terminal. The program can also be checked here to see if it is consistent.

## Using RISC-V Architecture
1. The above code `sum.c` is now compiled for a 64-bit RISC-V architecture with the target architecture as `rv64i`, using the below instruction. The output will now be a file named `sum.o`.



























































# References:
[^1]: VirtualBox: https://www.virtualbox.org/
