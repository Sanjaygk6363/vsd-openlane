# Digital-Soc-Design

# Day 1
## The courses structure

![The courses structure](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(74).png)

->RTL Synthesis:
           RTL synthesis involves converting a hardware description language (HDL), such as Verilog or VHDL, into a gate-level representation. This representation comprises flip-flops, standard cells, and interconnected logic gates sourced from a technology library. Synthesis is typically performed using tools like Yosys, with technology mapping accomplished post-synthesis using tools like abc.

->Floorplanning :
                 It involves arranging components in a chip to meet design goals like performance and area utilization. It minimizes wire lengths and signal delays while optimizing power distribution. There are two types: chip-level, which organizes overall components, and macro-level, which details specific blocks. Tools like OpenROAD are used for floorplanning.

->Placement:
          Determining optimal component locations for performance, power efficiency, and area utilization. OpenROAD used for Global and Detailed Placement.

->Clock Tree Synthesis:
              Efficient distribution of clock signal with minimal skew, jitter, and power consumption. Done before signal routing using OpenROAD.

->Routing:
Establishing physical connections between components using available metal layers. The router leverages specifications from the Process Design Kit (PDK), which defines parameters like thickness and pitch for each metal layer. Sky-130 PDK defines six routing tiers.

------------------------------------------------------------------------------------------------------------------------------
## Labs: Introduction about the Openlane and its commands

![introduction also](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(77).png)

## commands to enter Directory:
```bash
  cd Desktop
  cd work/tools
  cd openlane_working_dir
  cd openlane
```
## After getting into the directory, enter the commands
```bash
  docker
  pwd
  ls -ltr
```
![open lane](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(79).png)
--------------------------------------------------------------------------------------------------------------------
## To open the Openlane in interactive mode,
, 
```bash
 ./flow.tcl -interactive
```
To prepare the openlane,

```bash
  package require openlane 0.9
  prep - design picorv32a
```
![intera ctive](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(82).png)
-------------------------------------------------------------------------------------------------------------------------
## Final result Synthesis
To run the Synthesis
```bash
 run_synthesis
```
![synt hessis](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(83).png)


-> This contains all the details about the synthesis of the picorv32a 
------------------------------------------------------------------------------------------------------------------
- Number of cells: 14876
![cell no](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(83).png)
-----------------------------------------------------------------------------------------------------------------
- Number of FF: 1613
  ![flip flop](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(84).png)
---------------------------------------------------------------------------------------------------------------------------
 - The Chip Area of the module 147712.918400
![chip area](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(85).png)

------------------------------------------------------------------------------------------------------------------------------------------

AS for the Assignment to find the Flop ratio. This can be calculated by using the formula:

                     Flop ratio in (%) = Total No of D-FF
                                        --------------------  X 100
                                        Total No of Cells

                                              =   1613
                                                   --------   X 100
                                                   14876 

                               Flop ratio = 10.8429685

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
-----------------------------------------------------------------------------------------------------------------------------
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# Day 2

## Floorplanning
The 2nd day of the lab gives the complete flow of the Floorplanning and the placement process

In first we study about Optimise placement
![theory place](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(97).png)

and then the cell design flow

![cell design](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(101).png)


After the Synthesis process, type the command for running the Floor planning
![floorplan steps](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-01%2018-48-03.png)


To run floorplan
```bash
  run_floorplan
```
we will be getting a window like this
![floorplan_success](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-02%2022-04-40.png)

In this  location we can se the  floorplan.def file, we can able to see the area of the chip
![area](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-02%2022-04-40.png)


             1000 unit distance = 1 Micron

             Distance in micron =   value
                                  --------
                                   1000

            Die width in micron = 660685 
                                 ---------
                                   1000
                                
           Die height in micron =  671405 
                                  ---------
                                    1000

          Area of die in micron = 660.685*671.405 Square micron 

Open this directory to initiate the Magic Tool
![magic location]()


```bash
 magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
- Floorplan def in Magic
![magic opening]()



- Horizontal metal layer
![horizontal metal layer]()


- Vertical metal layer
![vertical metal layer](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/dc0da0f0-9cd7-49a5-a5a7-9dbcf22a91df)

- Standard cells
![standard cells](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/f388ecb6-ed25-4814-bc2e-37fe628ad201)

## Placement
To run the Placement, the command is
![run placement](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/1c2cf0a3-7b9d-4f59-9ad0-2eea22a6f466)

```bash
    run_placement
```
Commands to load placement def in magic
![placement location](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/433d133e-f0a8-45f9-8a95-eaaf79077762)

```bash
    magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
