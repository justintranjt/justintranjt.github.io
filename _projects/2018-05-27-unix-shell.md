---
layout: post
title: "Unix Shell (C)"
date: 2018-05-27
description: Implements a content-aware image resizing algorithm to analyze images for redundant areas and automatically crops these sections of the images
image: /projects/Shell.png
---
![]( /projects/Shell.png )*The Unix shell called ish (Interactive SHell) running multiple commands*

Creating a functioning Unix shell boils down to a 3-step process:
1. Fetch a line of input into the shell and lexically analyze the characters to break the line into a variety of specially categorized tokens.
2. Decode the collection of tokens and create a command consisting of the command name and optional arguments and input and output buffers.
3. Execute the given command.

ish.c: 

lexAnalyze.c/h:

synAnalyze.c/h:

command.c/h: Abstract data type

dynarray.c/h: Abstract object

program.c/h: Stateless module

token.c/h: Abstract data type

[All code for the project can be found here](https://github.com/justintranjt/Unix-Shell).
