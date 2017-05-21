Face-Miller is a CNC programming utility that creates a climb milling CNC program which can be used to machine a rectangular flat surface. The output CNC program can be interpreted by a 3-axis CNC machine running [GRBL](https://github.com/grbl/grbl), and the toolpath can be visually previewed at [Q'n'dirty toolpath simulator](https://nraynaud.github.io/webgcode/).

Here is a preview image of a toolpath generated by Face-Miller. The view is from a diagonal perspective to the flat surface of the face. Feed motions are represented with white lines. Rapid motions are represented with pink and red lines.
![Toolpath Preview](/img/Toolpath-Preview.png)


[Click here for a link to a video sample](https://www.youtube.com/watch?v=xK7AqyGdtgA) of a CNC router running a program generated by Face-Miller.


Here is an image of a series of pads that were machined using CNC programs generated by Face-Miller. These pads eventually served as a base for mounting a workholding table which is parallel to the mill's XY plane.
![Use Case](/img/Use-Case.png)

In order to run Face-Miller and generate a CNC program, you must first be able to navigate your computer's file directory and execute commands from a shell, and you must have Ruby 2.0.0 installed. Other Ruby versions may work as well, but are untested.

To run Face-Miller, first download the .zip file and extract the contents to a directory of your choice. Then, access that directory with your shell, navigate into the ./bin directory, and execute:

```bash
ruby Face-Miller.rb
```

You will then be prompted to provide geometry and machining parameters. Type in your parameter value and press enter. Once you have finished providing inputs, a CNC program will appear in your shell. This program only controls feed motions and feedrate speeds. Other control-specific parameters, such as spindle speed, coolant control, tool numbers, etc. will have to be manually added to this program before running it in the CNC machine. You can preview the toolpath by copying and pasting the CNC program into [G-Code Q'n'dirty toolpath simulator](https://nraynaud.github.io/webgcode/).

Here is an example of a shell session for generating the CNC program: 

ruby Face-Miller.rb

What is the length of the material to be face-milled in the X direction?
3.0

What is the length of the material to be face-milled in the Y direction?
3.0

What is the tool radius?
0.125

What is the radial depth of cut?
0.225

What is the feedrate?
15.0

At the end of the program, the tool will retract to a safe height above the material before rapid motion to (X=0, Y=0).
What is the safe height for rapid XY motion?
0.25

CNC mill setup instructions: The tool will rapidly approach the workpiece in the +X direction from the -X direction. It will then start cutting in the +Y direction. On the machine, X=0 and Y=0 should be set to the furthest -X and -Y point on the workpiece, with empty space on the -X side of the workpiece. Before running your CNC program, move the tool to the empty space to the -X side of the workpiece, and set your tool at the Z depth for your desired axial depth of cut.

Here is your CNC program: (Edit this to add spindle speed, coolant control, tool numbers, etc. as necessary)

   G0X-0.25Y-0.25  
   G1X0.1Y0.1F15.0  
   G1Y2.9  
   G1X2.9  
   G1Y0.1  
   G1X0.325  
   G1Y2.675  
   G1X2.675  
   G1Y0.325  
   G1X0.55  
   G1Y2.45  
   G1X2.45  
   G1Y0.55  
   G1X0.775  
   G1Y2.225  
   G1X2.225  
   G1Y0.775  
   G1X1.0  
   G1Y2.0  
   G1X2.0  
   G1Y1.0  
   G1X1.225  
   G1Y1.775  
   G1X1.775  
   G1Y1.225  
   G1X1.45  
   G1Y1.55  
   G1X1.55  
   G1Y1.45  
   G91G0Z0.25  
   G90  
   G0X0.0Y0.0  

This application was authored by Nick Edwards in 2015-2016. To contribute to this code base, create a pull request to https://github.com/edwardsCNC/Face-Miller
