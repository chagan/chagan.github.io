---
layout: post
title: Sunday Update No. 5
---

##The Numbers
* Total commits: 11
* Repos contributed to: 3
* Most popular repo: [Leaflet Slider Template](https://github.com/chagan/LeafletSliderTemplate/commits?author=chagan)
* Most popular days: Mar. 17-20, 2 commits each

##What I learned
Last time I learned that travel and family can get in the way of side projects. This time I learned that work can have the same effect.

This is my first full week of commits in five weeks. Oddly enough, that first week I missed (Feb. 21), was the weekend before Chicago's mayoral election and the [launch of a new project](http://interactive.wbez.org/elections/artifacts/2015/) for election night. Since then I've also been supporting a [campaign finance tracker](http://interactive.wbez.org/campaigncash/) we built earlier in the month.

While my github log [shows a number of missed days](https://github.com/chagan), I feel like I've been working and writing more code than ever, so I'm not so worried about actually missing days.

While there's a lot I'd like to cover, in this post I wanted to highlight the project I finished most recently and that might have the most use for others.

### Leaflet Slider Template
One of the projects I put together after the election was an update for the the [mayoral dot map](http://wbezdata.tumblr.com/post/86343915004/mapping-rahm-emanuels-2011-victory-and-how-that) we did last year. I wasn't sure the best way to show a comparison between the two, but eventually decided to try and build a before-and-after style slider.

I started with [KnightLabs' juxtapose.js](http://juxtapose.knightlab.com/), a library for achieving the effect with two photos. Pretty quickly I decided that it was going to be more work to modify that project than start fresh with a different approach.

I found a tutorial close to what I wanted on the [mapbox website](https://www.mapbox.com/mapbox.js/example/v1.0.0/swipe-layers/), but there were a few issues. One, I wanted the range slider to be a line down the entire map, and two, the tutorial didn't really work, as the slider would stop changing the tile layers after a zoom.

I thought it would be a simple change to the style, but that was before I learned to vagaries of the html5 range slider and what it takes to get it working on Chrome, Firefox and IE (at any level).

First off, [this post](http://brennaobrien.com/blog/2014/05/style-input-type-range-in-every-browser.html) helped a lot in getting everything put together.

Starting at the end, here are all the styles I needed to turn the normal range to a simple black line that stretched from the top of the container to the bottom:

{% highlight css %}
/* Main slider styles */
.range {
  position:absolute;
  top:0px;
  margin:0px;
}

input[type=range] {
    -webkit-appearance: none;
    z-index: 99;
}

input[type=range]::-webkit-slider-runnable-track {
    width: 100%;
    height: 0px;
    margin-left: -20px;
    margin-right: -20px;
}

input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none;
    border: none;
    height: 9000px;
    width: 40px;
    background: #333;
    background-clip:content-box;
    margin-top: 0px;
    cursor: col-resize;
    padding:0px 17px;
}

input[type=range]:focus {
    outline: none;
}

/* Firefox slider styles */
@-moz-document url-prefix() {
    input[type=range]{
        /*required for proper track sizing in FF*/
        width: calc(100% + 40px);
        z-index: 99;
        border: 0px solid white;
        padding:0px;
        margin-left: -20px;
    }
}

input[type=range]::-moz-range-track {
    width: calc(100% + 40px);
    height: 0px;
}

input[type=range]::-moz-range-thumb {
    border: none;
    height: 9000px;
    width: 6px;
    background: #ED1C24;
    background-clip:content-box;
    margin-top: 0px;
    cursor: col-resize;
    padding:0px 17px;
}

input[type=range]:-moz-focusring{
    outline: none;
    outline-offset: -1px;
}

input[type=range]:focus::-moz-range-track {
    background: #ccc;
    opacity: 0;
}

input[type=range]::-moz-focus-outer {
    border: 0;
    }

/* IE slider styles */
input[type=range]::-ms-track {
  width: 100%;
  height: 9000px;
	background:transparent;
}

input[type=range]::-ms-thumb {
    border: none;
    height: 9000px;
    width: 6px;
    background: #333;
    background-clip:content-box;
    margin-top: 0px;
    cursor: col-resize;
}

input[type=range]::-ms-fill-lower {
	background:transparent;
}
{% endhighlight %}
[Here's the finished version of the project](http://wbezdata.tumblr.com/post/112635810189/one-dot-for-every-voter-comparing-rahm-emanuels), and here's a [template version available on github](https://github.com/chagan/LeafletSliderTemplate).

The main thing I learned from doing it this way? It's not worth it. Knowing what I know now, I would have turned around sooner and used something like jquery ui or maybe even had tried harder to work with juxtapose. And as much as people like to make fun of Internet Explorer, the differences between Chrome and Firefox were even worse. Using the range slider is a pain, will be difficult to maintain going forward and a hassle for anyone to modify. 

Still, I hope the template will be useful to anyone else looking to do something like this, even if they just pull out the guts and use a different input method.

This is the first truly open-sourced project I've done on my own, and I hope to hear if anyone has suggestions for improvements. I know this isn't the best solution to the problem, and I'd love to work to make this better going forward.

##This week
Again, a lot of items I talked about last week are still on this week's to-do list

* I need to write up my formal goals list for this project
* Continue to add features to the blog (archives, comments, etc ...)
* Write up my process for actually creating the blog in more depth
* Write up the process for the campaign finance tracker