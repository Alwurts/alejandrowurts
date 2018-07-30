---
layout: single
title: IOT LED Matrix Display
categories: projects
tags: matrix-iot
header:
  overlay_image: /assets/images/iot-display/sketch-matrix-display.jpg
  show_overlay_excerpt: true
  teaser: /assets/images/iot-display/8x8-matrix-how.jpg
excerpt: IOT LED Matrix Display concept
author_profile: false
---

My initial toughts about the project.

ESP32 - Takes care of the driving of the matrix as well as connection to a MQTT broker

2 x 4 in 1 Led Matrix - Configured into 16 x 32 to display more options

Buzzer - For alarm setup

For the broker i can also try to run it in the broken surface pro that i have


MQTT Broker - Adafruit.io will handle the feeds going into the ESP32 free version only allows 10 feeds and 30 data connections per minute.

Adafruit IO library takes care of receiving and sending feeds

MQTT library to connect to the broker

Zapier - Will handle the connections between email, weather, to do list etc

Feautures - 
- Time out of the internet, which adafruit.io already provides so no need for a feed.
- Google calendar notification when an event is coming up
- To do list notification maybe use google task for this
- Alarm clock iot will have to see what service we use to integrate or maybe a simple Android app to set the alarm

To use less feeds we can send multiple related data in one feed for example

Alarm feed

1300:1/0700:0\

So i can brake one feed into a multiple alarms : separates data in a single alarm like if it is enable (0 or 1) and / separates alarms with \being the ending.

A decoding code can be developed in order to be able to set different alarms or a pre-defined number of alarms can be set which would be easier.

Setting an alarm will be the most important thing at first so here is what im thinking so far

ESP32 side - The ESP32 has internal variables to store the alarms through hardware buttons these can be changed, if a change is done manually on the clock then the ESP32 should update the feed of the alarm in order to keep everything syncronized, the thing i will have to check if i can get the values to the esp32 even after they have been send that is i can always get the last message on the feed this depends on the broker hence depends on adafruit.io

Alarm App Side - Depending if i decided to create my own app or if i decide to use an existing service. If i create my own when an alarm is changed or added, it should publish the new value to the feed, of course with a 30ish second delay in order to not publish the data every time i make a change, this will save connections to the broker, in order to keep the app synchronised with the clock the app should get the newest value from the feed.


<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.