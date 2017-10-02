---
layout: post
title: "Hacker News Twitter Bot (Python)"
date: 2017-08-26
description: Automatically tweets and provides an updated screenshot of the top posts on Hacker News 
image: /projects/hnewsbot.PNG
---
![]( /projects/hnewsbot.PNG )*The Twitter bot working as planned*

# Why create this project?

To put my newfound Python skills to practice, I decided on creating a project that would first and foremost be personally useful to me. What did that mean in the end? I chose to create a small automated bot that would replace an existing Twitter account I followed ([@newsycombinator](https://twitter.com/newsycombinator)) which linked to the top articles posted on the popular computer-science-oriented news aggregator known as [Hacker News](https://news.ycombinator.com)

With that I created [@HackerNewsPosts](https://twitter.com/HackerNewsPosts)

# Why fix what isn't broken?

The changes I made were small quality-of-life improvements that would improve my overall experience with viewing Hacker News articles from my Twitter feed. Often, I can't even be bothered to go out of my way to search for interesting articles from the news sources themselves or even on Hacker News. So, Twitter has become a way for me to aggregate those interesting sources all onto one handy, updated page.

But why not stick with following @newsycombinator for my Hacker News needs? My gripes with the account came down to its lack of links to the ever-important comments sections of respective posts in addition to the constant tweeting of duplicate posts. My goal was to improve on these shortcomings by fixing these problems and even creating my own killer features if possible (all while putting my skills to the test).

# What makes [@HackerNewsPosts](https://twitter.com/HackerNewsPosts) different?

My Twitter bot takes care of the previously mentioned shortcomings by adding a story link and comments section link to each post and making sure that the same post is never tweeted more than once. Every post made by the bot features the newest stories to make it onto the front page of Hacker News since the last tweet cycle (1 hour).

In addition, the bot's banner on Twitter is updated during every cycle with a screenshot of Hacker News' frontpage. Sometimes it's the small changes that make a difference.

# How was the bot made?

To put it shortly, the project is hosted on a Heroku server and utilizes [Tweepy](https://github.com/tweepy/tweepy) to make the tweets and update the banner. The bot was scheduled to run every hour with the help of the [APScheduler library](https://apscheduler.readthedocs.io/en/latest/). [Haxor](https://github.com/avinassh/haxor) was used to access the Hacker News API without having to deal with pesky JSON files. [Selenium](http://www.seleniumhq.org/) and [Pillow](https://github.com/python-pillow/Pillow) allowed for screenshotting and image manipulation while [PhantomJS](http://phantomjs.org/) was used as the headless browser accessing the Hacker News front page.

# Miscellaneous information

Note: The bot does tweet some duplicate tweets from time to time. For some reason it only applies to 1 to 2 out of the 10 posts on the page that make it through Twitter's duplicate removal algorithm in addition to Tweepy's duplicate prevention. More progress will be made on that in the future but for now, it still handles duplicates better than @newsycombinator.

To follow the Twitter account, head over to [@HackerNewsPosts](https://twitter.com/HackerNewsPosts).

If there are any questions feel free to contact me through Email. [All code for the project can be found on the repo](https://github.com/justintranjt/hacker-news-twitter-bot).
