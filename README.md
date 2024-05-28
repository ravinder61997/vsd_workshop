# VSD Digital VLSI SoC Design and Planning
# DAY-1 
The introductory workshop on Day 1 provided a comprehensive overview of the RTL to GDSII flow, elucidating the seamless transformation of Verilog code into physical design. Participants gained insights into the fundamental principles underlying the RISC-V processor architecture, and how these concepts translate into layout design. Crucially, the session delved into the intricate relationship between software applications and hardware, elucidating the pivotal role of compilers in bridging these domains. Additionally, attendees were introduced to the concept of Process Design Kits (PDKs), further enhancing their understanding of the integrated circuit design process.
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


























