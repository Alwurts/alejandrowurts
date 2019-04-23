---
layout: single
title: Wii Nunchuck Hack!!! Making it a Remote Controller
categories: projects
tags: bb9e
header:
  overlay_image: /assets/images/header/wii-chuck.png
  show_overlay_excerpt: true
  teaser: /assets/images/teaser/wii-chuck.png
excerpt: BB9E Robot / Design and built from scratch by Alwurts
author_profile: false
sidebar:
  nav: "bb9e"
toc: true
toc_label: "Contents"
toc_icon: "cog"
comments: true
---
Wii Nunchuck Hack!!! Diy Robot Remote
===========

Hardware
-------------

The hardware that we use to control the robot is a hacked Nintendo Wii Nunchuck that contains an accelerometer, two buttons and a joystick coupled with an Arduino Nano, battery supply and a HC-05 acting as a master to communicate with the HC-06 on the robot, the pictures of the remote control can be seen next.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/wii-4.png){:.align-center} <center><small><i>Hacked controller.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/wii-2.png){:.align-center} <center><small><i>Power Inputs and cable power On connector.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/wii-1.png){:.align-center} <center><small><i>Uncovered hacked controller.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/wii-3.png){:.align-center} <center><small><i>Uncovered hacked controller.</i></small></center>

The main control that we use is the joystick in that the x axis of it controls the acceleration given by the main dc motor and the y axis of the joystick controls the lateral movement given by the pendulum servo. 

For a detailed guide on wiring visit [this website](https://create.arduino.cc/projecthub/infusion/using-a-wii-nunchuk-with-arduino-597254).

Arduino Code
----------

The library used with Arduino can be found [here](https://github.com/coopermaa/Wiichuck) and is written by [jnw.walker@gmail.com](jnw.walker@gmail.com).

```c++

/*
 * Code for custom wireless controler for a 1/3rd Scale BB9E, arduino reads value from the 
 * Wii Nunchuck via I2C and transmits using HC-05 Bluetooth as master via UART
 * Created by: Alwurts alejandro.wurtsss@udlap.mx
 * Date: 26/04/18
 * Libraries: Wiichuck library by jnw.walker@gmail.com  / https://github.com/coopermaa/Wiichuck
 * 
 */

#include <Wiichuck.h>     
#include <Wire.h>         // Allows communication with I2C devices

Wiichuck wii;

byte modeSelect = 1;       // Variable to store mode being used


void setup() {
  Serial.begin(9600);     // Starts serial for communication with HC-05
  wii.init();             // Start Command
  wii.calibrate();        // Calibration Command
  
}

void loop() {

  
  
  if (wii.poll()) {                 // Checks if wiichuck is transmitting

    if (wii.buttonZ()==1 and wii.buttonC()==1){    // If both wiichuchk button pressed calibrate accelerometer
       wii.calibrate();
       //Serial.println("calibrated");
    }
    if (wii.buttonZ()==1 and wii.buttonC()==0){    // Mode 1 (Joystick Drive only), mapped to Z button
       modeSelect= 0;
       wii.calibrate();
       //Serial.println("mode 1");
       //Serial.println(modeSelect);
    }
    if (wii.buttonC()==1 and wii.buttonZ()==0){    // Mode 2 (Full drive and head movement), mapped to C
       modeSelect= 1;
       //Serial.println("mode 2");
       //Serial.println(modeSelect);
    }
    
    
    //if(Serial.available()>0){       // Communication are send in format (Main Motor):(Pendulum):(Head X):(Head Y)/
                                
      if(modeSelect==1){            // This mode only runs BB9E with joystick from wiichuck 
        //Serial.println("mode 1");
        //Serial.println(modeSelect);
        Serial.print((wii.joyY())*2.5);   // Main Motor Value / Better to code value to -255 - 255 in here to save processing in robot
        Serial.print(":");
        Serial.print(((wii.joyX())+100)*.8);   // Pendulum Servo Value / Better to code value to 30 - 150 in here to save processing in robot
        Serial.print(":");
        Serial.print(90);           // Head x Servo Value (Static in this mode)
        Serial.print(":");
        Serial.print(90);           // Head y Servo Value (Static in this mode)
        Serial.println("/");
        
      } 
      if (modeSelect==0){    // This mode maps head movement to x,y acceleration from wiichuck
        //Serial.println("mode 2");
        //Serial.println(modeSelect);
        Serial.print((wii.joyY())*2.5);   // Main Motor Value
        Serial.print(":");
        Serial.print(((wii.joyX())+100)*.8);   // Pendulum Servo Value
        Serial.print(":");
        Serial.print(((wii.accelX())+100)*.8);           // Head x Servo Value mapped to x accelerometer
        Serial.print(":");          
        Serial.print(((wii.accelY())+100)*.8);           // Head y Servo Value mapped to y accelerometer
        Serial.println("/");
      }
    //}
  }
  //delay(500);
}

```

Below you can see a GIF of the controller while being used with the Robotic Sphere Drive
================

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/wii-gif.gif "Wii Remote Robot Sphere")



<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.