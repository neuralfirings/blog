---
layout: post
title: Wifi Connected LED using Guide.js
date: '2015-08-02 19:22:57'
---

I wasn't kidding when I said I'd use [Guide.js](https://github.com/neuralfirings/guide), my new framework for writing guides and tutorials. Here's a rewrite of my ESP8266 to LED tutorial. I think it's much neater than the [previous version](http://blog.nyl.io/esp8266-led-arduino/). 

---

<div class="guide-step">  
  <div class="guide-main">
<iframe class="imgur-embed" width="100%" height="360" frameborder="0" src="http://i.imgur.com/GfD93zj.gifv#embed"></iframe>
</div>
<div class="guide-text">
<h2 class="guide-title">Ingredients</h2>
<ul><li><a href="http://amzn.to/1Lu6QHu">ESP8266-01 Wifi Module</a></li>
<li><a href="http://amzn.to/1OIMPLp">White LED</a></li>
<li><a href="http://amzn.to/1ISi1tf">FTDI Cable</a></li>
<li><a href="http://amzn.to/1OXGV9W">Lipo 3.7V Battery</a></li>
</ul>

</div>
</div>

<div class="guide-step">  
  <div class="guide-images">
    <img src="http://blog.nyl.io/content/images/2015/07/esp_led_dataflow.png" data-caption="Diagram of Workflow">
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Workflow</h2>
<ul>
<li>PHP page writes on/off instructions to JSON file based on user input</li>
<li>ESP8266 pings light.json, reads instructions, and turns on/off led</li<
</ul>
  </div>
</div>



<div class="guide-step">  
  <div class="guide-main">
```
$ sudo nano light.json
$ chmod 755 -R light.json
```
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 1: Create JSON using Shell Scripts</h2>
<ul>
<li>go to the directory of your PHP file</li>
<li>create light.json</li>
<li>assigns permission so index.php can write to it</li>
</ul>
  </div>
</div>

<div class="guide-step">  
  <div class="guide-main">
```
<?php  
$light = $_GET['light'];
if($light == "on") {  
  $file = fopen("light.json", "w") or die("can't open file");
  fwrite($file, '{"light": "on"}');
  fclose($file);
} 
else if ($light == "off") {  
  $file = fopen("light.json", "w") or die("can't open file");
  fwrite($file, '{"light": "off"}');
  fclose($file);
}
?>

<a href="?light=on">Turn On</a>  
<a href="?light=off">Turn Off</a>  
<div>  
  <?php
    if($light=="on") {
      echo("Turn LED on.");
    }
    else if ($light=="off") {
      echo("Turn LED off.");
    }
    else {
      echo ("Do something.");
    }
  ?>
</div>  
```
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 2: PHP <small><a href="https://raw.githubusercontent.com/neuralfirings/esp8266led/master/www/index.php"><i class="fa fa-cloud-download"></i></a></small></h2>

<ul>
<li>Button links to page with url parameters light=on or light=off</li>
<li>PHP looks for URL parameters and writes to light.json</li>
</ul>
  </div>
</div>


<div class="guide-step">  
  <div class="guide-images">
    <img src="http://blog.nyl.io//content/images/2015/08/espled_flashmode.png" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 3. Wire Things Up in Flash Mode</h2>
    

<ul>
<li>ESP's VCC > VCC</li>
<li>ESP's CH_PD > VCC</li>
<li>ESP's GND > GND</li>
<li>ESP's RX > FTDI's TX</li>
<li>ESP's TX > FTDI's RX</li>
<li>ESP's GPIO0 > GND<br />(indicate flash mode)</li>
<li>LED's GND > GND</li>
<li>LED's PWR > ESP's GPIO2</li>
</ul>

  </div>
</div>


<div class="guide-step">  
  <div class="guide-images">
    <img src="http://blog.nyl.io/content/images/2015/07/arduino_pref.jpg" data-caption="Install ESP: Preferences" />
    <img src="http://blog.nyl.io/content/images/2015/07/arduino_boardmanagerurl.jpg" data-caption="Install ESP: Add Board Manager URL" />

    <img src="http://blog.nyl.io/content/images/2015/08/arduino_esp_setup.jpg" data-caption="Install ESP: Set Options for ESP8266" />

  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 4. Install ESP in the Arduino IDE</h2>

Install ESP8266 Board
<ul>
<li> Go to preferences</li>
<li> Copy <a href="http://arduino.esp8266.com/package_esp8266com_index.json">this link's url</a> into "Additional Board Manager URLs" box</li>
<li>Click OK</li>
</ul>
Update Settings
<ul>
<li>Board: Generic ESP8266</li>
<li>CPU Frequency: 80 MHz</li>
<li>Flash size: 4M</li>
<li>Upload speed: 115200</li>
<li>Port: my USB port (this shows up once you plugged everything in)</li>
<li>Programmer: AVRISP mkll</li>
</ul>
</li>
</ul>
  </div>
</div>



<div class="guide-step">  
  <div class="guide-main">

```
#include <ESP8266WiFi.h>
#include <ArduinoJson.h>

const char* ssid     = "";  
const char* password = "";

const char* host     = ""; // Your domain  
String path          = "/path/to/light.json";  
const int pin        = 2;

void setup() {  
  pinMode(pin, OUTPUT); 
  pinMode(pin, HIGH);
  Serial.begin(115200);

  delay(10);
  Serial.print("Connecting to ");
  Serial.println(ssid);

  WiFi.begin(ssid, password);
  int wifi_ctr = 0;
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("WiFi connected");  
  Serial.println("IP address: " + WiFi.localIP());
}

void loop() {  
  Serial.print("connecting to ");
  Serial.println(host);
  WiFiClient client;
  const int httpPort = 80;
  if (!client.connect(host, httpPort)) {
    Serial.println("connection failed");
    return;
  }

  client.print(String("GET ") + path + " HTTP/1.1\r\n" +
               "Host: " + host + "\r\n" + 
               "Connection: keep-alive\r\n\r\n");

  delay(500); // wait for server to respond

  // read response
  String section="header";
  while(client.available()){
    String line = client.readStringUntil('\r');
    // Serial.print(line);
    // we’ll parse the HTML body here
    if (section=="header") { // headers..
      Serial.print(".");
      if (line=="\n") { // skips the empty space at the beginning 
        section="json";
      }
    }
    else if (section=="json") {  // print the good stuff
      section="ignore";
      String result = line.substring(1);

      // Parse JSON
      int size = result.length() + 1;
      char json[size];
      result.toCharArray(json, size);
      StaticJsonBuffer<200> jsonBuffer;
      JsonObject& json_parsed = jsonBuffer.parseObject(json);
      if (!json_parsed.success())
      {
        Serial.println("parseObject() failed");
        return;
      }

      // Make the decision to turn off or on the LED
      if (strcmp(json_parsed["light"], "on") == 0) {
        digitalWrite(pin, HIGH); 
        Serial.println("LED ON");
      }
      else {
        digitalWrite(pin, LOW);
        Serial.println("led off");
      }
    }
  }
  Serial.print("closing connection. ");
}  
```

  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 5: Arduino Code <small><a href="https://raw.githubusercontent.com/neuralfirings/esp8266led/master/arduino/part2_parseresponse/part2_parseresponse.ino"><i class="fa fa-cloud-download"></i></a></small></h2>


<ul>
<li>Connect to Wifi</li>
<li>Read light.json file</li>
<li>Parse the JSON</li>
<li>Turn on/off LED</li>
</ul>

  </div>
</div>




<div class="guide-step">  
  <div class="guide-images">
    <img src="http://blog.nyl.io/content/images/2015/07/esp8266_led_battery_bb.png" data-caption="" />
  </div>
  <div class="guide-text">
    <h2 class="guide-title">Step 6. Wire Things Up in Run Mode</h2>
    

<ul>
<li>ESP's VCC > VCC</li>
<li>ESP's CH_PD > VCC</li>
<li>ESP's GND > GND</li>
<li>LED's GND > GND</li>
<li>LED's PWR > ESP's GPIO2</li>
</ul>

  </div>
</div>

## Next Steps

There you have it! Not bad. I like it much better than the old, unorganized version. A few things I'd like to add:

* Table of Contents and the ability to link to various sections
* A way to parse this using Markdown, HTML is just... sigh...
* A way to have a carousel of images combined with code, iframes, and other custom elements
* Wrap all the guide-step classes in a guide class, then add things for displaying intro descriptions, ingredients lists, TOC, etc.

Ok. Now go make stuff.
