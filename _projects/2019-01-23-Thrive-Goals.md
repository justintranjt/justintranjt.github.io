---
layout: post
title: "Thrive Goals (Flask, Vue.js, PostgreSQL)"
date: 2019-01-23
description: A full-stack web application to help incoming Princeton students structure their workflows for major assignments and projects through efficient goal-setting and deliverable scheduling.
image: /projects/thriveGoals.png
---
![]( /projects/thriveSplash.png )*A screenshot from the Splash page of Thrive*

# Why build Thrive Goals?
Our software helps people break large projects down into manageable subgoals in a goal hierarchy, reducing procrastination and making work more enjoyable and intrinsically motivating. Our system provides users with modifiable templates created by learning specialists and other students to help them structure their work processes for major assignments like papers and coding projects.

Thrive is targeted at Princeton University students and is therefore gated by Princeton's CAS authentication server.

Our system will help professors convey specific task strategies for completing assignments. For example, a professional may indicate that the first goal in writing a paper is gathering quotes before structuring an argument. 

By defining tasks and the order in which they should be completed, the instructor is telling the student how to approach complex work that may otherwise make the student anxious and disoriented. If a student doesn’t  know where to start or how to proceed, they are more likely to procrastinate and experience anxiety.

Just as importantly, Thrive enables the students to see that they are making progress towards their goals as they check off each item on the task hierarchy. The goal will turn green when marked complete and a status bar will show the student’s progress which makes the work more enjoyable for the student since they see tangible progress at each stage. 

# What main features does Thrive provide?
![]( /projects/thriveGoals.png )*A screenshot from the main Goals page of Thrive*

# How was Thrive built?
![]( /projects/thriveUML.png )*A simplified UML Diagram of the Thrive tech stack*

## Backend Systems
### PostgreSQL (SQL Database)
We use a PostgreSQL 10.6 database hosted on Heroku to store data. Specifically, there is just one table called ‘templates’ that consists of the following three columns: username, templateName, and templateJSON.

![]( /projects/thriveDB.png )*A simple view of the database structure used by Thrive*

Once a user creates a template, a new row is created for them in the database. As aforementioned, this row will have their netID, name of their template, and all associated data with the template “templateJSON” (i.e. the fields in goalObject.py stored in a JSON String).

### Flask (Python)
The Flask 1.0.2 microframework for Python 3 is used to write the RESTful API that synchronizes with the client-side Vue.js frontend as well as handle other backend operations such as serving as a layer for accessing the database, page routing, sessions (in conjunction with Beaker sessions), CAS authentication, and many other functions critical to the infrastructure of the application. Note that this Flask application is deployed and served to browsers using Heroku.

### Goal Objects (Python)
Each of a user’s goals are represented with a goal object. For example, a template may have 3 goals. Goal objects can and generally do contain other goal objects. The goal objects stored in each row of the database represent the root nodes of  “goal object tree”. Essentially, the root node contains a list of child goal objects, each element of which may potentially contain its own list of children. 

Everything about a user goal is contained in its corresponding goal object and is able to be adjusted by calling functions of the goal object. Properties of the goal object include the goal title, completion, progress, time spent on the goal, the netID attached to the goal, its parent goal (if it exists), and any subgoals (if they exist).

## Frontend Systems
### Vue.js (Javascript)
We chose Vue to serve as our front-end Javascript framework for a few reasons. As with all Javascript frameworks, it enables us to use AJAX to communicate between the different sections of our tech stack and render new data without requiring the user to reload the page. We chose Vue because it was extremely easy to understand given the limited Javascript knowledge among the developers on our team. The file structure was easy to set up and allowed for a simple one-file-per-webpage structure. This was the major reason for choosing Vue over something more involved such as React or Angular (which would require some more background Javascript knowledge).

### Bootstrap-Vue
Alongside Vue, a standard library for organizing and formatting our application on differently-sized desktop and laptop devices (responsive web design) was needed. We chose Bootstrap as some team members had prior experience using the library and because the barrier to entry was low as the grid-based library was easy to pick up and learn. This also enabled us to make the application usable on mobile devices, essentially making the device cross-platform and accessible for users on nearly any device. The Goals page was the main area of concern but Bootstrap allowed for the columns to be reduced in size on mobile, allowing for comfortable use.

## Backend-Frontend Integration
### RESTful API (Flask)
A RESTful API is used to access data from user actions between the Vue.js frontend and any CRUD operations that are made to the backend. The RESTful API was created with Flask as each method configured with an app.route decorator indicates a route handler for the frontend to consume.

### Axios/AJAX
To connect the client-side Vue.js frontend with the backend, we use the Axios library to send AJAX requests (which are implemented in Axios as XMLHTTPRequests internally). This allows the frontend to perform CRUD operations that affect the database or are affected by the database without having to reload the entire page.

Vue methods that make requests to the RESTful API requests utilize Axios along with variable values found in unique URL paths. GET, PUT, POST, and DELETE requests wrap up important values in JSON format and send them to the API to be handled. Some requests sent with Axios do not contain a JSON file but instead encode the URL sent to the API with the values instead. This is seen in the methods swapGoals (thriveApp.py) and swapGoal (Goals.vue) respectively.

The backend then makes the appropriate changes to the database and sends the information back to the frontend with a JSON file containing a success or failure message.

## Interesting Design Choices
### How should we let users organize their goals?
Because every goal and subgoal is organized in a table in top-down fashion, users can organize their goals easily with buttons on the side to change the positioning of the goal. We had played around with draggable rows on the table at first but realized draggability on a mobile browser would be difficult to implement when a user scrolls through the application. The buttons were a safer and dependable option.
 
### Do we let users create an unlimited number of nested subgoals?
We had a difficult time deciding if users should be able to infinitely nest their subgoals under top-level goals. Ultimately, we approached this from a standpoint of “What would best benefit somebody trying to organize their thoughts?” We decided that a user may organize their goals/steps towards an assignment with a number of complex and detailed steps but anything more than 2 subgoals attached to a goal could be allotted it’s own top-level goal. This would help the user organize their strategies and avoid making things too complex to follow. Additionally, the user interface begins to lose its aesthetic appeal after three levels of nesting, since the indentation would become excessive. 

### How do we represent each goal uniquely? How do we represent subgoals in relation to their parent goals?
Our data is fundamentally hierarchical. Goals are nested under parent goals and can themselves have subgoals. Essentially, the goals form a tree. This is not easily represented in a relational database, however using a non-relational database like MongoDB would be difficult since heroku doesn’t have built in support like it does for Postgres. Ultimately, we decided to represent goals as python objects which are converted into JSON Strings for database storage. These “goal objects” enable complicated tree operations while simultaneously being easy to store. 
 
Each goal object must contain a reference to its subgoal(s) as well as a reference to its single parent goal if it exists, which it doesn’t if we are at the root node. This is how we identify the root node goal object containing the template title. In this sense, each template is itself a “goal object”, specifically the root node of a goal tree, with its parent node set to None. 

Each goal must be unique (even if their titles are the identical). Rather than having object reference data types that would have to be maintained throughout the PostgreSQL database, Flask API, and Vue frontend, we chose to use a unique integer value that could be automatically assigned as a field of each created goal: The time it was created! So, a goal has its own unique time value corresponding to when it was created (in Unix time) that no other goal has.
