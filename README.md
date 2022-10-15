# SKY130 Physical Verification

 <!DOCTYPE html>
<html>
<head>
Here is my sharing from this 5 days online workshop on using Skywater Sky130A PDK
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/Workshop-Flyer.jpeg?raw=true" alt="Sky130 workshop" style="width:700px;"> 
</head>
<body>

<h2>Day 1 Lecture Summary: Introduction to SkyWater SKY130 and Open-Source EDA Tools</h2>
<p>
 Introduction to Skywater PDK
 The SkyWater Open Source PDK, provided by Google and the SkyWater Technology Foundry provide a fully open source Process Design Kit (PDK) which is used to design chips.<br> 
 
 The 130  refers to the feature size (in nanometer) of the process which is generally tells the minimum size of the transistor's gate length that can be processed as shown below: <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/gate-length.jpg" style="width:300px;"> <br>
 <br>
  The PDK can be obtained from this Github link: https://github.com/google/skywater-pdk <br>
 PDK Documentations: https://skywater-pdk.readthedocs.io/en/main/
 <br>
 <h3>open_pdks:</h3>
 open_pdks provided by  <a href="https://github.com/RTimothyEdwards/open_pdks">R. Timothy Edwards' github page</a> mainly uses the folowing <b>tools</b> to design a chip:<br>
  <br>
 <b>Xschem</b> - To draw the circuit's schematic<br> 
 <b>Ngspice</b> - SPICE simulation validationl<br>
 <b>Magic</b> - Chip's layout drawing tool and DRC validation<br>
 <b>Netgen</b> - LVS validation<br>
 <br>
 
 The libraries contained in open_pdks: <br>

 - Digital standard cells (ex: sky130_fd_sc_hd) <br>
 - Primitive devices/analog (ex: sky130_fd_pr) <br>
 - I/O cells (ex: sky130_fd_io) <br>
 - 3rd party libraries (ex: sky130_ml_xx_hd) <br>
 
The level of metal layers used in Sky130 PDK is shown below. The first metal layer (Titanium Nitride) from below is used for device's local interconnect. The next levels of metal layers (Aluminiumm) are used for inter-devices routing:  <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/sky130_layers.jpg?raw=true" style="width:700px;"> 
  <br>



 
 </p>
 
<h2>Day 1 Lab: Tool installations and basic DRC/LVS design flow</h2>
<p>
 Starting the lab, we check the availability of the installation of the main tools. The steps are:<br>
 <br>
 1. Open terminal: Right click anywhere (eg. Desktop or Home directory) and click ' <b>Open Terminal</b>'.<br>
 2. Type 'magic' to open Magic as below. If Magic is opened, the installation is ok:<br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/magic_open.jpg?raw=true" style="width:300px;"> <br>
 3. For other tools: Type and enter 'netgen', 'xschem' and 'ngspice' one by one to see if tool software can be started: <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/all_tools_starttest.jpg?raw=true" style="width:300px;"> <br>
 <br>
 The installed tools are not installed with Sky130 PDK yet. But first we will create a folder called 'inverter' and 3 folders inside the inverter folder. Create folder command in linux is 'mkdir' as shown below:<br>
  <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/3_folders.jpg?raw=true" style="width:400px;"> <br>
 
 Then we will go to the next important step, which is to set up each directory for its respective tool to run properly with the SkyWater PDKs. <br>
To create a link between each tool folder and the SKY130 submodules in open_pdks, we will use the command: 'ln -s /file_path'
 The commands were done as below: <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/link_sky_pdk.jpg?raw=true" style="width:700px"> <br>
  <br>
 After entering the PDK linking command, we start Xschem and Magic to see if the PDK is loaded properly as shown below:<br>
  <br>
 Xschem with loaded Sky130A PDK, components selections are shown at start:<br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/xschem_pdk.jpg?raw=true" style="width:500px;"> <br>
 <br>
 Magic with loaded Sky130A PDK:<br>
<img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/magic_pdk.jpg?raw=true" style="width:500px;">  <br>
 
