---
layout: post
title: 3D Modeling and remixing using Fusion360
---

## The process

For project 3, we're supposed to make a sound controlled LED light. The LEDs should flicker when sound is recorded through the microphone component. We are provided with all the parts, and I started soldering once I turned on the soldering iron.
<br>
<br>
I first put the LEDs in, making sure to get the positive legs (the longer ones) in the right direction. Then I put the soldering iron on the pad and the legs, heating them up, and then applying solder to it. I like to move the iron along the legs to remove the sharp tip it might create otherwise. I did this to all the components. I had a little trouble soldering the battery case wires to the stand though, so I did it to the bottom soldering pads.
<br>
[![led1](/picture/3d-print-4/led1.jpg)](/picture/3d-print-4/led1.jpg)
<br>
For the case, I first created a sketch on my notebook, and I plan to glue them all together after the print is finished. The measurements were accurate, and I left 2mm of thickness for each side of the boxes.   
[![sketch1](/picture/3d-print-4/sketch.jpg)](/picture/3d-print-4/sketch.jpg)
When making the models, I added 2mm to each side of the print, but I forgot to add 2mm to each side for the PCB holder, and that caused a lot of trouble later on. 
<br><br>
I used the extrude tool and hole tool to make these three parts.
[![fusion-1](/picture/3d-print-4/fusion1.jpg)](/picture/3d-print-4/fusion.jpg)
Here is the first box that was 2mm too small on each side, causing the PCB to not fit.
[![fail-1](/picture/3d-print-4/fail1.jpg)](/picture/3d-print-4/fail1.jpg)
So I imported them all into prusa slicer, and scaled the part which I forgot to add 2 mm and sized it to 110%. This should do the trick.
[![fail-1](/picture/3d-print-4/3dprint.jpg)](/picture/3d-print-4/3dprint.jpg)
Sometimes I find it easier to fix the problem with a dumb solution, and if it doesn't work just do it again from scratch. This way I can learn a lot more than I thought I will.<br>
Thank you for reading!
<br><br>