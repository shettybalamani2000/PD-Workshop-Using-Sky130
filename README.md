# PD-Workshop-Using-Sky130
It’s a 5-day workshop of 5days on system on chip Design planning in OpenLANE flow using Google-skywater 130nm PDK.

# DAY-1
Started with open source EDA, OpenLANE directory structure and sky130
![image](https://user-images.githubusercontent.com/110526797/183294393-9e7b768e-823b-41b4-b7c1-ee2438d06a27.png)
![image](https://user-images.githubusercontent.com/110526797/183294420-0819398a-aaa2-4807-8eea-528a231601d5.png)

## Started with OpenLANE
Openlane consists of many stages 
1.Synthesis
  i.	yosys - Performs RTL synthesis
 ii.	abc - Performs technology mapping
iii.	OpenSTA - Performs static timing analysis on the resulting netlist to generate timing reports
2.	Floorplan and PDN
  i.	init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
 ii.	ioplacer - Places the macro input and output ports
iii.	pdn - Generates the power distribution network
 iv.	tapcell - Inserts welltap and decap cells in the floorplan
3.	Placement
  i.	RePLace - Performs global placement
 ii.	Resizer - Performs optional optimizations on the design
iii.	OpenPhySyn - Performs timing optimizations on the design
 iv.	OpenDP - Perfroms detailed placement to legalize the globally placed components
4.	CTS
  i.	TritonCTS - Synthesizes the clock distribution network (the clock tree)
5.	Routing *
  i.	FastRoute - Performs global routing to generate a guide file for the detailed router
 ii.	TritonRoute - Performs detailed routing
iii.	SPEF-Extractor - Performs SPEF extraction
6.	GDSII Generation
 i.	Magic - Streams out the final GDSII layout file from the routed def
7.	Checks
 i.	Magic - Performs DRC Checks & Antenna Checks
ii.	Netgen - Performs LVS Checks

## Initialising openlane
docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) openlane:rc6/openlane$docker
bash-4.2$ ./fow.tcl -interactive
%package require openlane 0.9
%prep -design picorv32a
![image](https://user-images.githubusercontent.com/110526797/183294618-df1dcabf-c8e0-47fa-9556-004093779d7e.png)
![image](https://user-images.githubusercontent.com/110526797/183294649-948f04aa-73c2-4fc9-bf46-f53f3cda3bdf.png)
![image](https://user-images.githubusercontent.com/110526797/183294664-db2b867a-1611-4183-9155-aedc6c889fc5.png)

## RUN SYNTHESIS
![image](https://user-images.githubusercontent.com/110526797/183294745-5357e0b3-6f5f-453a-943c-0fcc9fe6b4c8.png)

FLOP and BUFFER RATIO
![image](https://user-images.githubusercontent.com/110526797/183294786-5b956d13-69b2-4b25-8e43-a78f79407d25.png)
![image](https://user-images.githubusercontent.com/110526797/183294811-571de367-edd9-4dee-bfcc-7003ddbab838.png)
![image](https://user-images.githubusercontent.com/110526797/183294820-f3bf6826-2e0a-46b3-8f6f-77e2d39ac938.png)
Number of cells - 14876
Total Number of flops - 1613
Buffer count - 1656
Flop Ratio = Total Number of flops/ Number of cells =0.1084
Buffer count = No. of buffer/Number of cell = 0.1113

# DAY-2
## Introduction to floorplan and Review of floorplan layout in magic

![image](https://user-images.githubusercontent.com/110526797/183347310-96eca878-04a8-492f-8afa-787d8f21ce44.png)

Floorplan Description
![image](https://user-images.githubusercontent.com/110526797/183347428-639fca24-03d3-4a5b-bf1b-4871563326c7.png)
Floorplanning in OpenLANE is done using the following command.
 Command: run_floorplan
![image](https://user-images.githubusercontent.com/110526797/183347520-84b67848-d3c2-4846-8d41-82d779e5ff0b.png)
## Review of floorplan layout in magic
![image](https://user-images.githubusercontent.com/110526797/183347641-686df63f-b017-4240-b2b7-438085e997ab.png)
![image](https://user-images.githubusercontent.com/110526797/183347701-06ec5b96-f0d3-4005-a4cf-ea584a724ed3.png)
## Placement
Placement in OpenLANE is done using the following command.
Command: run_placement
The DEF file created during floorplan is used as an input to placement. Placement in OpenLANE occurs in two stages:
•	Global Placement
•	Detailed Placement
![image](https://user-images.githubusercontent.com/110526797/183347845-44e082e4-b5ed-4687-bda7-ad08171d4d0c.png)
![image](https://user-images.githubusercontent.com/110526797/183347929-65772834-e95a-4723-8438-3d1e0b2b225a.png)
# DAY-3
Designing library cell using magic layout, Spice Deck and ngspice characterization
## •	First step to git clone vsdstdcelldesign
     Link:  git clone https://github.com/nickson-jose/vsdstdcelldesign.gi
![image](https://user-images.githubusercontent.com/110526797/183348022-a377b5a6-7e56-4a51-8400-8dec8f2009be.png)
•	Sky130 layer layout of cmos inverter  in magic
![image](https://user-images.githubusercontent.com/110526797/183348092-81be3781-3deb-4d75-92b3-e73fe728f9de.png)
![image](https://user-images.githubusercontent.com/110526797/183348139-f91370c5-e32e-4c77-a77a-a69c3526f858.png)
![image](https://user-images.githubusercontent.com/110526797/183348177-a586ed92-f8f1-42e0-baee-d983e61d5ee8.png)
![image](https://user-images.githubusercontent.com/110526797/183348206-6f00d481-51ef-4dfd-a72d-372bc47cf38f.png)
## •	Extract SPICE Netlist from Standard Cell Layout
1.	Extract the circuit from the layout design.
Command: extract all
2.	Convert the extracted circuit to SPICE model.
Command: ext2spice cthresh 0 rthresh 0
         ext2spice
![image](https://user-images.githubusercontent.com/110526797/183348445-3f5c7dbb-aedd-446c-a74c-cdc1d1b02e6f.png)
![image](https://user-images.githubusercontent.com/110526797/183348479-4d1eada8-a590-43d3-89eb-18e88e379cbb.png)
###  Spice file created
![image](https://user-images.githubusercontent.com/110526797/183348572-0025d9b5-a2d5-4bc5-afec-b23730476447.png)
## Transient Analysis using ngspice
The SPICE netlist generated in previous step is simulated using the NGSPICE tool
Command to invoke ngspice tool:  ngspice <name-of-SPICE-netlist-file>
                       
### To plot waveform:  ngspice 1 -> plot Y vs time A
 ![image](https://user-images.githubusercontent.com/110526797/183348765-adf31691-5bf2-46f3-83d3-ab6964f9b48d.png)
 ![image](https://user-images.githubusercontent.com/110526797/183348793-fcd61061-83f9-4452-9f48-70d5f68ec6a2.png)


# DAY4
## Pre layout Timing Analysis 
Visit the vsdstdcelldesign directory and run magic tool for inverter
•	Check Grid Alignment
The inverter cell is laid out a grid that must match the pitch and offset at …./openlane/sky130_fd_sc_hd/tracks.info
This file contains the information of layer name and its dimensions, offset and pitch.
  ![image](https://user-images.githubusercontent.com/110526797/183348932-069787a8-3e2f-4d90-b880-dc1f2eed7e48.png)

•	Allignment of cell elements with the grid
![image](https://user-images.githubusercontent.com/110526797/183348998-3249e59d-6e25-492d-9d32-30a2869983ad.png)
![image](https://user-images.githubusercontent.com/110526797/183349047-8e74f466-109f-46fb-a04b-64d52e61a643.png)
•	LEF file Generation
![image](https://user-images.githubusercontent.com/110526797/183349125-27255a61-1847-45d9-a600-45304d4a270b.png)

•	To generate LEF file 
Command: lef_write
•	Save the LEF file in sky130_vsdinv.lef
![image](https://user-images.githubusercontent.com/110526797/183349186-e4b53404-edca-4be3-ad83-7f8ae115fb6d.png)
![image](https://user-images.githubusercontent.com/110526797/183349214-cd12129e-d024-4ab3-aed0-ee3b4ae23cc0.png)
•	Pshort model file
 ![image](https://user-images.githubusercontent.com/110526797/183349485-5eaff574-1af3-4f58-bd5c-1ed929bdfb6b.png)
 ## vim my_base.sdc file
  ![Screenshot (161)](https://user-images.githubusercontent.com/110526797/183349451-9794a4ae-9c8f-41e2-93f1-f0f33ad30c3c.png)
## Timing Violation Reduction
  The input capacitance of the sky130_fd_sc_hd__inv_8 is 17.65 pF and this value is used in my_base.sdc file for the load capacitance.To reduce timing violations
 ![Screenshot (163)](ht![image](https://user-images.githubusercontent.com/110526797/183350502-1d9aa219-1f52-4935-a3b9-5ec9c2e32109.png)
  #### pre_sta.conf
tps://user-images.githubusercontent.com/110526797/183350364-dabe51fe-43b3-489d-a34e-2c20e22bf4f6.png)
#### my_base.sdc
  ![image](https://user-images.githubusercontent.com/110526797/183350708-dde5313b-8ce2-4161-b807-b639846d2434.png)
### config.tcl file
 ![image](https://user-images.githubusercontent.com/110526797/183350861-e60d6fca-e9cf-427c-b8eb-56e230ba39e6.png)
### synthesis file
  ![image](https://user-images.githubusercontent.com/110526797/183350919-95adb33a-3928-4960-a98c-8a614d2aba99.png)
### static timing analysis
  ![image](https://user-images.githubusercontent.com/110526797/183351031-215e93a5-06c9-4beb-a317-6334899fc55a.png)
### Initial floorplan
 ![image](https://user-images.githubusercontent.com/110526797/183351126-e177745a-3e3a-45d4-95e7-538544621eff.png)
### Initial placement
  ![image](https://user-images.githubusercontent.com/110526797/183351272-2a42b236-bdce-47fd-9134-e6f30592a6d4.png)
### Global placement
  ![image](https://user-images.githubusercontent.com/110526797/183351338-4cf7a277-dd91-46eb-bc5e-80c4054b2f56.png)
### PDN file
  ![image](https://user-images.githubusercontent.com/110526797/183351396-e1fc9c2f-a8dc-4e2f-8bfe-a1e3ed61bd7d.png)
# DAY-5 
Power Distribution Network
•	The gen_pdn command was used to generate the pdn file
### Routing
  ![image](https://user-images.githubusercontent.com/110526797/183351531-99857e60-35b5-480d-bace-7fd7ba815f94.png)

  
  




















