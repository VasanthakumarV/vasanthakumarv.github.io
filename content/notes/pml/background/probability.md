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

We define the __probability density function__ or __pdf__ as the derivative of the cdf:

$$p(x) \triangleq \frac{d}{dx} P(x)$$

Given a pdf, we can compute the probability of a continuous variable being in a finite interval as follows:

$$\text{Pr}(a < X \le b) = \int_a^b p(x) = P(b) - P(a)$$

If the cdf is strictly monotonically increasing, it has an inverse, called the __inverse cdf__, or __percent point function (ppf)__, or __quantile function__.

If $P$ is the cdf of $X$, then $P^{-1}(q)$ is the value $x_q$ such that $\text{Pr}(X \le x_q) = q$; this is called the $q$'th quantile of $P$. The value $P^{-1}(0.5)$ is the median of the distribution, with half of the probability mass on the left, and half on the right.

# Sets of related random variables

Here we discuss distributions over sets of related random variables.

## Joint, marginal and conditional distributions

Suppose we have two random variables, $X$ and $Y$. We can define the __joint distribution__ of two random variables using $p(x,y) = p(X=x, Y=y)$ for all possible values of $X$ and $Y$. If the variables have finite cardinality, we can represent the joint distribution as a 2d table, all of whose entries sum to one.

Given the joint distribution, we define the __marginal distribution__ of an rv as follows:

$$p(X = x) = \sum_y p(X=x, Y=y)$$

We define the __conditional distribution__ of an rv using

$$p(Y=y|X=x) = \frac{p(X=x, Y=y)}{p(X=x)}$$

We can rearrange this equation to get

$$p(x,y) = p(x)p(y|x)$$

This is called the __product rule__. By extending the product rule to $D$ variables, we get the __chain rule of probability__:

$$p(\mathbf{x}\_{1:D}) = p(x_1) p(x_2|x_1) p(x_3|x_1,x_2) p(x_4|x_1,x_2,x_3) \ldots p(x_D|\mathbf{x}_{1:D-1})$$

## Bayes' rule

Combining the definition of conditional probability with the product and sum rules yields __Bayes' rule__,

$$p(Y=y|X=x) = \frac{p(X=x,Y=y)}{p(X=x)} = \frac{p(Y=y)p(X=x|Y=y)}{\sum_{y \prime} p(Y=y\prime) p(X=x|Y=y \prime))}$$

## Independence and conditional independence

We say $X$ and $Y$ are unconditionally independent or marginally independent, if we can represent the joint as the product of the two marginals, i.e.,

$$X \perp Y \Longleftrightarrow p(X,Y) = p(X)p(Y)$$

Unfortunately, unconditional independence is rare, because most variables influence most other variables. However, usually this influence is mediated via other variables rather than being direct. We therefore say $X$ and $Y$ are conditionally independent given $Z$ iff the conditional joint can be written as a product of conditional marginals:

$$X \perp Y | Z \Longleftrightarrow p(X,Y|Z) = p(X|Z)p(Y|Z)$$

We can write this assumption as a graph $X - Z - Y$, which captures the intuition that all the dependencies between $X$ and $Y$ are mediated via $Z$. By using larger graphs, we can define complex joint distributions; these are known as __graphical models__.

# Properties of a distribution

The most familiar property of a distribution is its __mean__, or __expected value__, often denoted by $\mu$. For continuous rv's, the mean is defined as follows:

$$\mathbb{E}[X] \triangleq \int_{\mathcal{X}} xp(x) dx$$

__Mean__

If the integral is not finite, the mean is not defined.

For discrete rv's the mean is defined as follows:

$$\mathbb{E}[X] \triangleq \sum_{x \in \mathcal{X}} x p(x)$$

However, this is only meaningful if the values of $x$ are ordered in some way (e.g., if they represent integer counts).

__Variance__

The __variance__ is a measure of the spread of a distribution, often denoted by $\sigma^2$.

$$\mathbb{V}[X] \triangleq \mathbb{E}[(X - \mu)^2] = \int (x - \mu)^2 p(x) dx = \mathbb{E}[X^2] - \mu^2$$

__Mode__

The __mode__ of a distribution is the value with the highest probability mass or probability density:

$$\mathbf{x}^* = \underset{x}{\text{argmax}}\ p(\mathbf{x})$$

If the distribution is multimodal, this may not be unique.

__Conditional moments__

When we have two or more dependent random variables, we can find the moments of one variable given the knowledge of the other.

$$\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X|Y]]$$

$$\mathbb{V}[X] = \mathbb{E}[\mathbb{V}[X|Y]] + \mathbb{V}[\mathbb{E}[X|Y]]$$
