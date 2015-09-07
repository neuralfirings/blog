---
layout: post
title: Making Custom PCBs
date: '2015-06-26 05:18:23'
---

<div class="box-danger">
PLEASE NOTE: I've written a <a href="http://blog.nyl.io/hello-world-custom-pcb-fritzing/">new and improved version of this guide</a>.<br /><br />Yeah! Updates!!</div>

We've all see something like this before. 

![](/content/images/2015/06/v2.jpg)

The simple breadboard with a messy, beautiful rainbow of wires sticking this way and that. This part of [a project](http://blog.nyl.io/dog-treat-dispenser-v3/) is where I control a stepper motor, which tells the dispenser to twist the fan looking thing and dispense a treat. Luckily, Adafruit has published [this exact tutorial](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-10-stepper-motors/overview). So I followed the Adafruit tutorial and plugged in a whole bunch of wires where the tutorial told me to plug. Easy enough! But now, how does one tidy things up? 

Why, **printed circuit boards**, of course! You know, those green things with lines all over them. Don't worry. It's not that hard. 

## Meet Fritzing, your friendly PCB designer

[Fritzing](http://fritzing.org/download/) is kind of like LEGOs of PCB design. It's simple, good for learning. A stepping stone to Eagle or KiCAD. 

### Step 1: Virtual Breadboard

This is my favorite part of Fritzing. As a novice hardware hacker, it helps that I start with something I already have working: breadboards and jumper wires. 

![](http://blog.nyl.io/content/images/2015/06/fritzing_breadboard-1.png)

With Fritzing, you start with a virtual breadboard set up. Click the "Breadboard" tab. Here, you can search for various components, like "breadboard" and "Raspberry Pi" and "L293D" (the motor driver I used). 

Add components to the workspace. Then click to start dragging wires around. Protip: press the control (Windows) or cmd (Mac) key to make the wires all bendy... just like in real life. 

### Step 2: Schematics

If you switch to the Schematics tab, you'll see an outline of the schematics. But... I didn't really deal with this view very much. So let's skip it. =P

### Step 3: PCB

Now we get to the fun part! When you open up the PCB view, you should see something like this. 

![](/content/images/2015/06/fritzing_pcb-1.png)

This is just the components you selected. Well, they are holes to plug in the components you selected. 

The dotted lines represent where the connections should go. Our goal is to turn these dotted line (airwires) into routes. To do this, just drag a dotted line into place. 

![](/content/images/2015/06/Pasted_Image_6_25_15__1_15_AM.png)

The goal is to create a board without any routes criss crossing with another route. That would be bad. Electricity would ram into one another and we will not have a good time. 

One way to tackle this is to use multiple layers. For me, 2 layers was sufficient to route all the airwires without anything crossing. 

To connect a route on the top layer with one on the bottom layer, you use via. As in, go from top to bottom via this connection. To do this add a bend point by right clicking on route then clicking "Add a Bendpoint." Then, right click on the bend point and choose "Convert Bendpoint to Via." Then you can right click on different parts of the route to move between layers. 

![](/content/images/2015/06/Pasted_Image_6_25_15__1_19_AM.png)

Eventually, all your routes come together nice and cleanly. You can check that your routes are indeed error free by using the nifty design checker (Tool Bar > Route > Design Rule Check). 

I ended up with something like this. 

![](/content/images/2015/06/Pasted_Image_6_25_15__1_25_AM-1.png)

The dots on top is just a marking I made to tell me which pins I need to solder. Or more importantly, which pins I can use as practice. My soldering skills are... lacking. 

You can add text (like the dots or the "badwolf v3" in the bottom left) by searching for "silkscreen" under the Parts section in the right toolbar. 

## Production

Now that we have a PCB sketch, let's get to making. 

What I ended up doing is exporting to Gerber files. It's a series of files that tells the machine where to drill holes, how to label things, and of course where to put down the copper so your precious electricity can flow to their rightful homes.

You can preview your Gerber files to make sure they work using [GerbLook](http://www.gerblook.org).

### PCB Prototyping Companies

I did a few searches, and found some good options. This is based on:

* shipping to Seattle 
* 2 layer board 
* board that measures 1.5x1.75 in<sup>2</sup>. 

Actual mileage may vary depending on your design. 

<table style="font-size: 0.75em">
<tr style="font-weight: bold"><td>Company</td><td>QTY</td><td>Lead Time (to Seattle)</td><td>Price</td><td>Limits/Pricing</td></tr>
<tr><td><a href="http://oshpark.com">OSHPark</a></td><td>3</td><td>10-14 business days<br />8-12 production + 2 shipping</td><td>$12<br />$12 PCB + $0 shipping</td><td>$5/in<sup>2</sup></td></tr>
<tr><td><a href="http://pcbnet.com">PCBNet</a></td><td>1</td><td>9 BDs<br />5 prod + 4 shipping</td><td>$25<br />$25 PCB + $0 shipping</td><td>under 60in<sup>2</sup></td></tr>
<tr><td><a href="http://imall.iteadstudio.com">ITEAD</a></td><td>10</td><td>6 BDs<br />4 prod + 2 shipping</td><td>$28<br />$10 PCB + $18 shipping</td><td>under 5x5cm<sup>2</sup></td></tr>
<tr><td><a href="http://imall.iteadstudio.com">ITEAD</a></td><td>10</td><td>20 BDs (could be longer)<br />4 prod + 16-? shipping</td><td>$15<br />$10 PCB + $5 shipping</td><td>under 5x5cm<sup>2</sup></td></tr>
<tr><td><a href="http://seeedstudio.com">SeeedStudio</a></td><td>1</td><td>18-48 BDs<br />3 prod + 15-45 shipping</td><td>$15<br />$10 PCB + $5 shipping</td><td>under 5x5cm<sup>2</sup</td></tr>
<tr><td><a href="http://seeedstudio.com">SeeedStudio</a></td><td>1</td><td>5 BDs<br />3 production + 2 shipping</td><td>$40<br />$10 PCB + $30 shipping</td><td>under 5x5cm<sup>2</sup></td></tr>
<tr><td><a href="http://fr.com">Fritzing</a></td><td>1</td><td>17-25 BDs<br />7-11 production + 10-14 shipping</td><td>$21<br />$17 PCB + $4 shipping</td><td>$5.20 + $0.96/cm<sup>2</sup></td></tr>
</table>

In the US, the fastest/cheapest seem to be OSHPark if you have small boards. OSHPark (stands for open source hardware park) charges by the square inch. So if you have a tinyass board like my dog treat thing, it's only $12 or less. If you have a 3x3in<sup>2</sup> board though, it's $45, even though each side only doubled in length. Yay. Behold the power of exponents. 

I ordered from ITEAD. Paid a little extra for DHL Express. Still, it came down to about $3/PCB since they ship 10 QTY. I did end up having to use an extra PCB because I'm apparently the kind of idiot who solders things backwards the first time around. 

![](http://blog.nyl.io/content/images/2015/06/01_boards.jpg)

Not bad, eh? 

Ok. Now go and make stuff. 