- Floorplan def in magic

![placement chip](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/2b8c7816-ecd2-4977-b9ab-3d4d27b021b2)

- Standard cell placement

![placement of standard cells](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/34c89e7c-60b0-4c62-a0c2-239ab8587e28)


# Day 3
The LAB for the day  gives the complete flow of the Inverter simulation using ngspice and Magic EDA tool

![git clone location](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/6792b4a2-e297-45b9-a673-0d898124685c)

Go to this directory to git clone the files
```bash
  /Desktop/work/tools/openlane_working_dir/openlane
```
Git clone the files from GitHub to your local pc
```bash
  git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```
![sky130 tech file](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/4970aa6b-c2e3-4a31-900d-8f7c3208640f)

open another terminal and go to the location
```bash
  /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic
```
copy the sky130A.tech file from this location to the git cloned location.
![copying tech files in git cloned file](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/220b4d3a-5c6e-482c-a01c-d602feefb34a)

Now initialize magic
```bash
  magic -T sky130A.tech sky130_inv.mag &
```
![initilaize magic](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/8651d7dc-79e8-4b83-8a33-c3ab7830925d)

- Inverter layout
 ![inverter layput](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/9c557272-c921-4aa6-a571-e06a8518016b)

- Nmos
 ![nmos](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/eae48418-76e1-4bad-9503-e715c1ccb326)

- Pmos
 ![pmod](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/3589c4e0-652b-4316-bae6-0012c5f30182)

- Connection between source and VDD in Pmos
 ![connection bw source and vdd](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/d52e1dcf-60a7-4994-9096-aa85b1b95d26)

- Connection between source and Ground in Nmos
 ![connection bw source and gnd in nmos](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/5d0a5d5b-f046-4ce0-b15a-2055898d4fe1)


Now open the tkcon window and type the commands for extracting the files
![extracting the file](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/753033b6-71f4-45ff-b6de-4990413618a3)
```bash
  pwd
  extract all
```
![extraction to spice](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/720f58de-86db-4785-afc6-0671fdcc5491)

```bash
  ext2spice cthresh 0 rthresh 0
  ext2spice  
```

![extraction spice file](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/f351c273-337c-401b-b5b8-b67783347268)

## Spice Simulation
Now in the git cloned location, we can able to see the sky130_inv.spice file

To install ngspice, use the commands in the terminal

```bash
  sudo apt -y install ngspice
```

Then run the spice file in ngspice
```bash
  ngspice sky130_inv.spice
```
![ngspice install and run](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/c3c71093-b3a5-4671-a86c-ec2cb6a9c955)

Spice Output
![spice output](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/0be58b4e-ebfc-43fc-8f15-bf88b13d32b6)


To plot the graph between Voltage and time type the command in ngspice

```bash
  plot y vs time a
```
![plot transient response](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/ab16409c-362b-4562-a423-ed0d302fd813)

- Transient response output
V = 3.3v \
80% of V is 2.64v\
20% of V is 0.65v
![transient reponse](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/068684d9-be72-4838-a202-7639274b11d7)
- 80% value
- ![80 percent value](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/412c7550-a754-4c47-9d01-dfecc11c1f3b)
- 20% value
- ![20 percent value](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/07704bef-85ae-4197-954d-47f64d3d11f3)

Rise transition time = Time taken for output to rise from 80% - Time taken for output to rise from 20% 
                    
                     = 2.4577 ns - 2.182 ns
                     =  0.06377 ns

- 20% value
-  ![fall transition 20 percent](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/88d55649-6fe8-4e1b-ad7d-7f650145593c)
- 80% value
- ![fall transition 80 percent](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/e13a8e1c-1992-4b1e-915f-4c13f33f3521)

Fall transition time = Time taken for output to fall from 20% - Time taken for output to fall from 80% 
                    
                     = 4.09511 ns - 4.05263 ns
                     =  0.04248 ns

V = 3.3v\
50% of V is 1.65v
![propagation delay in cell rise](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/85758fa4-2465-4560-823e-c7f6b4ded078)

Rise propagation delay = Time taken for output to rise to 50% - Time taken for input to fall to 50% 
                    
                     = 2.2113 ns - 2.15 ns
                     =  0.0613 ns
![propagation delay in cell fall result](https://github.com/SANGESH007/Digital-Soc-Design/assets/77070030/4b9e180d-8b70-4307-87da-2ce88a8f53e8)

Fall propagation delay = Time taken for output to fall to 50% - Time taken for input to rise to 50% 
                    
                     = 4.07806 ns - 4.05056 ns
                     =  0.0275 ns






