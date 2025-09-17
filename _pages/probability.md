---
title: Probability Redux
author: Ryley Higa
date: 2025-02-03
category: math
ordering: 001
layout: post
---

# Introduction
**Probability** is an important aspect of machine learning and deep learning because it allows us to quantify uncertainty of our predictions. One important aspect is that there is no absolute quantification of uncertainty meaning that two people can come up with valid, different models when observing the same data. Validity is determined by a set of rules governing probability rather than a strict source of truth. In this section, we will go over these rules as well as some applications.

# Random Variables
**Random variables** are functions that assign a numerical value to elements in the sample space. A random variable is **discrete** if we can assign probability mass to any value the random can take on. The function that assigns mass to discrete random variables is called a **probability mass function** (PMF).

$$
P(X=x) = p(x)
$$

Probability mass function have two constraints: the function must be greater than 0 and less than 1, and the total mass must equal 1.  

On the other hand, continuous random variables have no probability mass at a particular value. Instead we assign densities to continuous random variables and compute mass by integrating the density in an interval (say $[a, b]$). The function that assigns density to a continuous random variable is called a **probability density function** (PDF). 

$$
p(a < X < b) = \int_a^b p(x) dx
$$

Similar to probability mass, the probability density function must integrate to $1$ along the entire real line.  

For both probability density and continuous random variables, we can also define a **cumulative distribution function** (CDF) by the following definition: 

$$
F(x) = P(X \le x)
$$

For discrete random variables, we sum mass up to a point $x$:

$$
F(x) = \sum_{u=\infty}^x p(u)
$$

For continuous random variables, we integrate density up to a point $x$:

$$
F(x) = \int_{\infty}^x p(u) du
$$

Note that by fundamental theorem of calculus, the PDF is the derivative of the CDF.

Since CDFs are both valid for discrete and continuous random variables, we often create definitions and state theorems based on CDF so that we don't distinguish about whether 
were discussing discrete or continuous distributions. In this reading though we will talk mostly about discrete random variables and use the PMF in our definitions. 


# Joint and Conditional Distributions
**Joint distributions** are formed by the conjunction of two random variables. 

$$
p(x, y) = p(X=x \text{ and } Y=y)
$$

In joint distributions, we get the distribution of $x$ only by summing over all possible values that $y$ can take on. This process is called the **marginalization** or the **sum rule**. 

$$
p(x) = \sum_y p(x, y)
$$

From the joint distribution, we can also specify the conditional distribution $p(x \vert y)$, which tells us the probability of $x$ given we know about $y$. To get the **conditional distribution**, we renormalize the joint distribution by dividing by $p(y)$.   

$$
p(x \vert y) = \frac{p(x, y)}{p(y)}
$$ 

Two distributions are **independent** if their joint distribution can be factored into their marginal distributions, meaning $p(x, y) = p(x)p(y)$. This implies that $p(x|y) = p(x)$ and $p(y|x) = p(y)$. In other words, information about $Y$ does not affect the distribution of $X$ and likewise information about $X$ does not affect the ditribution of $Y$. 

## Bayes Rule and Interpretations of Probability
The definiton of conditional distributions leads to one of the most important rules in all of probability called **Bayes rule**. Bayes rule is so important that it formed the basis for reinterpreting what probability means.

// TODO

# Expectations and Variance
For any distribution, we can define the center of the distribution by its **expectation**. Expectations are the average value a random variable can take on weighted by their probability. 

$$
EX = \sum_x x p(x)
$$

Since random variables are functions that map to real numbers, any function $f$ that maps real numbers to real numbers applied to a random variable $X$ is still a random variable. 
This means we can take the expectation of functions of random variables:

$$
Ef(X) = \sum_x f(x) p(x)
$$

This is sometimes called the **Law of the Unconscious Statistician** (LOTUS) since it's such an intuitive rule that many statisticians assume it without a second thought.  

Based on LOTUS, we see that expectation are linear:  

$$
\begin{aligned}
E[aX + bY + c] &= \sum_{(x, y)} (ax + by + c) p(x, y) \\
  &= a \sum_x x \left(\sum_y p(x, y)\right) + b \sum_y y \left(\sum_x p(x, y)\right) + c \\
  &= a \sum_x x p(x) + b \sum_y p(y) + c \\
  &= aEX + bEY + c
