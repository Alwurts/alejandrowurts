---
layout: single
title: Precision 3D scanning using Gom scanner
categories: projects
tags: CAD
header:
  overlay_image: /assets/images/header/gom-scanner.png
  show_overlay_excerpt: true
  teaser: /assets/images/teaser/gom-scanner.png
excerpt: 3D scanning an object into a usable STL.
author_profile: false
comments: true
---
Precision 3D scanning using Gom scanner
===============

Introduction
----------------

The piece that we started with is a scale model of David statue, we wanted to scan this model as a practice on how 3D scanning can be a great tool in design.

The equipment we had available to do the task is an Gom Scanner Atos Core which is a high precision 3D scanner that uses photogrametry techniques to obtain detailed models of small objects.

Below you can see a picture of the scanner we used.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-1.jpg){:.align-center} <center><small><i>Gom Scanner Atos Core.</i></small></center>

Calibration
-------------

The scanner comes with a calibration piece that is stored in a heaby duty briefcase for protection.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-2.png){:.align-center} <center><small><i>Briefcase with calibration tool.</i></small></center>

The calibration tool is a white piece with holes which is placed on the scanner bed, the software in the scanner will then use this piece as a reference for measurements.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-3.png){:.align-center} <center><small><i>Calibration tool.</i></small></center>

The software also asks for a temperature measurement of the bed for which we used a thermometer.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-4.png){:.align-center} <center><small><i>Temperature measurement.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-5.png){:.align-center} <center><small><i>Temperature input window.</i></small></center>

Once we input the temperature the software will guide us on how to move the bed with the calibration tool.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-7.png){:.align-center} <center><small><i>Moving the bed with the calibration tool.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-8.png){:.align-center} <center><small><i>Software calibration instructions.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-9.png){:.align-center} <center><small><i>Software calibration instructions.</i></small></center>

When we complete the set of instructions the software provides, we will receive a window with the calibration confirmation as below picture shows.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-10.png){:.align-center} <center><small><i>Software calibration succesfull.</i></small></center>

Scanning
---------------

After calibration of the scanner we proceed to prepare the piece to scan. For this task a set of stickers were placed on the piece which the software uses as reference when rotating the piece on the scanning bed.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-13.png){:.align-center} <center><small><i>Tracking stickers.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-11.png){:.align-center} <center><small><i>Statue scale model to scan.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-12.png){:.align-center} <center><small><i>Statue scale model to scan.</i></small></center>

We then proceed to place the piece on the scanning bed using bluetack.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-14.png){:.align-center} <center><small><i>Piece placed on the scanning bed.</i></small></center>

Then using the software we started to capture geometry by taking pictures of different positions as we move and rotate the piece around.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-15.png){:.align-center} <center><small><i>Scan being taken on the software.</i></small></center>

Cleaning the scan
-----------------

The file received to be processed was in the format of .stl file which can be open and manipulated in several software tools. In our case we are interested in cleaning, combining and turning into a solid two separate pieces that we received by scanning a miniature statue of a David.

The software that we chosse to use wa mseshlab and meshmixer wich you are available as a free download, we use meshmixer because it offers an easy way of moving the scan around and also cleaning the parts that we don't need, while meshlab will be used to patch the parts of the scan that might be missing.

Meshmixer
==============
The scans received consisted of two .stl files that were the front and back part of the statue, this files had some cleaning since they had scans from the bluetack used to secure the piece to the bed, other than that the files were detailed and clean. In the next pictures we can see the two scans obtained.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-18.png){:.align-center} <center><small><i>File received for back section.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-19.png){:.align-center} <center><small><i>File received for front section.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-17.png){:.align-center} <center><small><i>File loaded in mesh mixer.</i></small></center>

In order to align the two parts correctly the transform tool was used which allows us to rotate, scale and translate the scan.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-20.png){:.align-center} <center><small><i>Transform tool in meshmixer.</i></small></center>

In order to clean each part we use the selection lazo tool which allows us to select a surface by drawing a circle around it. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-21.png){:.align-center} <center><small><i>Lazo selection tool in meshmixer.</i></small></center>

Then once you have the piece selected you can hit edit -> Discard or it's hot key x.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-22.png){:.align-center} <center><small><i>Selection to be deleted.</i></small></center>

The next step consist in combining the two halves of the statue which is done by using the Union tool that appears when you select the two scans.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-23.png){:.align-center} <center><small><i>Union tool in meshmixer.</i></small></center>

Once we had a single file, we proceeded two export it as an .ply file which can be further manipulated in Mesh lab in order to close the gaps in the scans.

Meshlab
=========

We use Meshlab to patch the surfaces that the scanner wasn't able to acquire.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-24.png){:.align-center} <center><small><i>File opened in Meshlab.</i></small></center>

Once we imported the .ply file into Meshlab we proceeded to use the screened poisson surface reconstruction tool that can be found under the filters -> Remeshing, Simplification and reconstruction, with its default settings. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-25.png){:.align-center} <center><small><i>Screened poisson surface reconstruction tool in Meshlab.</i></small></center>

After the computer handles the calculations we obtain a pretty good surface, were the newly generated surfaces integrate to the scanned ones. Next we save the file as both .ply and .stl to further use it in other applications like 3D printing. The next images show the finished scan in more detail.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-26.png){:.align-center} <center><small><i>Final 3D scan.</i></small></center>

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/CAD/gom/gom-27.png){:.align-center} <center><small><i>Final 3D scan close up.</i></small></center>

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.