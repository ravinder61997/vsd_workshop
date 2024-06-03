# VSD Digital VLSI SoC Design and Planning
# DAY-1 
The introductory workshop on Day 1 provided a comprehensive overview of the RTL to GDSII flow, elucidating the seamless transformation of Verilog code into physical design. We as participants gained insights into the fundamental principles underlying the RISC-V processor architecture, and how these concepts translate into layout design. Crucially, the session delved into the intricate relationship between software applications and hardware, elucidating the pivotal role of compilers in bridging these domains. Additionally, attendees were introduced to the concept of Process Design Kits (PDKs), further enhancing their understanding of the integrated circuit design process.
## OPENLANE in Terminal 
During this session, we'll dive into the synthesis process for the specific design, picorv32, utilizing the OpenLane flow. Our objective is to generate the netlist and other essential reports following the synthesis step.
•	Before proceeding, it's imperative to ensure the smooth operation of the virtual machine environment.
•	Once everything is confirmed to be functioning optimally, we'll observe a terminal interface within the virtual machine environment, resembling the following:

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/a834119a-7e98-430c-942b-f1f78c53096d)

•	Before moving forward, let's navigate to the directory path: Desktop/work/tools/openlane_working_dir/openlane. This directory is essential for executing the synthesis steps effectively.
•	After that we will type docker command. why we are using docker whats the purpose of this?
Docker is like a magic box that bundles up all the stuff needed to run a program, like OpenLane for chip design. It makes sure everything works the same no matter where you run it. So, instead of setting up everything from scratch, you just use this box, called a container, and everything runs smoothly, saving you time and headaches.
•	When we run docker command the terminal will look like the below image-

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/2ae9a9c3-0def-4905-8855-fe89175a3ed5)

•	Next, step is to run the /flow.tcl script -interactive command. It is widely used in EDA tools to automate tasks , such as synthesis,placement,routing,timing analysis.
•	-interactive – Instead of running the script non-stop it allow the user to enter additional commands or modify the execution flow integrity.
•	Hence after using this command we get the terminal like below image-

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/0d5e7d2e-d564-49fe-8190-ffef26425a20)

•	Before diving into the synthesis step, we need to execute these two commands:
1.)	package require openlane 0.9: This command ensures that we have the necessary OpenLane tools and libraries installed, specifically version 0.9, which is compatible with our setup.
2.)	prep -design picorv32a: This command prepares the environment for the specific design, picorv32a, ensuring that all required files, configurations, and settings are in place before proceeding further.
Executing these commands ensures that we're set up properly and ready to move forward with the synthesis process.

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/27f53357-3552-4e9c-890b-b90a7d654817)

•	Once these two commands are executed, you'll notice that a directory named "runs" is created. This directory serves as a structured repository where the results of each intermediate step are stored systematically. This organization allows for easy access and management of the synthesis process outputs, facilitating further analysis and debugging as needed.

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/1e825472-b308-4f9d-a571-35b0222c76f2)

•	We are now ready to execute the synthesis and produce a netlist from the design using the command run_synthesis.

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/9cc142e5-15eb-45b0-8f08-33d04d79d100)

### ASSIGNMENT-1
#### We need to find the Flip-flop ratio. But what is FF ratio and what it indicates?
The flip-flop ratio in digital design refers to the proportion of flip-flops (sequential elements) to the total number of logic gates (combinational elements) in a circuit. It signifies the balance between storage elements and logic elements within a design. A higher flip-flop ratio indicates a design with more sequential logic, potentially implying higher power consumption and slower clock speeds, while a lower ratio suggests more combinational logic, which might impact design timing and complexity.
•	In the generated netlist, the D flip-flops are denoted as dfxtp_2 

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/fbff20da-04ad-4f61-a9ee-ae676429460e)

•	Total number of cells are 14876 
•	From the total number of cells there are 1613 numbers of dff.

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/82792bc7-3fa8-4cb5-aad2-88e6e9ed76dd)

•	The calculated ratio based on this is approximately 10.8%, indicating that D flip-flops represent a minority of about 10.8% of the total cells in the design.

# Day 2
# Good Floorplan Vs Bad Floorplan and Introduction to Library cell 
### Introduction to Floorplan: 
Floorplanning is a critical step in VLSI design where the placement of major functional blocks is determined within the chip's layout. It significantly impacts the performance, power consumption, and manufacturability of the chip.
### Good vs. Bad Floorplan: 
A good floorplan optimizes area utilization, minimizes wire lengths, and ensures efficient heat dissipation. In contrast, a bad floorplan leads to wasted space, increased delay due to longer interconnects, and potential thermal issues.

