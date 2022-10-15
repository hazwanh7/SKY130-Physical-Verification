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
 Introduction to Skywwater PDK
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
 1. Open terminal: Right click anywhere (eg. Desktop) and click ' <b>Open Terminal</b>'.<br>
 2. Type 'magic' to open Magic as below:<br>
 <img src="https://github.com/hazwanh7/SKY130-Physical-Verification/blob/main/images/magic_open.jpg?raw=true" style="width:200px;"> <br>
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
