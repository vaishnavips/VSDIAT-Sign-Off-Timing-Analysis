# VSD-IAT: Sign-off Timing Analysis - workshop report


## Static Timing Analysis (STA):

Static Timing Analysis (STA) is a method used in digital circuit design to analyze and verify the timing performance of a digital design. STA checks that a design meets its timing requirements, ensuring that signals arrive at their intended destinations at the correct time, without any timing violations.

STA is performed by using a detailed digital circuit model and simulating its behavior to calculate the worst-case delay through the circuit. This delay calculation takes into account the various sources of delay, such as gate delays, interconnect delays, and clock skew.

STA is critical in the design process to ensure that the digital circuits operate correctly and meet their performance specifications. It is typically performed multiple times during the design cycle to ensure that the design meets its timing requirements at all stages of the design process.


## Contents

* Day 1  
* Day 2
* Day 3
* Day 4
* Day 5
* Acknowledgements


## Day 1


Summary:

OpenSTA:

OpenSTA is an open-source Static Timing Analysis (STA) tool that is widely used in digital circuit design. It provides an efficient and accurate way to analyze the timing behavior of digital circuits, including delay calculations, timing constraints, and report generation. It has a wide range of features that allow for detailed analysis of digital circuits. It supports both pre-layout and post-layout timing analysis and can be used with a variety of digital circuit formats. It also supports a variety of timing constraints formats, including SDC and SPEF.
Overall, OpenSTA is a powerful tool that provides designers with a comprehensive way to analyze and optimize the timing performance of digital circuits. Its open-source nature makes it a cost-effective option for both small and large design teams.

As a stand-alone executable it can be used to verify the timing of a design using standard file formats.

*	Verilog netlist
*	Liberty library
*	SDC timing constraints
*	SDF delay annotation
*	SPEF parasitics

OpenSTA uses a TCL command interpreter to read the design, specify timing constraints and print timing reports.


Lab:

