# PD_openlane_workshop_KunalGhosh
Documentation of the Openlane Sky130 workshop

# Day 1: Inception of opensource EDA, OpenLane and Sky130 PDK:
## Sky130_D1_SK1 - How to talk to computers:
### SKY_L1 - Introduction to QFN-48 Package, chip, pads, core, die and IP's: 
This is the aurdino board. 

<img width="1131" height="848" alt="Image" src="https://github.com/user-attachments/assets/cf39eda7-9e50-48d3-b958-e5149fbcaf9e" /> 

 **Fig 1.1: Aurdino board**


Here we consider only the  small part (the circled part which is the processor) which will be designed as a part of Physical design work. The components that consists the Aurdino board are the Processor/SoC, and the interfaces such as SDRAM, direct I2C, direct QSPI, GPIO0-7, PWM0-3, GPIO8-14, PWM4-5, JTAG-UART, FTDI, QSPI1-Flash, I2C0-EEPROM. The block diagram of the aurdino board is as shown below. 

<img width="1546" height="812" alt="Image" src="https://github.com/user-attachments/assets/7f78f813-0e40-41ed-b7a9-9d52f09ae4e5" />

**Fig 1.2: Block diagram of the Aurdino board**


The interanl structure of the processor is known as **package**. This is **Quad Flat No-leads(QFN-48)**. The pin locations are all driven by the Aurdino board that we will be designing. The size of the package shown below is 7mm*7mm. The chip is at the center of the package and is connected to the pins by the wire bounds.

<img width="1131" height="809" alt="Image" src="https://github.com/user-attachments/assets/3797eaef-0d41-43c0-8da3-e90eb7c46a30" />

**Fig 1.3: Internal structure of the Aurdino**


<img width="938" height="564" alt="Image" src="https://github.com/user-attachments/assets/808f8f81-eae8-4d9e-88f9-721badce87d0" />


**Fig 1.4 Pictorial representation of wire bounds**


A chip has various components in it as listed below:
- **Pads:** The pads are the one through which the signal can pass from out to in and vice versa. In general it can be compared to a door.
-  **Core:** This is the place of the chip where all the digital logic such as MUX, AND, OR, NOT gates, etc of the design are placed.
-  **Die:** This is the entire area of the chip, which is getting manufactured on the silicon wafer.

<img width="1249" height="807" alt="Image" src="https://github.com/user-attachments/assets/aad12eae-6eae-4dcf-99c3-2d7a2203e934" />

**Fig 1.5: Different parts of the chip**

Considering an example of RISC-V processor, few components of its digital logic includes of ADC, DAC, PLL, SRAM. These components are termed as **The Foundary IP's (Foundary Intellectual proprties)**. They have some king of intellectual property within them to build the blocks.
The foundary is a place or an industry with lot of machines. As a VLSI engineer, we have to communicate with these machines with the help of some interfaces. 
The SPI, RISC-V SoC are **the Macros**. 
The Macros are the pure digital logic.

<img width="833" height="567" alt="Image" src="https://github.com/user-attachments/assets/53b0ba88-5a4a-4565-bedc-3997f8f33a56" />


**Fig 1.6: Foundary IP's**


### SKY_L2 - Introduction to RISC-V Instruction set Architecture (ISA):

The top level description of ISA is this is the language using which we are going to talk to the computers.
**C program ---> Assembly level program ---> Machine level langauage (Binary form)**
The binary format is then fed into the layout and then the execution proceeds and we get the required output.
There is a need of one more interface between RISC-V and the layout, that is the **Hardware descriptive language (HDL)**. 

RISC-V Architecture will have some kind of specifications. HDL is used to implement these specifications of RISC-V Architecture


<img width="1266" height="743" alt="Image" src="https://github.com/user-attachments/assets/83bfb70e-a36b-4d29-84fb-6a371280b131" />

**Fig 1.7: RISC-V Architecture**


### SKY_L3 - From software applications to Hardware:

We have lot number of applications in our gadgets. All these applications gets exeuted on the single hardware present in the gadget.There is a interface between the application and the hardware and that is **the system software** whose output would be binary and is then sent to the hardware unit.

The important parts of the system software are the **Operating system (OS)**, the **Compiler** and the **Assembler**. 

Some of the functions that the **OS** performs are as follows:
- Handling the IO operations
- Allocating the memory
- Low level system functions

The **compiler** converts the input (C, C++, Java, etc) which is obtained from any applications into a set of insructions that is compatible with the hardware.

**Input (C, C++, Java, etc) ---> Compiler ---> Instruction set** 

The **assembler** receives the input from the compiler, which is its output and then the assembler converts it into to machine level language i.e. binary format.

**Input (Output of the compiler) ---> Assembler ---> MAchine level language (Binary form)**

<img width="1797" height="1080" alt="Image" src="https://github.com/user-attachments/assets/df748978-7914-442b-a988-6e44d26661fa" />

