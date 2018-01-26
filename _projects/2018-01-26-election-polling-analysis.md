---
layout: post
title: "2016 Presidential Election Polling Analysis (R)"
date: 2018-01-26
description: A data analysis project looking at the state-by-state voting patterns from polls and actual results of the 2016 presidential election.
image: /projects/ElectionRMD.PNG
---
![]( /projects/ElectionRMD.PNG )*The RMarkdown output of a section from the data analysis*

# Why create this project?
The outcome of last year’s presidential election was a big surprise to many of us. Even on the day of the
election Clinton was estimated to have a winning chance of 71.4% compared to 28.6% for Trump by Nate
Silver.

We will use two datasets: aug_poll.Rdata and 2016_election_result.csv in this project.
aug_poll.Rdata contains poll data collected from polls that closed between Aug. 1, 2016 and Oct. 27, 2016.
This dataset was originally posted on fivethirtyeight.com.

In this project we will study the patterns of the errors in presidential election polling data. We would like to answer these questions:
• Do the errors seem random, and specifically are they distributed symmetrically around zero?
• Among the states with CI (confidence interval) estimates that are away from zero (i.e., among the states that we were confident about whom the winning candidate the state would be), how many of their CIs predicted the correct state winner?

# How was the analysis performed?



# Miscellaneous information

The analysis was originally created in a RMarkdown file. However, Github does not render RMarkdown files nicely. Thus, the file was converted to an ordinary R file with a littany of comments.

To view the RMarkdown output of the file please visit [this link](https://github.com/justintranjt/2016-election-analysis/blob/master/election.pdf).

If there are any questions feel free to contact me through Email. [All code for the project can be found here](https://github.com/justintranjt/2016-election-analysis).
