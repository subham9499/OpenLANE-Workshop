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
      <a href="#Day 1 Inception of open-source EDA, OpenLANE and Sky130 PDK">Day 1 Inception of Open Source EDA</a>
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
      <a href="#Day 2 Floorplan and Placement">Day 2 Floorplan and Placement</a>
      <ul>
        <li><a href="#Floorplan">Floorplan</a></li>
        <li><a href="#View Floorplan in Magic">View Floorplan in Magic</a></li>
        <li><a href="#Placement">Placement</a></li>
        <li><a href="#View Placement in Magic">View Placement in Magic</a></li>
      </ul>
    </li>
    <li>
      <a href="#Day 3 Design library cell using Magic Layout and ngspice characterization">Day 3 Design library cell using Magic Layout and ngspice characterization</a>
      <ul>
        <li><a href="#Clone the git repo containing skywater spice model files and copy the skywater tech file into folder">Clone the git repo containing skywater spice model files and copy the skywater tech file into folder</a></li>
        <li><a href="#Viewing the Inverter Standard cell in Magic">Viewing the Inverter Standard cell in Magic</a></li>
        <li><a href="#DRC">DRC</a></li>
        <li><a href="#Extraction to Spice using Magic">Extraction to Spice using Magic</a></li>
        <li><a href="#Spice Simulation">Spice Simulation</a></li>
      </ul>
    </li>
    
  </ol>
  </details>
      

<!-- Day 1 Inception of Open Source EDA -->
## Day 1 Inception of open-source EDA, OpenLANE and Sky130 PDK

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

Go to openlane directory and type `./flow.tcl` to invoke the openlane tool

![](/images/2.png)

  - ./flow.tcl is the script which runs the OpenLANE flow
  - OpenLANE can be run interactively or in autonomous mode. 
  - To run it interactively we use the command `/flow.tcl -interactive`
  - To run it in autonomous we use the command `/flow.tcl -design <design name>'
   

### Package Importing
We need to import all the pacakages required to run this flow:
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
Prep is used to make file structure for our design. To set this up do:
![](/images/8.png)

After running this look in the openlane/design/picro32a folder and you will see runs folder being created. Inside the runs folder we will have a folder with the present date and inside it we have these folders :
  ![](/images/7.png)

The config.tcl file shown in this folder contains all the parameters used by OpenLANE for this specific run.

### Synthesis

To run synthesis type '%run_synthesis'. Now open sysnthesis folder under reports:
![](/images/9.png)

yosys_2.stat.rpt folder is the one we use for calculating buffer ratio ,flop ratio etc.

## Day 2 Floorplan and Placement

### Floorplan 

To run the floor plan in openlane :
![](/images/10.png)

Important points:
- Standard cells doesn't get placed in floor plan but in the placement stage.
- Precedence order: sky130A_sky130_fd_sc_hd.cofig.tcl > config.tcl >floorplan.tcl

### View Floorplan in Magic

Syntax for viewing floorplan in magic is:
`magic -T <magic tech file> lef read <lef file> def read <def file>`
![](/images/11.png)

Therefore for viewing floorplan in magic we need :  Magic technology file, i.e sky130A.tech, merged lef file and def file of floorplan 

Press s followed by v to select and view the whole design:
![](/images/12_1.png)

### Placement

In the placement stage the positions of standard cells get fixed. Placement in OpneLANE happens in two stages:
 1.Global Placement - Optimization is the main criteria here. Optimize by reducing wire length by reducing Half perimeter wire length(HPWL). It is not legal placement i.t standard cells in rows might overlap
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

Press s followed by v to select and view the whole design:
![](/images/15.png)

## Day 3 Design library cell using Magic Layout and ngspice characterization

### Clone the git repo containing skywater spice model files and copy the skywater tech file into folder

Cloning:
![](/images/17.png)

The vsdstdcelldesign directory:
![](/images/18.png)

Copying skywater.tech file:
![](/images/19.png)

The vsdstdcelldesign directory after copying skywater.tech file into it:
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

The DRC(Design Rule Check) errors are highlighted by dottend lines. DRC should be 0 for the component to fabricated.
![](/images/26.png)

DRC options:
![](/images/27.png)

### Extraction to Spice using Magic
`extract all` creates the .ext file and `ext2spice` creates the .spice file from the .ext file
Commandands to extract to spice :
![](/images/28.png)


The `.ext` and `.spice` files being created:
![](/images/29.png)

### Spice Simulation

The scale should be set 0.01u because in the layout each box is 0.01x0.01u:
![](/images/30.png)

Spice Deck:
![](/images/31.png)

Opening the inverter spice file in ngspice:
![](/images/32.png)

Plotting output, input vs time in ngspice -> `plot y vs time a`
![](/images/33.png)
![](/images/34.png)

 



  









