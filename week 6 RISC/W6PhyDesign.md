
# Digital VLSI SoC Design and Planning


<!---
Comments
-->

>  Week 6 digital VLSI SoC design and planning workshop with complete RTL2GDSII flow

## Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK 

### Theory

<details>
  <summary>
Expand or Collapse
  </summary>

#### Package

* In any embedded board we have seen, the part of the board we consider as the chip is only the ***PACKAGE*** of the chip which is nothing but a protective layer or packet bound over the actual chip and the actual manufatured chip is usually present at the center of a package wherein, the connections from package is fed to the chip by ***WIRE BOUND*** method which is none other than basic wired connection.


#### Chip

* Now, taking a look inside the chip, all the signals from the external world to the chip and vice versa is passed through ***PADS***. The area bound by the pads is ***CORE*** where all the digital logic of the chip is placed. Both the core and pads make up the ***DIE*** which is the basic manufacturing unit in regards to semiconductor chips.


* ***FOUNDRY*** is the place where the semiconductor chips are manufactured and ***FOUNDRY IP's*** are Intellectual Properties based on a specific foundry and these IP's require a specific level of intelligence to be produced whereas, repeatable digital logic blocks are called ***MACROS***.


#### ISA (Intruction Set Architecture)

* A C program which has to be run on a specific hardware layout which is the interior of a chip in your laptop, there is certain flow to be followed.
* Initially, this particular C program is compiled in it's assembly language program which is nothing but ***RISC-V ISA (Reduced Instruction Set Compting - V Intruction Set Architecture)***.
* Following this, the assembly language program is then converted to machine language program which is the binary language logic 0 and 1 which is understood by the hardware of the computer.
* Directly after this, we've to implement this RISC-V specification using some ***RTL (a Hardware Description Language)***. Finally, from the RTL to ***Layout*** it is a standard PnR or RTL to GDSII flow.


* For an application software to be run on a hardware there are several processes taking place. To begin with, the apps enters into a block called system software and it converts the application program to binary language. There are various layers in system software in which the major layers or components are OS (Operating System), Compiler and Assembler.
* At first the OS outputs are small function in C, C++, VB or Java language which are taken by the respective compiler and converted into instructions and the syntax of these instructions varies with the hardware architecture on which the system is implemented.
* Then, the job of the assembler is to take these instructions and convert it into it's binary format which is basically called as a machine language program. Finally, this binary language is fed to the hardware and it understands the specific functions it has to perform based on the binary code it receives.


* For example, if we take a stopwatch app on RISC-V core, then the output of the OS could be a small C function which enters into the compiler and we get output RISC-V instructions following this, the output of the assembler will be the binary code which enters into your chip layout.


* For the above stopwatch the following are the input and output of the compiler and assembler.


* The output of the compiler are instructions and the output of the assembler is the binary pattern. Now, we need some RTL (a Hardware Description Language) which understands and implements the particular instructions. Then, this RTL is synthesised into a netlist in form of gates which is fabricated into the chip through a physical design implementation.


* There are mainly 3 different parts in this course. They are:
1. RISC-V ISA
2. RTL and synthesis of RISC-V based CPU core - picorv32
3. Physical design implementation of picorv32


#### Open-source Implementation

* For open-source ASIC design implemantation, we require the following enablers to be readily available as open-source versions. They are:-
1. RTL Designs
2. EDA Tools
3. PDK Data

* Initially in the early ages, the design and fabrication of IC's were tightly coupled and were only practiced by very few companies like TI, Intel, etc.
* In 1979, Lynn Conway and Carver Mead came up with an idea to saperate the design from the fabrication and to do this they inroduced structured design methodologies based on the λ-based design rules and published the first VLSI book "Introduction to VLSI System" which started the VLSI education.
* This methodology resulted in the emergence of the design only companies or ***"Fabless Companies"*** and fabrication only companies that we usually refer to as ***"Pure Play Fabs"***.
* The inteface between the designers and the fab by now became a set of data files and documents, that are reffered to as the ***"Process Design Kits (PDKs)"***.
* The PDK include but not limited to Device Models, Technology Information, Design Rules, Digital Standard Cell Libraries, I/O Libraries and many more.
* Since, the PDK contained variety of informations, and so they were distributed only under NDAs (Non-Disclosure Agreements) which made it in-accessible to the public.
* Recently, Google worked out an agreement with skywater to open-source the PDK for the 130nm process by skywater Technology, as a result on 30 June 2020 Google released the first ever open-source PDK.


* ASIC design is a complex step that involves tons of steps, various methodologies and respective EDA tools which are all required for successful ASIC implementation which is achieved though an ASIC flow which is nothing but a piece of software that pulls different tools togather to carry out the design process.


#### OpenLANE Open-source ASIC Design Implementation Flow

