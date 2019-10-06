---
layout: post
title: "Attention in Neural Networks - A Primer"
description: "Why I ported a Tensorflow project to PyTorch"
tag:
  - deep-learning
  - pytorch
  - tensorflow
---

When I'm learning a new topic, I used to take notes. The very act of writing helps me concentrate better, and also remember the information for a longer time. Ultimately, I found writing to be slow and tiring, and so I switched to typing such notes in *org-mode*. (See my [other post for why I chose org-mode](/blog/why-i-use-org-mode/)). I take a similar approach with Machine Learning concepts. I start with notes on theory, and then move to apply those concepts in projects.

Recently, I was interested in Attention mechanisms and came across this impressive project: [greentfrapp/attention-primer](https://github.com/greentfrapp/attention-primer). The project starts with a simple implementation of the Scaled Dot-Product Attention mechanism, demonstrated on a toy example. It then proceeds to add and demonstrate the other basic units of the [Transformer architecture](https://arxiv.org/abs/1706.03762). The code and the theory is nicely explained, and I highly encourage others to go through the 4 Tasks as well. Thanks [@greentfrapp](https://github.com/greentfrapp)!


The project uses TensorFlow (<1.0). To support my learning, I converted the TensorFlow code to PyTorch. This way, I'm more aware of the minute details of the implementation.

The fork with PyTorch code is here: [sainathadapa/attention-primer-pytorch](https://github.com/sainathadapa/attention-primer-pytorch).
