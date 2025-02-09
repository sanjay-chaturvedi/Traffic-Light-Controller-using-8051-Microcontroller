# Traffic-Light-Controller-using-8051-Microcontroller
## Hardware: Development board and symbolic traffic light 
A four way traffic light controller logic is implemented in 8051 microcontroller. The development board is created using a pre-fabricated PCB from "Vegakit". I populated the PCB with all the required components. The simple arrangement of four-way traffic lights is setup using LEDs on a dot PCB board.

![Combined_Image](https://github.com/user-attachments/assets/f4f806b3-658e-4962-a018-11a4e9c1ed5e)

## Logic  implementation in 8051 microcontroller PORTs
The values of PORTs in each of the state of traffic light is shown in the below image. During transition from one state to other, all four traffic lights go yellow for a defined duration.

![Presentation_2](https://github.com/user-attachments/assets/be6f7d35-4cb9-453f-8885-9d7b5b922884)

## Assembly code implementing above logic
Tha mian program is as follows:

```assembly
org 0000h
BACK:   ACALL YELLOW
	ACALL DELAYSHORT
	MOV P0, #03H
	MOV P1, #08H
	MOV P2, #08H
	MOV P3, #08H
	ACALL DELAYLONG
	ACALL YELLOW
	ACALL DELAYSHORT
	MOV P0, #08H
	MOV P1, #03H
	MOV P2, #08H
	MOV P3, #08H
	ACALL DELAYLONG
	ACALL YELLOW
	ACALL DELAYSHORT
	MOV P0, #08H
	MOV P1, #08H
	MOV P2, #03H
	MOV P3, #08H
	ACALL DELAYLONG
	ACALL YELLOW
	ACALL DELAYSHORT
	MOV P0, #08H
	MOV P1, #08H
	MOV P2, #08H
	MOV P3, #03H
	ACALL DELAYLONG
	ACALL YELLOW
	ACALL DELAYSHORT
	LJMP BACK
```

The subroutine for turning on the yellow light is "YELLOW", as shown below.

```assembly
YELLOW: MOV PO, #04H
	MOV P1, #04H
	MOV P2, #04H
	MOV P3, #04H
	RET
```

The time duration for which trafficlights are green and red, is implemented using the subroutine "DELAYLONG". 

```assembly
DELAYLONG: 
	H4: MOV R1, #3
	H3: MOV R2, #14
	H2: MOV R3, #248
	H1: MOV R4, #255
	DJNZ R4, H1
	DJNZ R3, H2
	DJNZ R2, H3
	DJNZ R1, H4
	RET
```

The time duration for which trafficlights are yellow, is implemented using the subroutine "DELAYSHORT". 

```assembly
DELAYSHORT:
	H7: MOV R1, #14
	H6: MOV R2, #248
	H5: MOV R3, #255
	DJNZ R3, H5
	DJNZ R2, H6
	DJNZ R1, H7
	RET
```
