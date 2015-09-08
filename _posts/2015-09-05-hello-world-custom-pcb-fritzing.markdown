---
layout: post
title: ! 'Hello World: Design PCBs with Fritzing'
date: '2015-09-05 16:26:00'
---

##### This post is part of the [Hello World Projects](/helloworld).

---

The simple breadboard with a messy, beautiful rainbow of wires sticking this way and that. Easy enough! But now, how does one tidy things up? 

Why, **printed circuit boards**, of course! You know, those green things with lines all over them. Don't worry. It's not that hard. Meet Fritzing, your friendly PCB designer. [Fritzing](http://fritzing.org/download/) is kind of like LEGOs of PCB design. 

[Download Fritzing Here.](http://fritzing.org/download/) 

<div class="guide-step">
  <div class="guide-images">
    <img src="/content/images/2015/09/breadboard1_an.png" data-caption="breadboard view"/>
    <img src="/content/images/2015/09/breadboard2.png" data-caption="components added" />
    <img src="/content/images/2015/09/breadboard3_an-1.png" data-caption="changing wire colors & adding bend points" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 1: Breadboard Layout</h2>
    <ul>
      <li>Open Fritzing</li>
      <li>Add components to the workspace</li>
      <li>Click and drag to add wires</li>
      <li>Change wire colors</li>
      <li>Add bend points to wires by clicking & dragging</li>
    </ul>
    Bonus: Take a screenshot or save as image file--helpful for sharing projects or documenting your work. 
  </div>
</div>


<div class="guide-step">
  <div class="guide-images">
    <img src="/content/images/2015/09/pcb1_an.png" data-caption="default view" />
    <img src="/content/images/2015/09/pcb_an.png" data-caption="" />
    <img src="/content/images/2015/09/pcb_via-1.png" data-caption="vias" />
    <img src="/content/images/2015/09/pcb3.jpg" data-caption="click on any point to see where the trace hits" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 2: Design the PCB</h2>
    <strong>1. Click the PCB tab</strong><br />
    <strong>2. Route wires</strong> so the traces don't cross
    <ul>
      <li>Drag dotted lines to make traces</li>
      <li>Right click trace to move trace between layers</li>
      <li>Right click bend point to make a via, which connects the two layers</li>
      <li>Click on bendpoints or connection points to see where the trace travels</li>
    </ul>

    <strong>3. Resize the board</strong>
    <ul>
      <li>Drag corners of the board</li>
    </ul>

    <strong>4. Adjust the text</strong>
    <ul>
      <li>Click the component, you'll see dotted lines around the component</li>
      <li>Drag label to reposition</li>
      <li>Right click to change rotation</li>
      <li>Double click to change the text</li>
    </ul>

  </div>
</div>



<div class="guide-step">
  <div class="guide-images">
    <img src="/content/images/2015/09/pcb8_routing.jpg" data-caption="routing options"/>
    <img src="/content/images/2015/09/pcb8_view.jpg"  data-caption="view options"/>
  </div>
  <div class="guide-text">
    <h3 class="guide-title">Additional Options</h3>
    <strong>Routing options</strong>
    <ul>
      <li><strong>Design rule check: always use this before sending PCB to fab</strong></li>
      <li>Autorouter/design rule settings</li>
      <li>Autoroute: I don't use this much</li>
    </ul>
    <strong>View options</strong>
    <ul>
      <li>Set Grid Size</li>
      <li>Align to Grid: snaps wires/components to the grid</li>
    </ul>
  </div>
</div>


<div class="guide-step">
  <div class="guide-images">
    <img src="/content/images/2015/09/pcb9.jpg" data-caption=""/>
    <img src="/content/images/2015/09/finder.jpg" data-caption="zip up all gerber files"/>
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 3. Export Gerber File</h2>
    <ul>
      <li>Click arrow next to "Export to PCB"</li>
      <li>Click "Extended Gerber"</li>
      <li>Zip all Gerber Files for uploading to PCB factory</li>
    </ul>
  </div>
</div>

<div class="guide-step">
  <div class="guide-images">
    <img src="/content/images/2015/09/oshpark.png" data-caption=""/>
    <img src="/content/images/2015/09/oshpark2_an.png" data-caption=""/>
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 4. Order PCBs from a Service Provider</h2>
    I like <a href="http://oshpark.com">OSHPark</a>. They are a bit slow (~2 weeks to Seattle), but very cheap for small boards ($5/inch2).
  </div>
</div>

## Other PCB Prototyping Companies

I did a few searches, and found some good options. These are quotes based on shipping a 2 layer 1.5x1.7 inch board to Seattle, WA. Actual mileage may vary depending on your design and location. 

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

You can also use [PCB Shopper](http://pcbshopper.com/) to compare price and lead time across other manufacturers. Though, I've found that some of the prices are off. Especially shipping prices, which can account for a good chunk when ordering small batches from China. 

Cool? Cool. Now go make things. 

