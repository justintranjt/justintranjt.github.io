---
layout: post
title: "Avogadro Estimation (Java)"
date: 2017-07-29
description: Estimates the Avogadro Constant by analyzing Brownian motion in polystyrene beads suspended in water
image: /projects/frame00000.jpg
---
![]( /projects/frame00000.jpg )*An individual frame showing the polystyrene beads illuminated against a backdrop of water*

The final project for Princeton University's Intro to Computer Science course involves providing an estimate for Avogadro's Constant (6.02 x 10<sup>23</sup>) using a scientific method involving the analysis of Brownian motion. [All code for the project can be found on the repo](https://github.com/justintranjt/avogadro-estimate). [This assignment](http://www.cs.princeton.edu/courses/archive/spr17/cos126/assignments/atomic.html) was created by David Botstein, Tamara Broderick, Ed Davisson, Daniel Marlow, William Ryu, and Kevin Wayne of Princeton University in 2005 and was personally completed in Spring 2017.

At its core, the estimation comes from gathering data from recorded footage of polystyrene beads undergoing [Brownian motion](https://en.wikipedia.org/wiki/Brownian_motion) in water. The change in position for each bead within each video experiment can be fitted to the Stokes-Einstein relation. Four Java files were needed to translate that data into a single estimation for Avogadro's constant:

[Blob.java](https://github.com/justintranjt/avogadro-estimate/blob/master/src/Blob.java): Representation of a set of light pixels (connected or unconnected) defined as a complete set representing a polystyrene "blob". Has a defined mass and center of mass coordinates in the x-y plane. 

[BeadFinder.java](https://github.com/justintranjt/avogadro-estimate/blob/master/src/BeadFinder.java): Designates a blob of a minimum designated number of pixels as a "bead". Takes in a picture containing blobs and determines which blobs can be considered beads using a recursive depth-first search algorithm. This filters out all extraneous light in each frame of the video to track the actual polystyrene beads in question.

[BeadTracker.java](https://github.com/justintranjt/avogadro-estimate/blob/master/src/BeadTracker.java): Tracks beads and their movement from one frame of a video to the next. Prints the distance change (radial displacement) of each bead after each frame change.

[Avogadro.java](https://github.com/justintranjt/avogadro-estimate/blob/master/src/Avogadro.java): Calculates a self diffusion constant which is then used to approximate the Boltzmann constant and Avogadro's number from the radial displacements found from BeadTracker.java.

What did we do exactly with our code? We simply separated all pixels in the black and white video into two categories: Blobs of light and dark water. The blobs were further divided into polystyrene beads represented by a large set of light pixels and noisy light pixels. Each of those beads was tracked between frames to determine their displacements and that magically allowed us to find Avogadro's constant. In this case, it was found to be the following: 

![]( /projects/avogadro.PNG )*An estimate for Boltzmann's Constant and Avogadro's Number using data from all 10 trials of the experiment*

Not bad, eh? But how exactly did the radial displacements from Brownian movement lead to this constant?

Magic?

Not quite. It's a **bit more complex than that. We first find the diffusion constant with our data in order to approximate the Boltzmann constant and finally predict Avogadro's constant.**

Einstein's relation equation states that <img src="http://mathurl.com/y8oqhwwk.png"></img> where **t** is the time between movements, **σ<sup>2</sup>** is the variance of random movements, and **D** is the diffusion constant we are looking for. The Einstein relation also states that the random displacement of a polystyrene bead with the above variance equation. 

Thankfully, we found the variance of movements by observing the displacements of the polystyrene beads undergoing Brownian motion which can be boiled down to the following equation <img src="http://mathurl.com/ybf33jtf.png"></img>. **r<sup>2</sup><sub>n</sub>** represents radial displacement and is approximated from the 2-dimensional X and Y movement of the beads.

From there, we have the means to calculate the Diffusion constant, **D**. After that, we can calculate the Boltzmann constant with the [Stokes-Einstein relation](https://en.wikipedia.org/wiki/Einstein_relation_(kinetic_theory)#Stokes-Einstein_equation) describing a particle in a viscous solution: <img src="http://mathurl.com/y8h7z7y5.png"></img> where **k** is the Boltzmann constant. With some simple algebra we calculate the Boltzmann constant. T (absolute temperature), η (viscosity of water), and ρ (radius of a polystyrene bead) are all assumed to be constants measured at the beginning of the experiment.

Finally, we can relate the Boltzmann constant to Avogadro's constant with <img src="http://mathurl.com/y7y2velj.png"></img> from the Ideal Gas Law. There we have it! Our estimate for Avogadro's constant came out to be approximately 10% off the actual value. Not bad for some video analysis of light.
