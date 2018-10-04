---
layout: post
title: "Snippets"
headerImage: false
author: sainathadapa
---

**_This page has code, graphics, or small pieces of text that may not warrant writing a full blog post_**

<div class="breaker"></div>

* TOC
{:toc}

<div class="breaker"></div>

### 2018-04-30 Crude implementation of dplyr's glimpse function in Python
I like the R's `str` function, or better the dplyr's `glimpse` function. I tried to replicate most of the functionality in this function: [gist.github.com/sainathadapa/08c1028c92684fe1ec89ecb5d5629a57](https://gist.github.com/sainathadapa/08c1028c92684fe1ec89ecb5d5629a57). Sample output from the function:
```
In [3]: df = pd.DataFrame({'var1': [1, 2, 3], 'var2': ['a', 'b', 'c']})
In [5]: glimpse(df)
Shape:  (3, 2)
var1 int64  0 NAs : 1, 2, 3
var2 object 0 NAs : a, b, c
```
<div class="breaker"></div>

### 2017-04-05 Statewise distribution of Top 100 Engineering Institutions

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Statewise distribution of Top 100 Engineering Institutions<a href="https://t.co/cWlsMDdcq2">https://t.co/cWlsMDdcq2</a> <a href="https://t.co/9hr9FGt8ab">pic.twitter.com/9hr9FGt8ab</a></p>&mdash; Sainath Adapa (@sainathadapa) <a href="https://twitter.com/sainathadapa/status/849608950601461760">April 5, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

<div class="breaker"></div>

### 2017-02-17 Failed attempt at plotting import-export relationships among Indian states

<a href="/images/import-export.jpg" target="_blank"><img src="/images/import-export.jpg" alt="import-export"></a>

I found the above table from the [Economic Survey 2016-17](http://indiabudget.nic.in/es2016-17/echapter.pdf). I (naively) thought a sankey chart would suit this type of data well. I made a couple of sankey charts after extracting the data from the pdf. [Link to the sankey chart](/import-export-states-sankey) and [link to the source code](https://gist.github.com/sainathadapa/ff621ec86f464538119200b30eedba36).

<div class="breaker"></div>

### 2017-02-17 Generating a consolidated RSS feed from various sources
I wrote a script that creates a consolidated feed from various subreddits and other RSS/Atom feeds (I use Google news feeds for specific topics), ensuring that the feed doesn't have duplicate entries. [Here is the source code.](https://github.com/sainathadapa/generate-rss-feed)

<div class="breaker"></div>

### 2016-10-30 Simple S3 class for circular objects such as hour, day of week, etc
For some objective that I long forgotten, I needed a hour-minute (without the date part) object, which would wrap back to 00:00 after 23:59. I managed with using POSIXct objects when I actually needed this class. Today, I wrote a small S3 class implementation of it, in case I needed it at a later time. Head over to [README](https://github.com/sainathadapa/circularObjs) page, if you want to know the further details.


