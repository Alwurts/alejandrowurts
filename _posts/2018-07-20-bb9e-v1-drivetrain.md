---
layout: single
title: BB9E V1 Drivetrain
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

gallery-CAD-v1.2:
  - url: /assets/images/bb9e/v1/body-v1.2-1.png
    image_path: /assets/images/bb9e/v1/body-v1.2-1.png
    alt: "placeholder image 1"
    title: "Render of V1.2 CAD Design."
  - url: /assets/images/bb9e/v1/body-v1.2-2.png
    image_path: /assets/images/bb9e/v1/body-v1.2-2.png
    alt: "placeholder image 2"
    title: "Render of V1.2 CAD Design."
  - url: /assets/images/bb9e/v1/body-v1.2-3.png
    image_path: /assets/images/bb9e/v1/body-v1.2-3.png
    alt: "placeholder image 3"
    title: "Render of V1.2 CAD Design."
  - url: /assets/images/bb9e/v1/body-v1.2-4.png
    image_path: /assets/images/bb9e/v1/body-v1.2-4.png
    alt: "placeholder image 4"
    title: "Render of V1.2 CAD Design."
  - url: /assets/images/bb9e/v1/body-v1.2-5.png
    image_path: /assets/images/bb9e/v1/body-v1.2-5.png
    alt: "placeholder image 5"
    title: "Render of V1.2 CAD Design."
  - url: /assets/images/bb9e/v1/body-v1.2-6.png
    image_path: /assets/images/bb9e/v1/body-v1.2-6.png
    alt: "placeholder image 6"
    title: "Render of V1.2 CAD Design."
gallery-assembly-v1.2:
  - url: /assets/images/bb9e/v1/body-v1.2-assembly-1.jpg
    image_path: /assets/images/bb9e/v1/body-v1.2-assembly-1.jpg
    alt: "placeholder image 1"
    title: "Initial assembly fo the 3D printed parts."
  - url: /assets/images/bb9e/v1/body-v1.2-assembly-2.jpg
    image_path: /assets/images/bb9e/v1/body-v1.2-assembly-2.jpg
    alt: "placeholder image 2"
    title: "More servos mounted, finally looked like something."
  - url: /assets/images/bb9e/v1/body-v1.2-assembly-3.jpg
    image_path: /assets/images/bb9e/v1/body-v1.2-assembly-3.jpg
    alt: "placeholder image 3"
    title: "Final assembly of the drivetrain without microcontroller and battery."
---
BB9E V1 Drivetrain System
===========

This post is the first entry in my pursuit to build a 1/3rd scale functional BB9E droid. 
In here you will find a description of my implementation of a drivetrain for my droid.

Dimensions and existing builds analysis
--------
Official dimensions haven't been realized, but thankfully the community has quickly risen up and provided us with the dimensions. This have been obtained by measuring pictures from the BB8 in the red carpet.


<figure style="width: 300px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bb9e/bb8-dimensions.png" alt="">
  <figcaption>Real scale dimension of BB8 droid.</figcaption>
</figure> 

For my droid i wanted to mantain the size small so it was easy to work with and build i finally decided for a sphere size of 200m.

The first time we saw BB8 in real life was in the red carpet of the Oscars, the Mechanism used for this was complex and consisted of two motors that rotate the whole sphere in order to move forward or backwards. 

In order to be able to turn this mechanism used two drive systems, the first one consisted in a pendulum that moves the left or right of the sphere in order to shift the weight of the mechanism does creating a non-holonomic system where the droid can turn within a certain curvature. 
The other type of rotation was implemented in the form of a rotating platform that creates a rotating momentum does allowing the sphere to spin in its main vertical axis.

The last part is the Head movement mechanism which is especially important since it's one of the BB8 main characteristics. This consisted of two shafts that rotate about the center of mass of the sphere, combining this two movements allows the head two move in 2 dimensions.

{::comment}
ADD PICTURES OF DRIVE SYSTEM FROM RED CARPET
{:/comment}

<figure class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bb9e/redcarpet-drivetrain.jpg" alt="">
  <figcaption>Drivetrain of the BB8 droid that appeared in the Oscars red carpet.</figcaption>
</figure> 

Drivetrain System V1 Initial toughts
---------

I decided that for my drive system I would use a simpler option which is to remove the flywheel for axis rotation, the other driving options like the pendulum rotation system would be implemented as well as the Head movement mechanism; My implementation of the drive systems produces a non-holonomic movement that coupled with a software controller allows the robot to move around pretty easily.

