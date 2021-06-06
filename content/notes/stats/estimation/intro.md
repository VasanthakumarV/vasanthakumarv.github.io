+++
title = "Parameter estimation"
weight = 1
+++

# Introduction

Parameter estimation is an essential part of statistical inference where we use our data to guess the value of an unknown variable. The true goal of parameter estimation is not simply to estimate a value, but rather to assign a probability for a range of possible values.

# Normal distribution

The normal distribution is a continuous distribution (like beta distribution) that describe the strength of possible beliefs in the value of an uncertain measurement, given a known mean and standard deviation. The PDF of the normal distribution is:

$$N(\mu, \sigma) = \frac{1}{\sqrt{2\pi \sigma^2}} \times e^{ -\frac{ (x - \mu)^2 }{ 2\sigma^2 } }$$

# Parameter estimation using Beta distribution

Mean of a beta distribution is given by:

$$\mu\_{\text{Beta}} = \frac{\alpha}{\alpha + \beta}$$

# Visualizing and interpreting CDF

The PDF is most useful visually for quickly estimating where the peak of a distribution is, and for getting a rough sense of the width (variance) and shape of a distribution. However, with PDF it is very difficult to reason about the probability of various ranges visually, the CDF is a much better tool for this.

- Finding __median__ is easy, we can simply draw a line from the point where the cumulative probability is 0.5.
- To estimate the probability between two values, we can trace lines from the x-axis at these points, then see where they meet up with the y-axis. The distance between the two points is the approximate integral.
- For estimating __confidence intervals__, we draw lines from 0.1 and 0.9 to cover 80 percent and then simply see where on the x-axis these interset with our CDF.

# Quantile function

Inverse of CDF is quantile function.
