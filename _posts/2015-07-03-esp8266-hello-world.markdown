---
layout: post
title: Hello (ESP8266) World
date: '2015-07-03 17:32:04'
---

Yesterday, I sat down and played with my shiny new ESP8266 module. I also got the [Huzzah Breakout Board](http://adafruit.com/products/2471) from Adafruit, which uses an ESP module. Actually, I'm still trying to figure out just what is the difference between ESP8266, Huzzah, and NodeMCU.

So far, I've accomplished the following:

* Gotten an LED to blink on the Huzzah
* Gotten the Huzzah to read not one, but TWO webpages

<iframe class="imgur-embed" width="100%" height="404" frameborder="0" src="http://i.imgur.com/RPGykw3.gifv#embed"></iframe> 

### The hardware wirings
![](/content/images/2015/07/huzzahblink.jpg)

I'll post more interesting projects later when I have more time to fiddle.

### The code

I use [CoolTerm](http://freeware.the-meiers.org/) for Mac and followed [Adafruit's tutorial](https://learn.adafruit.com/adafruit-huzzah-esp8266-breakout).

1. Click Options
1. Plug in USB
1. Click "Re-Scan Serial Ports"
1. Set Port dropdown to "usbserial-blahblah"
1. Set Baudrate to 9600
1. Click Terminal (left side)
1. Check the "Handle BS and Del Character," without which I can't use backspace[^n].
1. Click OK
1. Click Connect 
1. Type in the following code line by line

```
gpio.mode(5, gpio.OUTPUT)
while 1 do
  gpio.write(5, gpio.HIGH)
  tmr.delay(1000000)   -- wait 1,000,000 us = 1 second
  gpio.write(5, gpio.LOW)
  tmr.delay(1000000)   -- wait 1,000,000 us = 1 second
end
```

As for the ESP8266? Well, I got the ESP8266 plugged into my laptop... that's it.

Yeah, still need work here. I would like to just use the ESP because I can get these for $2 on Ebay. I mean, the Huzzah breakout isn't going to break the bank. It's only $10 on Adafruit. But still, that's a 20% decrease in my BOM[^n]!

I think I will continue to fiddle around with Adafruit's Huzzah Breakout. It would be nice to figure out how to hook the ESP8266 module directly to an Arduino or something, but I'm not sure what's the deal with that right now. 

[^n]: Sidenote: I had no idea how many typos I made. I rely on the backspace a LOT!
[^n]: bill of materials = BOM