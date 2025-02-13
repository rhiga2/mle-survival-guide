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
* A function applied to a random variable is a random variable itself (i.e. $f(X)$ is a random variable). 

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
### Law of the Unconscious Statistician Lotus (LOTUS)

$$
E[g(X)] = \int g(u) f_X(u) du 
$$

### Linearity of Expectation

$$
\begin{gathered}
E[aX + b] = \int (au + b) f_X(u) du = aE[X] + b \\
E[X + Y] = E[X] + E[Y]
\end{gathered}
$$

### Variance
* Variance measures the spread of a distribution. High variance means high spread. 
* Let $\mu = E[X]$ of random variable $X$, the variance is defined as:

$$
\begin{aligned}
\text{var}(X) = E[(X - \mu)^2] = E[X^2 - 2\mu X + \mu^2] \\
\text{var}(X) = \mu^2 - E[X^2]
\end{aligned}
$$

### Law of Total Expectations
### Moments
### Moment Generating Functions

## Transformation of Random Variable


# Joint and Conditional Random Variables
## Joint Distributions
* If the random variables are independent, then the expectation of the product of $X$ and $Y$ is

$$
E[XY] = \int \int uv f_{X. Y}(u, v) du dv = \int du u f_X(u) \int dv v f_Y(v) = E[X]E[Y]
$$

## Covariance and Correlation

## Sum of Random Variables
* Since LOTUS applies to joint distributions, the expectation of the sum is the sum of expectations.

$$
\begin{aligned}
E[X + Y] &= \int \int (u + v) f_{X, Y}(u, v) du dv \\
  &= \int \int u f_{X, Y}(u, v) du dv + \int \int x f_{X, Y}(u, v) du dv \\
  &= \int du u \left( \int dv f_{X, Y}(u, v) \right) + \int dv v \left( \int du f_{X, Y}(u, v) \right) \\
  &= E[X] + E[Y]
\end{aligned}
$$ 

* If the random variables are independent, then the variance of the sum is the sum of variances.

$$
\begin{aligned}
\text{var}(X + Y) = E[(X+Y)^2] \\
\end{aligned}
$$

## Conditional Expectations
* The conditional expectation $E[X | Y]$ is a function of $Y$ and is thus a random variable.
* By LOTUS and the law of total expectation,

$$
E[E[X|Y]] = \int f_Y(v) E[X|Y=v] dv = E[X]
$$

* More generally we have $E_Z[E[X|Y, Z]] = E[X|Y]$. 


# Convergence of Random Variables

## Law of Large Numbers and Central Limit Theorem
## Concentration Inequaties

# Information Theory
## Entropy
* Entropy is the measure of uncertainty in a distribution / random variable.

$$
H[X] = -E[\log f_X(u)] = -\int f_X(u) \log f_X(u) du
$$

## KL Divergence

## Mutual Information
* Tells us how close $X$ and $Y$ are indenpdent random variables.
