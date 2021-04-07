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
