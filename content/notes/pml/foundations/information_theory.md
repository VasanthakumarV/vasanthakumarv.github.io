+++
title = "Information theory"
weight = 6
+++

# Entropy

The __entropy__ of a probability distribution can be intepreted as a measure of uncertainty, or lack of predictability, associated with a random variable drawn from a given distribution. We can also use entropy to define __information content__ of a data source. A distribution wit high entropy will have high information content.

## Entropy for discrete random variables

The entropy of a discrete random variable $X$ with distribution $p$ over $K$ states is defined by

$$\mathbb{H}(X) \triangleq \sum\_{k = 1}^{K} p(X = k) \text{log}\_2(X = k) = -\mathbb{E}\_X[\text{log\ }p(X)]$$

## Cross entropy

The cross entropy between distribution $p$ and $q$ is defined by

$$\mathbb{H}(p, q) \triangleq -\sum\_{k=1}^{K} p\_k \text{log\ } q\_k$$

# Relative entropy (KL divergence)

Given two distribution $p$ and $q$, it is often useful to define a distance metric to measure how "close" or "similar" they are. More precisely, we say that $D$ is a divergence if $D(p, q) \geq 0$ with equality iff $p = q$, it does not have to be a metric and satisfy triangle inequality $D(p, r) \leq D(p, q) + D(q, r)$.

For discrete distributions, the KL divergence is defined as follows:

$$\mathbb{KL}(p || q) \triangleq \sum\_{k = 1}^{K} p\_k \text{log\ } \frac{p\_k}{q\_k}$$

This naturally extends to continuous distributions as well:

$$\mathbb{KL} p(p || q) \triangleq \int p(x)\ \text{log\ } \frac{p(x)}{q(x)}\ dx$$

# Mutual information

The KL divergence gave us a way to measure how similar two distributions were. How should we measure how dependent two random variables are? One thing we could do is turn the question of measureing the dependence of two random variables into a question about the similarity of their distribution. This gives rise to the notion of __mututal information__ (MI) between two random variables, which is defined below.

$$\mathbb{I} (X; Y) \triangleq \mathbb{KL} (p(x, y) || p(x)p(y)) = \sum\_{y \in Y} \sum\_{x \in X} p(x, y)\ \text{log\ } \frac{p(x, y)}{p(x) p(y)}$$

MI measures the information gain if we update from a model that treats the two variables as independent $p(x)p(y)$ to one that models their true joint density $p(x, y)$.
