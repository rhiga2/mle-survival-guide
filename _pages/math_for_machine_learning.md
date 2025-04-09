---
title: Probability and Statistics for Machine Learning
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

For both discrete and continuous random variables, we can also define a cumulative distribution by the following definition: 

$$
F(x) = P(X < x)
$$

Note that the cumulative distribution is monotonically non-decreasing. 

## Joint and Conditional Distributions
Joint distributions are formed by the conjunction of two random variables. 

$$
p(x, y) = p(X=x \text{ and } Y=y)
$$

In joint distributions, we get a **marginalized distribution** in $x$ by summing over all possible values that $y$ can take on.

$$
p(x) = \sum_y p(x, y)
$$

From the joint distribution, we can also specify the conditional distribution $p(x \vert y)$, which tells us the probability of $x$ given we know about $y$. To get the conditional distribution, we renormalize the joint distribution by $p(y)$.   

$$
p(x \vert y) = \frac{p(x, y)}{p(y)}
$$

## Expectations and Covariances
For any distribution, we can define the center of the distribution by its **expectation**. Expectations are the average value a random variable can take on weighted by their probability. 

$$
E[X] = \begin{cases}
\sum_x x p(x) & \text{ x is dicrete } \\
\int_x x p(x) dx & \text{ x is continuous} 
\end{cases}
$$

The most important property of expectations is linearity as it's used in many scenarios:

$$
E[aX + bY + c] = aE[X] + bE[Y] + c
$$

Similar to how expectation defines the center of the distribution, **variance** (and likewise **standard deviation** which is just the square root of variance) defines how spread the distribution is from the expectation. 

$$
\begin{aligned}
\text{var}(X) &= E[(X - E[X])^2] \\
  &= E[X^2 - 2XE[X]] + E[X]^2 \\
  &= E[X^2] - E[X]^2
\end{aligned}
$$

The quantity $E[X^n]$ is often referred to as the **nth moment**.

## Gaussians
**Gaussian** distributions are continuous probability distributions that show up in a wide range of fields such as statistics. We define Gaussian distributions uniquely by it's mean $\mu$ and variance $\sigma^2$:

$$
p(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} \exp \left( \frac{1}{2 \sigma^2} (x - \mu)^2 \right)
$$

## Convergence
Just like how a sequence of numbers can converge, a sequence of random variables (known as **random processes**) can also converge. Suppose we want to design a robot that guesses a secret number $X$ hourly (each hourly guess is denoted by the random process $X_n$). A bad guess means that the deviation $\lvert X_n - X \rvert$ is large (greater than some value $\epsilon$). If the robot guesses the number with low deviation in one trial run that may be drawn to luck, we want to make sure that our robot design repeatedly converges for multiple different trials. In the following section, we will use this analogy to explain each notion of convergence:
1. Convergence in distribution: the weakest definition of convergence we will discuss. When our random process converges in distribution, that means over time the distribution of our robot's guesses converges to the same distribution that we use to pick our secret number $X$. The actual deviation $\lvert X_n - X \rvert$ is not guaranteed to be small.

$$
\lim_{x \rightarrow \infty} F_n(X) = F(X)
$$

2. Converge in probability: when the random process converges in probability, that means probability of bad guesses (large deviations) becomes more rare over time. Convergence in probability implies converge in distribution. Note that convergence in probability does say anything about the actual size of the deviation. 

$$
\lim_{n \rightarrow \infty} P(\lvert X_n - X \rvert  > \epsilon) = 0
$$

3. Convergence in expectation: when the random process converges in expectation, the expected deviation goes to $0$ over time. This means that the deviation cannot be too large or too likely. Since convergence in expectation constrains both the size and likelihood of large deviation, this notion of convergence is stronger than convergence in probability. 

$$
\lim_{n \rightarrow \infty} E[\lvert X_n - X \rvert] = 0
$$

4. Almost sure convergence: when the random process converges almost surely, the robot will eventually stop making guesses with large deviation over time. The probability of finding a trial where this does not occur is effectively $0$.

$$
P \left(\lim_{n \rightarrow \infty} X_n = X \right) = 1
$$

# Statistics
## Law of Large Numbers and Central Limit Theorem
## Estimation
## Confidence Intervals
## Hypothesis Testing
## Bayesian Statistics

# Information Theory
## Entropy
## KL Divergge
