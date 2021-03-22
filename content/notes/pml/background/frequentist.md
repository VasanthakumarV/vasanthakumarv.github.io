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

$$\mathbf{F}(\bm{\theta})_{ij} = -\mathbb{E}\_{\mathbf{x} \sim \bm{\theta}} \left[ \frac{\partial^2}{\partial\theta_i \theta_j} \text{log}\ p(\mathbf{x}|\bm{\theta}) \right]$$

Since Hessian measure the curvature of the likelihood, we see that the FIM tells us how well thelikelihood function can identify the best set of parameters.

## Connection between FIM and KL divergence

The FIM can be viewed as an approximation of the KL divergence between two similar distribution.

Let $p_{\theta} (\mathbf{x})$ and $p_{\theta\prime}(\mathbf{x})$ be two distributions, where $\bm{\theta^\prime} = \bm{\theta} + \bm{\delta}$. We can measure how close the second distribution is to the first in terms of their predictive distribution as follows:

$$\mathbb{KL}(p_\theta || p_{\theta\prime}) = \mathbb{E}[ \text{log}\ p_{\theta}(\mathbf{x}) -\text{log}\ p_{\theta\prime}(\mathbf{x}) ]$$

Let us approximate this with a second order Taylor series expansion:

$$\mathbb{KL}(p_{\theta} || p_{\theta\prime}) \approx -\bm{\delta}^\top \mathbb{E}[\nabla \text{log}\ p_\theta (\mathbf{x})] - \frac{1}{2} \bm{\delta}^\top \mathbb{e}[ \nabla^2 \text{log}\ p_\theta (\mathbf{x}) ]\bm{\delta}$$

Since the expected score function is zero, the first term vanishes,

$$\mathbb{KL} \approx \frac{1}{2}\bm{\delta}^\top \mathbf{F}(\bm{\theta}) \bm{\delta}$$

# Sampling distributions

In frequentist statistics, uncertainty is not represented by the posterior distribution of a random variable, but instead by the __sampling distribution__ of an __estimator__.

An estimator is a decision procedure that specifies what action to take given some observed data. In the context of parameter estimation, where the action space is to return a parameter vector, we will denote this by $\hat{\bm{\theta}} = \pi(\mathcal{D})$, $\hat{\bm{\theta}}$ could be MLE estimate, MAP estimate, or the method of moments estimate. 

The sampling distribution of an estimator is the distribution of the results we would see if we applied the estimator multiple times to different datasets sampled from some distribution; in the context of parameter estimation, it is the distribution $\hat{\theta}$, viewed as a random variable that depends on the random sample $\mathcal{D}$.

