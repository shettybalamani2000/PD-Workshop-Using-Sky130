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

























