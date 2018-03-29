---
layout: post
title:  'Learn inverse kinematics of a planar 2 DoF robot
'
date:   2018-03-29 20:34:13 +0100
categories: jekyll update
---

## The network's architecture

![ff net]({{ "/assets/ff_net.svg" | absolute_url }} "Feed Forward Network")\\
*Fig. 1: The network's architecture to learn inverse kinematics.*

A simple fully connected network with one hidden layer and 128 units is used to produce joint coordinates $\mathbf{y}$ in joint space, given the tool center point's position $\mathbf{x}$ in cartesian space.

## 10 epochs

<video width="80%" controls autoplay loop>
  <source src="{{ "/assets/10_epochs.mp4" | absolute_url }}" type="video/mp4">
Your browser does not support the video tag.
</video>
*Fig. 2: The robot's attempt to follow a circle after 10 epochs of training.*

## 100 epochs

<video width="80%" controls autoplay loop>
  <source src="{{ "/assets/100_epochs.mp4" | absolute_url }}" type="video/mp4">
Your browser does not support the video tag.
</video>
*Fig. 3: The robot's attempt to follow a circle after 100 epochs of training.*

## 1,000 epochs

<video width="80%" controls autoplay loop>
  <source src="{{ "/assets/1000_epochs.mp4" | absolute_url }}" type="video/mp4">
Your browser does not support the video tag.
</video>
*Fig. 4: The robot's attempt to follow a circle after 1000 epochs of training.*

## 100,000 epochs

<video width="80%" controls autoplay loop>
  <source src="{{ "/assets/100000_epochs.mp4" | absolute_url }}" type="video/mp4">
Your browser does not support the video tag.
</video>
*Fig. 5: The robot's attempt to follow a circle after 100,000 epochs of training.*
