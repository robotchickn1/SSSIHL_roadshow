# SSSIHL_roadshow


This is the code written by me as part of the **RISC-V** (pronounced "RISK - Five") Roadshow held in Sri Sathya Sai Institute of Higher Learning, Prashanti Nilayam Campus. 

Hosted by Dr. Kunal Ghosh of VSI.

# Process:
1. Install gedit: sudo apt install gedit.
2. Create a C Code: (say, give the sum of all numbers from 1 to n).
3. gcc that .c file; also some ./a.out to check if the code is correct. (as in compile it to gates)
4. Add a new architecture: RISC-V i.e. riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o yourfilename.o yourfilenmae.c
5. riscv64-unknown-elf-objdump -d yourfilenmae.o
