---
layout: post
title: Sunday Update No. 4&#58; The streak is dead - Long live the streak
---

##The Numbers
* Total commits: 6
* Repos contributed to: 3
* Most popular repo: [Grading Rahm](https://github.com/wbez/GradingRahm)
* Most popular days: Jan. 27, 2 commits
* Favorite commit message: ["Tweaks to everything. Final version before launch. Why am I still up."](https://github.com/wbez/GradingRahm/commit/15cdc4b3c88f26af9394fc3bd40f4be3bf033258) 

##What I learned
Mainly I learned that waking up at 4 a.m. and flying 2,500 miles with a 2-month-old baby is a good combination to kill a github streak.

Friday we flew from Chicago to Oakland, and after a day with family and a baby who hadn't slept in 19 hours, I forgot to work on any of my projects. My streak ended at 29 days, the first 29 days of 2015.

I woke up Saturday morning and realized what had happened. While it was incredibly discouraging to see the streak end this early in the project, I'm still planning to continue. Really, happening this soon is even more reason to keep trying to move forward. It won't even take that long to beat my new longest streak.

So here we go. This post is starting a new streak, and now I have a number smaller than 365 to shoot for.

What was even more discouraging was that I spent more time coding (and learned more) in the past two weeks than I had at any other time in the project.

In my [previous post](http://chagan.github.io/sunday-update-3/) I discussed a private repo I was spending a lot of time on. That private project is now public, and you can find it at [wbez.org/GradingRahm](http://interactive.wbez.org/gradingrahm) and the code for the project [in this repo](https://github.com/wbez/GradingRahm).

I laid out one of the things I learned in the last post, but there are a few other things I wanted to document here:

###Consistent navigation
One of our main goals with the page was to make it mobile-friendly. Our main website isn't great on anything other than a desktop, so we're trying to make more content that's good on multiple devices. That led to a few issues with presentation, mostly around our navigation. 

I wanted to avoid the [ubiquitous hamburger menu](http://blog.manbolo.com/2014/06/30/apple-on-hamburger-menus), so we decided to take our navigation from the left rail to the top of the page on tablet and mobile views. We used an unordered list with four elements to hold the four sections of the project. This made it easy to run the elements vertically on large screens and horizontally on smaller devices. 

Still, to keep everything responsive, the height and width needed to be dynamic and fill the space available. I set the width of the main ul to 80%, but the height of li's was based on the height of the title text and the Font Awesome icon for each section. Not a big deal except that we had two sections of one word and two with a pair of words. At widths where those two words could be on one line, all the boxes had the same height. At widths where the two words were split on two lines, those boxes were taller than the single word sections.

I tried a number of solutions until I realized what I really needed were new lines on the single word sections at certain widths. Since our navigation was auto-generated through jinja templates, I needed to find a way to do it without adding line breaks by hand in the html. I found a way to do this all through css using the after property and inserting a pair of linebreaks using content and white-space properties.

```
    span.education:after {
        content:"\a\a";
        white-space: pre;
    }
```

This feels a little hacky, so I'll likely revisit it before using it again, but it ended up working for our needs.

###Daily graphics rig
We pulled out another NPR repo for this project: [The Daily Graphics Rig](https://github.com/nprapps/dailygraphics). The DGR makes it easy to produce small one-off graphics for stories, with a number of reusable templates built into the project. The rig uses fabric commands to start new directories for each graphic, either a blank template or one based on D3. A small flask app renders the graphic so you can preview in the browser and generates embed code to add it to the project. Fabric scripts handle graphic creation and deployment to S3. NPR [has a blog post](http://blog.apps.npr.org/2014/05/27/dailygraphics.html) laying out how they use the rig if you want a sense of the basics.

Each Grading Rahm story came with one to three charts (we made nine total), so I knew generating the visualizations quickly would be key to getting everything published on time. While there was a little extra effort at the beginning to get the rig set up and figure out how everything worked, I ended up being able to test out ideas quickly and produce well-made final graphics in a minimum amount of time. I even added one template of my own (a stacked area chart, though [we may not use it too often](http://vizwiz.blogspot.com/2012/10/stacked-area-chart-vs-line-chart-great.html)).

The one issue using the rig on a project like this is loading nine iframes for the graphics. It actually complicated some other [bootstrap elements we were using](http://getbootstrap.com/javascript/#scrollspy). For future projects I hope to customize our fork a little more and incorporate the final graphics into the project itself and not as embedded elements.

###Working together
This was the first real project I did with a coworker taking a large role. 

While I set up the backend (with a lot of help from the [NPR app template](https://github.com/nprapps/app-template)), Curious City reporter/designer/all-around-awesome-person Logan Jaffe did most of the design work.

We worked out of the same repo, but I took the project the first week and handed it over to her once the main skeleton was in place. We both committed changes to the master branch and didn't do a lot of simultaneous work, which made sense for this project. She couldn't style things that weren't in place, and I couldn't tweak responsive elements that didn't have final styles.

While overall this worked fine, it did create bottlenecks for both of us, so I want to sit down with our team and figure out if there's an easier way for us to do everything. That may be doing all changes in branches, splitting up the project into smaller pieces (front and back end are huge chunks) or more pair programming, but things got done in a timely fashion.

##This week
Again, a lot of items I talked about last week are still on this week's to-do list

* I need to write up my formal goals list for this project
* Continue to add features to the blog (archives, comments, etc ...)
* Write up my process for actually creating the blog in more depth
* While the above are still important, I've finished the major project at work so I might actually get some of them done.