simple.v - Design in Verilog format.
![day 1 simple v ](https://user-images.githubusercontent.com/37980845/220631092-340a2f85-15b9-4714-96d8-da20041cb9d2.png)

Design constraints file with clock, input delay, input rise and fall transition delay, load and output delays defined.
![day 1 simple sdc](https://user-images.githubusercontent.com/37980845/220632169-5ecc3abe-25d1-4b03-9def-ecf9873e61d5.png)

Run script run.tcl

![day 1 run tcl](https://user-images.githubusercontent.com/37980845/220633120-ffdd90f0-c9f1-4668-b87d-1653efe0dbb6.png)

After execution: 
![day 1 output 1](https://user-images.githubusercontent.com/37980845/220634625-e5a4b5bb-f569-44c5-b281-e030cf24b6d0.png)

Delays, time instant, slack calculation can be observed in the execution result displayed.
Slack violation:
![day 1 output 2](https://user-images.githubusercontent.com/37980845/220635307-781b7a9c-abe8-4dac-99df-3f74a8140c80.png)

Slack conditions satisfied:
![day 1 output 3](https://user-images.githubusercontent.com/37980845/220635432-f2aff203-b746-4ec1-ad13-ae77793db77e.png)


## Day 2


Summary:

Overview of clock gating checks, Asynchronous pin related checks, Data to Data check, design rule check, latch based timing and STA text reports.


Lab:

Exercises: 

- To find all the cells in simple_max.lib: 211 cells

![day 2 ex 1 part 1](https://user-images.githubusercontent.com/37980845/220643334-c77e09f3-910f-4b1d-ab8e-e85b6e24dfcd.png) ![day 2 ex 1 part 2](https://user-images.githubusercontent.com/37980845/220643394-3f0ff764-3129-471b-987f-86ebac2aff27.png) ![day 2 ex 1 part 3](https://user-images.githubusercontent.com/37980845/220643427-43cc8352-41d1-4723-b492-1a2bb261d658.png) ![day 2 ex 1 part 4](https://user-images.githubusercontent.com/37980845/220643477-c0c7b63c-a102-483c-b962-cf66610a0d32.png) ![day 2 ex 1 part 5](https://user-images.githubusercontent.com/37980845/220643584-93a56456-0b9e-416a-84f9-b3fc2be2b0e1.png) ![day 2 ex 1 part 6](https://user-images.githubusercontent.com/37980845/220643634-7ba385da-10c5-4254-afff-7bb3fccea18e.png) ![day 2 ex 1 part 7](https://user-images.githubusercontent.com/37980845/220643709-193c7a72-727b-46ee-9818-d464d60346cd.png)

- To find all the pins of NAND2_X1 in simple_max.lib: 2 input pins a and b, output pin o

![day 2 ex 2 part 1](https://user-images.githubusercontent.com/37980845/220644729-f0f300d4-8c72-4686-94a0-2fadbaf52dd0.png) ![day 2 ex 2 part 2](https://user-images.githubusercontent.com/37980845/220644853-4bfe1404-8f08-42f3-9539-a9d710c475f9.png)

- Difference between NAND2_X1 and NAND3_X1: From the NAND2_X1 image above and NAND3_X1 image below, the differences are: NAND2_X1 is 2 input nand, NAND3_X1 is 3 input nand and the capacitances on the pins are different for both the gates.

![day 2 nand diff actual 1](https://user-images.githubusercontent.com/37980845/220645517-1d5bdabe-3947-418b-a480-13946ab2e046.png) ![day 2 nand diff actual 2](https://user-images.githubusercontent.com/37980845/220645563-8df4013f-e62c-48aa-b1ca-2c31b8c53e58.png)

When executed, the timing report shows the input (external) delays,  timing values referred from liberty files, and indicates the path type (max indicates setup analysis), the rise and fall edges.

![day 2 run log study](https://user-images.githubusercontent.com/37980845/220648694-a9d4af8a-d791-4898-ba51-fb0e81e2aa03.png)

SPEF (Standard Parasitic Exchange Format) file:

![day 2 spef file](https://user-images.githubusercontent.com/37980845/220650354-9fd70c02-bbee-4ff8-95fe-277dcc915447.png)

It is automatically generated by the tool and describes the parasitic information of the design. It is mainly used to pass parasitic information from one tool to another.

A SPEF file has 4 main sections:
* Header
* Name Map
* Top Level Ports
* Parasitic description

read_spef is the command for SPEF parsing.


## Day 3


Summary: 

Understanding slack calculation, multiple clocks, timing arcs and timing sense, cell delays and clock network.


Lab:

![day 3 design considered](https://user-images.githubusercontent.com/37980845/220658198-d42131b1-c5d2-490f-95d7-451f559eaef6.png)
 
In the above block, the following are some paths between F1 and F2.

* F1:CK→U3→U4→U6:A2→U7:A1→F2:D
* F1:CK→U6→U4→U5:A1→U7:A2→F2:D
* F1:CK→U6:A1→U7:A1→F2:D
* F1:CK→U6→U5:A2→U7:A2→F2:D

The following are the run script for slack computation (report_checks -from F1/CK) and the report generated after execution:

![day 3 from f1 ck](https://user-images.githubusercontent.com/37980845/220694677-bcc06a4a-e37b-4029-b4fb-bcb573be6364.png)

![day 3 slack violation snap](https://user-images.githubusercontent.com/37980845/220695138-eaa935fe-9edc-4444-a94e-b3f277c181c8.png)


The following report is for endpoint_count 5:

![image](https://user-images.githubusercontent.com/37980845/220662216-badd4526-da9e-45ae-8fca-8c02b537d20d.png)

![image](https://user-images.githubusercontent.com/37980845/220662303-4a1e0bf0-458b-45dd-b1e0-88137c55e4a0.png)

![image](https://user-images.githubusercontent.com/37980845/220662361-96e5f986-2b46-48d6-89c5-d450cac26ead.png)



![image](https://user-images.githubusercontent.com/37980845/220689302-e8b5195a-15cc-44b8-877a-209c5810159b.png)
The following report is for endpoint_count 100:

![image](https://user-images.githubusercontent.com/37980845/220686122-a5c46d66-0895-4b9b-96f4-d6bb7e1f81d0.png)

![image](https://user-images.githubusercontent.com/37980845/220687240-612e471b-425b-4c9a-905f-d0029677c873.png)

![image](https://user-images.githubusercontent.com/37980845/220687838-45b53d8a-15ad-4d1e-bb2f-caeb57d2f2c9.png)

![image](https://user-images.githubusercontent.com/37980845/220689014-21cc6213-f9c9-4b31-a684-85f0ddb3b9bd.png)


## Day 4


Summary: Crosstalk and noise, operating modes and other variations, clock gating checks and checks on async pins.


Lab:

Clock gating checks:
![day 4 clock gating check verilog file](https://user-images.githubusercontent.com/37980845/220696167-be7dd31b-db70-4a02-a0f3-b4a0884bebac.png)
Report generated when executed:

![image](https://user-images.githubusercontent.com/37980845/220696697-4430514d-52f3-4337-b7ec-824ac3d735e5.png)
![image](https://user-images.githubusercontent.com/37980845/220696748-58dc0ea4-860a-4818-a0bf-70b3609da86f.png)
![day 4 clock gating check output 3](https://user-images.githubusercontent.com/37980845/220696847-d9245ce4-e2bd-4c71-a24d-5cbba12746eb.png)


Async pin checks:
![day 4 slack met verilog file](https://user-images.githubusercontent.com/37980845/220699196-540e22e0-6f9f-4a8b-af33-395078fde71f.png)
Report generated when executed:

![day 4 slack met op 1](https://user-images.githubusercontent.com/37980845/220699300-09746741-93e7-40e5-989e-e50f7330ef18.png)


## Day 5


Summary: Clock groups, clock properties, timing exceptions, and multiple modes.


Lab:

Common Path Pessimism Removal(CPPR):

CPPR is used to eliminate this pessimism by identifying and removing the common path(s) in the circuit. This is achieved by creating a new circuit model that replaces the common path(s) with a single shared delay element. The worst-case delay is then calculated using this new model, which provides a more accurate and less pessimistic estimate.

![image](https://user-images.githubusercontent.com/37980845/220701623-63615302-40be-4b08-8e4b-513f49d4b3a3.png)

Report generated before enabling CPPR:
![day 5 cppr 1](https://user-images.githubusercontent.com/37980845/220703527-fa8b36d6-463f-41b4-af7f-8c9334b512e0.png)

Enabling CPPR will considerably improve the slack, as below:
![day 5 runtcl crpr enabled](https://user-images.githubusercontent.com/37980845/220704177-1ef422e6-9fc0-471a-8e23-cba1b24226ae.png)

Report generated after enabling CPPR:
![day 5 cppr enabled output](https://user-images.githubusercontent.com/37980845/220704352-83bf4e94-bd5b-405b-9024-060b5ddcc4cd.png)

Engineering Change Order (ECO):

In the ECO cycle, we perform various analysis one by one for every check which we need to close but not closed till PnR stage. There are specialized signoff tools that help us to analyze the issue and also suggest the changes we need to do in order to close the issue. The suggested change is captured in an eco file. In this lab we will focus on ECO for timing purposes, this is done to fix setup and hold violations. 

![image](https://user-images.githubusercontent.com/37980845/220709409-e9c67de5-0d00-41e6-8ba7-d8eb9eaae3a7.png)

Slack computed after ECO insertion:
![day 5 runtcl op -1](https://user-images.githubusercontent.com/37980845/220712637-a58af1c0-22f3-4fb2-8ab4-a7b2e10d0b68.png)

The differences between s27.v and s27_eco.v:
s27.v:

![day 5 s27 v](https://user-images.githubusercontent.com/37980845/220717385-3110c64c-9129-497d-a78a-40381ca43cf5.png)

s27_eco.v:

![day 5 s27 eco v](https://user-images.githubusercontent.com/37980845/220717426-0127ff9b-c57c-4dde-a20b-060b9311d3f0.png)


# Acknowledgements

  * Kunal Ghosh, Co-founder of VLSI System Design (VSD) Corp. Pvt. Ltd.
  * Vikas Sachdeva, Advisor, Tech and VLSI Coach, Trainer and Innovator at vlsideepdive.


## Resources

- https://github.com/vikkisachdeva/openSTA_sta_workshop/tree/master/vlsideepdive_openSTA_labs
- https://github.com/The-OpenROAD-Project/OpenSTA
- https://www.vlsisystemdesign.com/spef-format-part-1/


