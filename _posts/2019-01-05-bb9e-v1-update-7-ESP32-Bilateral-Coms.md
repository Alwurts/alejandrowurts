---
layout: single
title: ESP32 and Wi-Fi UDP for Robot Communication
categories: projects
tags: bb9e
header:
  overlay_image: /assets/images/header/esp32-udp.png
  show_overlay_excerpt: true
  teaser: /assets/images/teaser/esp32-udp.png
excerpt: Robot Sphere BB9E Project / Design and built from scratch by Alwurts
author_profile: false
sidebar:
  nav: "bb9e"
toc: true
toc_label: "Contents"
toc_icon: "cog"
comments: true
---
ESP32 and Wi-Fi UDP for Robot Communication
===========

Introduction
----------

To develop the system an ESP32 wireless transceiver is used with its integrated Wi-Fi and using Arduino as a programming interface. The wireless transceiver can be used for robotics control and should be able to handle simultaneous connections from 3 or more microcontrollers.

As part of a robotics project where a BB8 like sphere robot is being developed, for the electronics the first type of wireless system we used was Bluetooth classic, which offers ease of use with modules such as the HC-05 and a relatively low latency on the connection, however Bluetooth classic can't handle more than one simultaneous connection and for a system that requires the PCB to be as small as possible due to space constrains using external modules can become an obstruction.

To solve the problem of space a wireless system using an ESP32 and Wi-Fi connectivity was developed in conjunction with a low latency transport protocol such as UDP

ESP32 is a fairly new microcontroller that packs a lot into a single development board, it contains features such as:

-	Dual Core 32-Bit processor
-	520Kb SRAM
-	Wi-Fi: 802.11 b/g/n
-	Bluetooth: v4.2 BR/EDR and BLE
-	Internal RTC
-	Integrated touch sensors
-	Temperature sensor
-	16 Channel PWM

The reason to use the ESP32 for this system is the integrated wireless connectivity and how it can be used as a transceiver to remotely control a robot while saving space in the PCB since we don't need an external wireless module such as an HC-06 Bluetooth.

Wi-Fi UDP Library
--------------

The Wi-Fi UDP library that we are going to use comes bundled with the Arduino IDE and the methods available for the Wi-Fi UDP class are as follows:

| **Function** | **Description** | **Syntax** |
| --- | --- | --- |
| begin()  | Initializes the UDP instance at the specified port  | Udp.begin(port); |
| available()  | Returns number of bytes in the data that has arrived and can only be called after Udp.parsePacket() function  | Udp.available(); |
| beginPacket()  | Begins connection with another instance of UDP with specified IP and Port.  | Udp.beginPacket(hostIP, port); |
| endPacket()  | Closses the connection in which data is being sent and returns 1 if data was sent successfully.  | Udp.endPacket(); |
| write()  | Writes data to the other UDP instance  | Udp.write(Data); |
| parsePacket()  | Process the data that has arrived and has to be called before Udp.read() | Udp.parsePacket(); |
| peek()  | Reads 1 byte from the data without continuing the stream of data.  | Udp.peek(); |
| read()  | Reads data in a specified buffer  | Udp.read(buffer,maxsize); |
| flush()  | Clears the buffer.  | Udp.flush |
| stop()  | Disconnect from current server.  | Udp.stop();  |
| remoteIP() | Returns the IP address of the current incoming packet after Udp.parsePacket();  | Udp.remoteIP(); |
| remotePort()  | Returns the port of the UDP connection. | Udp.remotePort(); |


Arduino Bilateral communication between 2 ESP-32
----------------

To connect and transfer information between two ESP32 with one acting as an access point and the other as a client we use the following code

**Access Point / Server Code**

```c++

#include <WiFi.h>
#include <WiFiUdp.h>

WiFiUDP Udp; // Creation of wifi Udp instance

char packetBuffer[255];

unsigned int localPort = 9999;

const char *ssid = "BB9ESERVER";  
const char *password = "BB9ESERVER";

void setup() {
  Serial.begin(115200);
  WiFi.softAP(ssid, password);  // ESP-32 as access point
  Udp.begin(localPort);
  }

void loop() {
  int packetSize = Udp.parsePacket();
  if (packetSize) {
    int len = Udp.read(packetBuffer, 255);
    if (len > 0) packetBuffer[len-1] = 0;
    Serial.print("Recibido(IP/Size/Data): ");
    Serial.print(Udp.remoteIP());Serial.print(" / ");
    Serial.print(packetSize);Serial.print(" / ");
    Serial.println(packetBuffer);

    Udp.beginPacket(Udp.remoteIP(),Udp.remotePort());
    Udp.printf("received: ");
    Udp.printf(packetBuffer);
    Udp.printf("\r\n");
    Udp.endPacket();
     }
}
```
**Client Code**

```c++
#include <WiFi.h>
#include <WiFiUdp.h>

WiFiUDP Udp;  // Creation of wifi Udp instance

char packetBuffer[255];

unsigned int localPort = 9999;

const char *ssid = "BB9ESERVER";  
const char *password = "BB9ESERVER";

IPAddress ipServidor(192, 168, 4, 1);   // Declaration of default IP for server
/* 
 *  The ip address of the client has to be different to the server
 *  other wise it will conflict because the client tries to connect
 *  to it self.
 */
IPAddress ipCliente(192, 168, 4, 10);   // Different IP than server
IPAddress Subnet(255, 255, 255, 0);

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  WiFi.mode(WIFI_STA); // ESP-32 as client
  WiFi.config(ipCliente, ipServidor, Subnet);
  Udp.begin(localPort);
}

void loop() {
//unsigned long Tiempo_Envio = millis();

//SENDING
    Udp.beginPacket(ipServidor,9999);   //Initiate transmission of data
    
    Udp.printf("Millis: ");
    
    char buf[20];   // buffer to hold the string to append
    unsigned long testID = millis();   // time since ESP-32 is running millis() 
    sprintf(buf, "%lu", testID);  // appending the millis to create a char
    Udp.printf(buf);  // print the char
    
    Udp.printf("\r\n");   // End segment
    
    Udp.endPacket();  // Close communication
    
    Serial.print("enviando: ");   // Serial monitor for user 
    Serial.println(buf);
    
delay(5); // 
 
//RECEPTION
  int packetSize = Udp.parsePacket();   // Size of packet to receive
  if (packetSize) {       // If we received a package
    
    int len = Udp.read(packetBuffer, 255);
    
    if (len > 0) packetBuffer[len-1] = 0;
    Serial.print("RECIBIDO(IP/Port/Size/Datos): ");
    Serial.print(Udp.remoteIP());Serial.print(" / ");
    Serial.print(Udp.remotePort()); Serial.print(" / ");
    Serial.print(packetSize);Serial.print(" / ");
    Serial.println(packetBuffer);
  }
Serial.println("");
delay(5);
}


```

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.