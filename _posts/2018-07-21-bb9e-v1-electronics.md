---
layout: single
title: BB9E V1 Electronics
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
---

BB9E V1 Electronics control
===========


Electronics development
--------

BB9E Sphere electronics

In this section we will look at the electronics required to drive the robot. When thinking about what electronics to use the main considerations where the next ones:

- Arduino compatible microcontroller.
- Small electronics components so it would fit easier on the robot.
- Servo motors with enough torque to move the pendulum and head drive system.
- Geared DC motor with enough torque to use for the main drive system
- Large battery for weighing down the robot since it uses a pendulum driven system and also to get a longer operation time.
- Bluetooth connection for ease of remote control.
- H bridge driver for the main drive motor.


Main PCB Board V1.1
-------

For my V1 prototype of the electronics I decided to go with the next components, it's worth nothing that In order to save money I used motors from old toys and  cheap china components instead of buying original ones, through my testing so far nothing has failed.

- Arduino Nano: It's smaller size it's perfect for my needs and it also offers enough GPIO as well as PWM port for driving the motors and servos, and at the time of initial development enough memory for my overall needs.

- HC-06: Bluetooth classic slave module that communicates with the Arduino via serial port; If given the option buy the HC-05 instead of the HC-06 since it allows for Master/Slave control, I bought the lather simply because I didn't know this.

- L293D: This is a half H bridge driver, that can drive currents up to 1A; My single main drive motor that I recovered from an old toy when testing it only asked for about 400mA so the L293D is able to drive it with any problems.

- 4 x 18650 batteries: I had laying around some cheap 18650 batteries which had a 3000mAh advertised capacity, when testing them it was closer to 600mAh; I decided to go for a 2S2P configuration which would give me a 7.4V output with an estimated capacity of about 1.2 Ah.

- LM2596 Buck converter: In order to step down the 7.4V output from the batteries I used variable regulated output buck converter to take it to 5V for the use of microcontroller and the Servo motors.

- 3 x MG90S: This are small form factor servo motors that come with metal gears with an advertised stall torque of about  1.8Kg, they turned out to be perfect for my drive system applications.

- Geared DC motor: This motor I had laying around from a RC car that I disassembled, I decided to use them since it already had the gears in an integrated housing which solves a lot of problems when installing them.

- Miscellaneous components: Female and Male pin headers , as well as IC socket.


For the V1.1 implementation of my electronics a perforated breadboard was used; In here I mounted the Arduino Nano and L293D, as well as the headers needed for the connections of the motors while the Buck converter and the HC-06 were left hanging in the air with jumper cables connecting them.


 ![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/pcb-v1-1.jpg){: .align-center}
 ![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/pcb-v1-2.jpg){: .align-center}

 

A lot of solder had to be used  to run the 5V connection as well as some jumper cables to get the signals to where I need it them; While not very pretty it served the needs of the projects as it could fit inside the pendulum along with the battery.

Main PCB Board V1.2
----------

The part used for the V1.2 prototype are the same as the V1.1 the change comes in that I decided to try and make my own printed circuit board using the laser printer toner transfer method, I'm not going to go into the making of this process since there are a lot of other great resources on the internet already available.

Using this method is probably the easiest as it doesn't require specialized tools but by any means this is not an easy process if you're a beginner; I had previously tried to make a PCB for a school project which wasn't successful so I was a little skeptical about the results that I was going to get.

For the design of the PCB I used Easy EDA software as is free and also very easy and convenient to use, if you are making a simple design I highly recommend going this route; You can also get the PCB done by them for very cheap, but me being a maker and all I decided to go for the DIY version. The design in Easy EDA can be found in the next picture.

  ![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/gerber-v1.png){: .align-center}

For this iteration of the board I decided to mount the HC-06 directly to the PCB as well as adding connections ports for an accelerometer which I plan to use for stabilization in the future.

After several tries and a lot of patience I was able to get the next result.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/pcb-v1.2-1.jpg){: .align-center}
![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/pcb-v1.2-3.jpeg){: .align-center}

And whit all the components mounted it looks something like this, pretty neat for a diy board; In the second picture the PCB is located in top of the battery pack, connected and running from it.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/pcb-v1.2-4.jpeg){: .align-center}
![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/pcb-v1.2-5.jpeg){: .align-center}
Battery 
======

The batteries used in this project where Lithium Polymer 18650 format, these batteries come in different capacities; one has to be careful when buying these since you can find fake high capacity batteries that in reality are a third or lower of what is advertised.

When I bought my batteries I could tell they were fake ones since they had an advertised rating of 4000mAh, but since they were very cheap in about $5 USD for 5 pieces it was worth the risk; in reality when testing each of them turned out to be closer to the 600mAh mark not even a quarter of advertised, nevertheless I still used them for my project and they turned out to work excellent.

When thinking about using Lithium batteries one has to be very careful of over-charge or over-discharge since they are delicate and could become death if not charged properly; to overcome this problems a specialized battery charger comes in handy, the one that I used was the IMAX B6; Another circuit that comes in handy is BMS (Battery Management System) which connects directly to the battery pack in order to protect it while using it.

The configuration that I decided to use was 2S2P which means 2 batteries connected in series with 2 other batteries connected in parallel; Using this configuration allowed me to get 7.4V out of them with an estimated capacity of around 1200mAh.

The proper way to attach the batteries together is using a spot welder with nickel strips as connections; the reason for this is that a spot welder transfers the least amount of heat which can damage the batteries; Since I didn't have neither of those items I decided to solder using a normal soldering iron and 16 AWG cable for the connections, this method turned out to be very hard and I could tell the batteries where getting very hot but nevertheless I was able to do it and the batteries seemed to work fine. I also attached a balancing cable to the battery pack in order to properly use it with the battery charger.

In order to make the battery pack look nicer I wrapped into the desired shape using electricians tape and proceeded to solder the leads in which I used female header as connection to the main PCB, using female headers is not a good idea as they can easily be switched around and damage the electronics but that's what I had available at the time; A proper battery connection should be applied in the next revision as well as connecting batteries using a spot welder.


 
