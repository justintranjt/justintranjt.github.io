---
layout: post
title: "Content-Aware Image Resizing (Java)"
date: 2018-05-27
description: Implements a content-aware image resizing algorithm to analyze images for redundant areas and automatically crops these sections of the images
image: /projects/seamCarved.jpg
---
![]( /projects/seamCarved.jpg )*Multiple possible outputs of a seam-carved image*

A picture says a thousand words, and in the case of this project, a picture only has to show the most essential of its components. This project simply implements the **seam carving** algorithm detailed in the [paper published by Mitsubishi researchers](http://graphics.cs.cmu.edu/courses/15-463/2007_fall/hw/proj2/imret.pdf).

Essentially, the algorithm determines the areas with the lowest *energy* as determined by individual pixels relative to the color of the pixels adjacent to it. By forming a seam of low energy pixels, the image can remove the seam and resize the image without this redundant information. This simple but powerful algorithm is often an assignment for university algorithms courses due to its focus on efficiency when manipulating a matrix of pixels and performing a variety of transformations on these pixels.

All code is found in a single file that represents the image data as a **Picture** data type that contains the aforementioned seams of low-energy pixels.

If there are any questions feel free to contact me through Email. [All code for the project can be found here](https://github.com/justintranjt/SeamCarver).
