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

One of our main goals with the page was to make it mobile-friendly. Our main website isn't great on anything other than a desktop, so we're trying to make more content that's good on multiple devices. That led to a few issues with presentation, mostly around our navigation. 

I wanted to avoid the ubiquitous hamburger menu, so we decided to take our navigation from the left rail to the top of the page on tablet and mobile views. We used an unordered list with four elements to hold the four sections of the project. This made it easy to run the elements vertically on large screens and horizontally on smaller devices. Still, to keep everything responsive, the height and width needed to be dynamic and fill the space available. I set the width of the main ul to 80%, but the height of li's was based on the height of the title text and the Font Awesome icon for each section. Not a big deal except that we had two sections of one word and two with a pair of words. At widths where those two words could be on one line, all the boxes had the same height. At widths where the two words were split on two lines, those boxes were taller than the single word sections.

I tried a number of solutions until I realized what I really needed were new lines on the single word sections at certain widths. Since our navigation was auto-generated through jinja templates, I needed to find a way to do it without adding line breaks by hand in the html. I found a way to do this all through css using the after property and inserting a pair of linebreaks using content and white-space properties.

```
    span.education:after {
        content:"\a\a";
        white-space: pre;
    }
```

##This week
Again, a lot of items I talked about last week are still on this week's to-do list

* I need to write up my formal goals list for this project
* Continue to add features to the blog (archives, comments, etc ...)
* Write up my process for actually creating the blog in more depth
* While the above are still important, I've finished the major project at work so I might actually get some of them done.