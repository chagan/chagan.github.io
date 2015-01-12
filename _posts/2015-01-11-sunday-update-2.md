---
layout: post
title: Sunday Update No. 2
---
This was my first full week with the project. While I kept up on my commit-a-day goal, the pace is still pretty slow (see below). Overall I'm happy though, and the streak is still alive.

##The Numbers
* Total commits: 6
* Total issues reported: 2
* Repos contributed to: 3
* Most popular repo: [google-doc-json](https://github.com/chagan/google-doc-json)
* Most popular days: Jan. 4,6 and 9; 2 commits each 

##What I learned
I'm realizing the main thing I'm learning through this has nothing to do with code and everything to do with habits and outlook.

Our first child was born in November, which means I started this project with a 2-month-old baby in the house. That's meant some nights I'm anxiously looking for something quick to finish on a project and trying to push commits to a repo at 10 p.m. between shifts putting my daughter to sleep.

But that's 1) temporary in as much as she'll start sleeping better (I'm told) as she gets a little older and 2) exactly how it should be.

I'm a father first and everything else second, be it work, hobbies or elaborate self-motivation projects. My wife has been incredibly supportive around this project, helping when she can and also being encouraging about me taking an extra minute to figure a problem out.

I've also found that some of my best ideas have come walking my daughter around the apartment late at night. Some people think better in the shower, apparently I'm at my best on sleep-deprived early-morning walks. Who knew.

As for the coding, this week I spent most my time working on my Google Doc to JSON uploader script, which downloads a Google spreadsheet, converts it to JSON and loads it to S3 (read more on the use case in [last week's post](http://chagan.github.io/sunday-update-1/)).

This time last week I had the spreadsheet downloading and a conversion script to change the csv to json. This week I added the ability to upload to S3 using the AWS Command Line Utility and Fabric. I've used projects that included awscli in the past, but this was my first time working with it directly. I was able to get it working with our station AWS account, which was a minor achievement for me. Everything is still pretty basic, but it does exactly what I set out for it to do.

I also added a basic flask app that allows users to call the script from the browser without having to use the command line at all. This is a step to making the entire process, from updating the doc to uploading it to our servers, available to out head of podcasts if I happen to be away. This can also be reused for any process that requires a download-convert-upload process, potentially anything we use handlebars for.

It's going to look like I missed a day this week, but that's because we restarted an app project at WBEZ that should be launching in the next few months. It's still private for now, but I'm excited to really dig back into it and finally release it.

Oh, and another I learned is that Sublime has an option to [add spellcheck to markdown documents](https://coderwall.com/p/j3tjtq/spell-check-for-markdown-in-sublime-text).

I did a little work on the blog, adding an about page and a few other tweaks, but that leads into ...

##This week
I missed most of the goals I wrote about last week, so a lot of them still stand.

* I need to write up my formal goals list for this project
* Continue to add features to the blog (archives, comments, etc ...)
* Write up my process for actually creating the blog in more depth
* Hit most of my goals for the gdoc uploader, but need to go back in and clean up and expand some of the elements. Specifically, need to go in and add arguments for many of the options that are currently hard coded.