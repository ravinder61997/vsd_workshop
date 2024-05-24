# vsd_workshop
This repositry contains the complete flow of RTL to GDSII.
The introductory workshop on Day 1 provided a comprehensive overview of the RTL to GDSII flow, elucidating the seamless transformation of Verilog code into physical design. Participants gained insights into the fundamental principles underlying the RISC-V processor architecture, and how these concepts translate into layout design. Crucially, the session delved into the intricate relationship between software applications and hardware, elucidating the pivotal role of compilers in bridging these domains. Additionally, attendees were introduced to the concept of Process Design Kits (PDKs), further enhancing their understanding of the integrated circuit design process.
OPENLANE in Terminal 
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
ASSIGNMENT-1
	We need to find the Flip-flop ratio. But what is FF ratio and what it indicates?
The flip-flop ratio in digital design refers to the proportion of flip-flops (sequential elements) to the total number of logic gates (combinational elements) in a circuit. It signifies the balance between storage elements and logic elements within a design. A higher flip-flop ratio indicates a design with more sequential logic, potentially implying higher power consumption and slower clock speeds, while a lower ratio suggests more combinational logic, which might impact design timing and complexity.
•	In the generated netlist, the D flip-flops are denoted as dfxtp_2 
![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/fbff20da-04ad-4f61-a9ee-ae676429460e)
•	Total number of cells are 14876 
•	From the total number of cells there are 1613 numbers of dff.
![image](https://github.com/ravinder61997/vsd_workshop/assets/170663775/82792bc7-3fa8-4cb5-aad2-88e6e9ed76dd)
•	The calculated ratio based on this is approximately 10.8%, indicating that D flip-flops represent a minority of about 10.8% of the total cells in the design.









