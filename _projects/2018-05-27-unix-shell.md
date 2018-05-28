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

Step 1 is achieved by simulating a DFA in which each state is determined by the character read in from a line of input. The states result in the creation of an "ordinary" or "special" token depending on the type of character and adds these to a dynamically sized array that will be later processed into a single command in the second step.

Special characters aer denoted by "<" or ">" and indicate that the following tokens represent a stdIn or stdOut file that input or output will be redirected to.

![A snippet from LexAnalyze.c showing a portion of the DFA](/projects/ShellLex.png)

Step 2 creates the command by parsing the tokens found in the dynamic array and associating the correct fields with each token. For instance, the token following a stdIn or stdOut redirection token (< or >) must designate the name of a file. Additional arguments for commands that require arguments (such as "cd") are also considered. A data type contained in command.c/h applies these fields to the tokens.

After processing all the tokens and forming an argument, Step 3 is implemented by handling external commands that are handled by the OS such as "date", "vi", and many more. This is done through a simple fork() process that then calls the command with execvp().

In addition, built-in commands native to the Shell are manually implemented in a variety of static functions found in ish.c handling the setting and unsetting of environment variables, the "exit" command, and "cd".

The shell also has a unique way of exiting via keyboard shortcuts as handled by signal handlers. The standard Ctrl-C shortcut exits the shell immediately if a child process is being run via a command but only exits the shell when the parent process is stagnant if Ctrl-C is inputted twice within a 3s period.

![The unique Ctrl-C behavior implemented using signal handlers](/projects/ShellAlarm.png)

A unique workaround was created in which the SIGALRM signal would be handled by a signal handler that would call an **additional** signal handler that handled SIGINT (Ctrl-C) if Ctrl-C was triggered twice within a 3s alarm period.

For example, the first time a user inputs Ctrl-C while the Shell is not handling a process triggers the SIGINT handler that calls a 3s alarm. At the moment, the SIGINT does not cause the shell to exit as normal and instead calls the alarm. The second time the user inputs Ctrl-C within the 3s window, the signal is then passed from the alarm signal handler back to the SIGINT handler which resets Ctrl-C to trigger a default SIGINT signal, exiting the shell.

ish.c: Executed and displays Shell while calling each step of the process. Contains functions handling all built in commands and passes external commands to the OS to execute.

lexAnalyze.c/h: Lexically analyzes a line of input text per Step 1 and produces tokens categorized as ordinary or special.

synAnalyze.c/h: Syntactically parses the tokens from the lexical analyzer and separates the tokens into being the program name, arguments, and redirection files based on the order of input.

command.c/h: Abstract data type representing a program name, its optional arguments, and its optional redirection files.

dynarray.c/h: Abstract object representing a dynamically sized array capable of holding tokens as input.

program.c/h: Stateless module containing the current program name.

token.c/h: Abstract data type representing the input tokens typed by the user.

[All code for the project can be found here](https://github.com/justintranjt/Unix-Shell).
