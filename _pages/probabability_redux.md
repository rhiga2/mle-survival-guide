---
title: Probability Redux
author: Ryley Higa
date: 2025-02-03
category: math
ordering: 002
layout: post
---

# Probability Spaces

# Random Variables
* A random variable is a function mapping the sample space to a number. 
* If set of values $X$ can take on is countable, $X$ is discrete. Otherwise, continuous.
* We can assign a probability to some value of $X$ if $X$ is discrete. If $X$ is continuous, we can only assign a probability that $X$ falls in set.

## Probability Mass Function (PMF)
## Probability Density Function (PDF)
## Cumulative Distribution Function (CDF)
* CDF defines the how likely $X$ is less than some value.

$$
\begin{gathered}
F_X(u) = P(X < u) \\
F_X(u) = \begin{cases}
  \sum_{k = -\infty}^u p_X(k) & \text{X discrete} \\
  \int_{-\infty}^u f_X(t) dt & \text{X continuous} \\
\end{cases}
\end{gathered}
$$

## Expectations
### Law of the Unconscious Statistician Lotus
### Moments
### Moment Generating Functions


# Joint and Conditional Random Variables
## Joint Distributions
## Sum of Random Variables
* Let $Z = X + Y$.
* Since LOTUS applies to joint distributions as well, the expectation of $Z$ is

$$
\begin{aligned}
E[Z] &= \int \int (u + v) f_{X, Y}(u, v) du dv \\
  &= \int \int u f_{X, Y}(u, v) du dv + \int \int x f_{X, Y}(u, v) du dv \\
  &= \int du u \left( \int dv f_{X, Y}(u, v) \right) + \int dv v \left( \int du f_{X, Y}(u, v) \right) \\
  &= E[X] + E[Y]
\end{aligned}
$$ 
## Conditional Expectations


## Law of Large Numbers 
## Central Limit Theorem
## Concentration Inequaties
