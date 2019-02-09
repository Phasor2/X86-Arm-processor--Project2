# Assembly-langguge-X86-Arm-processor-ECE371--Project2

Full report open "Project2.docx"
and Codes open "* .txt"


# PART 1 LEDS SEQUENCE

## Part 1 Flowchart 
![alt-text](https://github.com/Phasor2/Assembly-langguge-X86-Arm-processor-ECE371--Project2/blob/master/Project%202%20part%201%20ECE371.png)

# GPIO1 pins Table 
```
Setting up table pin for GPIO1 base address 0x4804C000
GPIO1
Bit#	31	30	29	28	27	16	25	24	23	22	21	20	19	18	17	16
Function		Button						LED3	LED2	LED1	LED0					
OE in binary	1	1	1	1	1	1	1	0	0	0	0	1	1	1	1	1
OE in hex	F	E	1	F
CLEAR in hex	0	1	E	0

GPIO1
Bit#	15	14	13	12	11	10	9	8	7	6	5	4	3	2	1	0
Function																
OE in binary	1	1	1	1	1	1	1	1	1	1	1	1	1	1	1	1
OE in hex	F	F	F	F
CLEAR in hex	0	0	0	0

```


# Part 1 Algorithm 
```
Start up the module
Clear the pin on the module 
Setting up leds output pins
Toggle leds
Start the loop:
Adding LED 0 for 1 second
Adding LED 1 so LED 0,1 for 1 second
Adding LED 2 so LED 0,1,2 for 1 second
Adding LED 3 so LED 0,1,2,3 for 1 second
And turn off all LEDs for 1 second
Repeat the loop.
```

# Low Level algorithm
```
Note: base address for GPIO1_control register is 0x4804C000
Wake up module GPIO1 Store a 0x2 in address 0x44E000AC CM_PER_GPIO1_CLKCTRL
Clear pin 21 to 24 by storing 0x01E00000 at the address 0x4804C190 for GPIO1_CLEARDATAOUT 
Setting up pin 21 to 24 to output enable for (0 is enable) by And the value 0xFE1FFFFF with the value taken from the 0x4804C134 of GPIO1_OE

Toggle leds subroutine
Loop:
Go load 0x00200000 value to turn on LED 0 and send
Call Delay 1 second 
Go Load 0x00400000 value to turn on LED 1 and send
Call Delay 1 second 
Go load 0x00800000 value to turn on LED2 and send
Call Delay 1 second 
Go load 0x01000000 value to turn on LED3 and send
Call Delay 1 second 
Clear process:
Set GPIO1 bits 0x01E00000 to GPIO1_CLEARDATAOUT at 0x4804C190
SET GPIO1 bits to outputs by RMW 0xFE1FFFFF to GPIO1_EN at 0x4804C134
Send: Write LED value to GPIO1_SETDATAOUT register at 0x4804C194
Call Delay 1 second 
Go to loop 
	
 Delay 1 second:
	Load value R2 with 0x00400000
Substract R2 
Call Delay 1 second again until flag z is set
The branch to the current work
```


