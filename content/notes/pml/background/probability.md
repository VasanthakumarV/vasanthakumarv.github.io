+++
title = "Probability"
+++

# Introduction

Using __Bayesian__ interpretation of probability, the term probability is used to quantify our __uncertainty__ or ignorance about something, hence it is fundamentally related to information.

The uncertainity in our predictions can arise for two fundamentally different reasons. The first is due to the ignorance of the underlying hidden causes or mechanism generating our data. This is called __epistemic uncertainty__, since epistemology is the philosophical term used to describe the study of knowledge. However, a simpler term for this is __model uncertainty__. The second kind of uncertainty arises from intrinsic variability, which cannot be reduced even if we collect more data. This is sometimes called __aleatoric uncertainty__, derived from the Latin word for "dice", although a simple term would be __data uncertainty__.

# Fundamental rules of probability

We define an __event__, denoted by the binary variable $A$, as some state of the world that either holds or does not hold. The expression $\text{Pr}(A)$ denotes the probability with which you believe event $A$ is true. We write $\text{Pr}(\overline{A})$ to denote probability of event $A$ not happening.

We denote the __joint probability__ of events $A$ and $B$ both happening as follows:

$$\text{Pr}(A \cap B) = \text{Pr}(A, B)$$

If $A$ and $B$ are independent events, we have

$$\text{Pr}(A, B) = \text{Pr}(A)\text{Pr}(B)$$

The probability of event $A$ or $B$ happening is given by

$$\text{Pr}(A \cup B) = \text{Pr}(A) + \text{Pr}(B) - \text{Pr}(A \cap B)$$

If the event are mutually exclusive, we get

$$\text{Pr}(A \cup B) = \text{Pr}(A) + \text{Pr}(B)$$

We define the __conditional probability__ of event $B$ happening given that $A$ has occured as follows:

$$\text{Pr}(B|A) \triangleq \frac{\text{Pr}(A, B)}{\text{Pr}(A)}$$

We say that event $A$ is __conditionally independent__ of event $B$ if

$$\text{Pr}(A|B) \triangleq \text{Pr}(A)$$

This is a symmetric relationship. We use the notation $A \perp B$ to denote this property.

Two events, $A$ and $B$, are conditionally independent given a third event $C$ if $\text{Pr}(A|B,C) = \text{Pr}(A|C)$. Equivalently, we can write this as $\text{Pr}(A,B|C) = \text{Pr}(A|C) \text{Pr}(B|C)$. This is written as $A \perp B|C$

# Random variables

Suppose $X$ represents some unknown quantity of interest, we can represent our beliefs about its possible values using a __probability distribution__.

## Discrete random variables

The set of values an rv $X$ can take on is called the __state space__. If this is finite or countably infinite, $X$ is called a discrete random variable. We define the __probability mass function__ or __pmf__ as a function which computes the probability of events which correspond to setting the rv to each possible value:

$$p(x) \triangleq \text{Pr}(X = x)$$

The pmf satisfies the properties $0 \le p(c) \le 1$ and $\sum_{x \in X}p(x) = 1$.

$p(x) = \mathbb{I}(x = 1)$ is a defenerate distribution, where $\mathbb{I}()$ is binary indicator function.

## Continuous random variables

If $X \in \mathbb{R}$ is real-valued quantity, it is called a __continuous random variable__.

We define the __cumulative distribution function__ or __cdf__ of the rv $X$ as follows:

$$P(x) \triangleq \textbf{Pr}(X \le x)$$

(Note that we use a capital $P$ to represent the cdf). Using this, we can compute the probability of being in any interval as follows:

$$\text{Pr}(a < X \leq b) = P(b) - P(a)$$

Cdfs are monotonically non-decreasing functions.
