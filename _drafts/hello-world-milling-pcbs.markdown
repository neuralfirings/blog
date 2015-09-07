---
layout: post
title: Hello World, Milling PCBs
---

##### This post is part of the [Hello World Projects](/helloworld).

---

There are many ways to create custom PCBs (printed circuit boards). I like milling because the CNC mill can etch the traces, drill the through-holes, and cut the board all with one machine. All in a few minutes if your board is small. 

![](/content/images/2015/09/tracetest_an.jpg)

My friendly neighborhood [SoDo MakerSpace](http://sodo.ms) has a Shapeoko 2, which I've been using. In this tutorial, I'll show you how mill some PCBs. 

---

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Ingredients</h2>
    <strong>Software</strong>
    <ul>
      <li><a href="http://fritzing.org/download/">Fritzing <i class="fa fa-external-link"></i></a></li>
      <li><a href="https://inkscape.org/en/download/">Inkscape <i class="fa fa-external-link"></i></a></li>
      <li><a href="http://www.makercam.com/">MakerCAM <i class="fa fa-external-link"></i></a> (website)</li>
    </ul>
    <strong>Hardware</strong>
    <ul>
      <li><a href="http://amzn.to/1VFUA9e">Engraving Bit (20<sup>o</sup>, 0.2mm) <i class="fa fa-external-link"></i></a></li>
      <li><a href="http://amzn.to/1ip1txr">Drill Bit (0.9mm) <i class="fa fa-external-link"></i></a></li>
      <li><a href="http://amzn.to/1Uzp8qR">Square Nose Endmill (1/16 inch) <i class="fa fa-external-link"></i></a></li>
      <li><a href="https://www.inventables.com/technologies/circuit-board-blanks">Copper FR1 Boards <i class="fa fa-external-link"></i></a>, NOT FR4!! <tip class="fa  fa-question-circle" data-content="FR4 is made with fiberglass. When milled, little bits of fiberglass can get inside your lungs and if that happens, you're going to have a bad time." /></li>
      <li><a href="http://www.shapeoko.com/">Shapeoko 2 <i class="fa fa-external-link"></i></a> running on GRBL</li>
    </ul>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 1: Export to SVG</h2>
    In Fritzing:
    <ul><li>Export SVG: <click>Export PCB > Etchable SVG</click></li></ul>
    <br />
    <div class="fa-bullet"><i class="fa fa-external-link"></i>
      <a href="">How to design PCBs with Fritzing <i class="fa fa-external-link"></i></a>.
    </div>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 2: Process SVG with InkScape</h2>
    <ul>
      <li>Open InkScape (<a href="">download <i class="fa fa-external-link"></i></a>)</li>
      <li><click>Edit > Select All (Ctrl+A)</click></li>
      <li><click>Object > Ungroup (Ctrl+Shift+G)</click>, repeat until you see "No groups to ungroup" in the bottom</li></ul>
      </li>
      <li>[Optional] <click>View > Outline</click> <tip class="fa fa-question-circle" data-content="This is so you can see the difference in the following step" /></li>
      <li><click>Path > Stroke to Path</click></li>
      <li><click>Path > Union</click></li>
      <li><click>File > Save As > *.svg</click></li>
    </ul>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 3: Open SVG with MakerCam</h2>
    <ul>
      <li>Go to <a href="http://makercam.com">makercam.com <i class="fa fa-external-link"></i></a></li>
      <li>Open SVG: <click>File > Open SVG</click></li>
    </ul>
    <br />
    <strong>Some Navigation Tips</strong>
    <ul>
      <li> To Pan: <click>Toolbar > Hand Icon</click></li>
      <li> To Zoom: <click>Toolbar > Plus/Minus Icon</click> or Scroll Up/Down</li>
      <li> To Select: <click>Toolbar > Arrow Icon</click>, then click or click+drag to select</li>
    </ul>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 3: Make Copper Trace</h2>
    <ul>
      <li>Select copper trace outlines</li>
      <li>Create Profile <click>CAM > Profile</click></li>
    </ul>
    <table class="small">
      <tr><th>Profile for Traces</th><th><12 mil</th><th>>12 mil</th></tr>
      <tr><td>tool diameter (in)</td><td>0.01</td><td>0.008</td></tr>
      <tr><td>target depth (in)</td><td>0.008</td><td>0.006</td></tr>
      <tr><td>inside/outside</td><td colspan=2>Outside</td></tr>
      <tr><td>safety height (in)</td><td colspan=2>0.5
        <tip class="fa fa-question-circle" data-content="You should tweak this number to match your set up. If you have jigs or other items that exceed 0.5 inches, for example, increase this number!" />
      </td></tr>
      <tr><td>stock surface (in)</td><td colspan=2>0</td></tr>
      <tr><td>step down (in)</td><td>0.004</td><td>0.003</td></tr>
      <tr><td>feedrate (in/min)</td><td colspan=2>6</td></tr>
      <tr><td>plunge rate (in/min)</td><td colspan=2>10</td></tr>
      <tr><td>direction</td><td colspan=2>counter clockwise</td></tr>
    </table>
    <div class="fa-bullet"><i class="fa fa-gear"></i> Tool: Engraving Bit (20 deg, 0.2mm)</div>
  </div>
</div>
<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 4: Make Through Hole</h2>
    <ul>
      <li>Select through hole outlines</li>
      <li>Create Profile: <click>CAM > Drill Operation</click></li>
    </ul>
    <table class="small">
      <thead><th colspan=99>Through Hole Profile:</th></thead>
      <tr><td>tool diameter (in)</td><td>0.035433</td></tr>
      <tr><td>target depth (in)</td><td>0.075</td></tr>
      <tr><td>drill location</td><td>path center</td></tr>
      <tr><td>hole spacing (in)</td><td>0.5</td></tr>
      <tr><td>safety height (in)</td><td>0.5</td></tr>
      <tr><td>stock surface (in)</td><td>0</td></tr>
      <tr><td>peck distance (in)</td><td>0.05</td></tr>
      <tr><td>plunge rate (in/min)</td><td>5</td></tr>
    </table>
    <div class="fa-bullet"><i class="fa fa-gear"></i> Tool: Drill Bit (0.9mm)</div>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 5: Make Board Outline</h2>
    <ul>
      <li>Select through hole outlines</li>
      <li>Create Profile: <click>CAM > Profile Operation</click></li>
    </ul>
    <table class="small">
      <thead><th colspan=99>Board Outline Cut Profile:</th></thead>
      <tr><td>tool diameter (in)</td><td>0.0625</td></tr>
      <tr><td>target depth (in)</td><td>-0.075</td></tr>
      <tr><td>inside/outside</td><td>Outside</td></tr>
      <tr><td>safety height (in)</td><td>0.5</td></tr>
      <tr><td>stock surface (in)</td><td>0</td></tr>
      <tr><td>step down (in)</td><td>0.015</td></tr>
      <tr><td>feed rate (in/minute)</td><td>6</td></tr>
      <tr><td>plunge rate (in/minute)</td><td>10</td></tr>
      <tr><td>direction</td><td>Counter Clockwise</td></tr>
    </table>
    <div class="fa-bullet"><i class="fa fa-gear"></i> Tool: Square Endmill (1/16 in)</div>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 6: Calculate GCode</h2>
    <ul>
      <li><click>Cam > Calculate All</click></li>
    </ul>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 7: Add Tabs</h2>
    <ul>
      <li>Select Board Outline Path</li>
      <li>Add Tabs: <click>CAM > Add Tab to Selected</click>
    </ul>
    <table class="small">
      <tr><th colspan=99>Tab Settings</th></tr>
      <tr><td>tab spacing (in)</td><td>1</td></tr>   
      <tr><td>tab width (in)</td><td>0.05</td></tr>
      <tr><td>tab height (in)</td><td>0.25</td></tr>
    </table>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 8: Export GCode</h2>
    <ul>
      <li><click>Cam > Export GCode</click></li>
      <li>Select one path at a time</li>
      <li>Click "Export Selected Toolpath"</li>
    </ul>
    <br />
    <table class="small">
      <tr><th colspan=99>Tools to use during CNC</th></tr>
      <tr><td>traces</td><td>engraving bit (20 deg, 0.2mm)</td></tr>
      <tr><td>holes</td><td>drill bit (0.9 mm)</td></tr>
      <tr><td>board</td><td>square endmill (1/16 in)</td></tr>
    </table>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h3 class="guide-title">Check Your Code</h3>
    <ul>
      <li>Go to: <a href="http://nraynaud.github.io/webgcode/">G-Code Q'n'dirty Simulator <i class="fa fa-external-link"></i></a></li>
      <li>Copy/Paste the GCode (.nc) text data into left box <tip class="fa fa-apple" data-content="For Mac users, just drag in the GCode (.nc) file." />
      </li>
      <li>Click Simulate Button</li>
    </ul>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 9: Mill It!</h2>
    <ul>
      <li>Clamp board in</li>
      <li>Turn Shapeoko On</li>
      <li>Unlock <a href="http://zapmaker.org/projects/grbl-controller-3-0/">GRBL Controller <i class="fa fa-external-link"></i></a> <tip class="fa fa-info-circle" data-content="You can use other GCode senders, of course, but the GRBL is the one I'm most familiar with." /></li>
      <li>Click <c>Choose File</c> button</li>
      <li>Bring Engraving Bit to touch the surface of the board</li>
      <li>Click the "Start" button</li>
    </ul>
    <br />
    <div class="fa-bullet"><i class="fa fa-repeat"></i> Repeat for through holes (w/ drill bit), then the board cut (w/ endmill)</div>
    </ul>
  </div>
</div>


<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 10: Snap the Tabs</h2>
    Snap and you're set!
  </div>
</div>

#### Related Tutorials:
- [Hello World, Custom PCBs with Fritzing](http://blog.nyl.io/hello-world-custom-pcb-fritzing/)

Got it? Got it. Now go make things. 

<!--
<div class="guide-step">
  <div class="guide-images">
    <img src="http://www.nyl.io/temp.jpg" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title"></h2>
    <ul>
      <li></li>
    </ul>
  </div>
</div>
-->
