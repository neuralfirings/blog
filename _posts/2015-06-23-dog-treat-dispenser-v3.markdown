---
layout: post
title: Internet Dog Treat Dispenser (v3)
date: '2015-06-23 16:36:47'
---

Once upon a time, a few dog people (people who love dogs, not dog+people hybrids) made a remote controlled dog treat dispenser. You know, because that's what dog people do at hackathons. Things like this:

[![](/content/images/2015/06/v1.jpg)](http://ajaxthedog.com/post/29945882455/)

It dispenses treats with a text message. The Arduino is connected to the computer, which listens for the text. 

[Version 2](http://blog.nyl.io/remote-dog-treat-dispenser-v2/) was a little tidier. We made it using a Raspberry Pi instead of a computer, which meant it didn't have to be tethered to a computer. It plugs right into a an USB wall output or battery pack. 

![](/content/images/2015/06/v2.jpg)

Now, V2 was nice and dandy, but it was still messy. I mean, look at all those wires. So I decided to fix that. By making a custom PCB (printed circuit board). I mean, **how hard can it be?**

It turns out: **not that hard!** Nowadays, with better software, the internet to connect you with manufacturers, it's getting easier and easier. 

## V3: Internet Dog Treat Dispenser

For the electronics, I used [Fritzing](http://fritzing.org/home/), which is an open source, free schematics and PCB designer. I like it because you start with a visual representation of the breadboard, Raspberry PI, and whatever components. You drag and drop the exact components you need and wire it up exactly how you'd wire it up in real life. From there, the virtual wiring turns into schematics and PCB layout. 

### Step 1: Real World
![](/content/images/2015/06/v2_realworld.jpg)

### Step 2: Virtual Bread Board
![](/content/images/2015/06/fritzing_breadboard-1.png)

### Step 3: PCB!
![](/content/images/2015/06/fritzing_pcb.png)

Routing the PCB was kind of fun, like solving a puzzle. 

Fritzing exports to Gerber files, which most PCB manufacturers take. I spent a little while Googling around for cheap PCB prototypers (low volume, relatively quick turnaround). I ended up using [ITEAD](http://imall.iteadstudio.com/) in Shenzhen. For a PCB of this size (1.5x1.75 inches), they will produce 10 QTY for $10. Not a bad deal. 

For a more detailed write up of how I made Custom PCBs, check out [this blog post](http://blog.nyl.io/making-custom-pcbs/). The Fritzing and Gerber files are available on [this project's GitHub Page](https://github.com/neuralfirings/badwolf). 

There were a few places that had cheap PCBs, most of them are based in China. The kicker is the shipping. The main reason I went with ITEAD was because they offered the "cheapest" expedited shipping options--$18 for DHL Express 3 Days. 

Fast forward a week (it took them 6 business days from order to delivery!), I got a fresh pack of custom PCBs from China!!

![](/content/images/2015/06/01_boards.jpg)

A few headers here, a few <small>crappy</small> soldering there...

![](/content/images/2015/06/02_boardassembly.jpg)

## BAM! ELECTRONICS!

![](/content/images/2015/06/03_board.jpg)

One end has a 13x2 pin Raspberry Pi header. There's also 6 positive headers sticking out for the stepper motor. So, plug it into a Raspberry Pi, which is sitting in a cushy 3D printed box. Then plug the stepper motor into the PCB..

![](/content/images/2015/06/04_plugitin.jpg)

Add some more 3D printed parts (all designed in [Blender](http://blender.org) by the way)

![](/content/images/2015/06/05_fan.JPG)

Woo!!! Remote control dog (or human) treat dispenser!!! 

![](/content/images/2015/06/06a_openlid.jpg)

One USB connects to a webcam, and a micro USB connects to power. Best of all? No messy wires, no scotch tape. 

It comes with a nifty web interface, so you can see and hear a live stream of your nice or naughty pet. Give treats according.

![](/content/images/2015/06/09_screenshot.png)

<img src="/content/images/2015/06/07_dispense_open_lo.gif" style="width: 100%" />

Then put the lid on, and you're ready to rumble. 

![](/content/images/2015/06/06c_closelid.jpg)

---

## Want more details? I'll give you more details.

* [Detailed write up on the Electronics part](http://blog.nyl.io/making-custom-pcbs/)
* Coming soon: Detailed write up on 3D printing the case
* Coming soon: Detailed write up on the software piece (I used Python, Node.js, Regular ol' front end JavaScript)