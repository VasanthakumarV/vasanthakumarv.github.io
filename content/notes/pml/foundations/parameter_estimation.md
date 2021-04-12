+++
title = "Parameter Estimation"
weight = 3
+++

# Introduction

Till now we assumed all the parameters $\bm{\theta}$ of each building block in our model were known. Now we discuss how to learn these parameters from data, $\mathcal{D} = \\{ (\mathbf{x}_n, \mathbf{y}_n) : n = 1 : N \\}$. We will focus on computing a point estimate $\hat{\bm{\theta}}(\mathcal{D})$, and ignore any notion of uncertainty in our estimate.

The process of estimating $\bm{\theta}$ from $\mathcal{D}$ is called model fitting or training, and is at the heart of machine learning. There are many methods of producing such estimates, but most boil down to an optimization problem of the form

$$\hat{\bm{\theta}} = \text{argmin}\ \mathcal{L}(\bm{\theta})$$

where $\mathcal{L}(\bm{\theta})$ is some kind of loss function or objective function.

## Maximum likelihood estimate (MLE)

The most common approach to parameter estimation is to pick the parameters that assign the highest probability to the training data, this is called maximum likelihood estimation or MLE.

$$\hat{\bm{\theta}} \triangleq \underset{\theta}{\text{argmax}}\ p(\mathcal{D}|\bm{\theta})$$

We usually assume the training examples are independently sampled from the same distribution, so the (conditional) likelihood becomes

$$p(\mathcal{D}|\bm{\theta}) = \prod_{n=1}^{N} p(\mathbf{y}_n | \mathbf{x}_n, \bm{\theta})$$

This is known as the "independent and identically distributed" __iid__ assumption. We usually work with log likelihood, which is given by

$$LL(\bm{\theta}) \triangleq \text{log}\ p(\mathcal{D}|\bm{\theta}) = \sum_{n=1}^{N}\text{log}\ p(\mathbf{y}_n | \mathbf{x}_n, \bm{\theta})$$

This decomposes into sum of terms, one per example, Thus the MLE is given by

$$\hat{\bm{\theta}}\_{mle} = \underset{\theta}{\text{argmax}} \sum\_{n=1}^{N} \text{log}\ p(\mathbf{y}\_n | \mathbf{x}\_n, \bm{\theta})$$

Since most optimization algorithms are designed to minimize cost functions, we can redefine the objected function to be conditional __negative log likelihood__ or __NLL__, minimizing NLL will give the MLE:

$$\hat{\bm{\theta}} = \underset{\theta}{\text{argmin}} - \sum\_{n=1}^{N} \text{log}\ p(\mathbf{y}\_n | \bm{\theta})$$

# Empirical risk minimization (ERM)

We can generalize MLE by replacing the conditional log loss term with any other loss function, to get

$$\mathcal{L}(\bm{\theta}) = \frac{1}{N} \sum_{n=1}^{N} l (\mathbf{y}_n, \bm{\theta}; \mathbf{x}_n)$$

This is known as empirical risk minimization or ERM, since it is the expected loss where the expectation is taken wrt the empirical distribution.

## Log loss

Consider a probabilistic binary classifier, which produces the following distribution over labels:

$$p(\widetilde{y} | \mathbf{x}, \bm{\theta}) = \sigma(\widetilde{y}\eta) = \frac{1}{1 + e^{-\widetilde{y}\eta}}$$

where $\eta = f(\mathbf{x}; \bm{\theta})$ is the log odds. Hence the log loss is given by

$$l\_{ll}(\widetilde{y}, \eta) = - \text{log}\ p(\widetilde{y}, \eta) = \text{log}(1 + e^{-\widetilde{y}\eta})$$

Like log loss, hinge loss is another convex upper bound function:

$$l\_{hinge}(\widetilde{y}, \eta) = \text{max}(0, 1 - \widetilde{y}\eta) \triangleq (1 - \widetilde{y}\eta)\_{+}$$

# Regularization

A fundamental problem with MLE and ERM, is that it will try to pick parameters that minimize loss on the training set, but this may not result in a model that has low loss on future data. This is called __overfitting__.

The main solution to overfitting is to use __regularization__, which means to add penalty term to NLL, thus we optimize an objective of the form

$$\mathcal{L}(\bm{\theta}; \lambda) = \left[ \frac{1}{N} \sum\_{n=1}^{N} l(\mathbf{y}\_n, \bm{\theta}\_n; \mathbf{x}\_n) \right] + \lambda C(\bm{\theta})$$

## Early stopping

A very simple form of regularization, which is very effective in practice (especially for complex models), is known as __early stopping__. If we detect signs of overfitting (by monitoring the performance on validation set), we can stop the optimization process, to prevent the model memorizing too much information about the training set.

## Using more data

As the amount of data increases, the chance of overfitting (for a model of fixed complexity) decreases (assuming the data contains informative examples). __Learning curve__ is a plot made between error and training set size.

# The method of moments


