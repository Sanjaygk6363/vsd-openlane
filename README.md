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

 Optimise placement
      Optimize Plecement:- In optimize placement we will resolve the problem of distancing.Lrt's take the example of FF1 to Din2. There must be a wire going from Din2 to FF1 but before going into routing the desing or wiring we will try to estimate the capacitances. If we lokk the capacitance from Din2 to FF1 it is every huge because wire length is huge in that case even the resutance will also be huge because of that length. If we send the signal from Din2 then it will be difficult for FF1 to catch that input because distance is large. So we can place some intermediate steps to maitain the Signal integrity. By this the input is succesfully driven to the FF1 from Din2. These intermediate steps are called here Repeaters , Repeaters are basically buffers that will recondition the original signal and make a bew signal which replicate the original signal and send it forward this process repeates untill we reach to the actual cell where we want to send the input in this way signal integrity is maintained. By using repeaters we resolve the problem of signal integrity but there will be a loose of area because more and more repeaters are used more area will be used of the particular floorplan.

![cell design](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(101).png)
 cell design flow
         Need for libraries and characterization
Every ICdesign Flow needs to go through the several steps. First step to go through is Logic Synthesis, let's say if we have a functionality which is coded in a form of an RTL so first we need to convert the functionality into legal hardware is refered to as Logic Synthesis. Ouput of the logic synthesis is arrangement of gates that will represent the original functionality that has been described using an RTL. Next step of logic synthesis is Floorplaning, in this we omport the output of logic synthesis and decide the size of the Core and Die. The next step after floorplaning is Placement, in this we take the particular logic cell send place them on the chip in such a fashion that initial timing is better. Next step is CTS(Clock tree synthesis), in this we take care that clk should reach each and every signal at the same time also take care of each clk signal has equal rise and fall.Next step is Routing, routing has to go through the certain flow dependendent on the characterization of the flip flop.And now comes the last step STA(Static timing analysis), in this we try to see the set up time, hold time, maximum achieved frequency of the circuit. One common thing across all stages 'GATES or Cells'.


![theory place](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(97).png)

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




