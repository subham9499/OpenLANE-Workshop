# OpenLANE-Workshop


<!-- PROJECT LOGO -->
<br />
<p align="center">

  ![](/images/advanced_physical_design.png)

  <h3 align="center">Advanced Physical Design - OpenLANE Workshop</h3>
</p>



<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#About-the-Workshop">About the Workshop</a>
      <a href="#Setting up OpenLANE">Setting up OpenLANE</a>
      <a href="#RTL to GDSII flow">RTL to GDSII flow</a>
      <a href="#The OpenLANE Flow">The OpenLANE Flow</a>
      <a href="#Day-1-Inception-of-open-source-EDA-and-introduction-to-OpenLANE-and-Sky130-PDK">Day 1 Inception of Open-Source EDA and Introduction to OpenLANE and Sky130 PDK</a>
      <ul>
        <li><a href="#skywater-pdk-files">Skywater PDK Files</a></li>
        <li><a href="#invoking-openlane">Invoking OpenLANE</a></li>
        <li><a href="#package-importing">Package Importing</a></li>
        <li><a href="#design-folder">Design Folder</a></li>
        <li><a href="#design-folder-hierarchy">Design Folder Hierarchy</a></li>
        <li><a href="#configuration-files">Configuration Files</a></li>
        <li><a href="#prepare-design">Prepare Design</a></li>
        <li><a href="#synthesis">Synthesis</a></li>
      </ul>
      </li>
    <li>
      <a href="#Day-2-Floorplan-and-Placement">Day 2 Floorplan and Placement</a>
      <ul>
        <li><a href="#Floorplan">Floorplan</a></li>
        <li><a href="#Aspect-Ratio-and-Utilization-Factor">Aspect Ratio and Utilization Factorn</a></li>
        <li><a href="#Preplaced-Cells">Preplaced Cells</a></li>
        <li><a href="#Decoupling-Capacitors">Decoupling Capacitors</a></li>
        <li><a href="#Power-Planning">Power Planning</a></li>
        <li><a href="#View-Floorplan-in-Magic">View Floorplan in Magic</a></li>
        <li><a href="#Placement">Placement</a></li>
        <li><a href="#View-Placement-in-Magic">View Placement in Magic</a></li>
        <li><a href="#Standard-Cell-Characterization">Standard Cell Characterization</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day-3-Design-library-cell-using-Magic-Layouta-and-ngspice-characterization">Day 3 Design library cell using Magic Layout and ngspice characterization</a>
      <ul>
        <li><a href="#Clone-the-git-repo-containing-skywater-spice-model-files-and-copy-the-skywater-tech-file-into-folder">Clone the git repo containing skywater spice model files and copy the skywater tech file into folder</a></li>
        <li><a href="#Viewing-the-Inverter-Standard-cell-in-Magic">Viewing the Inverter Standard cell in Magic</a></li>
        <li><a href="#DRC">DRC</a></li>
        <li><a href="#Extraction-to-Spice-using-Magic">Extraction to Spice using Magic</a></li>
        <li><a href="#Spice-Simulation">Spice Simulation</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day-4-Pre-layout-timming-analysis-and-CTS">Day 4 Pre-layout timming analysis and CTS</a>
      <ul>
        <li><a href="#LEF-File">LEF File</a></li>
        <li><a href="#PnR-Guidelines-while-making-Standard-Cell-set">PnR Guidelines while making Standard Cell set</a></li>
        <li><a href="#Converging-grid-definitions-to-track-definitions">Converging grid definitions to track definitions</a></li>
        <li><a href="#Creating-Port-Definition">Creating Port Definition</a></li>
        <li><a href="#Setting-port-class-and-port-use-attributes">Setting port class and port use attributes</a></li>
        <li><a href="#Creating-lef-file">Creating lef file</a></li>
        <li><a href="#Including-Custom-Cells-in-OpenLANE">Including Custom Cells in OpenLANE</a></li>
        <li><a href="#Fixing-Slack-Violations">Fixing Slack Violations</a></li>
        <li><a href="#Viewing-the-Custom-Inverter-cell-in-Magic">Viewing the Custom Inverter cell in Magic</a></li>
        <li><a href="#Clock-Tree-Synthesis">Clock Tree Synthesis</a></li>
        <li><a href="#OpenROAD">OpenROAD</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day-5-Final-steps-for-RTL2GDS">Day 5 Final steps for RTL2GDS</a>
      <ul>
        <li><a href="#Checking-which-part-of-flow-we-are-in">Checking which part of flow we are in</a></li>
        <li><a href="#Power-Distribution-Network">Power Distribution Network</a></li>
        <li><a href="#Routing">Routing</a></li>
        <li><a href="#SPEF-Extraction">SPEF Extraction</a></li>
      </ul>
      </li>
    <li>
      <a href="#Contact">Contact</a>
      </li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
      
    
  </ol>
  </details>
      
