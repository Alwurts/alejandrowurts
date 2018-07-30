---
layout: single
title: IOT LED Matrix Display - Concept
categories: projects
tags: matrix-iot
header:
  overlay_image: /assets/images/iot-display/sketch-matrix-display-crop.jpg
  show_overlay_excerpt: true
  teaser: /assets/images/iot-display/8x8-matrix-how.jpg
excerpt: IOT LED Matrix Display concept
author_profile: false
---

The starting idea was to make a 8x16 LED matrix alarm clock for my bed side table, but in the process of thinking I decided I would implement IOT functions into it as well as using two 8 x 32 Matrixes.

IOT LED Matrix Display Side
-----

Functions to be implemented:

- Time tracking using RTC module as well as updating from the internet.
- Google calendar notification when an event is coming up.
- To do list notification with google task integration.
- Alarm clock.

The Matrixes should be able to be configured into a 8 x 64 format or a 16 x 32 format, my initial sketches of how this will work can be seen in the next picture.

 ![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/iot-display/sketch-matrix-display.jpg){: .align-center}

 As for the electronics / software part of the system I have planned the next parts.

- ESP32: Takes care of the driving of the matrix as well as connection to a MQTT broker.
- Buzzer: Will provide the sound needed for an alarm.
- MQTT: mqtt connection to a broker to handle IOT functions, the broker is going to run in a Raspberry Pi in my local network.

Raspberyy Pi / Server side
----------

The brains of the IOT operation will be in the rapsberry pi using a mosquitto broker and red node in order to fulfill automation of tasks. From here you can set the alarms, information to be displayed etc.

Another part to be developed will be integration of the alarm clock into android using an existing alarm clock app or creating my own; This will allow me to create or changes the alarms easily from my phone.


<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.