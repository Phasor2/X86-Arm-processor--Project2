# X86-Arm-processor-ECE371--Project2

Full report open "Project2.docx"
and Codes open "* .txt"


# PART 1 LEDS SEQUENCE

## Part 1 Flowchart 
![alt-text](https://github.com/Phasor2/Assembly-langguge-X86-Arm-processor-ECE371--Project2/blob/master/Part%201%20ECE371.png)

# Part 2 SETTING UP INTERRUPT
## Part 2 Flowchart 
![alt-text](https://github.com/Phasor2/Assembly-langguge-X86-Arm-processor-ECE371--Project2/blob/master/Part%202%20ECE371.png)

## Interrupt controller unmask
When unmasking the POINTRPEND for GPIO1. We have to look up the which pin in the interrupt control that was mask. The table below will show us how the mask of falling edge detect button work. We will use this table to unmask the DTIMER3 in the part 3. I will have separate table template for DTIMER3
![alt-text](https://github.com/Phasor2/Assembly-langguge-X86-Arm-processor-ECE371--Project2/blob/master/UNMASK%20interrupt.png)

# PART 3 SETTING UP DTIMER
## Part 3 Flow chart 
![alt-text](https://github.com/Phasor2/Assembly-langguge-X86-Arm-processor-ECE371--Project2/blob/master/Part%203%20ECE371.png)

## Setting up register Timer3
![alt-text](https://github.com/Phasor2/Assembly-langguge-X86-Arm-processor-ECE371--Project2/blob/master/setting%20up%20register%20timer3.png)

Using Timer3 TCLR register to control the clock. TLDR will be the register to reload the value. The DTIMER will generate interrupt when it overflows. We chose 32.768 KHZ clock for DTIMER3. It means 372768 pulse per second. 372768 in hex would be 0x00008000. To get the desired time, follow the formula:
```
Desired time (1 second) = 0x1_0000_0000 – 0x0000_8000 = 0xFFFF8000 
```
