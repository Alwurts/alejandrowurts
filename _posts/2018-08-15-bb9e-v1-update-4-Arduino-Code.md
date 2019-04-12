---
layout: single
title: BB9E V1 Project Update 4 - Arduino Software and Remote Controller
categories: projects
tags: bb9e
header:
  overlay_image: /assets/images/bb9e/starfield.jpg
  show_overlay_excerpt: true
  teaser: /assets/images/bb9e/bb9e-teaser.jpg
excerpt: BB9E Robot / Design and built from scratch by Alwurts
author_profile: false
sidebar:
  nav: "bb9e"
toc: true
toc_label: "Contents"
toc_icon: "cog"
comments: true
---
BB9E V1 Arduino Software and Remote Controller
===========

The control board for the robot features an Arduino Nano, a L293D H Bridge motor controller, a DC-DC Buck regulator, bluetooth HC-06 and servo headers the software that runs on this control boar is developed using the Arduino plattform.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/pcb-v1.2-5.jpeg){:.align-center}

The code is a very basic implementation of what the robot is going to become, and only contains the necessary parts to receive signals, decode them and set the actuator positions according to the values received. 

The following code contains libraries and snipets of code that were not developed by me and all the rights for them belong to their rightfull owners.

If you want to download the Arduino .ino file click [here](https://goo.gl/NDkKzh)

```c++
/*
 * Code for custom 1/3rd Scale BB9E, arduino reads value from the HC-06 Bluetooth via UART 
 * Movement of sphere drive mechanism is a Non-Holonimic System
 * Motor main drive consists of Main motor for Forwards/Backwards and Pendulumn Servo for Left/Right
 * Head movement consists of two servo motor to move the head in the top half of the sphere
 * Created by: Alwurts 
 * Date: 22/03/18
 * Libraries: Servo Arduino Library
 */

// Libraries to be used
 
#include <Servo.h>

// Variables 

String dataReceived;        // String to store value received through UART from HC-06     

Servo pendulumServo, headServoX, headServoY;   // Creates Servo objects to wich we write values.

// Actuators position variables
int mainMotorValue = 0;     // Main Motor value initialized to static robot position
int pendulumValue = 81;     // Pendulumn Servo value initialized to static robot position
int HeadXValue = 90;        // Head X Servo value initialized to static robot position
int HeadYValue = 90;        // Head Y Servo value initialized to static robot position


// Pinout of devices connected to the arduino nano

int motorInput3 = 8;    // Input3 of 1293d connected to pin 8 of arduino as output 
int motorInput4 = 7;    // Input4 of 1293d connected to pin 7 of arduino as output
int enableInput = 5;    // Enable input of l293d connected to pin 5 of arduino as output, must be pwm capable

int pendulumPin = 11;   // Pin to set as output for Pendulumn Servo, must be pwm capable
int headXPin = 10;      // Pin to set as output for Head Servo X, must be pwm capable
int headYPin = 9;       // Pin to set as output for Head Servo Y, must be pwm capable

      
void setup()
{
  
    Serial.begin(9600);    // UART Communication with HC-06

    // Attach correct servo object to correct pwm output pin
    
    pendulumServo.attach(pendulumPin);
    headServoX.attach(headXPin);
    headServoY.attach(headYPin);

    // Set as output correct pins for the 1293d driver for the main motor
    
    pinMode (enableInput, OUTPUT); 
    pinMode (motorInput3, OUTPUT);
    pinMode (motorInput4, OUTPUT);
    
} 

void loop()
{
   if(Serial.available()>0)      
   {
      dataReceived = Serial.readStringUntil('/');   // Receive value through serial port until it finds "/" and assigns to string
      valuedecode(dataReceived);                    // Send value to the decoder function
      
      pendulumServo.write(pendulumValue);     // If value received is not 0 -180 you need to convert it
      headServoX.write(HeadXValue);           // If value received is not 0 -180 you need to convert it
      headServoY.write(HeadYValue);           // If value received is not 0 -180 you need to convert it

      /* We receive -255 - 255 from controller motor turns in different direction depending on
      *  Input 3 and Input 4
      *     1           0    =   Left
      *     0           1    =   Right
      *     1           1    =   Stop
      *     
      *  Then enable input controls speed with pwm output 0 - 255 
      */
      
      if (mainMotorValue > 0){      // If value received is less than 0 turn left
        
        digitalWrite (motorInput3, LOW);           
        digitalWrite (motorInput4, HIGH);
        analogWrite(enableInput,mainMotorValue);
        
        } else {                      // If value is greater than 0 turn right 
          
          digitalWrite (motorInput3, HIGH);
          digitalWrite (motorInput4, LOW);
          analogWrite(enableInput,abs(mainMotorValue));     // Speed value to be set must be converted to 0-255 with abs() function
          
        }
      } else {
        mainMotorValue = 0;     // Main Motor value initialized to static robot position
        pendulumValue = 81;     // Pendulumn Servo value initialized to static robot position
        HeadXValue = 90;        // Head X Servo value initialized to static robot position
        HeadYValue = 90;        // Head Y Servo value initialized to static robot position
      }
      
   }

void valuedecode (String serialIn){      // Function to decode incoming value in format  (Main Motor):(Pendulum):(Head X):(Head Y)/

  // More values can be decoded by adding new delimitators
  int commaIndex = serialIn.indexOf(':');                           // First delimitator ":"
  int secondCommaIndex = serialIn.indexOf(':', commaIndex+1);       // Second delimitator ":"
  int thirdCommaIndex = serialIn.indexOf(':', secondCommaIndex+1);  // Third delimitator ":
  
  mainMotorValue = serialIn.substring(0, commaIndex).toInt(); 
  pendulumValue = serialIn.substring(commaIndex+1, secondCommaIndex).toInt();
  HeadXValue = serialIn.substring(secondCommaIndex+1,thirdCommaIndex).toInt();
  HeadYValue = serialIn.substring(thirdCommaIndex+1).toInt();
  }

```

Remote Controller with MIT App Inventor 2
--------------

One of the options that I developed as a remote controller was in the form of a android app using MIT App Inventor 2 as the platform to create the app.

MIT App Invetor is an online development platform that allows you to easily create android applications which in my case allowed me to have a functioning app in one night of work, this app has the following features.

- Custom starting screen
- Bluetooth connectivity
- Control by slider of the actuators of the robot
- Two modes of operation for the pendulum that drives the robot these are by slider and by using the phone accelerometer

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/mit-ai2/mit-ai2-screen-1.png){: .align-center} <center><small><i>Start screen.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/mit-ai2/mit-ai2-screen-2.png){: .align-center} <center><small><i>Main controls screen.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/mit-ai2/mit-ai2-screen-3.png){: .align-center} <center><small><i>Settings screen.</i></small></center>

The form of programming in this plattform is by using blocks which make large project a little messy with all the projects scattered around as you can see in the next picture.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/mit-ai2/mit-ai2-blocks-1.png){: .align-center} <center><small><i>Programming blocks.</i></small></center>

The block that you can see in the next pictures is the one that puts together the values of the sliders and sends them through bluetooth using a timer trigger.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/mit-ai2/mit-ai2-blocks-2.png){: .align-center} <center><small><i>Block that handles bluetooth.</i></small></center>

The compiled app once its runned in an android phone looks like the next picture in which the sign saying bluetooth not conected will not disappear until the robot is connected to the phone through pairing.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/mit-ai2/mit-ai2-phone-1.png){: .align-center} <center><small><i>App running on the phone.</i></small></center>

The .aia file which is used by MIT App Inventor can be found [here](https://goo.gl/BSvook) or download the compiled apk for android os [here](https://goo.gl/cojNgC)

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.