On day 1, we covered the workshop agenda, introduced OpenLane, and discussed the various tools involved. Using the example of the existing design, picorv32a, we generated a netlist through the synthesis step. Now, we need to focus on the floorplanning and placement of the specified design.
Utilization Factor ,Aspect Ratio,De-coupling Capacitor and Power Planning -
So we understood the basic of floorplaning and what are differences between good and bad floorplan. Now we will understand the very essential parameter for floorplaning as given below-
### 1.	Utilization factor 
The core utilization factor in floorplanning is a measure of how efficiently the core area of a chip is utilized. It is calculated as the ratio of the area occupied by the design's core logic to the total core area available. For example, if a design's core logic occupies 80% of the available core area, the core utilization factor would be 0.8 or 80%. A higher utilization factor indicates better utilization of the core area and potentially more efficient chip design
### 2.	Aspect Ratio 
Aspect ratio in chip design refers to the ratio between the width and height of the chip's core area. It is calculated by dividing the width of the core by its height. For example, if a chip's core area is 10mm wide and 5mm high, the aspect ratio would be 2:1. Aspect ratio plays a crucial role in floorplanning and layout optimization, influencing factors such as wire lengths, routing congestion, and overall chip performance
### 3.	Decoupling Capacitor 
A decoupling capacitor is an electronic component used in circuit design to reduce noise and stabilize power supply voltages. It is placed strategically near integrated circuits (ICs) to provide a local energy reservoir, minimizing voltage fluctuations caused by rapid changes in current demand within the ICs.
### 4.	Power Planning
Power planning is a crucial step in chip design that involves ensuring stable and efficient distribution of power throughout the integrated circuit (IC). It includes strategies such as placing power rails, adding decoupling capacitors, and optimizing power grid routing to minimize voltage drops and noise. Effective power planning is essential for maintaining reliable operation and reducing power consumption in IC designs.
### 5.	Pin Placement 
Pin placement is the process of strategically positioning input/output (I/O) pins on a chip's layout to facilitate connectivity with external devices and other components. It involves determining the locations and assignments of pins based on design specifications, signal integrity requirements, and routing considerations. Proper pin placement is critical for ensuring efficient signal routing, minimizing signal delays, and maintaining overall design functionality.
### 6.	Placement Blockages 
Placement blockage refers to designated areas within a chip's layout where certain components or structures are not allowed to be placed. These blockages are defined to ensure proper spacing, avoid interference, or reserve space for specific functions such as routing channels or power distribution. Placement blockages are crucial for maintaining design integrity, preventing signal degradation, and optimizing chip layout for efficient manufacturing processes.
#### Step to run Floorplan Using Openlane – 
•	Before starting floorplanning, we need certain configuration switches or parameters that we can obtain from OpenLane's configuration-

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/aa757ae6-5cc5-4a4b-9f94-fdf2906b6030)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/ca088a29-2079-4e0d-a687-df0e9e040039)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/1063cd5c-898f-4162-989c-0ce09532a783)

•	While the default core utilization ratio is set at 50% and the aspect ratio at 1, these values can be adjusted according to specific requirements. Other parameters can also be modified as needed to meet the given specifications. 
•	We can see this core utilization when we execute the command floorplan.tcl – 

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/4049a680-3d86-4fb8-b7d0-ba53fed03632)

•	After Completion of Synthesis we will our design is ready for floorplan so we will execute the run_synthesis command and it will generate the Power distribution network (PDN).

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/1034b7a7-906c-44be-bdd0-1f1c7ca70589)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/b3c0fe18-47e8-423c-930e-daff760ce597)

•	Now we after synthesis and PDN generation we will see the layout of floorplan in magic tool by using the below command - magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/72402657-bf72-4cb5-9ff3-f41a50ee1fd4)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/34c2218e-e4dc-4203-b04c-2ea047cf0478)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/66ff061e-24ea-4a91-81f9-b8e3350e573d)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/d97ad3b9-2bd5-41c3-82b6-a265fab20f6b)

Placement done in two steps  1st is global and after that detailed.

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/79980f41-306e-4656-a05f-aefdbba42bdc)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/0ef62d71-0877-4675-a915-04cfb28f4922)