**Fig 1.8: From software applications to Hardware**

## Sky130_D1_SK2 - SoC Design and Openlane:
### SKY_L1 - Introduction to all the components of open-source digital ASIC design:
#### Digital ASIC Design:
To design the Application specific integrated circuits in automatic way, few elements are necessary such as,
- Hardware descriptive language (HDL) or the Register Transfer Level (RTL) of the IP's
- EDA tools
- Process Design Kit (PDK) data
 
<img width="785" height="330" alt="Image" src="https://github.com/user-attachments/assets/40c1571f-c981-419d-928b-e8e505c1963c" />

**Fig 1.9: Essential components fot ASIC designing**

#### What is PDK?
PDK is the collection of files used to model the fabriation process for the EDA tools used to design an IC. The files that are included are as follows,
- Process Design rules: DRC, LVS, PEX
- Device models
- Digital standard cell libraries
- I/O libraries, etc

#### Open-source Digital ASIC design:
**RTL Designs:**
- librecores.org
- opencores.org
- github.com

**EDA tools:**
  - Openlane
  - Qflow
  - Openroad

**PDK:**
- FOSS 130nm Production PDK by Google and Skywater

<img width="664" height="674" alt="Image" src="https://github.com/user-attachments/assets/afde51be-168a-41a5-bf0f-56de7fd75ff2" />

**Fig 1.11: Open-source elements**

#### ASIC design flow:
The main objective of ASIC design flow is to **convert RTL code to GDSII**. Also known as **Automated PnR/Physical Implementation**.

### SKY_L2 - Simplied RTL2GDS flow:
#### Simplied RTL to GDSII flow:

<img width="834" height="507" alt="Image" src="https://github.com/user-attachments/assets/24ebf363-cc5c-40a3-835b-8eb2ccdf2b75" />

**Fig 1.12:Simplified RTL to GDSII**

The major implementation steps in the flow includes,
- Synthesis
- Floorplannig/Powerplanning
- Placement
- Clock tree synthesis (CTS)
- Routing
- Signoff

#### Synthesis:
**Synthesis** is a stage where the RTL design is converted to a circuit which is made out of the components from the standard cell library (SCL). The resultant circuit is described in HDL and is termed as the **Gate level netlist**. 

The **standard cells** have regular layout with **uniform height** and **variable width**.

<img width="834" height="644" alt="Image" src="https://github.com/user-attachments/assets/c036823a-6026-4583-b70c-1070d5d905c0" />

**Fig 1.13: Synthesis**

#### Floorplanning and Powerplanning:
- **Floorplanning** is the partioning the chip die between different system building blocks and place the I/O pads.
-  **Macro floorplanning** is the stage where we define the macro dimensions, pin locations row and routing tracks are defined.

-  **Powerplanning:**
   - The power network is being constructed.
   - Typically the chips is supplied with multiple VDD and VSS stripes.
   - The power plan is connected to all the components through rings and vertical and horizontal metal straps.
   - The horizontal and vertical metal structure are meant to **reduce the resistance hence the IR drop**.
   - To address the **Electromigration (EM)** problem, typically the power distribution network uses upper metal layers as they are thicker than lower metal layers and hence have lower metal resistance.

- **Placement:**
  - In this stage the placement of the cells on the floorplan rows, that are aligned with the sites take place.
  - Connected cells in the netlist should be placed very closed to each other to reduce the inter-connect delay and also to ensure sucessful routing in the later stages.
  - Typically the placement is completed in two steps namely,
    - **Global** - Tries to find the optimal positions for all the standard cells. Those positions are not necessarily legal ones. The cells may overlap or go off rows.
    - **Detailed** - The positions obtained from the global placement are minimally altered to be legal.

- **Clock tree synthesis:**
  - Create the clock distribution network.
  - The clock distribution network is similar to a tree.
  - The clock distribution network is used to deliver the clock signal to all the sequential elements (Example: Flip-flops), with minimum skew and latency (ideally zero which is hard to achieve).
  - **Clock skew** means the arrival of the clock signal at different components at different times.
  - Some of the tree structures are, H, X, fish bone structure, etc.

- **Routing:**
  - This includes the signal routing.
  - Impements the interconnects using the available metal layers.
  - The SKY130 PDK define 6 routing layers. The lowest layer known as the **local interconnect layer**.
  - As the routing grid is huge the **Divide** and **Conquer** method is used in routing.
  - **Global routing** - Generate sthe routing guides
  - **Detailed routing** - Implements the actual wiring using the routing guides.

 - **Signoff:**
   - Once done with routing, the layout is made to undergo few of the verification steps as mentioned below.
     - **Physical verification:**
       - **Design rule correction (DRC)**
       - **Layout vs Schematic (LVS)**
     - **Timing verification**
       - **Static timing analysis (STA)**
    - The final layout follows all the design rules.
    - The final layout should also match the gate level netlist
