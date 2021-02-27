# Shopbot-control-MATLAB
 MATLAB GUI for coordinating Shopbot CNC, Fluigent pressure controller, and cameras


All of the code for this GUI can be found in supportgui2.mlapp, which is built for MATLAB in appdesigner. You can use this file by running "appdesigner" in the MATLAB command line, then opening the .mlapp file.

The code is built to run a custom 3D printer built from:
-- A shopbot desktop CNC mill, for stage movement
-- A Fluigent MFCS mass flow controller, for extruding ink via air pressure
-- Webcams
-- Scientific (PointGrey/FLIR) cameras

The cameras allow for in-situ imaging of the nozzle during printing. 

The Shopbot is controlled by Sb3 software, which can receive commands from the command line. Sb3 software uses .sbp files, which are similar to .gcode files, but use a command dictionary that is tailored to CNC mills. Shopbots are also capable of running .gcode files. The MATLAB program generates .sbp files and tells the Sb3 software to run them. Within the .sbp files are commands to set output flags, which are stored as Windows Registry Keys. The MATLAB program can watch the keys and respond to changes. We use those output flags to signal to the Fluigent that it is time to start and stop flow on the available pressure channels. Alternatively, we can use those flags to signal to the camera that it is time to take a picture. A more detailed description of how this works is available in Leanne Friedrich's dissertation: http://leanfried.com/LF_dissertation.pdf

The .sbp files in this folder are sample files which are designed to write polygons on a slide. Slide1.sbp is the actual file that gets sent to the shopbot. slide1_base.txt is a more generic version of slide1.sbp that is missing some state variables like the print speed, allowing the GUI to more rapidly produce .sbp files. slide1_pics.sbp is a script for taking pictures of already printed slides. slide1_pics_base.txt is a more generic version of slide1_pics.sbp that is missing some state variables like the origin location.