•	Now after generating floorplan layout we will generate placement layout in magic tool- magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/8014bf26-0e27-4196-8045-f053b8b04fad)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/d3456429-3eb7-40f2-be5e-92e77c7547d6)

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/b035b49f-31d9-45c4-9ee2-f0444420a352)

# DAY-2 Assignment-1
•	To view the floorplan, we need to examine the results. In the results, there is a DEF (Design Exchange Format) file available. Opening this file provides all the information about the die area, specified as (0 0) to (660685 671405). The unit distance is given in microns (1000), meaning 1 micron equals 1000 database units. Therefore, 660685 and 671405 are in database units. By dividing these values by 1000, we can determine the dimensions of the chip in micrometers

![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/f1970b8a-0aac-40e1-b833-02d1b6bfb35e)

So, the width of chip is 660.685 micrometer and height of the chip is 671.405 micrometer.

# Day-3
# Design Library Using magic layout and Ng spice characterization
## L0 – SPICE DECK Creation for CMOS inverter 
The aim is to create a SPICE (Simulation Program with Integrated Circuit Emphasis) deck for a CMOS circuit that involves defining the circuit components, their interconnections, and the simulation parameters. 

<img width="402" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/bb711dc0-7337-41c6-8d73-d7d54230b9d5">

<img width="399" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/63dc6a5b-f728-46ea-a526-359f57945be0">

## L1 – SPICE SIMULATION LAB FOR CMOS INVERTER
### a.)	When the width of the both n and p mos are same (wp =wn).

<img width="319" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/f9ffaad4-2177-442b-bfbf-8dd0f5106b20">

### b.)	When width of n and p mos are not equal (wp = 2.5*wn) 

<img width="329" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/f9959661-5892-4317-90ea-e0b282eed51d">

RESULTS OBTAINED – 

<img width="231" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/1788fa87-0007-4ac2-84a7-6594e92206bd">

<img width="251" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/07ea1859-cc93-4596-8a65-aec5cde72e43">

## L2 – SWITCHING THRESHOLD Vm
The switching threshold 𝑉𝑚 of a CMOS inverter is the input voltage at which the output voltage is equal to the input voltage. At this point, the inverter is transitioning from one logic level to another (e.g., from high to low or low to high). The switching threshold is an important parameter because it defines the inverter's behaviour in terms of noise margin and signal integrity.

<img width="354" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/39169eb7-3f22-40a2-8c52-ace91ee3a444">

<img width="357" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/70beec04-d63d-4dc9-ba3c-9bf9c1bcf720">

## L3 – Static and Dynamic simulation of CMOS inverter 

<img width="382" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/4a9d5ad4-a620-43d3-93fe-22412ee75216">

## L4 – LAB STEPS TO GIT CLONE vsdstdcelldesign
### 1.	Clone a custom inverter standard cell design from a GitHub repository.
#### Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane
#### Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign
#### Change into repository directory
cd vsdstdcelldesign
#### Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .
#### Check contents whether everything is present
Ls -ltr
#### Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

<img width="366" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/44e111d6-9412-4b97-98c2-5a5416fdc267">

### 2. Now we will load inverter layout in magic tool 

<img width="388" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/05739bfb-7d69-47af-b6fa-e6b02d41c946">

<img width="398" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/a95fd1da-077a-45b9-a9c4-b491cc966128">

### 3.	SPICE extraction of an inverter using the Magic tool involves generating a SPICE netlist from the layout. (#as shown in the above fig)
#### Check current directory 
pwd 
#### Extraction command to extract to .ext format
extract all
#### Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0
#### Converting to ext to spice
ext2spice
#### Here we used vim command to edit SPICE file

<img width="433" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/4da1fa2b-5b8a-465b-8fd7-dc5b8442f3f7">

### 4.	Post-layout ngspice simulations.
Here are the given commands to perform ngspice simulations
#### Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice
 
#### Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a

<img width="374" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/53b1910c-1aae-4cbd-8510-87dc5243702f">

<img width="368" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/34017336-b3a3-4f06-b762-1538e6af6e77">

Here I have given the screenshot of generated plot of O/P (a) vs O/P(y) - 

<img width="376" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/650cc103-f01e-40dd-9b97-24669eeeb472">

## ASSIGNMENT -1
After getting plot we have to find out the value of 4 – parameter –
1.	Rise Transition time. 
2.	Fall Transition time.  
3.	Fall cell delay. 
4.	Rise cell delay.

