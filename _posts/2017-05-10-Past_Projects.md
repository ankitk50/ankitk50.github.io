---
layout: post
title: Past Projects and Research
---
I spend a lot of my time learning and creating, and I'm trying to be better about documenting the process. To that end, this post will be a summary of some projects I worked on with colleagues while I was in school.
<p align="center"> 
<img src="/blog/assets/bus.jpg" width="400" height="215" alt="Buss arrival detection">
</p>

<!--more-->
---

## Project 1: Bus arrival detection using BLE beacons and acoustics

The project aimed at tracking the position of a bus approaching a bus-stop using Blue-tooth Low Energy (BLE). 

**Prototype**

The prototype was built over a raspberry-pi 4. A 16x2 LCD screen was used to display details of beacons in range.

<p align="center"> 
<img src="/blog/assets/hmsoft-min.jpg" width="400" height="255" alt="Buss arrival detection">
</p>


**Architecture and Working**

The architecture had a BLE beacon (installed inside the bus) and a Raspberry-pi with BLE scanner (installed at the bus-stop). The beacon broadcasted details of the bus needed which is scanned by Raspberry-pi and is displayed at a bus-stop. 

Raspberry-pi also Gaussian Mixture Model(GMM) based audio classifier trained with different audio samples of the traffic noise. 

Once a bus was detected, the classifier was used to evaluate the traffic congestion and calculate the estimated time of arrival(ETA) of the bus. The details would be displayed on the LCD screen. As soon and the bus arrives at the bus-stop, details of the bus are announced and displayed on the screen.

The project was done at Design Innovation Center(DIC), Panjab University. The experimental observations were published in the [paper]({{site.url}}/blog/assets/ICCCN-17-126.pdf) of ICCCN-2017 organized at NITTTR, Chandigarh.


---

## Project 2: Warehouse Management Robot

The robot prototype was developed as a part of [E-yantra Robotics Competition](https://www.e-yantra.org/) organized by IIT Bombay. The robot uses an ATmega256 by Atmel. The robot was equipped with various sensors for positioning and motion.

We were given a map which had black lines to aid the movement of the robot. The map had some points designated as pick-up zones and deposit zones.

The task of the robot was to identify valid packages based on the color. For e.g. black packages were considered invalid and hence were not picked by the robot. The robot had to search the entire map for valid packages. These packages were picked up by the robot from the pick-up zones and deposited in specified zones on the map. The robot used the shortest possible path to travel from one point to the other.

Here's a short video with our robot in action:
<p align="center"> 
<iframe width="560" height="315" src="https://www.youtube.com/embed/KoRefZWZhJM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

---

## Teaching : Embedded systems

The early exposure to research made me realize that nothing could be more rewarding than exploring new ideas, executing them, and along the way sharing your learning with others. At Design and Innovation Center, Panjab University, I started a group, **‘Embedded group of UIET’** to promote interdisciplinary research among students. I started interacting and teaching sessions after college hours on programming and embedded hardware design. The sessions were open for everyone and became an active space for exchanging ideas on cross-disciplinary research. 50+ students used to take part in these sessions daily. My joy lies in the fact that the group is still active and continues to act as one of the most prominent platforms of technical learning and student projects in the university.  For this initiative, I also received a letter of appreciation from the director of the institute.

<p align="center"> 
<img src="/blog/assets/egu.jpg" width="560" height="315" alt="Buss arrival detection">
</p>

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/oldMagnum) or connect with me on [LinkedIn](https://www.linkedin.com/in/ankitk50/).


