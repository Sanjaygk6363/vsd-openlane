# Digital-Soc-Design

# Day 1
## The courses structure

![The courses structure](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/images/day1/Screenshot%20(74).png)

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

![introduction also](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/images/day1/Screenshot%20(77).png)

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
![open lane](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/images/day1/Screenshot%20(79).png)
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
![intera ctive](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/images/day1/Screenshot%20(82).png)
-------------------------------------------------------------------------------------------------------------------------
## Final result Synthesis
To run the Synthesis
```bash
 run_synthesis
```
![synt hessis](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/images/day1/Screenshot%20(83).png)


-> This contains all the details about the synthesis of the picorv32a 
------------------------------------------------------------------------------------------------------------------
- Number of cells: 14876
![cell no](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/images/day1/Screenshot%20(83).png)
-----------------------------------------------------------------------------------------------------------------
- Number of FF: 1613
  ![flip flop](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/images/day1/Screenshot%20(84).png)
---------------------------------------------------------------------------------------------------------------------------
 - The Chip Area of the module 147712.918400
![chip area](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/images/day1/Screenshot%20(85).png)

------------------------------------------------------------------------------------------------------------------------------------------

AS for the Assignment to find the Flop ratio. This can be calculated by using the formula:

                     Flop ratio in (%) = Total No of D-FF
                                        --------------------  X 100
                                        Total No of Cells

                                              =   1613
                                                   --------   X 100
                                                   14876 

                               Flop ratio = 10.8429685
