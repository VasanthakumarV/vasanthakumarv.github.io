+++
title = "Hypothesis testing"
weight = 1
+++

# Introduction

We estimate single unknown parameter of two variations of a product, then we run a Monte Carlo simulation and determine which hypothesis is likely.

# Monte Carlo simulation

Monte Carlo simulation is any technique that makes use of random sampling to solve a problem. In our case, we are going to randomly sample from the two distributions, where each sample is chosen based on its probability in the distribution, so that samples in a high probability region will appear more frequently. We are interested in finding out in how many of these samples one variant is better than the other, this will help us ascertain if one is superior over the other.

# Bayes factor and Posterior odds

The Bayes factor is a formula that tests the plausibility of one hypothesis by comparing to another. The result tells us how many times more likely one hypothesis is than the other.

We can combine Bayes factor with our prior beliefs to come up with the __posterior odds__, which tells us how much stronger one belief is than the other at explaining our data.

$$\text{Bayes factor} = \frac{ P(D | H\_1) }{ P(D | H\_2) }$$

$$\text{Posterior odds} = \frac{ P(H\_1) P(D | H\_1) }{ P(H\_2) P(D | H\_2) }$$

Guidelines for evaluation Posterior odds,

| Posterior odds | Strength of evidence |
|--- | --- |
| 1 to 3 | Interesting, but nothing conclusive |
| 3 to 20 | Looks like we are onto something |
| 20 to 150 | Strong evidence in favor of $H\_1$ |
| > 150 | Overwhelming evidence |
