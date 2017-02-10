---
layout: post
title: "Population pyramid charts for the States of India"
description: "Population pyramid charts, and some observations about inter-state variation in age and sex distributions"
category: blog
tag:
  - R
  - rstats
  - population
  - demographics
  - india
headerImage: false
image: "/images/states-sorted-mean-age2.svg"
author: sainathadapa
---

I searched for [Population pyramid](https://en.wikipedia.org/wiki/Population_pyramid) charts for individual states online, to study inter-state variation in distributions of age and sex distributions, but couldn't find any. I was able to find the related census data at [data.gov.in](https://data.gov.in), and so started working on making some the population pyramid charts myself. This also served as a good use case for using the search functionality that I added to [ogdindiar](https://github.com/steadyfish/ogdindiar).

# Source Code
The data, code and the generated images are available at [github.com/sainathadapa/population-pyramid-states-india](https://github.com/sainathadapa/population-pyramid-states-india). Please feel free to create an issue at the github repo or comment here if any part of the code is unclear.

# Gathering data
I started out looking for data by searching for the phrase 'state population' in [data.gov.in](https://data.gov.in) portal, and was able to find the data that I was looking for. The datasets are located in the catalog: [Population in single year age by Residence and Sex - India and States](https://data.gov.in/catalog/population-single-year-age-residence-and-sex-india-and-states). Unfortunately, each page in this catalog shows a maximum of 6 datasets, and there is no option to filter by a word or a phrase. This is where the functionality that I have written for ogdindiar comes into play (see PRs [#17](https://github.com/steadyfish/ogdindiar/pull/17) and [#18](https://github.com/steadyfish/ogdindiar/pull/18) for more details). I used the `ogdindiar::get_datasets_from_a_catalog` function to get the list of all datasets in this catalog, and filtered the list to get the datasets that I need. Some states had data for both 2001 and 2011 census, but some had only 2001 census data. I used the latest census data for each state/UT. Code for data collection and parsing is present in the files [001_get_dataset_links.R](https://github.com/sainathadapa/population-pyramid-states-india/blob/master/001_get_dataset_links.R) and [002_download_and_parse.R](https://github.com/sainathadapa/population-pyramid-states-india/blob/master/002_download_and_parse.R).

# Population Pyramid charts
The obvious thing to do next is to create the population pyramid charts. I also remembered reading about the questionable utility of population distribution charts before, and after a little bit of searching, found [this post](http://www.randalolson.com/2015/07/14/rethinking-the-population-pyramid/) by Randal Olson. I created the standard pyramid chart for each state, and also a couple of charts described in the Randal Olson's post.

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

You can find the charts for all the states and union territories [here](/blog/pop-charts-all/).

# Population distribution charts for all the states, sorted by mean age:
This chart can be helpful in understanding the variation in age mix between different states.
<a href="/images/states-sorted-mean-age.svg" target="_blank"><img src="/images/states-sorted-mean-age.svg" alt="all-states-pop-distr"></a>

Another chart, this time with traditional population pyramids:
<a href="/images/states-sorted-mean-age2.svg" target="_blank"><img src="/images/states-sorted-mean-age2.svg" alt="all-states-pop-distr2"></a>

# Chart to understand the variation in sex ratio among different age groups and states
<a href="/images/states-sorted-sex-diff.svg" target="_blank"><img src="/images/states-sorted-sex-diff.svg" alt="states-sorted-sex-diff"></a>


