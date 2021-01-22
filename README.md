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
    
  </ol>
  </details>
      

<!-- Day 1 Inception of Open Source EDA -->
## Day 1 Inception of open-source EDA, OpenLANE and Sky130 PDK

### Skywater PDK Files

The pdk folder has all the information related to the pdk we are using,The Skywater PDK in our case.The Syywater 13 0 is a 130nm PDK files we are working with are described under $PDK_ROOT. There are three subdirectories needed for the workshop:

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

Go to openlane directory and type '$./flow.tcl' to invoke the openlane tool

![](/images/2.png)

  - ./flow.tcl is the script which runs the OpenLANE flow
  - OpenLANE can be run interactively or in autonomous mode. 
  - To run it interactively we use the command '$/flow.tcl -interactive'
  - To run it in autonomous we use the command '$/flow.tcl -design <design name>'
   

### Package Importing
We need to import all the pacakages required to run this flow:

![](/images/3.png)

### Design Folder
All designs run within OpenLANE are extracted from the openlane/designs folder:

![](/images/4.png)
These are the built in designs. If we need to add our own design, we need to create a folder of our design here.

### Design Folder Hierarchy
WE will be using picorc32a design:

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

To run synthesis type '%run_synthesis'. Now a sysnthesis folder:

![](/images/9.png)

yosys_2.stat.rpt folder is the one we use for collculating buffer ratio ,flop ratio etc.








