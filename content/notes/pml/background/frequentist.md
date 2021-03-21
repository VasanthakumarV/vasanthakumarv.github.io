+++
title = "Frequentist statistics"
+++

# Introduction

Bayesian statistics treats parameters of models just like any other random variable, and applies the rules of probability theory to infer them from data. Attempts have been made to devise approaches to statistical inference that avoid treating parameters like random variables, and which avoid the use of priors and Bayes rule. The alternative appraoch is known as __frequentist statistics__, __classical statistics__ or __orthodox statistics__.

The basic idea is to represent uncertainty by calculating how a quantity estimated from data would change if the data were changed. By contrast the Bayesian approach views probability in terms of information rather than repeated trials.

# Fisher information matrix (FIM)

In this section we discuss an important quantity called the Fisher information matrix, which is related to the curvature of the log-likelihood function.

The __score function__ is defined as the gradient of the log-likelihood:

$$\mathbf{s(\boldsymbol{\theta})} \triangleq \text{log}\ p(\mathbf{x}|\boldsymbol{\theta})$$

FIM is defined as the covariance of the score function.

## Connection between FIM and the Hessian of the NLL

__Lemma__ _The expected value of the score function is zero i.e.,_

$$\mathbb{E}_{p(\bm{x | \theta})} [\nabla \text{log}\ p(\mathbf{x|\bm{\theta}})] = \bm{0}$$

__Theorem__ _If $\text{log}\ p(\mathbf{x}\bm{\theta})$ is twice differentiable, and under certain regularity conditions, the FIM is equal to the expected Hessian of the NLL, i.e.,_

$$\mathbf{F}(\bm{\theta})_{ij} = -\mathbb{E}\_{\mathbf{x} \sim \bm{\theta}} \left[ \frac{\partial^2}{\partial\theta_i \theta_j} \text{log} p(\mathbf{x}|\bm{\theta}) \right]$$

Since Hessian measure the curvature of the likelihood, we see that the FIM tells us how well thelikelihood function can identify the best set of parameters.


