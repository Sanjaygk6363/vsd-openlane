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

Use this command to initiate the Magic Too

```bash
 magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```
- Floorplan def in Magic
![magic opening](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-02%2022-25-35.png)



- Horizontal metal layer
![horizontal metal layer](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-03%2011-03-27.png)

## Placement
To run the Placement, the command is


```bash
    run_placement
```
Commands to load placement def in magic


```bash
    magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
- Floorplan def in magic

![placement chip](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-03%2011-03-27.png)

- Standard cell placement

![placement of standard cells](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-02%2022-25-35.png)


/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////




