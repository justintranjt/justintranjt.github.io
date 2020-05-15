---
layout: post
title: "2020: A Princeton Space Odyssey (JavaScript/Node.js + WebPack)"
date: 2020-05-14
description: A space exploration arcade game built with Node.js and graphics library three.js along with physics from cannon.js.
image: /projects/hud.jpg
---

![2020: A Princeton Space Odyssey's introductory Menu screen](/projects/menu.png)

# Introduction

## [Play "2020: A Princeton Space Odyssey"](https://teferiemmanuel.github.io/2020-A-Princeton-Space-Odyssey/)

The year is 2020, and you are stranded in outer space, far far away from home. To get home you must travel through a series of wormholes. But here’s the catch, you need fuel to travel through these wormholes.

Pilot a spaceship flying through outer space as you attempt to warp home by collecting fuel charges. The primary objective will be achieved by the player collecting fuel charges as they spawn while avoiding flying asteroids or picking up powerups to become invulnerable to asteroid collisions.

Last as long as possible out in space, pilot!

# What are the basics of the game?

The player must pilot a spaceship in first-person perspective and collect fuel charges to stay alive for as long as possible. While flying through space, they'll have to avoid asteroids flying through space while attempting to collect powerups that provide temporary protection from these flying hazards.

All objects are rendered with three.js with physics interaction to detect collisions using cannon.js. The environment is a skybox formed from a composite image of a space world with randomized particles to give depth to the world.

All objects are procedurally generated as well so that players have a unique experience with each new run.

# How was the game made and what challenges did you run across?

A detailed summary of our challenges can be found in our fully documented paper below. Check it out along with a deeper look into our design decisions and possible future expansions.

# Where can I find the most pivotal details?

All code can be found in the [Github repo](https://github.com/teferiemmanuel/2020-A-Princeton-Space-Odyssey).

The full paper can be found [here](https://github.com/teferiemmanuel/2020-A-Princeton-Space-Odyssey/blob/master/FinalWriteup.pdf).

The slide deck for a quick summary can be found [here](https://github.com/teferiemmanuel/2020-A-Princeton-Space-Odyssey/blob/master/%5BFinal%20Presentation%5D%202020_%20A%20Princeton%20Space%20Odyssey.pptx).

The demo recording can be found [here](https://www.youtube.com/watch?v=na-db3yqfvQ).
