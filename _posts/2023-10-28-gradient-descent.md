---
title: Gradient Descent
date: 2024-03-02 11:33:00 +0800
categories: [Deep Learning]
tags: [DL]
pin: false
math: true
mermaid: false
toc: true
---

## Overview

Okay, its been awhile but I've been learning a lot. This is one of the highlights...

Gradient descent is essentially the "bread and butter" of deep learning with neural networks.
Neural networks are basically a bunch of simple (or not so simple) components connected together in series (or not in series).
These connected components serve as a function in which data (*x*) goes in and an output (*y* or *f(x)*) comes out. 

$$ f(x) = w*x + b $$

The idea is to figure out what values of *w* and *b* will result in a function that "approximates" some real-world relationship between our input data (*x*) and our output (*y*) (typically a prediction). For example, let's say you have data (*x*) that is information including the time of day, the weather, the day of the week, the day of the year, etc. and you want to make a prediction (*y*) that is the amount of traffic on the roads under those specific circumstances. You would have to find values of *w* and *b* that accurately evaluate to a correct prediction given the input (*x*). The "bread and butter" approach to finding *w* and *b* is **gradient descent**.

## Derivatives

Gradient descent utilizes the derivative, a concept from Calculus. Essentially the derivative of a function (also called the gradient) is its rate of change. For example, see the image below:

![]({{site.url}}/assets/img/favicons/derivative_of_f.png)

In the above image, the derivative of *f(x)* at point *x* is -0.47. This represents the slope of the rate of change and its direction. This is also referred to as "the derivative of *f* with respect to (w.r.t) *x*".

<u>NOTE</u>: If you are unfamiliar with derivatives or the rules of derivation I recommend going to YouTube to watch a video or two about it.

## High-level Gradient Descent

$$ f(x) = w*x + b $$

First, we typically call our values of *w* and *b* weights and biases, respectively. What we want to do is consider our weights and biases as a function of loss. The loss is the metric used estimate how wrong the function *f(x)* is. **The lower the loss, the better**. If we were to graph our weights and biases as a function of our loss. The weights and biases would be on the x-axis and the loss would be on the y-axis. Then, like in the figure above, we find the derivative of our loss with respect to our weights and the derivative of the loss with respect to our biases. We can denote this as $$ \frac {dL}{dw} $$ and $$ \frac {dL}{db} $$. We take our derivates and use them to update our weights and biases. 

$$ w' = w - \frac {dL}{dw} $$ 

$$ b' = b - \frac {dL}{db} $$ 

The subraction of the gradients is the "descent" part of "gradient descent". We want to follow the gradient downward towards lower loss values. If we keep updating the weights and biases based on their derivatives, we will land on values of *w* and *b* that minimize the loss (that result the least amount of error).

## Considerations

In practice, we do not update the weights and biases using their gradients directly. We typically use what's called a learning rate to do smaller updates (or steps) towards the minimum loss value (minima). The learning rate (*lr*) is a coefficient greater the 0 and less that 1. See the example below:

$$ w' = w - lr*\frac {dL}{dw} $$ 

$$ b' = b - lr*\frac {dL}{db} $$ 

When we perform gradient descent, we are optimizing weights and biases from some starting value (initialization). In many applications the weights and biases are intialized randomly and/or at values such as 0 or 1. Gradient descent causes optimizes the weights and biases towards a **local minima** of the loss (the lowest loss in its immediate vicinity), which is not necessarily the **global minima** (the absolute lowest possible loss). We sometimes want to avoid these local minima since the global minima sits where weight/bias values perform as accurately as possible (given the number and type of weights and biases we have defined). Given one local minima, there is likely a deeper local minima that out-performs that one. In other words, we sometimes don't want to optimize into the first minima we find. 

<u>NOTE</u>: I say "we sometimes want to avoid..." because these local minima can perform very well despite not being the global minima. Local minima can perform with high levels of accuracy and robustness that will suffice for a given application.

The process of gradient descent that is described above is vanilla gradient descent (the most basic implementation). Other types of gradient descent are designed to solve problems such as falling in shallow local minima. There are many of these implementations. I recommend researching the most popular ones.

