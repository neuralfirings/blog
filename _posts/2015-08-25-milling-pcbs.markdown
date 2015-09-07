---
layout: post
title: Milling PCBs
date: '2015-08-25 06:03:30'
---

Well, the nice folks at [SoDo MakerSpace](http://sodo.ms) got me started on the CNC Mill and Laser Cutter. 

I used the smaller mill, a Shapeoko 2, to mill some PCBs. And by "some," I mean "one." Well, the first one broke into a hot mess. So I guess it was "some" after all. Don't get too excited, 'twas  but a simple hello world PCB (read: Battery > Resistor > LED).

I used [Richard Albritton's PCB-GCode Tutorial](www.richa1.com/RichardAlbritton/create-g-code-from-an-eagle-file/). PCB-Gcode is an Eagle add on. Yes. This means you need EagleCAD. The add on outputs to GCode, which the CNC can understand. There's a bunch of settings that Richard has fiddled around and tweaked for optimum optimumcy for the Shapeoko 2.

And drumroll...... 

### Top Layer Copper Path Outline

bzzzzzz bzzzzzzz

<iframe class="macdown-hide imgur-embed" width="100%" height="404" frameborder="0" src="http://i.imgur.com/Aiqasn9.gifv#embed"></iframe>

### Drilling Through Holes

boop! boop! boop!

<iframe class="macdown-hide imgur-embed" width="100%" height="404" frameborder="0" src="http://i.imgur.com/bRqK82h.gifv#embed"></iframe>


### Bottom Layer Copper Path Outline

Say what?! Yup! I did a two layer PCB with two tiny vias. I wanted to see if I can do a two sided PCB b/c I'm not patient enough to just route with one side. 

<iframe class="macdown-hide imgur-embed" width="100%" height="404" frameborder="0" src="http://i.imgur.com/h7XIdB2.gifv#embed"></iframe>

### ... and it works!

![](/content/images/2015/08/ledmill_front.jpg)

![](/content/images/2015/08/ledmill_back.jpg)

# ZOMG IT'S A CLOSE UP!

![](/content/images/2015/08/ledmill_02.jpg)

The routes are 16 mils, and it measures pretty accurate. Hooray!

---

I'm starting to use Eagle for a few things, and I know it's the more "professional" choice, but man do I enjoying using Fritzing!

So next up, using Fritzing to generate millable SVGs. Maybe even see if my bits has enough resolution to mill an Intel Edison breakout. Gasp.

Stay tuned dot dot dot.