\end{aligned}
$$

Similar to how expectation defines the center of the distribution, **variance** (and likewise **standard deviation** which is just the square root of variance) defines how spread the distribution is from the expectation. 

$$
\begin{aligned}
\text{var}(X) &= E[(X - E[X])^2] \\
  &= E[X^2 - 2XE[X]] + E[X]^2 \\
  &= E[X^2] - E[X]^2
\end{aligned}
$$

The quantity $E[X^n]$ is often referred to as the **nth moment**. Similar to variance and expectations, moments are very useful tools for describing distributions. The **moment generating function** (MGF) defined by $M_X(t) = E[e^{tX}]$ gets it's name because it can spit out the nth moment by taking the derivative and setting $t=0$. Thus it's easy to reason about distributions with simple MGFs since we can calculate as many moments as we need. 

$$
\frac{d^n}{(dt)^n}M_X(t) \Bigr|_{t=0} = E[X^ne^{tX}] \Bigr|_{t=0} = E[X^n]
$$

# Covariance and Correlation

# Bernoulli, Binomial, and Geometric Distributions
One of simplest discrete phenomenon we can reason about is a coin flip. We usually think of coin flips as 50-50 outcomes between heads and tails, but we can also use the Bernoulli distribution to reason about flips which may not be fair.  

# Gaussians
**Gaussian** distributions are continuous probability distributions that show up in a wide range of fields such as statistics. We define Gaussian distributions uniquely by it's mean $\mu$ and variance $\sigma^2$:

$$
p(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} \exp \left( \frac{1}{2 \sigma^2} (x - \mu)^2 \right)
$$

For multivariate Gaussians, instead of a single-valued mean and variance we instead have a vector of means $\mu$ for each random variable and a covariance matrix $\Sigma$. The covariance matrix not only captures the variance of each random variable along the diagonal, but also the covariances between random variables as well.  

$$
p(x) = \frac{1}{\sqrt{(2 \pi)^k |\Sigma|}} \exp \left( \frac{1}{2} (x - \mu)^T \Sigma^{-1} (x - \mu) \right)
$$


# Convergence of Random Variables
Just like how a sequence of numbers can converge, a sequence of random variables (known as **random processes**) can also converge. Suppose we want to design a robot that guesses a secret number $X$ hourly (each hourly guess is denoted by the random process $X_n$). A bad guess means that the deviation $\lvert X_n - X \rvert$ is large (greater than some value $\epsilon$). If the robot guesses the number with low deviation in one trial run that may be drawn to luck, we want to make sure that our robot design repeatedly converges for multiple different trials. In the following section, we will use this analogy to explain each notion of convergence:
1. Convergence in distribution: the weakest definition of convergence we will discuss. When our random process converges in distribution, that means over time the distribution of our robot's guesses converges to the same distribution that we use to pick our secret number $X$. The actual deviation $\lvert X_n - X \rvert$ is not guaranteed to be small.

$$
\lim_{x \rightarrow \infty} F_n(X) = F(X)
$$

2. Converge in probability: when the random process converges in probability, that means probability of bad guesses (large deviations) becomes more rare over time. Convergence in probability implies converge in distribution. Note that convergence in probability does say anything about the actual size of the deviation only about their rarity. 

$$
\lim_{n \rightarrow \infty} P(\lvert X_n - X \rvert  > \epsilon) = 0
$$

3. Convergence in expectation: when the random process converges in expectation, the expected deviation goes to $0$ over time. This means that the deviation cannot be too large or too likely. Since convergence in expectation constrains both the size and likelihood of large deviation, this notion of convergence is stronger than convergence in probability. Thus convergense in expectation implies convergence in probability.  

$$
\lim_{n \rightarrow \infty} E[\lvert X_n - X \rvert] = 0
$$

4. Almost sure convergence: when the random process converges almost surely, the likelihood that the robot will eventually stop making mistakes over time is one. Almost sure convergence is stronger than convergence in probability but not stronger than convergence in expectation. In fact, both convergence in expectation and almost sure convergence don't say anything about one another. 

$$
P \left(\lim_{n \rightarrow \infty} X_n = X \right) = 1
$$
