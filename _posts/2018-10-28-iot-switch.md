---
layout: single
title: IOT Switch
categories: projects
tags: iot-switch
header:
  overlay_image: /assets/images/header/iot-switch.png
  show_overlay_excerpt: true
  teaser: /assets/images/iot-switch/iot-switch.png
excerpt: IOT Switch / Design and built from scratch by Alwurts
author_profile: false
comments: true
---

IOT Switch
===========

For a while now we have seen lamps that can be turned on or off via your smartphone, or using something like Amazon Alexa or Google Home. I decided to give it a shot at building a device that can plug in into existing bulb sockets and allow for any type of bulb to be integrated into IOT.

Hardware
==========

For this project the list of parts is as follows.

- Nodemcu
- 5V relay
- 120/220V to 5V smartphone charger
- Socket for light bulb

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-switch/iot-switch-4.jpg){:.align-center}

The image below shows a diagram of how the parts for this project should be conected together. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-switch/iot-switch.png){:.align-center}

The first prototype I designed had a plug socket, but the funciontioning is the same as if it had a bulb socket. Below you can see a picture of the design I used for testing.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-switch/iot-switch-2.jpg){:.align-center}

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-switch/iot-switch-1.jpg){:.align-center}

Stripped 5V phone charger

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-switch/iot-switch-3.jpg){:.align-center}

Software
==========

The software side was developed using arduino, and consists on a sketch that connects to a MQTT broker and subscribes to a pre-defined topic. Within this topic we receive the on or off signal which in turn activates or deactivates the 5V relay which turns the bulb or on off.
The MQTT broker I used was Mosquitto running on a Raspberry Pi, but you can very well use something like cloudmqtt or adafruit.io

Below is the arduino code used.

```c++
#include <ESP8266WiFi.h>
#include <PubSubClient.h>
 
const char* ssid = "xxxxx";     // Your WIFI SSID
const char* password =  "xxxxxx";  // Your WIFI Password
const char* mqttServer = "192.168.0.31"; // Your Broker IP Address
const int mqttPort = 1883;

long lastReconnectAttempt = 0;

WiFiClient espClient;
PubSubClient client(espClient);

void callback(char* topic, byte* payload, unsigned int length) {
 
    if (strcmp(topic,"bedroom1")==0){
  
      if( (byte)payload[0] == '1'){
        
        digitalWrite(16, HIGH);  // Turn the LED off by making the voltage HIGH
      
      }
      if( (byte)payload[0] == '0'){
          
          digitalWrite(16, LOW);   // Turn the LED on by making the voltage LOW
      }
    }
}

boolean reconnect() {
  if (client.connect("Nodemcu 3.0")) {
    // Once connected, publish an announcement...
    client.publish("bedroom1","bedroom connected");
    // ... and resubscribe
    client.subscribe("bedlroom1");
  }
  return client.connected();
}

void setup() {

  pinMode(16, OUTPUT);
  pinMode(5, OUTPUT); 
  pinMode(4, OUTPUT); 
  pinMode(0, OUTPUT);  
 
  Serial.begin(115200);
  WiFi.begin(ssid, password);
 
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
  }
 
  Serial.println("Connected to the WiFi network");
 
  client.setServer(mqttServer, mqttPort);
  client.setCallback(callback);
 
  lastReconnectAttempt = 0;
  
  }
  
 


 
void loop() {
  
  if (!client.connected()) {
    long now = millis();
    if (now - lastReconnectAttempt > 5000) {
      lastReconnectAttempt = now;
      // Attempt to reconnect
      if (reconnect()) {
        lastReconnectAttempt = 0;
      }
    }
  } else {
    // Client connected

    client.loop();
  }
  
    client.publish("bedroom1", "stillalive");
  
}
```


<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.


 