<h3>Creating an inverter</h3>
 
 We will start creating an inverter by using the Xschem software to create the schematic and the symbol of an inverter.<br>
 
 <b>Some of useful Xschem shortcut keys: </b>
 m - move component(hover cursor on component first)<br>
 c - copy component<br>
 Del - Delete selected component<br>
 w - insert wire to route<br>
 q - edit component's parameters<br>
 Insert - bring insert component window
 
 We bring the component selection and insert window with 'Insert' key. Under the Skywater library directory (third one) we choose <b>sky130_fd_pr</b> library to choose nmos and pmos transistors:<br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/xschem_compont1.jpg?raw=true" style="width:400px;"> <br>
 We choose '<b>nfet01v8.sym</b>' which should have the extra 'B' terminal for bulk, and <b>pfet3_01v8.sym</b> with 3 terminals only as below: <br>

  <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/schem1.jpg?raw=true" style="width:200px;"> <br>
 
 Then to insert pins compomemts, we choose the device library and choose: <b>ipin.sym, opin.sym, iopin.sym</b> components and arrange as below:<br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/transistors_IO.jpg?raw=true" style="width:400px;"> 
 
 Hover to a component and press 'w' to insert and route <b>wire</b>, left-click to end the wire routing and press 'w' again to change wire routing direction. Complete wire route is as below:<br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/inverter_wire.jpg?raw=true" style="width:400px;"> 

There are two thing done in the next image: 1) rename all I/O pins 2) change the width of the nmos and pmos 3) change the voltage operation. To do this, right click on the component or press 'q' to bring the edit window. The complete inverter schematic (nevermind the selected pmos):<br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/complete_inverter.jpg?raw=true" style="width:400px;"> <br>
 
 To create a symbol from the inverter schematic, choose the menu below and save as inverter.sym:<br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/makesymbol.jpg?raw=true" style="width:400px;"> <br>
 
 After we have created and save the inverter as a symbol, load the symbol and should be as below. Note that it is not a complete testbench to simulate it:<br>
  <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/inverter_symbol.jpg?raw=true" style="width:400px;"> 
 
 We want to complete the testbench of the inverter to simulate it, to do this we insert more components from 'devices' library: <b>Vsource.sym, gnd.sym, Opin.sym</b> other than wire and I/O pins. Note also we edit the voltage value (right-click) as <b>V2: 1.8, V1: "PWL(0 0 20n 0 900n 1.8)</b>"
 <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/inverter_tb1.jpg?raw=true" style="width:700px;">  <br>
<br>
One more thing to insert into the testbench are 2 additional codes, we insert two <b>'code_shown.sym'</b> components from devices library. <br>
<img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/codeshown_sym.png?raw=true" style="width:400px;"><br>
The codes and final testbench will be:<br>
<br>
<img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/tb_final.png?raw=true" style="width:800px;"> <br>
<br>
 <img src="https://raw.githubusercontent.com/hazwanh7/SKY130-Physical-Verification/773e22be843c05a59893adc3d4ebdc4f0b1cf7c5/images/inverter_simulation.jpg" style="width:800px;"> <br>
 <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/xschm_setlvs.jpg?raw=true" style="width:500px;"> <br>
 <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/magic_impspice.jpg?raw=true" style="width:800px;">  <br>
  <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/mag_placement.jpg?raw=true" style="width:800px;">   <br>
   <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/mag_editparamtrans.jpg?raw=true" style="width:800px;"> <br>
 <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/inerter_layoutfinal.jpg?raw=true" style="width:400px;">  <br>
  <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/inverterext.jpg?raw=true" style="width:700px;">  <br>
   <br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/images2/netgen.jpg?raw=true" style="width:600px;"><br>
   <br>
 
  </p>
 
<h2>Day 2 Lecture Summary: Introduction to DRC and LVS</h2>
<p>This is a paragraph.</p>
 
<h2>Day 2 Lab: Labs for GDS readwrite, extraction, DRC, LVS and XOR setup</h2>
<p>This is a paragraph.</p>
 
<h2>Day 3 Lecture Summary:  Front-end and back-end DRC</h2>
<p>This is a paragraph.</p>
 
<h2>Day 3 Lab: Labs for all DRC rules </h2>
<p>This is a paragraph.</p>
 
<h2>Day 4 Lecture Summary: Understanding PNR and physical verification </h2>
<p>This is a paragraph.</p>

<h2>Day 5 Lecture Summary: Fundamentals of LVS </h2>
<p>This is a paragraph.</p>
 
<h2>Day 5 Lab: LVS Labs </h2>
<p>This is a paragraph.</p>

</body>
</html> 
