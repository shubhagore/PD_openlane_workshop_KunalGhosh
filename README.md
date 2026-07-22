# PD_openlane_workshop_KunalGhosh
Documentation of the Openlane Sky130 workshop

# Day 1: Inception of opensource EDA, OpenLane and Sky130 PDK:
## Sky130_D1_SK1 - How to talk to computers:
### SKY_L1 - Introduction to QFN-48 Package, chip, pads, core, die and IP's: 
This is the aurdino board. 

<img width="1131" height="848" alt="Image" src="https://github.com/user-attachments/assets/cf39eda7-9e50-48d3-b958-e5149fbcaf9e" /> 
 **Fig 1.1 Aurdino board**


Here we consider only the  small part (the circled part which is the processor) which will be designed as a part of Physical design work. The components that consists the Aurdino board are the Processor/SoC, and the interfaces such as SDRAM, direct I2C, direct QSPI, GPIO0-7, PWM0-3, GPIO8-14, PWM4-5, JTAG-UART, FTDI, QSPI1-Flash, I2C0-EEPROM. The block diagram of the aurdino board is as shown below. 

<img width="1546" height="812" alt="Image" src="https://github.com/user-attachments/assets/7f78f813-0e40-41ed-b7a9-9d52f09ae4e5" />
**Fig 1.2 Block diagram of the Aurdino board**


The interanl structure of the processor is known as **package**. This is **Quad Flat No-leads(QFN-48)**. The pin locations are all driven by the Aurdino board that we will be designing. The size of the package shown below is 7mm*7mm. The chip is at the center of the package and is connected to the pins by the wire bounds.

<img width="1131" height="809" alt="Image" src="https://github.com/user-attachments/assets/3797eaef-0d41-43c0-8da3-e90eb7c46a30" />
**Fig 1.3 Internal structure of the Aurdino**



A chip has various components in it as listed below:
- **Pads:** The pads are the one through which the signal can pass from out to in and vice versa. In general it can be compared to a door.
-  **Core:** This is the place of the chip where all the digital logic such as MUX, AND, OR, NOT gates, etc of the design are placed.
-  **Die:** This is the entire area of the chip, which is getting manufactured on the silicon wafer.

Considering an example of RISC-V processor, few components of its digital logic includes of ADC, DAC, PLL, SRAM. These components are termed as **The Foundary IP's (Foundary Intellectual proprties)**. They have some king of intellectual property within them to build the blocks.
The foundary is a place or an industry with lot of machines. As a VLSI engineer, we have to communicate with these machines with the help of some interfaces. 
The SPI, RISC-V SoC are **the Macros**. 
The Macros are the pure digital logic.


### SKY_L2 - Introduction to RISC-V Instruction set Architecture (ISA):
The top level description of ISA is this is the language using which we are going to talk to the computers.
**C program ---> Assembly level program ---> Machine level langauage (Binary form)**
The binary format is then fed into the layout and then the execution proceeds and we get the required output.
There is a need of one more interface between RISC-V and the layout, that is the **Hardware descriptive language (HDL)**. 

RISC-V Architecture will have some kind of specifications. HDL is used to implement these specifications of RISC-V Architecture
