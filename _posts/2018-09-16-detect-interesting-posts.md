---
layout: post
title: "Detect interesting posts in RSS Feeds"
headerImage: false
author: sainathadapa
tag:
  - nlp
  - deep-learning
  - machine-learning
category: blog
description: ""
---

# Introduction
I'm a news addict, sort of. Let me explain.

I follow a bunch of RSS feeds (political and tech news, data science blogs, etc.) in Feedly. Whenever I have few minutes of free time, I open Feedly and browse through latest posts in there. If I find an item interesting, I'll click the link and read through the whole post. (This post is not about me trying to fight back against the habit, although I probably should).

A little back story, before moving to what this post is about: I started following [Android Police](https://www.androidpolice.com/) back when the mobile software was developing at a rapid pace, and I was using custom Android ROMs on my mobile. AP regularly has posts which are only relevant to US audience ([Google Pay adds support for 37 banks in the US](https://www.androidpolice.com/2018/09/13/google-pay-adds-support-30-banks-us/)). They also have weekly posts or other kind of regular posts, which I'm never interested in -  ([22 new and notable (and 1 WTF) Android apps from the last two weeks including Tor Browser, Yahoo!, and FameBit (9/1/18 - 9/15/18)](https://www.androidpolice.com/2018/09/15/22-new-notable-1-wtf-android-apps-last-two-weeks-including-tor-browser-yahoo-famebit-9-1-18-9-15-18/),  [Edge Action turns the edge of your screen into the most useful part of your phone [Sponsored Post]](https://www.androidpolice.com/2018/09/14/edge-action-turns-edge-screen-useful-part-phone-sponsored-post/)).

This is the basic issue that I want to solve. I do not want to browse through posts which I'm never interested in reading. Although the title of this post alludes to detecting interesting posts, the actual objective is to detect uninteresting posts.

# Data collection
I modified my usual setup, so that I can log all the posts that I see, and the ones that I click on.

The first part of the system is a [python script](https://github.com/sainathadapa/generate-rss-feed) that creates a RSS feed from a bunch of sources. The urls in this generated feed are modified so that they point to a Redirect service. The Redirect service is a simple PHP server that logs the post (thus enabling me to gather the posts that I clicked) and redirects the user to the actual post. The generated feed is fed into Feedly via Dropbox.

![flow-chart](/images/flow-chart.png)

# Some stats
I deployed the system during the last week of May. Here are some basic statistics using the data collected over the past few months:
- Average number of feed entries that were browsed per day: 155
- Average number of posts that were read through in full: 25

Top sources by number of entries, and corresponding percentage of articles read:

| Source                   | Total | Clicks | % clicks |
|--------------------------|-------|--------|----------|
| HackerNews               | 3868  | 1298   | 34       |
| Android Police           | 2026  | 118    | 6        |
| Google News - Andhra     | 1975  | 135    | 7        |
| Ars Technica             | 1526  | 158    | 10       |
| Google News - Vijayawada | 1371  | 76     | 6        |
| LiveMint - Opinion       | 862   | 170    | 20       |
| RBloggers                | 693   | 35     | 5        |
| OReilly                  | 258   | 60     | 23       |
| Tomasz Tunguz            | 224   | 4      | 2        |
| Reddit - Linux Gaming    | 212   | 41     | 19       |


# Deep Learning
To predict the probability of a click, I have used the [ULMFiT model](https://arxiv.org/pdf/1801.06146.pdf) (recently released, it has achieved SOTA results in six different text classification tasks). ULMFiT consists of 3 steps:
1. General-domain LM pre-training
2. target task LM fine-tuning
3. target task classifier fine-tuning

For the first step, I used the weights made available by [Fast.AI](http://files.fast.ai/models/wt103/). This model was trained using the Wikitext-103 dataset. Since the amount of text in the current dataset is small, I chose to skip the second step, and proceeded to train the classifier after loading the pre-trained weights.

Here are the ROC curves of the classifier on the validation set:
