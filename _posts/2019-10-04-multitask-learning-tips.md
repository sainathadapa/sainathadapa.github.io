---
layout: post
title: "Multi-task learning - Tricks of Trade"
description: "Summary of a talk by Rich Caruana"
tag:
  - deep-learning
---

This is a summary of the talk about Multi-task learning by Rich Caruana at ICML 2019. The talk and the slides can be viewed at [SlidesLive](https://slideslive.com/38917666/tricks-of-the-trade-1). Here are the tricks discussed during the talk:

1. If you can't use certain attributes as inputs (one reason being they might not be available at runtime), use them as outputs.
2. Instead of throwing away features during feature selection, use these unimportant features as outputs.
3. When the output space is huge (e.g. Weather forecasting), the number of weights in the final (fully connected) layer will be massive - 1000 hidden units * 10M-100M tasks = 10B-100B weights in the last layer! Hence it is not currently feasible to train such a model. Here, for example, instead of having every latitude, longitude, altitude, time step combination as output space, bring the latitude and longitude into the input space and thus reduce the output space to manageable size.
4.  If you can define multiple losses for your task, train jointly using all these losses. Create multiple copies of outputs and each set for a particular loss function.
5. Even if you only have a single loss function, make multiple copies of outputs after the last hidden layer. This shouldn't work but seems like it helps a bit, as each of these outputs are initialized a little bit different at the start.
6. Do not assume that training all tasks together is good for all tasks! At minimum, train tasks together, and also as separate tasks. Find out the tasks that work well when trained separately. If feasible, train all pairs of tasks together to create "help-hurt matrix".
7. Task A may help Task B, but B may hurt Task A. Sometimes easy tasks don't benefit from hard tasks, but hard tasks benefit from easy. Try to find optimal network and extra tasks for each task, 1-at-a-time.
8. Benefit of Transfer learning depends on sample size. At very small dataset size, Multi-task learning (MTL) and Single-task learning (STL) are similar in performance. As the number of data points increase, MTL performs better than STL. But once you reach large enough sample size, STL is better.
9. If a complex task can be decomposed into sub-components, those are often helpful extra tasks.
10. Extra tasks that force model to attend to important aspects of the data can be very valuable! Task that force attention are often from the future.
11. Not all tasks train at the same rate. Ideally we want all tasks to peak at about the same time, or want helper tasks to peak just before the main task. One approach is to early stop each task individually, making a snapshot of net at each task's peak epoch. Another approach is to retrain the model after adjusting the learning rate to speed-up and slow-down tasks.

References:
- [Tricks of Trade - 1](https://slideslive.com/38917666/tricks-of-the-trade-1)
- [Tricks of Trade - 2](https://slideslive.com/38917691/tricks-of-trade-2)
