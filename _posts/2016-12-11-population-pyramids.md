---
layout: post
title: "Population pyramid charts for the States of India"
description: "Population pyramid charts, and some observations about inter-state variation in age and sex distributions"
tag:
  - rstats
  - demographics
  - ggplot
---

I looked for [Population pyramid](https://en.wikipedia.org/wiki/Population_pyramid) charts for individual states online, to explore the inter-state variation in distributions of age and sex distributions, but couldn't find any. I was able to find the 2011 Census data at [data.gov.in](https://data.gov.in), and so, I started working on making some the population pyramid charts myself.

# Source Code
The data, code and the generated images are available at [github.com/sainathadapa/population-pyramid-states-india](https://github.com/sainathadapa/population-pyramid-states-india). Please feel free to create an issue at the github repo or comment here if any part of the code is unclear.

# Population Pyramid charts
While creating the charts, I remembered reading about the questionable utility of population distribution charts before, and after a little bit of searching, found [this post](http://www.randalolson.com/2015/07/14/rethinking-the-population-pyramid/) by Randal Olson. I created the standard pyramid chart for each state, and also a couple of charts described in the Randal Olson's post.

Here are the Population distribution charts for  the state of Andhra Pradesh (including Telangana):

<a href="/images/ANDHRA PRADESH-1.svg" target="_blank" style="float: left; width: 30%; margin-right: 1%; margin-bottom: 0.5em;">
  <img src="/images/ANDHRA PRADESH-1.svg" alt="Andhra Pradesh - 1" />
</a>
<a href="/images/ANDHRA PRADESH-2.svg" target="_blank" style="float: left; width: 30%; margin-right: 1%; margin-bottom: 0.5em;">
  <img src="/images/ANDHRA PRADESH-2.svg" alt="Andhra Pradesh - 2" />
</a>
<a href="/images/ANDHRA PRADESH-3.svg" target="_blank" style="float: left; width: 30%; margin-right: 1%; margin-bottom: 0.5em;">
  <img src="/images/ANDHRA PRADESH-3.svg" alt="Andhra Pradesh - 3" />
</a>
<p style="clear: both;" />

You can find the graphs for all the states and union territories [here]({{ site.baseurl }}{% link _posts/2016-12-11-pop-charts-all.md %}).

# Population distribution charts for all the states, sorted by mean age:
This chart can be helpful in understanding the variation in age mix between different states.
<a href="/images/states-sorted-mean-age.svg" target="_blank"><img src="/images/states-sorted-mean-age.svg" alt="all-states-pop-distr"></a>

Another chart, this time with traditional population pyramids:
<a href="/images/states-sorted-mean-age2.svg" target="_blank"><img src="/images/states-sorted-mean-age2.svg" alt="all-states-pop-distr2"></a>

# Chart to understand the variation in sex ratio among different age groups and states
<a href="/images/states-sorted-sex-diff.svg" target="_blank"><img src="/images/states-sorted-sex-diff.svg" alt="states-sorted-sex-diff"></a>


*Post updated on 2018-05-08*
