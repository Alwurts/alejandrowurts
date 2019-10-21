---
layout: single
title: IOT Convertible LED Matrix Clock
categories: projects
tags: IOT
header:
  overlay_image: /assets/images/header/iot-led.png
  show_overlay_excerpt: true
  teaser: /assets/images/teaser/iot-led.png
excerpt: IOT Convertible Matrix Concept
author_profile: false
comments: true
toc: true
toc_label: "Contents"
toc_icon: "cog"

gallery-make-1:
  - url: /assets/images/iot-display/make-1.jpg
    image_path: /assets/images/iot-display/make-1.jpg
    alt: "Double Height Matrix"
    title: "Double Height Matrix"
  - url: /assets/images/iot-display/make-2.jpg
    image_path: /assets/images/iot-display/make-2.jpg
    alt: "Single Height Matrix"
    title: "Single Height Matrix"

---

Introduction
------------

The starting idea for the project was to design a LED Matrix Alarm Clock that is made from off the shelf parts such as the MAX7219 - 4 in 1 LED Matrix, together with 3D Printed parts.

This clock would use a Wi-Fi capable chip such as an ESP32 in order to drive the LED Matrix as well as allowing the implementation of a variety of IOT related functions in the future.

Some concept functions are:

- Time tracking using NTP server from the internet.
- MQTT Integration
- Alarm clock.
- Node-RED Integration.

Convertible Concept
-----------

Initially I was going to design a clock that would have used a single 8 x 32 Matrix module, but as way of innovating on existing designs, I decided to use two 8 x 32 modules and design the case so that it would have a convertible aspect.

My initial concept of how I want the matrix to convert can be seen in the next picture. The Matrix should be able to convert its LED resolution from a 8 x 64 single height format to a 16 x 32 double height format and vice versa.

 ![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-display/sketch-matrix-display.jpg){: .align-center}<center><small><i>Convertible Matrix Concept</i></small></center>

Prototype V1
------------

For the  first prototype of the convertible concept, I used Fusion 360 to design a case with a hinge in the middle that allows the two 8 x 32 matrix to convert and does change resolution.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-display/design-1.png){: .align-center}<center><small><i>Convertible Matrix Design</i></small></center>

As mentioned in the concept the prototype has two modes pictured below:

1. Double Height Mode 16 x 32 (first picture below)
  - This mode allows for the display of bigger numbers or letters.
2. Single Height Mode 8 x 64 (second picture below)
  - In this mode the letters are smaller but you have additional space to display other things.

{% include gallery id="gallery-make-1" class="center" caption="Convertible LED Matrix Prototype Modes of Operation" %}

Hardware V1
---------

The hardware used for this project is listed below and can be easily sourced from aliexpress or any other electronic component store.

