---
title: Math for Machine Learning and Deep Learning
author: Ryley Higa
date: 2025-02-03
category: math
ordering: 001
layout: post
---

# Probability
**Probability** is an important aspect of machine learning and deep learning because it allows us to quantify uncertainty of our predictions. One important aspect is that there is no absolute quantification of uncertainty meaning that two people can come up with valid, different models when observing the same data. Validity is determined by a set of rules governing probability rather than a strict source of truth. In this section, we will go over these rules as well as some applications.
## Random Variables
**Random variables** are functions that assign a numerical value to elements in the sample space. A random variable is **discrete** if we can assign **probability mass** to any value the random can take on. The function that assigns mass to discrete random variables is called a probability mass function (PMF).

$$
P(X=x) = p(x)
$$

Probability mass function have two constraints: the function must be greater than 0 and less than 1, and the total mass must equal 1.  

On the other hand, continuous random variables have no probability mass at a particular value. Instead we assign densities to continuous random variables and compute mass by integrating the density in a given subset. The function that assigns density to a continuous random variable is called a probability density function (PDF). 

$$
p(a < X < b) = \int_a^b p(x) dx
$$

## Joint and Conditional Distributions
Joint distributions are formed by the conjunction of two random variables. 

$$
p(x, y) = p(X=x \text{ and } Y=y)
$$

The **sum rule** (also known as **marginalization**) tells us how to relate single variable to joint distributions.  

$$
p(x) = \sum_y p(x, y)
$$

Note that the sum over all random variables in a joint distribution should equal $1$. On ther other hand, conditional distributions denoted as $p(x | y)$ are renormalized joint distributions such that the sum over $x$ for any $y$ is 1. The conditional distribution tells us the probability of $x$ given we know $y$.  

$$
p(x) = \sum_y p(x, y)
$$

## Expectations and Covariances
## Gaussians
The most important distribution is the Gaussian distribution (known as the bell curve or normal distribution). The density is defined by the function:

$$
p(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} \exp \left( \frac{1}{2 \sigma^2} (x - \mu)^2 \right)
$$

## Information Theory
