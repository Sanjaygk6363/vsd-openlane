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

![placement of standard cells](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-03%2011-03-32.png)

# cell design flow
![cell design](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(101).png)

cell design flow:
 
Need for libraries and characterization
Every ICdesign Flow needs to go through the several steps. First step to go through is Logic Synthesis, let's say if we have a functionality which is coded in a form of an RTL so first we need to convert the functionality into legal hardware is refered to as Logic Synthesis. Ouput of the logic synthesis is arrangement of gates that will represent the original functionality that has been described using an RTL. Next step of logic synthesis is Floorplaning, in this we omport the output of logic synthesis and decide the size of the Core and Die. The next step after floorplaning is Placement, in this we take the particular logic cell send place them on the chip in such a fashion that initial timing is better. Next step is CTS(Clock tree synthesis), in this we take care that clk should reach each and every signal at the same time also take care of each clk signal has equal rise and fall.Next step is Routing, routing has to go through the certain flow dependendent on the characterization of the flip flop.And now comes the last step STA(Static timing analysis), in this we try to see the set up time, hold time, maximum achieved frequency of the circuit. One common thing across all stages 'GATES or Cells'.

![cell design](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(143).png)

(![cell design](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(104).png)
In the above we can see the three sizes of same component where as the size increases the data flow will also increases it will be  used depends on the system which is being designed

# general timing charectarisation parameter
timing threshold definiton

A timing threshold is a predetermined limit of time set in a process. When a measurement or event reaches the threshold, it triggers a specific action.it depends on th usage of circuits power supply
       ![timi threshold](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(145).png)
       
 propagation delay
  delay is the time it takes for a change in voltage (the signal) to move through the different components. Each component introduces a slight delay, and the total delay affects how fast the circuit can operate.As in the above circuit we can calculate the delay of flow of data we can reduce them.
  
  ![prop delay](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(147).png)
       
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# day 3 :Design library cell using magic layout and ngspice characterization
  chapter 1:labs for CMOS inverter ngspice simulation

In this 2nd day of lab we are going to learn  about floorplan and placement

IO placer: 
we learn in previous vedio how the chip pins are arranged in equal distane (value 1) but here we change it by using a command"set" into a variable env(FP_IO_MODE) and make its value 2

# Switching Threshold Vm
In the next step we are going to do an spice simulation where we use two method
method 1:where both the N-MOS and P-MOS having same hite and length
method 2: In this the P-MOS is 2.5 times more than the N-MOS
as shown in below figure

![spice sim](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(149).png)

![spice sim](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(150).png)

Due to less amount of charge in the P-MOS to maintain the balance and also the flow of current we take more P-MOS 
As we can see in the above graph in the first method the current is less compared to method 2
and also it disapates faster than method 2

PICE deck creation for CMOS inverter
It is also a part where show the compostion the P-MOS and N-MOS in an CMOS inverter
![c mos](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(151).png)

In this we can see how the node is formed and also how to specifie the mosfet and circuit with theior characterstics
![char ect](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(152).png)

# Lab steps to git clone vsdstdcelldesign
In this we use a command "git clone" in the terminal to copy the data or directory fron the someone else github account
![git hub](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(153).png)

![git hub](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/ppopo.jpeg)

After the code git clone is executed then we can see the directory whic is highlighted in the pic

# Inverter Layout Design
By using magic tool we are going to check and analysis the CMOS structure

to identify N-MOS and P-MOS
![cmos](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-05%2015-42-39.png)

Verifying that Y o/p is connected to PMOS & NMOS drain
![veri fy](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-07%2014-34-56.png)

Verification of VPWR connectivity to PMOS
![verify c](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-07%2014-35-16.png)

Verification of VGND connectivity to NMOS
![vrei gnd](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-07%2014-35-08.png)

# Extraction of C-MOS file from Magic
here we use three command to extract the file
```bash
     pwd
     extract all
     ext2spice cthresh 0 rthresh 0
     extspice
```
![extra ct](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(154).png)

And then using command we can eddit the file according to the needs
```bash
     vim filename
```
![file op](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/ooooipoio.jpeg)

# Running ngspice:

To load spice file type the command - ngspice sky130_inv.spice followed by plot y vs time a

![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/graph.jpeg)

# 20%
![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/po12.png)

# 50%
![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/op24.png)

# 80%
![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/op23.png)

Calculation

Full transition time = 4.0955-4.0536 
                        = 0.0419ns 
                       = 41.9ps

Rise cell delay = Time taken for output to rise to 50% - Time taken for input to fall to 50%
                                                  = 1.65V

 # CMOS Fabrication process
  step1:
  ![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(159).png)

  step2:
  ![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(160).png)

  step3:
  ![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(162).png)

  step4:
  ![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(163).png)

  step5:
  ![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(164).png)

  step6:
  ![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(165).png)

  step7:
  ![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(166).png)

  step8:
  ![spi ce](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(167).png)

  ///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
  ---------------------------------------------------------------------------------------------------------------------------------
  //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
  # day 4 :Pre-layout timing analysis and importance of good clock tree

Rule 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.

Rule 2: Width of the standard cell should be odd multiples of the horizontal track pitch (taking 3 here)

Rule 3: Height of the standard cell should be even multiples of the vertical track pitch.

```bash

cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

magic -T sky130A.tech sky130_inv.mag &

```

![cmos](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-05%2015-42-39.png)

![verify c](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20from%202024-04-07%2014-35-16.png)

Coping the lef file & lib files to picrov32a design src directory
```bash
    cp filename address to be saved
```

![copy dir](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(170).png)

Editing config.tcl fie and new lef file to openlane flow

![new file](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/newfi.jpeg) 

#running openlane synthesis
first we use "docker "command to invoke bash script then use these command
```bash
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]      
add_lefs -src $lefs
run_synthesis
```
After these command the result will be
In this we can see the area of the cell
![verify c](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/newwifi1.jpeg)

In the below we can see the value "wns" also be called as slack
![verify c](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/newwif2.jpeg)

In this step thse commands are used
```bash
prep -design picorv32a -tag 01-04_12-54 -overwrite
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
echo $::env(SYNTH_STRATEGY)
set ::env(SYNTH_STRATEGY) "DELAY 3"
echo $::env(SYNTH_BUFFERING)
echo $::env(SYNTH_SIZING)
set ::env(SYNTH_SIZING) 1
echo $::env(SYNTH_DRIVING_CELL)
```
![verify c](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/new%20wifi3.jpeg)

In here we gor wns =-23.89

and after we will again perform synthesis

![verify c](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/new%20wifi%204.jpeg)

In this we move to do floorplan
![verify c]( https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/newwifi5.jpeg)

Here insted of Run_floorplan we use these command
```bash
init_floorplan
place_io
tap_decap_or
run_placement
```
![verify c]( https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/new%20wifi%206.jpeg)
![verify c]( https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/new%20wifi7.jpeg)
![verify c]( https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/ne%20wwifi8.jpeg)
![verify c]( https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/nwewifi9.jpeg)
after opening magic tool we get
![verify c]( https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/pop0o0o0.jpeg)
![o p](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/Screenshot%20(171).png)

# Timing Analysis with OpenSTA tool after synthesis
We will do STA on the initial picorv32a design which had timing violations.
herewe run the synthesis using the following commands in openlane directory
```bash
    docker
    ./flow.tcl -interactive
    package require openlane 0.9
    prep -design picorv32a
    set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
    add_lefs -src $lefs
    set ::env(SYNTH_SIZING) 1
    run_synthesis
```

![verify c](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day2/newwif2.jpeg)

Now, we also need to create my_base.sdc file containing the content shown in below image which is from "src" dirctory
![cdsv nj](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(179).png)

![cdsv nj](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%202024-04-10%20150932.png)

![cdsv nj](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(177).png)
# Clock Tree Synthesis(CTS):

 clock tree synthesis:   Efficient distribution of clock signal with minimal skew, jitter, and power consumption. Done before signal routing using OpenROAD.
here in the diagram we can how we connect clk1 to FF1 & FF2 of stage 1 and FF1 of stage 3 and FF2 of stage 4 with physical wire with Buffer
![clock tree](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(126).png)

and in this we see the connection of clk2 to other flip flopes
![clock tree2](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(127).png)

![clo ck](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(119)%20-%20Copy.png)

# power aware CTS
   it show about the power usage and limitaion of it in CTS
   ![p cts](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(117)%20-%20Copy.png)

   Let us examine one of the CLK networks. Due to the coupling capacitance between the wires, any switching activity occurring at the aggraser will consequently immediately affect the nearby net whenever switching activity occurs at the aggraser.The method by which we can shelter the internet from these issues is called shielding. Wire is inserted between any two wires in a shielding where coupling capacitance is generated. This additional wire is either grounded or linked to VDD.
The amount of delta delay that results from the bump that occurs when we go from logic '1' to logic '0' is visible. And in this case, skew is no longer 0. Therefore, crosstalk delta delay has the effect of making the screw value non zero

![oajh n](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(124).png)

 Timing analysis
  ![ti mu](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%202024-04-09%20155349%20-%20Copy.png)
  
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
-----------------------------------------------------------------------------------------------------------------------------------
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
## Day 5 -Final step for RTL2GDS using tritinRoute and openSTA

# Routing
Routing is the art of finding the most efficient path to connect two points (source and target) within a circuit layout. It's like planning the best route for a delivery truck, but on a microscopic scale! The ideal route minimizes distance while keeping things tidy
![roo ting](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(127).png)

# Lee's Alogorithum
Therse should not be zig-zag lines of connections most of the connections should be in L shape or in Z shape. So according to algorithm first it create some grids and grids are routing at the backend. It's called as routing grid. There are some numbers of grids on this routig having some dimensions. SO here we are having two points one is 'Source' and the other is 'Target'. With the help of this routing grid algorithm has to find out the best possible way between them.

First step is algorithm tries to lable all of the grids surrounded. Only the adjacent horizontal and vertical grids are labeled not the digonal one as shown in the image below.
![algo lee](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(128).png)
![algo lee](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%202024-04-09%20185932.png)
Another rooting formula is
![for mu](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%202024-04-09%20195053.png)

# Design Rule Check
 Wire width:- Width of the wire should be minimum that derived from the optical wavelenth of lithography technique applied.
 Wire Pitch:- The minimum pitch between two wire should be this much as shown in the figure below.
 Wire Spacing:- The wire spacing between two wires should be as shown in the image below.

# rule 1
![imahd nj](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(132).png)
# rule 2
![imahd nj](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(133).png)
# rule 3
![imahd nj](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(131).png)

## Power Distribution Network and routing

```bash
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a -tag 30-03)20-42
echo $::env(CURRENT_DEF)
```
up to now we have done CTS and now we are going to do the routing. but before routing we have to generate the PDNfile by using the command.
```bash
gen_pdn
run_routing
```
Loading PDN def in magic
![dr dg](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(172).png)

![sder gs](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(174).png)

## Routed DEF in magic show the layout in below format

![rout bh](https://github.com/Sanjaygk6363/vsd-openlane/blob/main/day1/Screenshot%20(176).png)


//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