In this section we will take a look at the mechanical part of the V1 design; The considerations for the prototype are the next ones:

-	200mm main sphere
-	Single geared DC motor drivetrain
-	Servo actuated pendulum rotation
-	Servo actuated head mechanism movement 
-	3D-Printed body parts for rapid prototyping
-	Plastic sphere body that can be opened

For the CAD design I used Fusion 360 which is a tool I'm skilled in using and offers some great tools for quick design.

Drivetrain V1.1 CAD
-------

The first initial design consisted of a pendulum with a central axis movement, in which the head mechanism would be mounted; I decided to discard this design since it didn't leave much room for electronic parts and the angle of the pendulum was restricted mainly due to it crashing to the main motor. The pictures of my initial design can be found in the next pictures.

{::comment}
ADD PICTURES OF V1.1
{:/comment}
<figure style="width: 400px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/body-v1.1-1.png" alt="">
  <figcaption>Render of V1.1 CAD Design.</figcaption>
</figure> 


Drivetrain V1.2 CAD
-------

After experimenting a bit with the v1.1 version in CAD i decided to ditch it and start almost from scratch with a new approach in the position of the pendulum servo motors.
Some of the consideration i took in this new design where the next ones:

- Add space in the pendulum base in order to house the batteries (4 x 18650).
-	Reduced main motor housing size.
- Change position of rotation servos.
-	Start designing head / dome movement mechanism.

The biggest flaw was that the pendulum would crash into the main motor and reduce the angle of rotation my approach to improve this flaw was to replace the main motor housing with a slot, and widen the pendulum so that the majority of the body would not crash into the main motor.

The design that i came up with can be observed in the next pictures.

{% include gallery id="gallery-CAD-v1.2" class="center" caption="Gallery of CAD render of drivetrain V1.2" %}

Head / Dome Movement mechanism V1.1
--------
For the head / dome movement I was constrained by having already a servo motor in the middle for the pendulum, so that didn't leave space for additional parts; One solution was to move the pendulum servo away from the center so that I had space to put another servo on its back.

As for the actual mechanism used to move the head I took some inspiration from the analog joysticks and how they can rotate 2 axis at the same time; For my build I created a custom version of it and added it to the body of my droid, the servos took the job of actuating the head movement.

<figure style="width: 400px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/head-mechanism.png" alt="">
  <figcaption>Head / Dome Movement mechanism.</figcaption>
</figure> 

In the above picture you can see a render of the final version of the mechanism where the head magnets will be located at the top of the shaft.

In practice the head shaft moves really well, but one thing that still has to be tested is attaching some weight to it such as the one the magnets give and seeing if the servos will be able to produce enough torque to maintain everything in its intented position.

As for the external part of the head such as the design, caster wheels, electronics etc., a separate article will be made for it which you can find in the [BB9E project page]({{ site.url }}{{ site.baseurl }}/bb9e/)


The inside of the head will also contain electronic components which will give a better look to the robot such as RGB light and a speaker, more on that on the electronics section.
The following is a render of the design I made in CAD

<figure style="width: 400px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bb9e/head-render.png" alt="">
  <figcaption>Head / Dome Render in CAD.</figcaption>
</figure> 

3D Printing
------


The body was then manufactured in a Stratasys SE 3D printer using ABS+ White which was made available to me in my college. The next picture shows the beginning of the 3D printing process.

<figure style="width: 400px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/3d-printer-running.jpg" alt="">
  <figcaption>Start of the 3D printing process.</figcaption>
</figure> 

The Stratasys 3D printers give beautiful results and the parts came out perfect, it even uses dissolvable support which makes the process that much easier. The next picture shows som of the pieces that came out.

<figure style="width: 350px" class="align-center">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/bb9e/v1/3d-printer-parts.jpeg" alt="">
  <figcaption>Printed parts.</figcaption>
</figure> 


After 3D the parts where ready I started the process of assembling which turned out to be not very difficult, thanks to me thinking about it when designing.

{% include gallery id="gallery-assembly-v1.2" class="center" caption="Assembly of 3D Printed parts" %}

Video of Drivetrain test
----------
The next video is of the droid doing one of it's first runs, I must say I am pretty pleased with how it move; Some improvement can be done to further stabilize the movement and they're coming on the V2 version of the drivetrain.

<iframe width="560" height="315" src="https://www.youtube.com/embed/QYErT10RhTw?rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>