First let’s understand what are those delay means - 
1.	Rise Transition time - Rise transition time is the time it takes for a signal to transition from a low voltage level (typically 20% of the maximum value) to a high voltage level (typically 80% of the maximum value). It is a critical parameter in evaluating the speed and performance of digital circuits.
2.	Fall Transition time - Fall transition time is the duration for a signal to change from a high voltage level (typically 80% of the maximum value) to a low voltage level (typically 20% of the maximum value). It is crucial for assessing the speed and performance of digital circuits.
3.	Fall cell delay – Fall cell delay is the time it takes for a cell's output to transition from a high voltage level to a low voltage level after the input signal triggers the change.
4.	Rise cell delay - Fall cell delay is the time interval between the input signal reaching a defined threshold and the output signal falling from a high to a low voltage level.

<img width="418" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/c010bbbb-047c-4ad6-866f-89261665454a">

Inside the box we have desired values from the plot now we can calculate the delays – 
X0 = 2.19884e-09   Y0 = 0.702651        X0’ = 2.31586e-09        Y0’ = 2.80043 
Rise Transition time(tr) = (X0’-X0)                   tr = 0.117 ns  
X0 = 4.05931e-09   Y0 = 2.80024           X0’ = 4.10707e-09      Y0’ = 0.700482 
 Fall Transition time(tr) = (X0’-X0)                   tr = 0.0477 ns
X0 = 2.14667e-09    Y0 = 1.7512         X0’ = 2.24138       Y0’ = 1.7504
Rise cell delay (trc) = (X0’-X0)                   trc = 0.09471 ns
X0 = 4.05264e-09    Y0 =   1.74977                            X0’ = 4.08713e-09      Y0’  = 1.75023
fall cell delay (tfc) = (X0’-X0)                   tfc = 0.035 ns

5.	Identify issues in the Design Rule Check (DRC) section of the old Magic Tech file for the SkyWater process and correct them.
Here are the following commands mentioned to download and view the corrupted skywater magic tech file – 
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

<img width="530" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/ee8acaa2-9a5e-4ba1-9a67-5831127269e0">

.magicrc file

<img width="527" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/0c1f4b49-61ac-46dd-a82f-8b77b656f44f">

open met3.mag file in magic tool as shown in below fig - 

<img width="432" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/84e1ef3c-a387-4960-8a04-87bc7e6274c2">

Different Layout and Different DRC as shown in below fig – 

<img width="399" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/e90fa383-668a-4124-b07a-5693a2ce03c2">

DRC for selected layout area - 

<img width="385" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/59d045b0-f286-4dcd-8080-9e914b4f5e84">

VIA2 file - 

<img width="398" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/49fc3eac-ef6b-498e-a4a3-2ad170d56223">

Screenshot of poly rules and link is given below - 
https://skywater- pdk.readthedocs.io/en/main/rules/periphery.html#poly

<img width="313" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/800e0178-e8fe-4ade-8772-b5e269a7e9ef">

The difftap.2 rule is incorrectly implemented, resulting in no DRC violation even when the spacing is less than 0.42µm.

<img width="338" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/66f1a797-5364-4a20-af80-023631dd1578">

To update DRC new command is inserted using vim in sky130A.tech

<img width="367" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/2a8e6882-6d47-430b-850b-13d961a6e6cb">

#### Loading updated tech file
tech load sky130A.tech
#### Must re-run drc check to see updated drc errors
drc check
#### Selecting region displaying the new errors and getting the error messages 
drc why

<img width="355" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/5bb45ec2-02d8-4430-9ac2-19366d535fd2">

<img width="368" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/92120127-1c05-43db-83ab-b9d8857636f7">

Incorrectly implemented nwell.4 complex rule correction – 
These are the following nwell rule -

<img width="341" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/b24b2dcc-c5f2-4d4c-b225-033ed1f45386">

Incorrectly implemented nwell.4 rule no drc violation even though no tap present in nwell – 

<img width="323" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/d2419445-402d-4a7e-a5c9-4acb58a37342">

To update DRC new command is inserted in sky130A.tech file 

<img width="376" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/6a6d9314-9e52-4a78-9065-1cd5303b029c">

<img width="386" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/1c829f11-97bf-4e72-ad9a-1f24e9c4aab4">

Command to run in magic tkcon window – 
#Loading updated tech file 
tech load sky130A.tech
#change drc style
drc style drc(full)
#check drc 
drc check
#See errors in selecting area 
drc why

<img width="372" alt="image" src="https://github.com/ravinder61997/vsd_workshop/assets/170663775/692ed706-7855-4209-a7c3-5b87cde7e8f3">























































