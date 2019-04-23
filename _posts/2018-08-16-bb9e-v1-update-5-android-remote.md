---
layout: single
title: Android Bluetooth Remote Controller
categories: projects
tags: bb9e
header:
  overlay_image: /assets/images/header/android-remote.png
  show_overlay_excerpt: true
  teaser: /assets/images/teaser/android-remote.png
excerpt: BB9E Robot / Design and built from scratch by Alwurts
author_profile: false
sidebar:
  nav: "bb9e"
toc: true
toc_label: "Contents"
toc_icon: "cog"
comments: true
---
BB9E V1 Android Bluetooth Remote Controller
===========

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