- [ESP32 Dev Module](https://es.aliexpress.com/item/32996463686.html?spm=a2g0o.productlist.0.0.3c951261FyCGcM&algo_pvid=fe65b736-98bd-4462-8feb-5aedd595f600&algo_expid=fe65b736-98bd-4462-8feb-5aedd595f600-0&btsid=1d21f65f-6515-4638-a7ee-fb718426b761&ws_ab_test=searchweb0_0,searchweb201602_6,searchweb201603_52)
- [4 in 1 LED Matrix](https://es.aliexpress.com/item/32955063973.html?spm=a2g0o.productlist.0.0.5faf22427ohR8w&algo_pvid=908bdd4a-43c9-4799-96fa-67888b426475&algo_expid=908bdd4a-43c9-4799-96fa-67888b426475-2&btsid=af042420-48c0-4721-a228-90c4c2cd5caa&ws_ab_test=searchweb0_0,searchweb201602_6,searchweb201603_52)
- [Reed Switch NO or NC](https://es.aliexpress.com/item/32803711882.html?spm=a2g0o.productlist.0.0.4bac27ba7a1k4D&algo_pvid=f8495f77-c746-4313-9437-0dd3a7a1b0e7&algo_expid=f8495f77-c746-4313-9437-0dd3a7a1b0e7-5&btsid=fca9746b-bca4-4ebf-b94d-b95ff157477e&ws_ab_test=searchweb0_0,searchweb201602_6,searchweb201603_52)
- [Push button](https://es.aliexpress.com/item/32857436208.html?spm=a2g0o.productlist.0.0.6856722dma8QMp&algo_pvid=8b1e2ecd-f2d0-4ab2-b6c1-a11da6293b5c&algo_expid=8b1e2ecd-f2d0-4ab2-b6c1-a11da6293b5c-8&btsid=a70abbb7-0e20-42dd-a259-751f0bbb4982&ws_ab_test=searchweb0_0,searchweb201602_6,searchweb201603_52)
- [5V DC Power supply and Jack](https://es.aliexpress.com/item/32961533195.html?spm=a2g0o.productlist.0.0.5e5b66b6Ci3hO3&algo_pvid=9a03429a-24c4-4bac-9798-cff5baddb697&algo_expid=9a03429a-24c4-4bac-9798-cff5baddb697-0&btsid=3b252948-2454-4d1f-bc86-3a234140381e&ws_ab_test=searchweb0_0,searchweb201602_6,searchweb201603_52)
- [Dupont Cables](https://es.aliexpress.com/item/32987024879.html?spm=a2g0o.productlist.0.0.173369003RYot6&algo_pvid=c6c8ff5a-22b7-42c0-9fcb-b9dd1f940a43&algo_expid=c6c8ff5a-22b7-42c0-9fcb-b9dd1f940a43-0&btsid=f919d28a-cc54-4e5d-ac24-8168c0d90f9c&ws_ab_test=searchweb0_0,searchweb201602_6,searchweb201603_52)

In order for the microcontroller to tell in which mode the clock is being used a reed switch was located on one matrix and a magnet on the other matrix. When the switch and the magnet come together they trigger a signal that tells the clock to be in double height mode, on the other instance, if they're apart from each other no signal is sent and the clock knows to be in single height mode.

Below is a picture of all the components and connections inside one side of the clock. For the prototype V1 the internals are still a bit messy, and use a lot of hot glue to keep everything in place, further improvements should tackle cable management and anchoring of components.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-display/cable-mess.jpg){: .align-center}<center><small><i>Internal connections and components of the clock</i></small></center>

Two buttons were added to the back of the matrixes to allow, control of different functions, in the case of the prototype V1 is used for brightness control.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-display/control-buttons.jpg){: .align-center}<center><small><i>Buttons to interact with the clock</i></small></center>

On the back you can find the cable that goes between the two displays, a 5V DC jack and a debug port where a USB cable can pass through.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-display/back-connections.jpg){: .align-center}<center><small><i>Outside connections of the clock</i></small></center>


Software V1
----------

The software was developed using Arduino on an ESP32 together with Magic Designs [MD_PAROLA](https://github.com/MajicDesigns/MD_Parola) library which makes it easy to develop the convertible concept, since by default it allows for the creation of display zones that can be controlled independently.

In order to keep this post as clean and short as possible, I won't be writing the whole code in this post, instead the code can be found [here]({{ site.url }}{{ site.baseurl }}/iot-led-clock-code). A lot of the code that I used for this project comes from the examples given by the [MD_PAROLA](https://github.com/MajicDesigns/MD_Parola) folks, so huge shout out to them.

Working prototype V1
------------

Below is a GIF, where you can see the functioning of the V1 prototype. Current features are:

- Convertible from 8 x 64 (single height) to 16 x 32 (double height) resolution.
- Big Clock on double height mode.
- Small Clock and text display available on single height mode.
- Brightness Up/Down control trough buttons.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-display/clock.gif){: .align-center}<center><small><i>Convertible Matrix Design</i></small></center>

The features implemented work great but still in the future I'm planning to implement a lot of things such as an IOT message dashboard so that it can show a variety of messages in the place of where it currently shows the static message "Alwurts".

IOT implementation will be done using MQTT protocol, which can be used with a variety of platforms such as adafruit.io or Node-RED. Once a connection to a server is stablished a number of features such as notifications can be implemented with ease using something like IFTTT.


<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.