* The main objective of the ASIC Design Flow is to take the design from the RTL (Register Transfer Level) all the way to the GDSII, which is the format used for the final fabrication layout.


* Synthesis is the process of convertion or translation of design RTL into circuits made out of Standard Cell Libraries (SCL) the resultant circuit is described in HDL and is usually reffered to as the Gate-Level Netlist.
* Gate-Level Netlist is functionally equivalent to the RTL.


* The fundemental building blocks which are the standard cells have regular layouts.
* Each cell has different views/models which are utilised by different EDA tools like liberty view with electrical models of the cells, HDL behavioral models, SPICE or CDL views of the cells, Layout view which include GDSII view which is the detailed view and LEF view which is the abstract view.


* Chip Floor Planning


* Macro Floor Planning


* Power Planning typically uses upper metal layers for power distribution since thay are thicker than lower metal layers and so have lower resistance and PP is done to avoid electron migration and IR drops.


* Placement


* Global placement provide approximate locations for all cells based on connectivity but in this stage the cells may be overlapped on each other and in detailed placement the positions obtained from global placements are minimally altered to make it legal (non-overlapping and in site-rows)


* Clock Tree Synthesis


* Clock skew is the time difference in arrival of clock at different components.
* Routing


* skywater PDK has 6 routing layers in which the lowest layer is called the local interconnect layer which is a Titanium Nitride layer the following 5 layers are all Aluminium layers.


* Global and Detailed Routing


* Once done with the routing the final layout can be generated which undergoes various Sign-Off checks.
* Design Rules Checking (DRC) which verifies that the final layout honours all design fabrication rules.
* Layout Vs Schematic (LVS) which verifies that the final layout functionality matches the gate-level netlist that we started with.
* Static Timing Analysis (STA) to verify that the design runs at the designated clock frequency.


</details>

### Implementation

Section 1 tasks:- 
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio.

```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```

* All section 1 logs, reports and results can be found in following run folder:


#### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform synthesis