## About the Workshop

In this workshop the aim was to learn the RTL to GDSII flow using the OpenLANE which is opensource. The work shop was a 5 day hands on workshop with theory and virtual labs covering all asspects of VLSI design flow from RTL to GDSII.
OpenLANE is tuned for  the Skywater 130nm open-source PDK and can be used to produce hard macros and chips.

## Setting up OpenLANE 

As OpneLANE is only available for linux based systems you would have to dual boot or use a virtual box .To set up OpenLANE in your local PC with virtual box you need :
1. Ubuntu OS
2. 25 GB Disk Space

For installation refer to : 
1.https://github.com/nickson-jose/openlane_build_script
2.[A complete guide to install OpenLANE and Sky130nm PDK](https://www.udemy.com/share/103wqAAEESeVZUR3QF/)
3.[A complete guide to install open-source EDA tools](https://www.udemy.com/share/101skKAEESeVZUR3QF/)

## RTL to GDSII flow

ASIC (Application Specific Integrated Circuit) Design Flow is an iterative and dynamic process which follows various steps.. The flow has 11 different stages as shown below :-

![](/images/images_asic_flow.png)

1. Chip Specification - The VLSI engineers are provided with the specifications according to which they need to  design circuits taht meets these constraints for their system.

2. Design Entry/Functional Verification - In this stage the RTL design and Behavioral Modeling  are performed using the Hardware Description Language (HDL).

3. RTL synthesis - In this stage the system taht was  designed is implemented  and represented and the netlists are tech-mapped to the specific logic gates. 

4. Partitioning of Chip - In this step demarcation of certain sections of the chip and designing each sub-section happens.

5. DFT Insertion - DFT (Design for test) Circuit is inserted.

6. Floorplanning - Placing the core and die happens in this stage. Also  Power Distribution Network is generated in this stage.

7. Placement Stage - In the placement stage the positions of standard cells get fixed. Placement in OpneLANE happens in two stages:
 1.Global Placement - Optimization is the main criteria here. Optimize by reducing wire length by reducing Half perimeter wire length(HPWL). It is not legal placement i.e standard cells in rows might overlap
 2.Detailed Placement - Legalization is the main criteria here.

8. Clock Tree Synthesis - This stage works towards building a clock distribution network that whose role is to deliver the clock to all associated sequential elements prresent in the design.

9. Routing - This stage implements the interconnect system between standard cells in the design and minimizes DRC errors. 

10. Final Verification - A final verification before sending the chip for fab is done here.

11. GDSII - Graphic Design System(GDS) is a document that contains the layout design of the chip. It comes in the binary format, which is readable by specific EDA tools.This file is sent to fabs to get fabricated.

## The OpenLANE Flow

The OpenLANE Flow is as follows:

![](/images/images_openlane_flow.png)

The various tools used by OpenLANE in ASIC Flo are :

1. **Synthesis**
    1. `yosys` - Performs RTL synthesis
    2. `abc` - Performs technology mapping
    3. `OpenSTA` - Pefroms static timing analysis on the resulting netlist to generate timing reports
2. **Floorplan and PDN**
    1. `init_fp` - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
    2. `ioplacer` - Places the macro input and output ports
    3. `pdn` - Generates the power distribution network
    4. `tapcell` - Inserts welltap and decap cells in the floorplan
3. **Placement**
    1. `RePLace` - Performs global placement
    2. `Resizer` - Performs optional optimizations on the design
    3. `OpenPhySyn` - Performs timing optimizations on the design
    4. `OpenDP` - Perfroms detailed placement to legalize the globally placed components
4. **CTS**
    1. `TritonCTS` - Synthesizes the clock distribution network (the clock tree)
5. **Routing** *
    1. `FastRoute` - Performs global routing to generate a guide file for the detailed router
    2. `TritonRoute` - Performs detailed routing
    3. `SPEF-Extractor` - Performs SPEF extraction
6. **GDSII Generation**
    1. `Magic` - Streams out the final GDSII layout file from the routed def
7. **Checks**
    1. `Magic` - Performs DRC Checks & Antenna Checks
    2. `Netgen` - Performs LVS Checks



## Day 1 Inception of Open-Source EDA and Introduction to OpenLANE and Sky130 PDK

### Skywater PDK Files

The pdk folder has all the information related to the pdk we are using, Skywater PDK in our case. Skywater130 is a 130nm PDK files. There are three subdirectories that we will be using:

![](/images/1.png)

  1. Skywater-pdk – Contains all the foundry provided PDK related files, i.e timming libraries, tech files etc
  2. Open_pdks – Contains scripts that are used to bridge the gap between closed-source and open-source PDK to EDA tool compatibility, like magic, netgen etc.
  3. Sky130A – The open-source compatible PDK files. Inside Sky-130A we have 2 subdirectories:
  
  ![](/images/1_1.png)
  
   i. libs.ref - Contains process specific files
  
   ![](/images/1_2.png)
   We will be using sky130_fd_sc_hd. The normenclature is as follows : 
   - sky130 is process name
   - fd is foundary name(skywater)
   - sc is for standard cell
   - hd is for high density
  
   ii. libs.tech - Contains files specific to tools
  
   ![](/images/1_3.png)

### Invoking OpenLane

Go to OpenLANE directory and type `./flow.tcl` to invoke the openlane tool.
To run OpenLANE interactively use the command `./flow.tcl -interactive`

![](/images/2.png)

  - ./flow.tcl is the script which runs the OpenLANE flow
  - OpenLANE can be run interactively or in autonomous mode. 
  - To run it interactively we use the command `/flow.tcl -interactive`
  - To run it in autonomous we use the command `/flow.tcl -design <design name>'
   

### Package Importing
We need to import all the pacakages required to run this flow.
Use the command `% package require openlane 0.9` 
![](/images/3.png)

### Design Folder
All designs run within OpenLANE are extracted from the openlane/designs folder:
![](/images/4.png)
These are the built in designs. If we need to add our own design, we need to create a folder of our design here.

### Design Folder Hierarchy
We will be using picorv32a design:
![](/images/5.png)

Each design hierarchy comes with two distinct components:
  1. Src folder - Contains verilog files and sdc constraint files
  2. Config.tcl files - Design specific configuration switches used by OpenLANE

An example of a configuration file is given:
  ![](/images/6.png)

### Prepare Design
`prep -design <design_name>` is used to make file structure for our design.

This command merges the cell LEF and technology LEF information and name sit as `merge.lef`
1.Cell LEF - Provids the user with information about the standard cells.
2.Tech LEF - Contains layer definitons and a set of restricted design rules.

To set this up do:

![](/images/8.png)

To create folder with custom name, use this command -> `prep -design <design_name> -tag <folder_name>` .Note that using thsi command doesn't overwrite the already existing folder with the same name. To overwrite the folder use the command -> `prep -design <design_name> -tag <folder_name> -overwrite`

After running this look in the `openlane/design/picorv32a` folder and you will see runs folder being created. Inside the runs folder we will have a folder with the present date and inside it we have these folders :
  ![](/images/7.png)

The config.tcl file shown in this folder contains all the parameters used by OpenLANE for this specific run.

### Synthesis

To run synthesis type `%run_synthesis`.Yosys and abc are the tools used in the OpenLANE flow for synthesis.  Now open sysnthesis folder under reports:
![](/images/9.png)

yosys_2.stat.rpt folder is the one we use for calculating buffer ratio ,flop ratio etc.

## Day 2 Floorplan and Placement

### Floorplan 

In the floorplanning stage the following things are done:
1.Set the core and die area
2.Placement of Macros and IO pins
3.Power distribution network(this is normally done in floorplanning stage but in OpenLANE its done after CTS)

Note that Standard cells doesn't get placed in floor plan but in the placement stage.

### Aspect Ratio and Utilization Factor

Aspect Ratio is defined as the ratio of the height of the core to the width of the core. This basically gives us an idea about the shape of the chip. Aspect ratio of 1 implies that the chip is square shaped.
Utilization Factor is as a measure of the area that is being utilized by the netlist. It's defined as the ratio of area occupied by the netlist, to the total area of the core available. It is generally ranges between 0.5 and 0.7.

### Preplaced Cells(MACROs)
Preplace cells or most prominently know as MACROs have reserved slots to be placed at and other cells are bloacled from using these slots during floorplanning. Example for this would be say a multiplier with 50 thousand gates, we need not implement it everytime , we should just implement it once and then instantiate it.

### Decoupling Capacitors
Decoupling capacitors are huge capacitors having charge up to source voltage and are placed near the preplaced cells. Voltage drops which are associated with interconnect wires can heavily affect noise margin or put it into indeterminate state.It acts as a resovoir when a transition happens in the circuit. It decouples the circuit from main suplly.

### Power Planning
We place Vdd and ground lines in the power planning process.Coupling capacitance is formed between interconnect wires, when a transition occurs, charge associated with coupling capacitors may be dumped to ground. If there aren't enough ground taps available, the charge will accumulate at the tap which will result in ground line acting as a large resistor which raises the ground voltage. These power lines dump power to the cells.

To run the floor plan in openlane :

![](/images/10.png)

Important points:
-To check clock period use the command `% echo $env(CLOCK_PERIOD)`
-To change clock period to say 15ns -> `set env(CLOCK_PERIOD) 15` 
- Precedence order: sky130A_sky130_fd_sc_hd.cofig.tcl > config.tcl >floorplan.tcl

### View Floorplan in Magic

Syntax for viewing floorplan in magic is:
`magic -T <magic tech file> lef read <lef file> def read <def file>`

![](/images/11.png)

Therefore for viewing floorplan in magic we need :  Magic technology file, i.e sky130A.tech, merged lef file and def file of floorplan 

Press `s` followed by `v` to select and view the whole design:

![](/images/12_1.png)

### Placement

In the placement stage the positions of standard cells get fixed. Placement in OpneLANE happens in two stages:
 1.Global Placement - Optimization is the main criteria here. Optimize by reducing wire length by reducing Half perimeter wire length(HPWL). It is not legal placement i.e standard cells in rows might overlap
 2.Detailed Placement - Legalization is the main criteria here.
 
 Placement in OpenLANE is done by:
 
 ![](/images/13.png)
 
 Reports after placement:
 
  ![](/images/14.png)
  
  ### View Placement in Magic
  
Syntax for viewing placement in magic is:
`magic -T <magic tech file> lef read <lef file> def read <def file>`

![](/images/16.png)

Therefore for viewing placement in magic we need :  Magic technology file, i.e sky130A.tech, merged lef file and def file of placement 

The layout post placement:
![](/images/15.png)

### Standard Cell Characterization

Standard Cell Libraries has cells with different functionalities and various flavours of the same cell. These cells need to be characterized by liberty files to be used by synthesis tools to determine optimal circuit arrangement. The open-source software GUNA is used for characterization.

## Day 3 Design library cell using Magic Layout and ngspice characterization

### Clone the git repo containing skywater spice model files and copy the skywater tech file into folder

The work done in Day 3 was mainly on a CMOS inverter designed in Magic tool. Worked on inverter available on nickson-jose 's github repo titled "vsdstdcelldesign".


First we clone the repo to our local system:

![](/images/17.png)

The vsdstdcelldesign directory is as follows:

![](/images/18.png)

Now we copy the skywater skywater.tech file:

![](/images/19.png)

The vsdstdcelldesign directory is as follows after copying skywater.tech file into it:

![](/images/20.png)

### Viewing the Inverter Standard cell in Magic

Invoking Magic:

![](/images/21.png)

Inverter Layout in Magic:

![](/images/22.png)

Layers and components of the inverter :

![](/images/23.png)

Point towards a part and press 's', then type `what` on tkcon window:

![](/images/24.png)

Point towards a part and press 's' three times to see all connections to that part:

![](/images/25.png)

### DRC 

The DRC(Design Rule Check) errors are highlighted by dottend lines. DRC should be 0 for the component to fabricated. If DRC is not equal to 0, it is marked red color indicating DRC error.

![](/images/26.png)

Options in the DRC menu are as follows:

![](/images/27.png)

### Extraction to Spice using Magic

`extract all` creates the .ext file and `ext2spice` creates the .spice file from the .ext file
Impementation is as follows:

![](/images/28.png)

The `.ext` and `.spice` files being created:

![](/images/29.png)

### Spice Simulation

The scale should be set 0.01u because in the layout each box is 0.01x0.01 um:

![](/images/30.png)

Spice Deck of the design is as follows:

![](/images/31.png)

Opening the inverter spice file in ngspice:

![](/images/32.png)

Plotting output, input vs time in ngspice -> `plot y vs time a`

![](/images/33.png)

![](/images/34.png)

Calculating Rise Time:
It is defined as time taken for the output to go from 20% of the final value to 80% of the final value. We see that the 20% of final voltage is   0.66V and the 80% value is 2.64V. At 0.66v, time was 2.18193ns and at 2.64v time was 2.24566ns. Therefore the rise time was found to be 63.7ps.

![](/images/72.png)

![](/images/73.png)

## Day 4 Pre-layout timming analysis and CTS

###  LEF File
The LEF file has the information about input ports, output ports , ground and power ports. These are th eonly information needed fo rplace and route. LEF file in a way protect our IP. Our aim is to extract lef file from mag file.

### PnR Guidelines while making Standard Cell set
1.Input and output port must liw on vertical and horizontal tracks.
2.Width of standard cell should be odd multiple of track horizontal pitch and likewise height should an odd multiple of track vertical pitch.

The track file:
![](/images/35.png)
![](/images/36.png)

### Converging grid definitions to track definitions

The grids that we see are according to the track definitions
![](/images/37.png)
The tool also works in the similar way. Routing of li1 lef can happen allong these grids. This fullfills the first requirement.

Second criteria:
We see that the width of standard cell should be odd multiple of track horizontal pitch (the cells inside the inner white line ,3 here(2 full and 2 halves)):
![](/images/38.png)

### Creating Port Definition

Select the port required and go to `Edit -> Text`. This has already been done in our example.

![](/images/39_1.png)

### Setting port class and port use attributes

The `class` and `use` are used by the LEF and DEF.
![](/images/39.png)

### Creating lef file

Command to create `.lef` file is -> `lef write`:

![](/images/40.png)

![](/images/41.png)

Viewing th lef file:

![](/images/42.png)

We see that setting a layer as port , it creates a PIN. 


Copy lef file to `picorv32a/src`:
![](/images/43.png)

Copy the libraries to `picorv32a/src`:

![](/images/44.png)

![](/images/45.png)

### Including Custom Cells in OpenLANE

Modify the `picorv32a/src/config.tcl` file as :

![](/images/46.png)

prep design  and this time if you are already using the older tag then use `prep -degign <design_name> -tag <tag_name> -overwrite`.
-overwrite is significant as it overwrites the new changes made in the configuration files.

After add these commands to include sky130_vsdinv.lef in ~/tmp/meged.lef in openlane flow:

`set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs`

![](/images/48.png)


Run synthesis:

![](/images/49.png)

We see slack violations after synthesis:

![](/images/50.png)

### Viewing the Custom Inverter cell in Magic

Run floorplan and placement. Invoke magic:
![](/images/53.png)

Our Standard Inverter cell is now integrated to the picorv22a layout:

![](/images/54.png)

Type the command `expand` in tkcon window to view layout:

![](/images/55.png)


Copy `my_base.sdc` to `picorc32a/src`:

![](/images/56.png)

my_base.sdc file is as shown:

![](/images/57_1.png)

Crate pre_sta.conf file and run `sta pre_sta.conf` in terminal.

pre_sta.conf
![](/images/58.png)

running `sta pre_sta.conf`:
![](/images/59.png)

![](/images/60_1.png)

### Fixing Slack Violations

Here we change the synthesis strategy from 2 to 1. 
![](/images/51.png)

Now to reduce the slack violation we will be upsizing the buffere with large delays. Note that we are doing this in terminal (with sta_ pre_conf.sta command) and not inside openlane.

We will upsize cell _41881_ which belongs to net _11341_.

![](/images/51_!.png)

Type command `report_net -connection _11341_` to get details about the net.

![](/images/51_@.png)

To upsize buffere _41881_ from 1 to 4 use the command :
`replace_cell _41881_ sky130_fd_Sc_hd__buf4`

To check reports type the command  :
`report_checks -fields {net cap slew input_pins} -digits 4`

![](/images/51_2.png)


Go on doing doing this with other bufferes to reduce the slack viloations in range (-1-0)(i.e expample 0.7).

Improvements in slack violations:
![](/images/51_4.png)

Now use the command `write_verilog <.v file_location>` to update the verilog file after pre_sta reduction in slack violations.

![](/images/51_5.png)

Note not to run synthesis again in openLANE flow and directly run floorplan after this.

### Clock Tree Synthesis

To run Clock tree synthesis in OpenLANE flow us e the command -> `% run_cts`

OpenLANE will add the necessary buffers required to make sure the timing rules are adhered and will modify our pre-existing netlist.
A file named "picorv32a.synthesis_cts.v" will be created in the /designs/picorv32a/runs/<tag_name>/results/synthesis directory.

### OpenROAD

Timing analysis is done in OpenLANE by creating a .db database file. This database file is created from the post-cts LEF and DEF files.
To invoke OpenROAD use command ->  `% openroad`.

Then type these command:

`% write_db pico_cts.db
% read_db pico_cts.db
% read_lef <Location_of_LEF_file> //Location of LEF file - /designs/picorv32a/runs/<tag_name>/tmp/merged.lef
% read_def <Location_of_DEF_file> //Location of DEF file - /designs/picorv32a/runs/<tag_name>/results/cts/picorv23a.cts.def
% read_verilog <Location_of_verilog_file> //Verilog file - /designs/picorv32a/runs/<tag_name>/results/synthesis/picorv32a.synthesis_cts.v
% read_liberty $::env(LIB_SYNTH_COMPLETE)
% link_design <design_name> //design name = picorv32a
% read_sdc <Location_of_sdc_file> //sdc file - /designs/picorv32a/runs/<tag_name>/src/my_base.sdc
% set_propagated_clock [all_clocks]
% report_checks -path_delay min_max -fields {slew trans net cap inpput_pin} -format full_clock_expanded -digits 4 `


## Day 5 Final steps for RTL2GDS

### Checking which part of flow we are in 

TO check which part of flow we currently are in use the command:
`% echo $::env(CURRENT_DEF)`

After the CTS when we use the command we see that  CURRENT_DEF holds the def file that we get after performing the cts stage.
![](/images/62.png)

### Power Distribution Network


TO generate PDN us the command:
`gen_pdn`

![](/images/63.png)

This creates power ring for the entire core, power halo for any preplaced cells, power straps to bring power into the center of the chip and power rails for the standard cells.

The distribution of power in the cell is as shown:

![](/images/70.png)

After the PDN stage run `% echo $::env(CURRENT_DEF)` command again, and you will see that the current file is pdn.def

![](/images/71.png)

### Routing

There are two types of routing : Global and Detailed routing. Global routing is done by FastRoute and Detailed routing is done by TritonRoute.
TritonRoute offers us various routing strategis.ROUTING_STRATEGY from 0 to 3 uses Triton-13 engine which has faster runtime and ROUTING_STRATEGY 14 uses Triton-14 engine which has better DRCs. For checking which strategy we are using use the command :

`% echo $::env(ROUTING_STRATEGY)`

After this run routing by using the command :
`run_routing`

![](/images/64.png)

Routing completed:

![](/images/65.png)

### SPEF Extraction

Once the routing is completed, the interconnect parasitics are extracted to perform sign off Post-STA analysis. These parasitics are extracted into a SPEF file.

The SPEF EXTRACTOR is yet to be integrated to OpenLANE, we have to run it separately. Its available in /work/tools directory. We have to run the python file named main.py in SPEF_EXTRACTOR directory. The command to do this is as folows:

`$ python3 main.py /designs/picorv32a/runs/<tag_name>/tmp/merged.lef /designs/picorv32a/runs/<tag_name>/results/routing/picorv32a.def`

![](/images/66.png)

After the extraction is complete we open the `/designs/picorv32a/runs/<tag_name>/results/routing` and we will finf .spef file created there:

![](/images/67.png)

## Contact

Subham Mohapatra - subham.m08@gmail.com

## Acknowledgements

* [Nickson Jose - VSD VLSI Engineer](https://github.com/nickson-jose)
* [Kunal Ghosh - Co-founder (VSD Corp. Pvt. Ltd)](https://github.com/kunalg123)







 



  









