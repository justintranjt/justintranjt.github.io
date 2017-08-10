---
layout: post
title: "Avogadro Estimation (Java)"
date: 2017-07-29
description: Estimates the Avogadro Constant by analyzing Brownian motion in polystyrene beads suspended in water
image: /projects/frame00000.jpg
---
![]( /projects/frame00000.jpg )*An individual frame showing the polystyrene beads illuminated against a backdrop of water*

The final project for Princeton University's Intro to Computer Science course involves providing an estimate for Avogadro's Constant (6.23 x 10<sup>23</sup>) using a scientific method involving the analysis of Brownian motion. [All code for the project can be found on the repo. ](https://github.com/justintranjt/avogadro-estimate). This assignment was created by David Botstein, Tamara Broderick, Ed Davisson, Daniel Marlow, William Ryu, and Kevin Wayne of Princeton University in 2005 and was personally completed in Spring 2017.

At its core, the estimation comes from gathering data from recorded footage of polystyrene beads undergoing Brownian motion in water. The change in position for each bead within each video experiment can be fitted to the Stokes-Einstein relation. Four Java files were needed to translate that data into a single estimation for Avogadro's constant:

Blob.java: 

BeadFinder.java:

BeadTracker.java:

Avogadro.java:
