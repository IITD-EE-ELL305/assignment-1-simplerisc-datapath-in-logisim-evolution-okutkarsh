[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/DOOroL-l)
# Design the microarchitecture for a SimpleRISC CPU that implements a subset of instructions that we studied in the class.

## Here are the specifications for the ISA

- 32 bit instructions and data
- 16 registers
- The following instructions will be supported (see opcodes from Sarangi pg. 112):
  - add reg, reg, (reg/imm)
  - sub reg, reg, (reg/imm)
  - cmp reg, reg, (reg/imm)
  - ld reg, imm[reg]
  - st reg, imm[reg]
  - beq label
  - bgt label
  - call label
  - ret
  - nop
- The instruction formats (branch, register and immediate) are summarized on Sarangi pg. 118 Table 3.11. Use that for the definition of the different fields within the instruction.

## Tools

Clone this repository on your own computer. You will need (logisim-evolution)[https://github.com/logisim-evolution/logisim-evolution/releases/tag/v3.8.0] to open and edit it.  
Some components that you will need for your microarchitecture, such as a data memory (DMEM), instruction memory (IMEM), register file (REGFILE) and even an ALU are already included in the simpleRISC_reduced.circ file. Please use those components only for DMEM, IMEM, REGFILE and ALU.  
Other components will be logic gates, muxes, demuxes, adders etc. Those can be found in the default logisim-evolution libraries on the left, so you will not need anything else.

## Assignment 1a

You can check the boxes below as you progress through the assignment, simply by putting an x in them:
- [ ] a
- [x] b

1. Implement the R-format instructions
- [ ] Fetch stage:
  - [ ] Add a clock and a register for PC to the circuit
  - [ ] Implement PC -> PC + 4
  - [ ] Check your circuit: Click on the "Simulate" tab on the left pane; then hit ctrl+R; then toggle the clock, i.e. click on the 'half-cycle' button under simulate (4th button from the left): you should see the value in PC increase by 4 every time!
  - [ ] Once this is working, add the IMEM module to the circuit and connect correctly to PC
  - [ ] Test: Add an LED Bar to the circuit; make it 32 bits with "One Wire" input format; connect it to the output of IMEM (INSTRUCTION pin); and re-run the simulation: you should see different LED patterns reflecting different data in the IMEM as you toggle the clock
  - [ ] Test: You can also change the values in IMEM: Open the test_imem file with notepad and simply change the 32-bit values; then check if the correct values are shown on your LED Bar!
  - [ ] Commit with message "basic setup" and push to Github
- [ ] Decode stage:
  - [ ] Add REGFILE to the circuit
  - [ ] Send correct parts of the instruction from the PC register to the REGFILE
  - [ ] Test: Connect LED Bars to rs1_data and rs2_data; right now there will be no content in the registers so the LEDs will be off, but later you will find them useful
  - [ ] Commit with message "R-type decode and fetch" and push to Github
- [ ] Execute stage:
  - [ ] Add the ALU component
  - [ ] Connect it correctly with the output of the REGFILE
  - [ ] Add a 'control circuit' that will take the instruction and generate the appropriate ALU_OP signal for the ALU to perform the operation  
        For this, you will have to open and study the ALU circuit to know what control signals to generate
  - [ ] Commit with message "Added ALU" and push to Github
- [ ] Write back stage
  - [ ] Write the results of the execution back to the register file
  - [ ] You will have to add a control signal, which takes the instruction as the input and uses it for enabling writing to the register file when appropriate
2. Add support for immediate format instructions
- [ ] I-type arithmetic instructions
  - [ ] Add a circuit for immediate generation (this circuit takes the instruction as the input and extracts the 'immediate' from it and makes it 32 bits long
  - [ ] Add a multiplexer to choose between immediate and register data as input to the ALU
  - [ ] Update the control circuit to support choosing between register and _imm_ at the mux
  - [ ] Test: Write a simple assembly program with only I- and R- format arithmetic instructions to load two numbers in two registers; then add them and store data in a third register (all these numbers will show up on your LED bars for you to test!)
  - [ ] Commit to git with message "Added I-format arithmetic instructions" and push to Github

End of assignment 1a. Congratulations! You now have a working CPU that can perform basic operations on numbers!