```bash
# Change directory to openlane flow directory
cd ~/Desktop/work/tools/openlane_working_dir/openlane


# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive
```
![openlane opening 1 1](https://github.com/user-attachments/assets/cc8bf309-0fe1-403b-b206-405db9bfa60e)
```
# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
set design_name  picorv32a
prep -design picorv32a
```

```
# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```
![design set 1 2](https://github.com/user-attachments/assets/9e4101f3-0b8b-4d51-8acb-a73a1b4d738c)
![synthesis 1 3](https://github.com/user-attachments/assets/14cfa39d-88b4-48bf-b2de-10385418292a)

```
# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```


#### 2. Calculate the flop ratio.

Screenshots of synthesis statistics report file with required values highlighted
![2 1 flop ratio ](https://github.com/user-attachments/assets/f289fa90-0f6e-4d24-b8cf-d4b1fa5ff4ce)
![2 2 flop ratio ](https://github.com/user-attachments/assets/fdbfa5a2-84b3-4009-888e-bdbe14fd1c77)


Calculation of Flop Ratio and DFF % from synthesis statistics report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```

## Section 2 - Good floorplan vs bad floorplan and introduction to library cells 

### Theory

### Implementation

Section 2 tasks:- 
1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2. Calculate the die area in microns from the values in floorplan def.
3. Load generated floorplan def in magic tool and explore the floorplan.
4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5. Load generated placement def in magic tool and explore the placement.

```math
Area\ of\ die\ in\ microns = Die\ width\ in\ microns * Die\ height\ in\ microns
```

#### 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Now we can run floorplan
run_floorplan
```

Screenshot of floorplan run
![3 1 floorplanrun](https://github.com/user-attachments/assets/ba9af06b-3315-426b-85ed-227ea025675a)
![3 2 floorplanrun](https://github.com/user-attachments/assets/69e6a8f0-014c-49d7-8213-a1a457de5336)


#### 2. Calculate the die area in microns from the values in floorplan def.

Screenshot of contents of floorplan def
![3 3 die area](https://github.com/user-attachments/assets/75fc78d3-64c9-4c0b-bc98-34c4e017552a)


According to floorplan def
```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685
```
```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```
```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```
```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```
```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```
```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```

#### 3. Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

```bash
# Change directory to path containing generated floorplan def
cd ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/01-11_09-04/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

Screenshots of floorplan def in magic

![4 1 magic](https://github.com/user-attachments/assets/d0ff205d-7dc8-4df8-865e-db7ff6db48a3)

Equidistant placement of ports

![4 2 magic](https://github.com/user-attachments/assets/e271e065-e409-4aba-9423-07267061dcf4)

Port layer as set through config.tcl
![4 3 magic](https://github.com/user-attachments/assets/c93a62f5-d554-4777-afb2-ef2eed77a227)

Decap Cells and Tap Cells

![4 4 magic](https://github.com/user-attachments/assets/7ad601de-380a-42f9-ac9c-5e589682808b)

Diogonally equidistant Tap cells
![4 6 magic](https://github.com/user-attachments/assets/92ac8c8f-b6f1-4d5d-b546-7c45d5f9f60c)

![4 7 magic](https://github.com/user-attachments/assets/69f1886f-cd0e-4f6f-8ba4-591fa08e8a42)

Unplaced standard cells at the origin

![4 8 magic](https://github.com/user-attachments/assets/c5f8b17e-9b4f-40b1-aacb-4467029e3208)

#### 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

```tcl
# Congestion aware placement by default
run_placement
```

Screenshots of placement run
![5 1 runplacement](https://github.com/user-attachments/assets/b6d4e4d6-d5f8-4fa3-8e92-dd2ec3880357)

![5 2 runplacement](https://github.com/user-attachments/assets/6a0cac7d-1204-4c44-83e7-d2649aa83283)

#### 5. Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshots of floorplan def in magic
![6 1 magic layout after placement](https://github.com/user-attachments/assets/9346bf08-5b2b-4453-924d-208a0a63578a)

Standard cells legally placed 
![6 2 magic layout after placement](https://github.com/user-attachments/assets/6e45d0a5-8c6d-435f-86d3-cb2ec505b2f6)

Commands to exit from current run

```tcl
# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```

## Section 3 - Design library cell using Magic Layout and ngspice characterization 

### Theory

### Implementation

* Section 3 tasks:-
1. Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using OpenLANE flow](https://github.com/nickson-jose/vsdstdcelldesign).
2. Load the custom inverter layout in magic and explore.
3. Spice extraction of inverter in magic.
4. Editing the spice model file for analysis through simulation.
5. Post-layout ngspice simulations.
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.



#### 1. Clone custom inverter standard cell design from github repository

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of commands run
![7 1 copy vsdstdcelldesign](https://github.com/user-attachments/assets/ac60fac1-90ea-4d6a-a932-c7cabf9d4e9e)


#### 2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic
![7 2 magic inverter](https://github.com/user-attachments/assets/a7fb505d-9f75-406e-882d-e076ff8f2b20)


NMOS and PMOS identified
![7 3 magic inverter nmos](https://github.com/user-attachments/assets/072d0521-696f-4948-862c-df0d4e9b975f)
![7 4 magic inverter pmos](https://github.com/user-attachments/assets/b97f358d-37a5-4911-ad38-248469c33821)


Output Y connectivity to PMOS and NMOS drain verified
![7 5 magic inverter y](https://github.com/user-attachments/assets/74e91c57-2945-4bc4-9767-e34aa299c263)


PMOS source connectivity to VDD (here VPWR) verified
![7 6 magic inverter vpwr](https://github.com/user-attachments/assets/42d5d624-23b7-47e2-88ba-0f4516abd5d0)


NMOS source connectivity to VSS (here VGND) verified
![7 7 magic inverter vgnd](https://github.com/user-attachments/assets/a0485ec6-77eb-4d1a-a82c-db62837fca8a)


Deleting necessary layout part to see DRC error
![7 8 magic inverter DRC with error](https://github.com/user-attachments/assets/04f93cf9-b718-4cc8-b3fc-b1400bb6a1be)


#### 3. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```tcl
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```

Screenshot of tkcon window after running above commands
![8 1 extraction](https://github.com/user-attachments/assets/21eb2a0e-9f71-4019-8130-0562ba1fa0b9)


Screenshot of created spice file
![8 2 after ext spice file](https://github.com/user-attachments/assets/6f5306ba-b46b-48d9-acf8-3b69f48902cb)


#### 4. Editing the spice model file for analysis through simulation.

Measuring unit distance in layout grid
![9 1 inverter box size](https://github.com/user-attachments/assets/a0667815-b5fe-4617-b910-183db48858e6)


Final edited spice file ready for ngspice simulation
![9 2 sky130_inv spice file updated](https://github.com/user-attachments/assets/08939adf-cc7c-4c3f-b616-4268209f89ff)


#### 5. Post-layout ngspice simulations.

Commands for ngspice simulation

```bash
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

Screenshots of ngspice run

![10 1 sky130_inv spice ngspice simulation](https://github.com/user-attachments/assets/cb9b8381-7c71-41bf-88d3-a0db094f2fb3)


Screenshot of generated plot

![10 2 sky130_inv spice ngspice output plot](https://github.com/user-attachments/assets/29e5a14a-ef29-484f-bd5a-7ba3a969dc3e)
![10 3 sky130_inv spice ngspice output plot](https://github.com/user-attachments/assets/9fd3aa24-a02d-456c-abe1-2ff6a53e0ed6)


Rise transition time calculation

```math
Rise\ transition\ time = Time\ taken\ for\ output\ to\ rise\ to\ 80\% - Time\ taken\ for\ output\ to\ rise\ to\ 20\%
```
```math
20\%\ of\ output = 660\ mV
```
```math
80\%\ of\ output = 2.64\ V
```

20% Screenshots
![10 4 sky130_inv spice ngspice rise plot 20%](https://github.com/user-attachments/assets/e5edfb68-a6d6-43d1-bb89-db51ade7a7a3)
![10 5 sky130_inv spice ngspice rise plot 20%](https://github.com/user-attachments/assets/3d3a3bc7-d9d9-49b0-86b2-c4da862113aa)


80% Screenshots
![10 6 sky130_inv spice ngspice rise plot 80%](https://github.com/user-attachments/assets/fea54849-c38e-4972-9a48-2b489b80e237)
![10 7 sky130_inv spice ngspice rise plot 80%](https://github.com/user-attachments/assets/921ba4b9-90be-471a-b43b-d298613f49ad)


```math
Rise\ transition\ time = 2.24638 - 2.18242 = 0.06396\ ns = 63.96\ ps
```

Fall transition time calculation

```math
Fall\ transition\ time = Time\ taken\ for\ output\ to\ fall\ to\ 20\% - Time\ taken\ for\ output\ to\ fall\ to\ 80\%
```
```math
20\%\ of\ output = 660\ mV
```
```math
80\%\ of\ output = 2.64\ V
```

20% Screenshots
![10 8 sky130_inv spice ngspice fall plot 20%](https://github.com/user-attachments/assets/ba136a9a-61a3-470f-959d-5f6d327a03b7)
![10 9 sky130_inv spice ngspice fall plot 20%](https://github.com/user-attachments/assets/14a3306c-aa23-4085-8ff2-261597a106a4)


80% Screenshots
![10 10 sky130_inv spice ngspice fall plot 80%](https://github.com/user-attachments/assets/4720904a-1d77-420a-9593-d45f5c117171)
![10 11 sky130_inv spice ngspice fall plot 80%](https://github.com/user-attachments/assets/a87c5bd9-8b8f-4319-882c-e62f8f1ab305)


```math
Fall\ transition\ time = 4.0955 - 4.0536 = 0.0419\ ns = 41.9\ ps
```

Rise Cell Delay Calculation

```math
Rise\ Cell\ Delay = Time\ taken\ for\ output\ to\ rise\ to\ 50\% - Time\ taken\ for\ input\ to\ fall\ to\ 50\%
```
```math
50\%\ of\ 3.3\ V = 1.65\ V
```

50% Screenshots
![10 12 sky130_inv spice ngspice rise delay](https://github.com/user-attachments/assets/be5697e4-5bbe-4ed9-a3db-3745c2c3ff96)
![10 13 sky130_inv spice ngspice rise delay](https://github.com/user-attachments/assets/b4e361f6-3e22-4ed8-9d3e-6a3b4741e72d)


```math
Rise\ Cell\ Delay = 2.21144 - 2.15008 = 0.06136\ ns = 61.36\ ps
```

Fall Cell Delay Calculation

```math
Fall\ Cell\ Delay = Time\ taken\ for\ output\ to\ fall\ to\ 50\% - Time\ taken\ for\ input\ to\ rise\ to\ 50\%
```
```math
50\%\ of\ 3.3\ V = 1.65\ V
```

50% Screenshots
![10 14 sky130_inv spice ngspice fall delay](https://github.com/user-attachments/assets/5cc0bed5-fbe9-46c0-a938-41bfc30b0653)
![10 15 sky130_inv spice ngspice fall delay](https://github.com/user-attachments/assets/18f6e5a1-8f14-4f75-8837-6129a194bba3)


```math
Fall\ Cell\ Delay = 4.07 - 4.05 = 0.02\ ns = 20\ ps
```

#### 6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

Link to Sky130 Periphery rules: [https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html)

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

```bash
# Change to home directory
cd

# Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -al

# Command to view .magicrc file
gvim .magicrc

# Command to open magic tool in better graphics
magic -d XR &
```

Screenshots of commands run
![11 1 DRC old tech file update](https://github.com/user-attachments/assets/6ed7c156-3947-4086-a5d0-3a72f748f63c)
![11 2 DRC old tech file update](https://github.com/user-attachments/assets/28900003-898e-4eff-ace5-e8c3ec4c3e92)


Screenshot of .![11 3 gvim  magicir file](https://github.com/user-attachments/assets/95018c95-0276-424b-b6b8-edf07762fc96)
magicrc file


**Incorrectly implemented poly.9 simple rule correction**

Screenshot of poly rules
![12 1 poly rules](https://github.com/user-attachments/assets/ed1b510f-f228-4061-998b-062e87919bbb)


Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u
![12 2 poly9 incorrect rule](https://github.com/user-attachments/assets/f03286e0-9c20-4b61-a7d5-b2260a53e99b)


New commands inserted in sky130A.tech file to update drc
![12 3 poly9 correct rule](https://github.com/user-attachments/assets/eabb15e1-697f-4a52-996e-63f83822ab89)
![12 4 poly9 correct rule](https://github.com/user-attachments/assets/499ede26-bde6-4a2e-a7b0-d8d1ab0f6cc7)


Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```

Screenshot of magic window with rule implemented
![12 4 poly9 DRC error](https://github.com/user-attachments/assets/5d7006cd-bdf0-42df-bb9a-8c98ee1a1753)

Commands to run in tkcon window

```tcl
# Loading updated tech file
tech load sky130A.tech

# Must re-run drc check to see updated drc errors
drc check

# Selecting region displaying the new errors and getting the error messages 
drc why
```


## Section 4 - Pre-layout timing analysis and importance of good clock tree 

### Theory

### Implementation

* Section 4 tasks:-
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
2. Save the finalized layout with custom name and open it.
3. Generate lef from the layout.
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
6. Run openlane flow synthesis with newly inserted custom inverter cell.
7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
9. Do Post-Synthesis timing analysis with OpenSTA tool.
10. Make timing ECO fixes to remove all violations.
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
12. Post-CTS OpenROAD timing analysis.
13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

* Section 4 - Tasks 1 to 4 files, reports and logs can be found in the following folder:


* Section 4 - Task 4 files, reports and logs can be found in the following folder:


* Section 4 - Task 5 files, reports and logs can be found in the following folder:


* Section 4 - Tasks 6 to 8 & 11 to 13 logs, reports and results can be found in following run folder:


* Section 4 - Tasks 9 to 11 logs, reports and results can be found in following run folder:


#### 1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.

Conditions to be verified before moving forward with custom designed cell layout:
* Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
* Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
* Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

Commands to open the custom inverter layout

```bash
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of tracks.info of sky130_fd_sc_hd
![13 1 track info](https://github.com/user-attachments/assets/e192ac2d-bb2d-4389-abd1-df4fa085aa76)


Commands for tkcon window to set grid as tracks of locali layer

```tcl
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```

Screenshot of commands run
![13 2 layout with grid](https://github.com/user-attachments/assets/995e61fa-9a4d-4bfa-b190-49a833aac569)



Condition 1 verified
![13 3 layout with grid cond1](https://github.com/user-attachments/assets/147112e9-be25-47ec-af94-a41bb2cd8565)


Condition 2 verified
![13 4 layout with grid cond2](https://github.com/user-attachments/assets/f2c69291-9e71-40d2-a2c3-51dfbdfc43cf)


```math
Horizontal\ track\ pitch = 0.46\ um
```


```math
Width\ of\ standard\ cell = 1.38\ um = 0.46 * 3
```



```math
Vertical\ track\ pitch = 0.34\ um
```



```math
Height\ of\ standard\ cell = 2.72\ um = 0.34 * 8
```

#### 2. Save the finalized layout with custom name and open it.

Command for tkcon window to save the layout with custom name

```tcl
# Command to save as
save sky130_vsdinv.mag
```

Command to open the newly saved layout


```bash
# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &
```

Screenshot of newly saved layout
![13 5 layout saved updated](https://github.com/user-attachments/assets/f9f69a9a-cbdd-4d15-b3c2-d2e1a136a089)


#### 3. Generate lef from the layout.

Command for tkcon window to write lef

```tcl
# lef command
lef write
```

Screenshot of command run
![13 6 lef file created](https://github.com/user-attachments/assets/6b557c77-435a-4be4-ba87-b3869a7a6ff7)

Screenshot of newly created lef file

![13 7 lef file created](https://github.com/user-attachments/assets/aa4dc097-cb53-46f6-a731-6bfdf3308466)



#### 4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

Commands to copy necessary files to 'picorv32a' design 'src' directory

```bash
# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

Screenshot of commands run
![13 8 command run](https://github.com/user-attachments/assets/60a55933-6738-477e-9cf3-639c7c9d5333)


#### 5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

Commands to be added to config.tcl to include our custom cell in the openlane flow

```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Edited config.tcl to include the added lef and change library to ones we added in src directory

![13 9 edited config tcl](https://github.com/user-attachments/assets/780c3bd2-df0d-42cc-aef5-578f41108e3f)


#### 6. Run openlane flow synthesis with newly inserted custom inverter cell.

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs



# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshots of commands run
![14 1 synthesis run after custom inverter included](https://github.com/user-attachments/assets/71e42084-7e48-41dd-9dc1-b3fb645bc760)

![14 2 synthesis run after custom inverter included](https://github.com/user-attachments/assets/6ef0f31b-a575-423d-8fbb-9be1f0bae6fe)

![14 3 synthesis run after custom inverter included](https://github.com/user-attachments/assets/d6513983-1367-4f6f-a005-cfaaa1c798a9)
![14 4 synthesis run after custom inverter included](https://github.com/user-attachments/assets/de9165f2-1384-493d-b573-2debb63b127c)


#### 7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing
![14 5 chip area before modified](https://github.com/user-attachments/assets/b3d03ec0-13d0-40ee-ac81-bb44b468c1d2)

![14 5 tns wns before modified](https://github.com/user-attachments/assets/2a8ec288-eb9c-4e22-96f6-0301dccec8e0)


Commands to view and change parameters to improve timing and run synthesis

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-11_08-51 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Screenshot of merged.lef in `tmp` directory with our custom inverter as macro
![14 6 merged lef in tmp](https://github.com/user-attachments/assets/5acc37ba-4cb1-4dc7-bc82-ccba8f2f23a9)


Screenshots of commands run
![14 7 command run](https://github.com/user-attachments/assets/318c1139-3894-4638-afe8-2e22f9cad5fe)
![14 8 command run](https://github.com/user-attachments/assets/3ba2c40c-490b-47d8-8c33-e8f84214c857)
![14 9 synthesis run after modified](https://github.com/user-attachments/assets/e9c17b89-9606-4d0d-af15-cd55d6c47ff0)

Comparing to previously noted run values area has increased and worst negative slack has become 0

![14 10 chip area after modified](https://github.com/user-attachments/assets/d1d166b2-33ef-4fcb-94d6-5e006af5129e)

![14 11 tns wns after modified](https://github.com/user-attachments/assets/934a219d-e001-4207-b86d-570aa81872ea)

#### 8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following command

```tcl
# Now we can run floorplan
run_floorplan
```

Screenshots of command run
![14 12 run floorplan](https://github.com/user-attachments/assets/a25ee482-8809-4fe5-95d8-df9e94f274d4)
![14 13 run floorplan error](https://github.com/user-attachments/assets/c4d91bed-a43c-48eb-a0b8-27e211e6ed9c)


Since we are facing unexpected un-explainable error while using `run_floorplan` command, we can instead use the following set of commands available based on information from `Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl` and also based on `Floorplan Commands` section in `Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md`

```tcl
# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
```

Screenshots of commands run
![14 14 run floorplan error solution](https://github.com/user-attachments/assets/49cac464-8d83-46d8-95c1-152b3c44c796)
![14 15 run floorplan error solution](https://github.com/user-attachments/assets/de3f2633-b6e6-44fe-a098-0690d3e7b902)

![14 16 run floorplan error solution](https://github.com/user-attachments/assets/2e47a0ae-5611-4a94-89ae-7562d4159cd7)


Now that floorplan is done we can do placement using following command

```tcl
# Now we are ready to run placement
run_placement
```

Screenshots of command run
![14 17 run placement](https://github.com/user-attachments/assets/95bddd8f-45de-4ba7-8255-841b9d4f9865)


Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-11_08-51/results

# Command to load the placement def in magic tool
 magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-11_08-51/tmp/merged.lef def read /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-11_08-51/results/placement/picorv32a.placement.def

```

Screenshot of placement def in magic
![15 1 def magic](https://github.com/user-attachments/assets/08c1a165-b007-434f-a259-38127a4c7a33)



Screenshot of custom inverter inserted in placement def with proper abutment
![15 2 def magic](https://github.com/user-attachments/assets/6f08d132-59c5-47b6-8981-7d8c370dbdce)


Command for tkcon window to view internal layers of cells

```tcl
# Command to view internal connectivity layers
expand
```

Abutment of power pins with other cell from library clearly visible
![15 3 def magic after expand](https://github.com/user-attachments/assets/2ffc01ad-8e04-4881-8a3c-6f2e8b2d2215)



#### 9. Do Post-Synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis 

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Commands run final screenshot
![15 4 synthesis success](https://github.com/user-attachments/assets/e98b9c2b-4599-405f-bca1-0c4569f9d691)



Newly created `pre_sta.conf` for STA analysis in `openlane` directory
![15 5 pre_sta conf](https://github.com/user-attachments/assets/3e044011-e713-42cf-8844-a65e3cb5b1f3)



Newly created `my_base.sdc` for STA analysis in `openlane/designs/picorv32a/src` directory based on the file `openlane/scripts/base.sdc`
![15 6 mybase sdc](https://github.com/user-attachments/assets/2a7f2149-5ee0-4a62-8f7e-00404cf55df3)


Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

Screenshots of commands run
![15 7 sta pre_sta conf](https://github.com/user-attachments/assets/e774fd9c-ba92-48d7-ab32-0ad3afe3287a)
![15 8 sta pre_sta conf](https://github.com/user-attachments/assets/78eb60f0-1496-4cff-9f2d-43869c085fa6)

![15 9 sta pre_sta conf](https://github.com/user-attachments/assets/d65cb837-8f73-4f2c-bb6a-e18aa2816127)

Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again

Commands to include new lef and perform synthesis 

```tcl
# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
 prep -design picorv32a -tag /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-11_08-51 -overwrite 

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to set new value for SYNTH_MAX_FANOUT
set ::env(SYNTH_MAX_FANOUT) 4

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Commands run final screenshot
![16 1 openlane run_synthesis](https://github.com/user-attachments/assets/0ca8889b-24e6-4c15-8ecd-613392d19dce)
![16 2 openlane run_synthesis](https://github.com/user-attachments/assets/07cba6d4-519e-4fb7-b253-1d9daaea98b2)


Commands to run STA in another terminal

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

Screenshots of commands run
![16 3 updated pre_sta conf](https://github.com/user-attachments/assets/3d8902d9-4a8d-4aa4-aa36-55e89d2876a9)

![16 4 updated pre_sta conf](https://github.com/user-attachments/assets/7cc19e0a-b0b5-44c5-9e6b-ac9d4231a190)

![16 5 updated pre_sta conf](https://github.com/user-attachments/assets/4a13202a-1894-48c6-89f8-e15a046087b7)

#### 10. Make timing ECO fixes to remove all violations.

OR gate of drive strength 2 is driving 4 fanouts
![16 6 slack inc due or gate 1](https://github.com/user-attachments/assets/d1c03ab7-8cf1-408e-bd97-10da0127c778)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11672_

# Checking command syntax
help replace_cell

# Replacing cell
replace_cell _14510_ sky130_fd_sc_hd__or3_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced
![16 7 change or gate 1](https://github.com/user-attachments/assets/56703055-d873-4c78-bd21-a33115b4bdca)
![16 8 updated 1 slack](https://github.com/user-attachments/assets/32d32ca6-cbfd-4829-abb9-a9e25d9458b0)
![16 9 updated 1 slack](https://github.com/user-attachments/assets/52825e7c-539c-471a-ba97-fd4e70caf550)

![16 10 updated 1 slack](https://github.com/user-attachments/assets/d00f7e50-bebe-4b5e-8328-f2790c22224c)

OR gate of drive strength 2 is driving 4 fanouts

![16 11 slack inc due or gate 2](https://github.com/user-attachments/assets/ec562821-fc46-470c-b96b-d8ada24d28a8)



Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11675_

# Replacing cell
replace_cell _14514_ sky130_fd_sc_hd__or3_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced
![16 12 change or gate 2](https://github.com/user-attachments/assets/a4413ac2-57bb-4ae1-b077-94ee5672be87)
![16 13 updated 2 slack](https://github.com/user-attachments/assets/d287d4c9-90d1-487e-bb5a-6da4d9ce4f15)
![16 14 updated 2 slack](https://github.com/user-attachments/assets/683f56a0-5922-459f-8949-778ec6309753)

![16 15 updated 2 slack](https://github.com/user-attachments/assets/18792292-11a1-4f20-b156-92ef98f909be)


OR gate of drive strength 2 driving OA gate has more delay
![16 16 change or gate 3](https://github.com/user-attachments/assets/c491974a-466a-4c1e-bcda-4dcadaa47cb0)


Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11643_

# Replacing cell
replace_cell _14481_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced
![16 17 updated 3 slack](https://github.com/user-attachments/assets/542613af-19ed-499c-8300-5602b7833c35)
![16 18 updated 3 slack](https://github.com/user-attachments/assets/95340e38-6683-4eb5-8115-0212fa05478c)
![16 19 updated 3 slack](https://github.com/user-attachments/assets/d9b4f4e4-d403-41c2-91de-290fd007a092)
![16 20 updated 3 slack](https://github.com/user-attachments/assets/3a1c603e-4109-487a-b5bd-77f43ccfdac8)


OR gate of drive strength 2 driving OA gate has more delay

![16 21 slack inc due or gate 4](https://github.com/user-attachments/assets/5be3d84b-23d5-4f6e-916d-8b428eb01b4d)

Commands to perform analysis and optimize timing by replacing with OR gate of drive strength 4

```tcl
# Reports all the connections to a net
report_net -connections _11668_

# Replacing cell
replace_cell _14506_ sky130_fd_sc_hd__or4_4

# Generating custom timing report
report_checks -fields {net cap slew input_pins} -digits 4
```

Result - slack reduced

![16 22 updated 4 slack](https://github.com/user-attachments/assets/e1e5a377-3d2a-41bc-8077-3d8fff9ab001)
![16 23 updated 4 slack](https://github.com/user-attachments/assets/ac84da0c-0fd0-4d1f-af7b-f1520f73daf1)

![16 24 updated 4 slack](https://github.com/user-attachments/assets/7e05e4d0-cecf-42c3-b13a-1538a837bba9)

![16 25 updated 4 slack](https://github.com/user-attachments/assets/ad7ff377-c41e-449b-a70c-daa7cc72aa93)


Commands to verify instance `_14506_`  is replaced with `sky130_fd_sc_hd__or4_4`

```tcl
# Generating custom timing report
report_checks -from _29043_ -to _30440_ -through _14506_
```

Screenshot of replaced instance
![16 26 updated 5 slack](https://github.com/user-attachments/assets/8953787e-42b8-4c4b-aae3-d89abe1e4aa3)



*We started ECO fixes at wns -23.9000 and now we stand at wns -22.6173 we reduced around 1.2827 ns of violation*

#### 11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.

Now to insert this updated netlist to PnR flow and we can use `write_verilog` and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist

Commands to make copy of netlist

```bash
# Change from home directory to synthesis results directory
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/

# List contents of the directory
ls

# Copy and rename the netlist
cp picorv32a.synthesis.v picorv32a.synthesis_old.v

# List contents of the directory
ls
```

Screenshot of commands run
![17 1 copy synthesis file](https://github.com/user-attachments/assets/e799926b-b07b-4988-9d20-e31005844e9f)



Commands to write verilog

```tcl
# Check syntax
help write_verilog

# Overwriting current synthesis netlist

write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/03-11_08-51/results/synthesis/picorv32a.synthesis.v


# Exit from OpenSTA since timing analysis is done
exit
```

Screenshot of commands run
![17 2 write_verilog synthesis](https://github.com/user-attachments/assets/471272a1-176b-413f-85df-4f89235c20f0)

![17 3 old synthesis file](https://github.com/user-attachments/assets/dba99a21-6a8b-40f6-b570-d4166f34abd8)

Verified that the netlist is overwritten by checking that instance `_14506_`  is replaced with `sky130_fd_sc_hd__or4_4`
![17 4 new synthesis file](https://github.com/user-attachments/assets/1f5cd439-2744-4814-b27f-6e8d45d5aa9f)



Since we confirmed that netlist is replaced and will be loaded in PnR but since we want to follow up on the earlier 0 violation design we are continuing with the clean design to further stages

Commands load the design and run necessary stages

```tcl
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts
```

Screenshots of commands run



#### 12. Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Check syntax of 'report_checks' command
help report_checks

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

Screenshots of commands run and timing report generated


#### 13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis after changing `CTS_CLK_BUFFER_LIST`

```tcl
# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Checking current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Setting def as placement def
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/placement/picorv32a.placement.def

# Run CTS again
run_cts

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts1.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Report hold skew
report_clock_skew -hold

# Report setup skew
report_clock_skew -setup

# Exit to OpenLANE flow
exit

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

# Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

# Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)
```

Screenshots of commands run and timing report generated



## Section 5 - Final steps for RTL2GDS using tritonRoute and openSTA

### Theory

### Implementation

* Section 5 tasks:-
1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
2. Perfrom detailed routing using TritonRoute.
3. Post-Route parasitic extraction using SPEF extractor.
4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

* All section 5 logs, reports and results can be found in following run folder:

[Section 5 Run - 26-03_08-45](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45)

#### 1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.

Commands to perform all necessary stages up until now

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Following commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts

# Now that CTS is done we can do power distribution network
gen_pdn 
```

Screenshots of power distribution network run



Commands to load PDN def in magic in another terminal

```bash
# Change directory to path containing generated PDN def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/tmp/floorplan/

# Command to load the PDN def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
```

Screenshots of PDN def



#### 2. Perfrom detailed routing using TritonRoute and explore the routed layout.

Command to perform routing

```tcl
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

# Command for detailed route using TritonRoute
run_routing
```

Screenshots of routing run


Commands to load routed def in magic in another terminal

```bash
# Change directory to path containing routed def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/results/routing/

# Command to load the routed def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```

Screenshots of routed def



Screenshot of fast route guide present in `openlane/designs/picorv32a/runs/26-03_08-45/tmp/routing` directory



#### 3. Post-Route parasitic extraction using SPEF extractor.

Commands for SPEF extraction using external tool

```bash
# Change directory
cd Desktop/work/tools/SPEF_EXTRACTOR

# Command extract spef
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.def
```

#### 4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/26-03_08-45/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.def

# Creating an OpenROAD database to work with
write_db pico_route.db

# Loading the created database in OpenROAD
read_db pico_route.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/synthesis/picorv32a.synthesis_preroute.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Read SPEF
read_spef /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.spef

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

Screenshots of commands run and timing report generated
