---
layout: post
title: Sunday Update No. 1
---

My plan for this project is to make Sunday my day to go back over what I've done in the past week and rehash what I've learned. This was a short week, but this excercise is all about establishing good habits, so here we go.

##The Numbers
* Total commits: 7
* Repos contributed to: 2
* Most popular repo: [google-doc-json](https://github.com/chagan/google-doc-json)
* Most popular day: Jan. 3, 4 commits

##What I learned
First off, I learned that even with a goal of only 15-30 minutes of coding a day, I need to manage my time better. 

Jan. 1 I was covering the WBEZ web desk by myself in a deserted office, so I had plenty of time to work on projects and even start this blog on my lunch break. The next day, though, was a full day at work that didn't include a lot of coding, and nothing I good push. I came home to a not-so-happy 2-month old and a tired wife, so I nearly missed commiting on day two, which would have killed this project after only 24-hours. Not a good start.

As for actual projects, the first and major one was this blog. It's setup using [Jekyll](http://jekyllrb.com/), [github pages](https://pages.github.com/), and the [Poole theme](https://github.com/poole/poole). I followed [this tutorial from Joshua Lande](http://joshualande.com/jekyll-github-pages-poole/), which made the whole process really straightforward and simple. I don't want to duplicate his post, so in short here was my workflow:

* Create a new repo for my main github pages location, chagan.github.io
* Clone Poole locally to a new chagan.github.io folder and delete the exiting git repo
* git init, add origin and then push to master
* Customize the blog _config.yml file and then add my first post
* Commit locally, push to master, and voila, a new blog at [chagan.github.io](http://chagan.github.io/)

The second one I've started is a project I've been promising to our podcast leader Joe DeCeault for a while.

Last year I made a new homepage for the [WBEZ podcasts](http://interactive.wbez.org/podcasts/) using handlebars. It's a simple page, but cleaner than our old site and functional on mobile, which our old page was not. It's feed using a Google spreadsheet that Joe updates and that I download as a csv, convert to json and then upload to an AWS ec2 instance we have running for special projects. It's all flatfiles so it could work on s3, but since we already had the ec2 running, we figured we'd use it.

While I have a solid workflow for the updates, there's no way for Joe (or anyone) to update the page without me, which is not a good setup. I want to create a way for anyone, regardless of coding knowledge or experience, to update the live site after changing the Google doc. Obviously this won't be for everyone, but I'm hoping that adding a few more people will stop situations where there's a critical update that gets ignored becuase I'm away.

I started a new google-doc-json repo and so far have a script that downloads a csv from a Google spreadsheet and converts it to json. I'm using part of the [NPR app template](https://github.com/nprapps/app-template) for downloading the Google doc, and then got some inspiration from [this Chris Keller gist](https://gist.github.com/chrislkeller/4700210) to finish the conversion to json. I originally had used [csvkit](https://github.com/onyxfish/csvkit) to convert the file, but handlebars requires a top-level key, which csvkit doens't support. I was ready to modify csvkit, but changed my mind after reading Chris' post. My solution is much simplier than his at the moment, but I may add similar features as I go.

So far I've gotten a lot more experience with reading and writing csv in python, something I always have to refresh on when I start a new project. I also used the csv.DictReader for the first time.

##This week
My goals for this week include formally writing up my goals for this project as a post. I haven't developed any specific outcomes I'd like for this year, so I want to make time to sit down and really try and visualize where I want to be at the end of this. I feel like without that I'm just going to be drifitng from project to project without stretching myself.

For the blog, I'd like to continue to add features. Maybe an archive and about page, social media buttons (in some form) and possibly comments. I could just us disqus, but I'm looking for another way at the moment. I'm also hoping to put together a longer writeup of the creation of the blog itself, detailing all my steps beyond the short workflow above.

On the google-doc-json project, I want to get a working version that loads the json to AWS. After that I'm going to go back and refactor the code to add more options for each part. Right now all the filenames are hard-coded, as are the sheet options when downloading a spreadsheet. After that I need to figure out how I want to make this accesible to other members of the team. My original thought was making a flask app that runs in the browser, but we'll see.