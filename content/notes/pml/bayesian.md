+++
title = "Probabilistic Inference"
date = 2020-02-23
+++

# Bayesian Inference

__Inference__ is the process of arriving at generalizations using sample data. __Bayesian Inference__ uses _Bayes' Theorem_ to model the probability of different hypotheses.

$$p(H=h|Y=y) = \frac{p(H=h)p(Y=y|H=h)}{p(Y=y)}$$

- $p(H=h|Y=y)$ is the _posterior distribution_
- $p(H=h)$ is the _prior distribution_
- $p(Y=y|H=h)$ is the _likelihood_, this is not a probability distribution
- $p(Y=y)$ is the _marginal likelihood_

# Bayesian Concept Learning

We can model the distribution of the hidden quantity of interest $h \in H$ from a set of observations, $D = {y_n : n = 1 : N}$, the goal is to infer the _hidden patterns_ or _concept_ from the underlying data.

Humans can _generalize_ a sequence of numbers, based on whether they are all powers of 2, or whether they are even numbers and other similar hypotheses. How do we emulate such process in machines. One classic approach is __Induction__, here we move from a _hypotheses space_ $H$ of concepts to _version space_ based on the observed data $D$, as more data comes in, we become more certain and the version space shrinks. But the version space theory cannot explain why people choose  _powers of two_ when they see $D = \\{ 16, 8, 2, 64 \\}$ and not _all even numbers_ or _powers of 2 except 32_. Bayesian Inference can help explain this behavior.

## Likelihood

To explain why people go with $h_{two}$ and not $h_{even}$ we will have to understand that it will __suspiciously coincidental__ for all the examples in $D = \\{16, 8, 2, 64\\}$ to be powers of two if the true underlying hypothesis was $h_{even}$.

## Prior

Priori is usefull because, the hypothesis _powers of 2 except 32_ is more likely than _powers of 2_, but the former more likely hypothesis is _unnatural_ and we can eliminate such concepts by assigning low priors. Background knowledge or Domain knowledge can be brought into a problem using the prior values.

## Posterior

Posterior is proportional to likelihood times prior, find below an image that shows how both influence the posterior in identifying the most likely hypothesis for the observed $D$.

{{ resize_image(path="notes/pml/pml_posterior.png", width=500, height=0 op="fit_width") }}
