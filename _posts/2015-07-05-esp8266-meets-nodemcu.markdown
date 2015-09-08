---
layout: post
title: ESP8266 meets NodeMCU
date: '2015-07-05 02:04:48'
---

Yesterday, I made great progress on playing around with the [ESP8266, the $2 Wifi Module](http://www.ebay.com/itm/151657399118)[^n]. I will continue to document my progress on this blog. First, I just want a place to dump all my notes. That way, if (when) shit start burning, I can at least replicate what I know to work. Second, other people might find it useful and if I can help you avoid some of the headaches I went through, then all the better. 

---

## The Hardware
### ESP8266
Ah, the [ESP8266, the $2 Wifi Module](http://www.ebay.com/itm/151657399118)[^n]. For the impatient, it's also [available on Amazon Prime for $8](http://www.amazon.com/dp/B00O34AGSU) with Prime Free Same Day Delivery[^n]. 

Isn't it just the most adorable thing? ![](/content/images/2015/07/IMG_5414.JPG)

### FTDI Cable
To connect to my laptop, I used Adafruit's [USB FTDI Cable](https://www.adafruit.com/products/70). ![](/content/images/2015/07/IMG_5415.JPG)

### Jumper Wires & Breadboard
You can use [female-to-male jumper wires](http://www.amazon.com/Jumper-Wires-Premium-200mm-Female/dp/B008MRZSH8) and [male-to-male jumper wires](http://www.amazon.com/dp/B00ARTWJ44) to connect the pins on the ESP to the FTDI Cable. You might also need a [breadboard](http://www.amazon.com/gp/product/B005GYAIES/) since two wires sometime go to one input. 

---

## The Software: NodeMCU
[NodeMCU](http://nodemcu.com/index_en.html) lets you use LUA scripting language to program the ESP8266. Apparently, there are some issues with memory going this route. I found it to be pretty straightforward. 

If you are comfortable with Arduino, there is an Arduino library. I'll cover how to use ArduinoIDE in a different post.

Here's what I did to get it working[^n]:

### 1. Hooked up ESP8266 in NodeMCU Flasher Mode
<table style="font-size: 0.8em">
<tr>
<td style="background: #fff"><img src="/content/images/2015/07/esp8266_dia.jpg" style="max-height:120px; margin: 0"/></td>
<td colspan=2 style="background: #fff"><img src="/content/images/2015/07/ftdi_dia-1.jpg" style="max-height: 120px; margin: 0"/></td>
</tr>
<tr><th>ESP8266</th><th>FTDI</th><th>Why?</th></tr>
<tr><td>VCC</td><td>VCC</td><td>POWER!</td></tr>
<tr><td>GND</td><td>GND</td><td>POWER!</td></tr>
<tr><td>TX</td><td>RX</td><td>Send info from esp to computer</td></tr>
<tr><td>RX</td><td>TX</td><td>Send info from computer to esp</td></tr>
<tr><td>GPIO0</td><td>GND</td><td>Ground to start update</td></tr>
<tr><td>GPIO2</td><td>None</td><td></td></tr>
<tr><td>Reset</td><td>None</td><td></td></tr>
<tr><td>CH_PD</td><td>VCC</td><td>Enables the chip</td></tr>
</table>

### 2. Flash NodeMCU Firmware
Mac/Linux Command Line can use Esptool (see below). Windows machines can use [NodeMCU-Flasher](https://github.com/nodemcu/nodemcu-flasher).

#### Get Port Name
I ran this command to get the port name for my USB. The USB has to be plugged in and hooked up for this to show. 

```
ls /dev/tty.*
```

On a Mac, you should get something like `/dev/tty.usbserial-ABC`. 

For Windows, you can use your Device Manager and look under "Ports (COM and LPT)". The Port Name should be `COM3` or something like that. You might have to install FTDI Driver first.

#### esptool

[Esptool](https://github.com/themadinventor/esptool) is a Python script that lets you flash the ESP8266 module. 

Download latest [NodeMCU Firmware](https://github.com/nodemcu/nodemcu-firmware/tree/master/pre_build/latest) (a file name "nodemcu_latest.bin") into some folder. Then, install Esptool, I used git clone to do this. You can also just download the python file, [esptool.py](https://github.com/themadinventor/esptool/raw/master/esptool.py). 

```
git clone https://github.com/themadinventor/esptool.git
cd esptool
python esptool.py --port <YOUR_PORT_NAME> write_flash 0x00000 <PATH_TO_FIRMWARE>
```

For example, say your port name is `/dev/tty.usbserial-ABC` and you downloaded the `nodemcu_latest.bin` to `/Users/me/nodemcu/nodemcu_latest.bin`, you'd write:

```
python esptool.py --port /dev/tty.usbserial-ABC write_flash 0x00000 /Users/me/nodemcu/nodemcu_latest.bin
```

### 3. Hooked up ESP8266 in NodeMCU Coding Mode
The coding mode is similar to Flash Mode, but without GPIO0 connected to ground.
<table style="font-size: 0.8em">
<tr>
<td style="background: #fff"><img src="/content/images/2015/07/esp8266_dia.jpg" style="max-height:120px; margin: 0"/></td>
<td colspan=2 style="background: #fff"><img src="/content/images/2015/07/ftdi_dia-1.jpg" style="max-height: 120px; margin: 0"/></td>
</tr>
<tr><th>ESP8266</th><th>FTDI</th><th>Why?</th></tr>
<tr><td>VCC</td><td>VCC</td><td>POWER!</td></tr>
<tr><td>GND</td><td>GND</td><td>POWER!</td></tr>
<tr><td>TX</td><td>RX</td><td>Send info from esp to computer</td></tr>
<tr><td>RX</td><td>TX</td><td>Send info from computer to esp</td></tr>
<tr><td>GPIO0</td><td>None</td><td></td></tr>
<tr><td>GPIO2</td><td>None</td><td></td></tr>
<tr><td>Reset</td><td>None</td><td></td></tr>
<tr><td>CH_PD</td><td>VCC</td><td>Enables the chip</td></tr>
</table>

### 4. Connect via Serial Terminal

For Mac/Linux, use the screen command line tool. Mac Users can also use [CoolTerm](http://freeware.the-meiers.org/). Windows users can use [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html). Other options are covered in [Sparkfun's Terminal Basics Guide](https://learn.sparkfun.com/tutorials/terminal-basics/all). This guide starts with detailed explanation and what this "terminal" thing is and a little history as well. A good read for the curious.

For NodeMCU, use `baud rate=9600`. I'm not sure if you have to, but all the tutorials I've read online says to use 9600. So sure, why not. 9600.

#### Screen Command

[Screen](https://kb.iu.edu/d/acuy) allows you to use multiple windows (virtual VT100 terminals) in Mac and Linux machines. You can call it using the command line:

```
screen <PORT_NAME> <BAUD_RATE>
```
Say, you get `/dev/tty.usbserial-ABC` as your USB port name and want to connect using `9600` baud rate. You would type in:
```
screen /dev/tty.usbserial-ABC 9600
```
To exit screen, `CTRL+A` theb `CTRL+\`one after the other. 

#### CoolTerm
You can also use [CoolTerm](http://freeware.the-meiers.org/) if you want a GUI tool. Open up CoolTerm, then click Options. Set the Baud Rate to 9600 and select the Port. You might have to click "Re-scan Serial Ports." 

Then under "Terminal" (option on the left side), check "Handle BS and DEL Character." This will enable you to use the backspace or delete key[^n].

Then click "OK" and click "Connect."

### 5. Start Coding!

You can try a simple hello world to see if it works. 

```
print("hello world")
```

This should return... well, hello world.

Try fiddling around with some of the [NodeMCU Examples](http://nodemcu.com/index_en.html#fr_5475f7667976d8501100000f). A complete list of functions you can call is [documented here](https://github.com/nodemcu/nodemcu-firmware/wiki/nodemcu_api_en).

#### init.lua
`init.lua` is the file your ESP8266 will run at boot. Just.. don't put an infinite loop into this file like I did the first time. If you do, you'll have to reflash your module.

Now, using a Serial Terminal you can type (or copy/paste) one line at a time. This might make your head explode. In comes luatool to save the day.

#### luatool
[Luatool](https://github.com/4refr0nt/luatool) is a Python script that enables you to edit Lua using whatever text editor you wish, and then send the file to the ESP8266 module. 

I used Git Clone to install. But you can download the [luatool.py file](https://github.com/4refr0nt/luatool/raw/master/luatool/luatool.py) instead.

```
git clone https://github.com/4refr0nt/luatool.git
cd luatool/luatool
```
Then you can upload a lua file in the currently directory using: 
```bash
python luatool.py --port <YOUR_PORT_NAME> --src <YOUR_FILE.lua>
```
For example, if you get `/dev/tty.usbserial-ABC` as your USB port name and want to upload `foo.lua`. You would type in:
```
python luatool.py --port /dev/tty.usbserial-ABC --src foo.lua
```

NOTE: you need to disconnect from all other connections to the ESP8266. So if you're using CoolTerm, click "Disconnect" at the top. If you're using `screen`, do `Ctrl+a` then `Ctrl+\` to disconnect.

## Next Steps

I've found this to be pretty nifty. Looking through the NodeMCU example, you can set up a simple web server, though the memory limits of Lua leaves much to be desired. 

Also, we tried on our local network and logging in takes a while. I'm not quite sure how networks work, but I'm sure that I experienced slowness. And I'm sure that I don't like slowness. 

### 1. Better way to parse HTTP Responses

The ESP8266 can also act as a client. It can read webpages and execute certain commands. I will need to write something to parse all the header junk out and return a JSON or something simple. Right now when I send a request, I get this monster:

```
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 05 Jul 2015 01:56:57 GMT
Content-Type: application/json; charset=utf-8
Transfer-Encoding: chunked
Connection: keep-alive
Status: 200 OK
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
X-UA-Compatible: chrome=1
ETag: "9bb58f26192e4ba00f01e2e7b136bbd8"
Cache-Control: max-age=0, private, must-revalidate
X-Request-Id: 8f9baf99-1418-4558-90ff-de1e2b55988a
X-Runtime: 0.016318
Vary: Origin

d
{"foo":"bar"}
0
```

All I really want is `{"foo": "bar"}` here. 

### 2. Better way to load up "large" lua scripts

I also need a way to write larger Lua scripts. `luatool` is ~~a bit~~ a lot shaky with larger files (>40 lines). Maybe I'll write a function that appends to a file rather than write a new file. 

Then again, maybe this is why people use ArduinoIDE to program the ESP8266 rather than NodeMCU. More on that later. 

🍻 Oh well, time to drink beer. Happy 4th of July, everyone! 🇺🇸


<!-- FOOTNOTES -->

[^n]: I have two modules coming from this eBay seller coming. Until I actually get their products, I can't vouch for the quality of this particular seller. That said, I have a board to play around with in the meanwhile. It theoretically should be the same product, but different sellers may vend different quality products. 
[^n]: This is the one I'm currently playing with, the $8 version from Amazon Prime. 
[^n]: What worked for me isn't guaranteed to work for you. I'm using a Mid 2010 Macbook Pro with OS X Yosemite installed. I also have a bunch of command line tools installed (like `git`) that you might need to install yourself. 
[^n]: I found the original instructions [here](http://www.whatimade.today/flashing-the-nodemcu-firmware-on-the-esp8266-linux-guide/).
[^n]: And boy, do I make a lot of typos! You don't realize how bad your typing accuracy is until they take away the backspace option. 