---
layout: single
title: UR5 DIY Color sensor
categories: projects
tags: ur5
header:
  overlay_image: /assets/images/header/ur5-color.png
  show_overlay_excerpt: true
  teaser: /assets/images/teaser/ur5-color.png
excerpt: UR5 DIY Implementation of color sensor using arduino
author_profile: false
toc: true
toc_label: "Contents"
toc_icon: "cog"
comments: true
---
V2 Drivetrain design and construction
===============

Introduction
----------------

The plan of this project is to design and build a sensor attachment for the UR5 robot which can be used to detect color.

For this sensor to be simulated and used in real life a scenario was developed in which the robot receives a box with bottles that can be red, blue or green in color and its task its to separate them according to the color into different boxes.

For the simulation to be performed RoboDK was used and the color sensor was also implemented in real life in order to perform the task using a UR5 robot which you can see in the next picture.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-1.jpg){:.align-center} <center><small><i>Actual robot used.</i></small></center>

Electronics Design
----------------

In the next picture you can see the diagram used to connect the TCS230 Color sensor together with the 2 relays and an arduino uno.


![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/color-schematic.png){:.align-center} <center><small><i>Schematic of the Arduino with the TCS230 sensor.</i></small></center>

Below you can see a drawing of the connections of the UR5 control box, the picture was obtained from the UR5 oficial manual which you can find [here](https://www.usna.edu/Users/weapron/kutzer/_files/documents/User%20Manual,%20UR5.pdf)

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-connection.png){:.align-center} <center><small><i>Connections of the UR5 control box.</i></small></center>

In the picture below you can see how the manual recomends for us to interact with the Digital I/O of the UR5 robot, the I/O use 24v while the arduino uses 5v for this reaon we are using relays to turn on or off the 24v signal to the UR5 robot.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-dio.png){:.align-center} <center><small><i>How to use the input of UR5 robot.</i></small></center>

Arduino Code
---------------

In order for the robot to know which color is being detected th relays will turn on or off according to next table. 

| **Relay 1 State** | **Relay 2 State** | **Color Represented** |
| --- | --- | --- |
| 0 | 0 | No color |
| 0 | 1 | Red |
| 1 | 0 | Green |
| 1 | 1 | Blue |

```c++

/*  Arduino Color Sensor implementation for UR5 robot using TCS230 Color sensor and Relays
 *      
 *  Code used for adaptation orginally written by Dejan Nedelkovski, www.HowToMechatronics.com
 *  
 */


                     // VCC Corresponds to BLUE
                     // GND Corresponds to GREEN

#define S0 4         // Corresponds to WHITE WITH TAPE
#define S1 5         // Corresponds to ORANGE
#define S2 6         // Corresponds to BLACK NO TAPE
#define S3 7         // Corresponds to BLACK WITH TAPE
#define sensorOut 8  // Corresponds to WHITE WITH OUT BLACK TAPE
#define relay1 9
#define relay2 10
#define relay3 11

int frequency1 = 0;
int frequency2 = 0;
int frequency3 = 0;

void setup() {
  
  pinMode(S0, OUTPUT);
  pinMode(S1, OUTPUT);
  pinMode(S2, OUTPUT);
  pinMode(S3, OUTPUT);
  pinMode(sensorOut, INPUT);
  pinMode(relay1, OUTPUT);
  pinMode(relay2, OUTPUT);
  pinMode(relay3, OUTPUT);

  
  // Setting frequency-scaling to 20%
  digitalWrite(S0,HIGH);
  digitalWrite(S1,LOW);
  
  Serial.begin(9600);
  
}

void loop() {
  
  // Setting red filtered photodiodes to be read
  digitalWrite(S2,LOW);
  digitalWrite(S3,LOW);
  // Reading the output frequency
  frequency1 = pulseIn(sensorOut, LOW);
  //Remaping the value of the frequency to the RGB Model of 0 to 255
  //frequency1 = map(frequency1, 59,180,255,0);
  // Printing the value on the serial monitor
  Serial.print("R= ");//printing name
  Serial.print(frequency1);//printing RED color frequency
  Serial.print("  ");
  //delay(100);

  // Setting Green filtered photodiodes to be read
  digitalWrite(S2,HIGH);
  digitalWrite(S3,HIGH);
  // Reading the output frequency
  frequency2 = pulseIn(sensorOut, LOW);
  //Remaping the value of the frequency to the RGB Model of 0 to 255
  //frequency2 = map(frequency2, 110,450,255,0);
  // Printing the value on the serial monitor
  Serial.print("G= ");//printing name
  Serial.print(frequency2);//printing RED color frequency
  Serial.print("  ");
  //delay(100);

  // Setting Blue filtered photodiodes to be read
  digitalWrite(S2,LOW);
  digitalWrite(S3,HIGH);
  // Reading the output frequency
  frequency3 = pulseIn(sensorOut, LOW);
  //Remaping the value of the frequency to the RGB Model of 0 to 255
  frequency3 = map(frequency3, 104,270,255,0);
  //Printing the value on the serial monitor
  Serial.print("B= ");//printing name
  Serial.print(frequency3);//printing RED color frequency
  Serial.println("  ");
  //delay(100);


  // Turnign on or off relays according to color
  
  if (frequency1 > 45){
    Serial.println("Blue");
    digitalWrite(relay1,HIGH);
    digitalWrite(relay2,LOW);
    digitalWrite(relay3,LOW);
  }else if (frequency1 < 45){
    Serial.println("Orange");
    digitalWrite(relay1,LOW);
    digitalWrite(relay2,HIGH);
    digitalWrite(relay3,LOW);
  }
}

```

CAD Design
-------------

A design of a mount was done in Fusion 360 in which velcro strips are going to be used to attach it to the last joint of the UR5 Robot. Below you can see some renders of the design.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-cad-2.png){:.align-center} <center><small><i>Color sensor mount design.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-cad.png){:.align-center} <center><small><i>Color sensor mount design with last joint.</i></small></center>

Prototype 1
---------------

The mount for the sensor was 3D printed and subsequently attached to the robot using velcro strips, together with long cabling required for the sensor to reach the control box.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-2.jpg){:.align-center} <center><small><i>Color sensor mounted to the robot with 3D printed mount.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-3.jpg){:.align-center} <center><small><i>Color sensor mounted to the robot with 3D printed mount.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-4.jpg){:.align-center} <center><small><i>Color sensor with cabling required.</i></small></center>

Robo DK Simulation
------------------

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/ur5/ur5-5.png){:.align-center} <center><small><i>Simulation setup for UR5 and color sensor.</i></small></center>

Video of the simulation
===============

<iframe width="560" height="315" src="https://www.youtube.com/embed/oK6uzF_Gx2k" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.