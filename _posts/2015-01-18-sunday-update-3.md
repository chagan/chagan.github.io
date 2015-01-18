---
layout: post
title: Sunday Update No. 3&#58; Parenting while sick and iterating in Flask templates
---
Week two is done. Again, pace is slow and again there were reasons. Again, streak is alive and I'm feeling good about the project.

##The Numbers
* Total commits: 10
* Repos contributed to: 3
* Most popular repo: Private (for now)
* Most popular days: Jan. 11, 3 commits
* Favorite commit message: ["What is the difference between a week and a month, really?"](https://github.com/chagan/chagan.github.io/commit/e09c9d7516d435133d0ace4f37367dedf0a33325) 

##What I learned
Mainly I learned how to parent while sick.

I got a major cold early this week and it's still hanging around. I missed a day of work and probably should have stayed home longer, as a sore throat held one for an extra day or two. That's an inconvenience normally but a huge issue when you have a 2-month-old who needs to be walked and shushed to sleep every night (multiple times).

You get no days off from parenting. There is no sick time or personal days. You show up everyday no matter what.

My wife took some extra bedtime shifts, but I learned both how to shush with only part of my throat and exactly how effective DayQuil can be. A few times I set her down in her crib and raced to the kitchen to release the deluge building in the back of my throat, but only once did I wake her with a cough. That felt like an accomplishment.

It was exhausting and unpleasant, but we got through it. Though of course this morning my wife told me her throat's starting to feel a little dry, so ...

With all that, though, I kept my goal of a commit a day.

This week's post is going to be a little shorter (ed. note: no, it actually became longer, go figure) as I did most of my coding with a private work repo, though there will be a longer post once that's published and public, which should be by the end of the month. 

I'm getting a lot of practice with Flask and jinja2 templates. We're again using the [NPR app template](https://github.com/nprapps/app-template), which is a Flask app with a number of helper elements and deployment tasks built in. Part of that is the [copytext](https://github.com/nprapps/copytext) library, which takes a Google spreadsheet, downloads it and then turns the resulting xlsx into a python object. My big success this week was tweaking that workflow a bit to fit a wrinkle in our current project.

Copytext renders a spreadsheet as an object with each sheet as a child. For example, this saves a spreadsheet as 'copy' and then accesses a sheet within it called topics:

{% highlight python %}
copy = copytext.Copy(app_config.COPY_PATH)
topics = copy['topics']
{% endhighlight %}

In most cases, you pass the 'COPY' object to flask as a context and then render it with jinja. In the template you can iterate over rows and cells, which works great when you have uniform lists of information. If everything has a title, author, text, etc., you're set.

In our current project that wasn't going to work. We have four sets of information with three children, but one child has children of its own that need to be iterated over. To fix that I did some preprocessing of the copy object, nesting the information from multiple sheets under one object:

{% highlight python %}
    for topic in topics:
        slug = topic['value']
        story_sheet = '%s_foo' % slug
        grades_sheet = '%s_bar' % slug

        topic_context = {}
        topic_context['foo'] = copy[foo_sheet]
        topic_context['bar'] = copy[bar_sheet]
        context['TOPICS'][slug] = topic_context
{% endhighlight %}

I then needed to figure out how to handle that within the jinja template, which led to a lot of reading about python dictionaries and [iteritems()](http://stackoverflow.com/questions/3744568/why-do-you-have-to-call-iteritems-when-iterating-over-a-dictionary-in-python), which makes the key,value pairs iterateable:

{% highlight python %}
{% raw %}
{% for key,value in TOPICS.iteritems() %}
	# some html
	{% for row in value.bar %}
		#some more html
	{% endfor %}
{% endfor %}
{% endraw %}
{% endhighlight %}

*Update: Also learned that jekyll doesn't play well with markdown code blocks that contain template for-loops. The solution is to use the [Liquid syntax highlighting and the raw tag](http://sarathlal.com/escape-liquid-template-tags-in-jekyll-posts/).*

Since our whole editorial team is working with the Google spreadsheet, this backend process keeps the doc clean, without needless nesting within the spreadsheet or rows with dozens of columns to hold all possible values for a topic. Little thing, but I could see us using this again in the future.

Also did a little bit of work on [google-doc-json](https://github.com/chagan/google-doc-json), a project that allows a user to download a Google spreadsheet (see a trend?), convert it to json and then upload it to S3, with the idea that it will be used by a handlebars.js template.

This week I added the ability to specify some command line arguments when running the script, but not sure of that's the route I want to go down. Also added a config.py file to hold some variables, and that might be more of what the final product is like.

##This week
Again, a lot of items I talked about last week are still on this week's to-do list

* I need to write up my formal goals list for this project
* Continue to add features to the blog (archives, comments, etc ...)
* Write up my process for actually creating the blog in more depth
* While the above are still important, I have a major deadline at work that will take up most of my coding time. That's not a bad thing, but will push those other items back another week. Still, I'm going to learn a lot from this and I'm happy to have the opportunity to do it.