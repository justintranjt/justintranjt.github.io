---
layout: post
title: "Avogadro Estimation (Java)"
date: 2017-07-29
description: Estimates the Avogadro Constant by analyzing Brownian motion in polystyrene beads suspended in water
image: /projects/frame00000.jpg
---
![]( /projects/frame00000.jpg )*An individual frame showing the polystyrene beads illuminated against a backdrop of water*

The final project for Princeton University's Intro to Computer Science course involves providing an estimate for Avogadro's Constant (6.23 x 10<sup>23</sup>) using a scientific method involving the analysis of Brownian motion. [All code for the project can be found on the repo.](https://github.com/justintranjt/avogadro-estimate). This assignment was created by David Botstein, Tamara Broderick, Ed Davisson, Daniel Marlow, William Ryu, and Kevin Wayne of Princeton University in 2005 and was personally completed in Spring 2017.

At its core, the estimation comes from gathering data from recorded footage of polystyrene beads undergoing [Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion) in water. The change in position for each bead within each video experiment can be fitted to the Stokes-Einstein relation. Four Java files were needed to translate that data into a single estimation for Avogadro's constant:

[Blob.java](https://github.com/justintranjt/avogadro-estimate/blob/master/src/Blob.java): Representation of a set of light pixels (connected or unconnected) defined as a complete set representing a polystyrene "blob". Has a defined mass and center of mass coordinates in the x-y plane. 

[BeadFinder.java](https://github.com/justintranjt/avogadro-estimate/blob/master/src/BeadFinder.java): Designates a blob of a minimum designated number of pixels as a "bead". Takes in a picture containing blobs and determines which blobs can be considered beads using a recursive depth-first search algorithm. This filters out all extraneous light in each frame of the video to track the actual polystyrene beads in question.

[BeadTracker.java](https://github.com/justintranjt/avogadro-estimate/blob/master/src/BeadTracker.java): Tracks beads and their movement from one frame of a video to the next. Prints the distance change (radial displacement) of each bead after each frame change.

[Avogadro.java](https://github.com/justintranjt/avogadro-estimate/blob/master/src/Avogadro.java): Calculates a self diffusion constant which is then used to approximate the Boltzmann constant and Avogadro's number from the radial displacements found from BeadTracker.java.

What did we do exactly with our code? We simply separated all pixels in the black and white video into two categories: Blobs of light and dark water. The blobs were further divided into polystyrene beads represented by a large set of light pixels and noisy light pixels. Each of those beads was tracked between frames to determine their displacements and that magically allowed us to find Avogadro's constant. In this case, it was found to be the following: 

![]( /projects/avogadro.PNG )*An estimate for Boltzmann's Constant and Avogadro's Number using data from all 10 trials of the experiment

Not bad, eh? But how exactly did the radial displacements from Brownian movement lead to this constant?

Magic.

Just kidding. It's a bit more complex than that.
