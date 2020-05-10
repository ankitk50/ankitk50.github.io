---
layout: post
title: Past Projects and Research
---

I spend a lot of my time learning and creating, and I'm trying to be better about documenting the process. To that end, this post will be a summary of some projects I worked on with colleagues while I was in school.

<!--more-->

---

## Project 1: Warehouse Management Robot

The robot prototype was developed as a part of [E-yantra Robotics Competition](https://www.e-yantra.org/) organized by IIT Bombay. The robot uses an ATmega256 by Atmel. The robot was equipped with various sensors for positioning and motion.

We were given a map which had black lines to aid the movement of the robot. The map had some points designated as pick-up zones and deposit zones.

The task of the robot was to identify valid packages based on the color. For e.g. black packages were considered invalid and hence were not picked by the robot. The robot had to search the entire map for valid packages. These packages were picked up by the robot from the pick-up zones and deposited in specified zones in the map. The robot used the shortest possible path to travel from one point to the other.

Here's a short video with our robot in action:
<p align="center"> 
<iframe width="560" height="315" src="https://www.youtube.com/embed/KoRefZWZhJM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>

---

## Project 2: Bus arrival detection using BLE beacons and acoustics

The project aimed at tracking the position of a bus approaching a bus-stop using Bluetooth Low Energy (BLE). 

**Architecture**

The architecture had a BLE beacon (installed inside the bus) and a Raspberry-pi with BLE scanner (installed at the bus-stop). The beacon broadcasted details of the bus needed which is scanned by Raspberry-pi and is displayed at a bus-stop. 

Raspberry-pi also Gaussian Mixture Model(GMM) based audio classifier trained with different audio samples of the traffic noise. Once a bus was detected, the classifier was used to evaluate the traffic congestion and calculate the estimated time of arrival(ETA) of the bus. The project was done under the supervision of Prof.Naveen Aggarwal at Design Innovation Center(DIC), Panjab University. The experimental observations were published in the [paper]({{site.url}}/blog/assets/ICCCN-17-126.pdf) of ICCCN 2017 organized at NITTTR, Chandigarh.

<p align="center"> 
<img src="/blog/assets/bus.jpg">
</p>

---

## Project 3: Depth Estimation

This project uses pairs of photos taken by an endoscope at slightly different depths and a SIFT algorithm to estimate the depth map for an area of interest.

<p align="center"> 
<img src="/assets/depth_map.png" alt="Depth image of a simulated image of a metronome." >
</p>

SIFT was used to create feature descriptors for two endoscopic images, taken at different depths. Using the SIFT descriptors, we identified the best-matching points in the pair of images and used those to calculate a transformation between the two images. From this transformation, we extracted an estimation for the distance between the end of the endoscope and the objects in the images.

---

## Project 4: DNA-Based Logic Gates

In my research as an undergraduate, I studied the construction of and uses cases for DNA-based logic gates. These gates rely on the predictable base-pairing of DNA to operate (A-T, C-G) and emulate the behavior of traditional logic gates: producing an output signal, given an input. The flow of a simple gate is pictured below, where A and A* are complementary strands of DNA. The gate wants to reach an equilibrium state in which all strands are perfectly paired with their match (ex. t-A is paired with t\*-A\*), and to reach this state, some displacement occurs.


<p align="center"> 
<img src="/assets/dna_gate3.png" alt="DNA logic gate with some input and output strands." >
</p>

Input strands are combined with a gate, and then these inputs start base-pairing with the gate; displacing the output strands. The final output strand typically has a fluorescent tag on it that can be measured once the strand is released (the signal is suppressed when the output strand is in a double-stranded configuration). Building off of this structure, pairs of gates can be used together to create AND and OR logic gates. These gates have the potential to be used in transistors or even in medicine that can target cells by their DNA/RNA markers.

---

## Project 5: DNA-Mediated Lithography

I recorded a [short, Vimeo video](https://vimeo.com/112122612) on lithography done in part by DNA-mediated etching of SiO2.

---

If you are interested in my work and thoughts, check out my [Twitter](https://twitter.com/cezannecam) or connect with me on [LinkedIn](https://www.linkedin.com/in/cezanne-camacho-422823b2/).


