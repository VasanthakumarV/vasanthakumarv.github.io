+++
title = "Bayesian statistics"
weight = 4
+++

# Introduction

So far, we have discussed several ways to estimate parameters from data, however, these approaches ignore any uncertainty in the estimates, which can be important. In this section we will use __posterior distribution__ to represent our uncertainty, this is the approach adopted in the field of Bayesian statistics. To compute the posterior, we start with a __prior__ distribution $p(\bm{\theta})$, which reflects what we know before seeing the data. We then define a __likelihood function__ $p(\mathcal{D}|\bm{\theta})$, which reflects the data we expect to see for each setting of the parameters.

$$p(\bm{\theta} | \mathcal{D}) = \frac{p(\bm{\theta})p(\mathcal{D}|\bm{\theta})}{\(\mathcal{D})} = \frac{p(\bm{\theta})p(\mathcal{D}|\bm{\theta})}{\int p(\bm{\theta}^\prime)p(\mathcal{D}|\bm{\theta}^\prime)d\bm{\theta}^\prime}$$

The denominator $p(\mathcal{D})$ is called the __marginal likelihood__, this is ignored when we just want to infer the relative probabilities of $\bm{\theta}$ values.

Once we computed the posterior over the parameters, we can compute the __posterior predictive distribution__ over outputs given inputs by __marginalizing out__ the unknown parameters.

$$p(\mathbf{y|x}, \mathcal{D}) = \int p(\mathbf{y|x,\bm{\theta}})p(\bm{\theta}|\mathcal{D})d\bm{\theta}$$

# Conjugate priors

In this section we consider a set of prior and likelihood paris for which we can compute the posterior in closed form. In particular, we will use priors that are "conjugate" to the likelihood, we say that a prior is a conjugate prior for a likelihood function if the posterior is in the same parameterized family as the prior.

## The beta-binomial model

We toss a coin $N$ times, and we want to infer the probability of heads.

### Binomial likelihood

We consider Binomial likelihood model, in which we perform $N$ trials and observe $y$ number of heads. The likelihood has the following form:

$$p(\mathcal{D} | \theta) = \binom{N}{y} \theta^y (1 - \theta)^{N - y}$$

The scaling factor $\binom{N}{y}$ is independent of $\theta$, so we can ignore it.

### Prior

To simplify the computations, we will assume that the prior is a conjugate prior of the likelihood function, this means that the posterior is in the same parameterized family as the prior.

To ensure this property when using Binomial likelihood, we should use a prior of the following form:

$$p(\theta) \propto \theta^{\breve{\alpha} - 1} (1 - \theta)^{\breve{\beta} - 1} = \text{Beta}(\theta | \breve{\theta}, \breve{\beta})$$

### Posterior

If we multiply the Binomial likelihood with the beta prior we get a beta posterior:

$$
\begin{aligned}
p(\theta | \mathcal{D}) & = \theta^{N\_1}(1 - \theta)^{N\_0} \theta^{\breve{\alpha} - 1}(1 - \theta)^{\breve{\beta} - 1} \\\\
& \propto \text{Beta}(\theta | \breve{\alpha} + N\_1, \breve{\beta} + N\_0) \\\\
& = \text{Beta} (\theta | \widehat{\alpha}, \widehat{\beta})
\end{aligned}
$$

where $\widehat{\alpha}$ and $\widehat{\beta}$ are the parameters of the posterior, the parameters of the prior are the hyper-parameters.

#### Posterior mode (MAP estimate)

The most probable value of $\theta$ is given by the MAP estimate

$$\widehat{\theta} = \underset{\theta}{\text{arg\ max\ log\ }} p(\theta | \mathcal{D})$$

One can show that this is given by

$$\widehat{\theta}\_{\text{map}} = \frac{\breve{\alpha} + N\_1 - 1}{\breve{\alpha} + N\_1 -1 + \breve{\beta} + N\_0 - 1}$$

#### Posterior mean

The posterior mode can be a poor summary of the posterior, since it corresponds to a single point. The posterior mean is a more robust estimate, since it integrates over the whole space.

If $p(\theta | \mathcal{D}) = \text{Beta}(\theta | \widehat{\alpha}, \widehat{\beta})$, then the posterior mean is given by

$$\bar{\theta} \triangleq \mathbb{E}[\theta | \mathcal{D}] = \frac{\widehat{\alpha}}{\widehat{\beta} + \widehat{\alpha}}$$

#### Posterior variance

To capture some notion of uncertainty in our estimate, a common approach is to compute the standard error of our estimate, which is just the posterior standard deviation:

$$\text{se}(\theta) = \sqrt{\mathbb{V}[\theta|\mathcal{D}]}$$

In the case of the Bernoullli model, we we showed that the posterior is a beta distribution, the variance of the beta posterior is given by

$$\mathbb{V}[\theta | \mathcal{D}] = \frac{\widehat{\alpha}\widehat{\beta}}{ (\widehat{\alpha} +\widehat{\beta})^2 (\widehat{\alpha} + \widehat{\beta} + 1) }$$

#### Posterior predictive

Suppose we want to predict future observations. A very common approach is to first compute an estimate of the parameters based on training data, $\widehat{\bm{\theta}}(\mathcal{D})$, and then plug that parameter back into the model and use $p(y|\widehat{\bm{\theta}})$ to predict the future, this is called a __plug-in approximation__. However, this can result in overfitting.

One solution to this is to compute a MAP estimate, and plug that in. Here we discuss a fully Bayesian solution, in which we marginalize out $\theta$.

The posterior predictive is given by the following, known as the (compound) beta-binomial distribution:

$$Bb(x | M, \widehat{\alpha}, \widehat{\beta}) \triangleq \binom{M}{x} \frac{B(x + \widehat{\alpha}, M - x + \widehat{\beta})}{B(\widehat{\alpha}, \widehat{\beta})}$$

### Marginal likelihood

The __marginal likelihood__ or __evidence__ for a model $\mathcal{M}$ is defined as

$$p(\mathcal{D | M}) = \int p(\bm{\theta} | \mathcal{M}) p(\mathcal{D} | \bm{\theta}, \mathcal{M}) d\bm{\theta}$$

When performing inference for the parameters of a specific model, we can ignore this term, since it is constant wrt $\bm{\theta}$. However, this quantity plays a vital role when choosing between different models, it is also usefull for estimating the hyperparameters from data (an approach known as empirical Bayes).

## The Dirichlet-multinomial model

In this section we generalize to $K$-ary variables.

### Likelihood

Let $Y \sim \text{Cat}(\bm{\theta})$ be a discrete random variable drawn from a categorical distribution. The likelihood has the form

$$p(\mathcal{D} | \bm{\theta}) = \prod\_{c = 1}^{C} \theta\_c^{N\_c}$$

### Prior

The conjugate prior for a categorical distribution is the __Dirichlet distribution__, which is a multivariate generalization of the beta distribution.

The pdf of the Dirichlet is defined as follows:

$$\text{Dir}(\bm{\theta} | \breve{\bm{\alpha}}) \triangleq \frac{1}{B(\breve{\bm{\alpha}})} \prod\_{k = 1}^{K} \theta\_{k}^{\breve{\alpha} - 1} \mathbb{I}(\bm{\theta} \in S\_K)$$

where $B(\breve{\bm{\alpha}})$ is the multivariate beta function,

$$B(\breve{\bm{\alpha}}) \triangleq \frac{ \prod\_{k=1}^{K} \Gamma (\breve{\alpha}\_k) }{ \Gamma( \sum\_{k=1}^{K} \breve{\alpha}\_k )}$$

### Posterior

We can combine the multinomial likelihood and Dirichlet prior to compute the posterior, as follows:

$$
\begin{aligned}
p(\bm{\theta} | \mathcal{D}) & \propto p(\mathcal{D}|\bm{\theta})\text{Dir}(\bm{\theta} | \breve{\bm{\alpha}}) \\\\
& = \left[ \prod\_k \theta\_k^{N\_k} \right] \left[ \prod\_k \theta\_k^{\breve{\alpha}\_{k} - 1} \right] \\\\
& = \text{Dir} (\bm{\theta} | \breve{\alpha}\_1 + N\_1, \ldots, + \breve{\alpha}\_K + N\_K) \\\\
& = \text{Dir} (\bm{\theta} | \widehat{\bm{\alpha}})
\end{aligned}
$$

where $\widehat{\alpha}\_k$ are the parameters of the posterior. So we can see that the posterior can be computed by adding the empirical counts to the prior counts. 

### Posterior predictive

The posterior prediction distribution is given by

$$p(y = k | \mathcal{D}) = \frac{ \tilde{\alpha}\_k }{ \sum\_{k^\prime} \widehat{\alpha}\_{k^\prime} }$$

### Marginal likelihood

The marginal likelihood for the Dirichlet-categorical model is given by

$$p(\mathcal{D}) = \frac{ B(\mathbf{N} + \bm{\alpha}) }{ B(\bm{\alpha}) }$$

where

$$B(\bm{\alpha}) = \frac{ \prod\_{k=1}^{K} \Gamma( \alpha\_k ) }{ \Gamma( \sum\_k \alpha\_k ) }$$

## The Gaussian-Gaussian model

In this section, we derive the posterior for the parameters of a Gaussian distribution. For simplicity, we assume the variance is known.

### Univariate case

If $\sigma^2$ is a known constant, the likelihood for $\mu$ has the form

$$p(\mathcal{D} | \mu) \propto \text{exp\ } \left( - \frac{1}{2\sigma^2} \sum\_{n=1}^{N} (y\_n - \mu)^2 \right)$$

One can show that the conjugate prior is another Gaussian, $\mathcal{N}(\breve{\mu}, \breve{\tau}^2)$. Applying Bayes' rule for Gaussians, we find that the corresponding posterior is given by

$$
\begin{aligned}
p(\mu | \mathcal{D}, \sigma^2) & = \mathcal{N}(\mu, \widehat{m}, \widehat{\tau}^2) \\\\
\widehat{\tau}^2 & = \frac{1}{ \frac{N}{\sigma^2} + \frac{1}{\breve{\tau}^2} } = \frac{\sigma^2 \breve{\tau}^2}{N \breve{\tau}^2 + \sigma^2} \\\\
\widehat{m} & = \widehat{\tau}^2 \left( \frac{\breve{m}}{\breve{\tau}^2} + \frac{N \bar{y}}{\sigma^2} \right) = \frac{ \sigma^2 }{ N\breve{\tau}^2 + \sigma^2 }\breve{m} + \frac{N \breve{\tau}^2}{ N\breve{\tau}^2 + \sigma^2 }\bar{y}
\end{aligned}
$$

where $\bar{y} \triangleq \frac{1}{N} \sum\_{n = 1}^{N} y\_n$ is the empirical mean.

# Credible intervals

A posterior distribution is a high dimensional object that is hard to visualize and work with. A common way to summarize such a distribution is to compute a point estimate, such as the posterior mean or mode, and then to compute a __credible interval__, which quantifies the uncertainty associated with that estimate.

__Central interval__ has $(1 - \alpha)/2$ mass in each tail. A problem with central intervals is that there might be points outside the central interval which have higher probability than the points that are inside. This motivates an alternative quantity known as the __highest posterior density__ or $HPD$ region which is a set of points which have a probability above some threshold.

# Computational issues

Given a likelihood $p(\mathcal{D} | \bm{\theta})$ and a prior $p(\bm{\theta} | \phi)$ with (fixed) hyperparameters $\phi$, we can compute the posterior $p(\bm{\theta} | \mathcal{D}, \phi)$ using Bayes' rule. However, actually performing this computation is usually intractable, expect for simple special cases, such as conjugate models, or models where all the latent variables come from a small finite set of possible values. We therefore need to approximate the posterior.

## Grid approximation

The simplest approach to approximate posterior inference is to partition the space of possible values for the unknowns into a finite set of possibilities, call them $\bm{\theta\_1, \ldots, \theta\_K}$ and then approximate the posterior by brute-force enumeration.

## Quadratic (Laplace) approximation

This method uses an optimization procedure to find the MAP estimate, and then approximates the curvature of the posterior at that point based on the Hessian.

## Variational approximation

__Variational inference (VI)__ is another optimization-based approach to posterior inference, but which has much more modeling flexibility (and thus can give a much more accurate approximation). 

VI attempts to approximate an intractable probability distribution, such as $p(\bm{\theta} | \mathcal{D}, \phi)$, with one that is tractable $q(\bm{\theta})$.

$$q^* = \text{argmin\ } D(q, p)$$

where $Q$ is some tractable family of distributions. If we define $D$ to be the KL divergence, then we can derive a lower bound to the log marginal likelihood; this quantity is known as the __evidence lower bound__ or __ELBO__.

## Markov Chain Monte Carlo (MCMC) approximation

Although VI is fast, optimization-based method, it can give a biased approximation ot the posterior, since it is restricted to a specfic function form $q \in Q$. A more flexible approach is to use a non-parametric approximation in terms of a set of samples. This is called a __Monte Carlo approximation__ to the posterior. The key issue is how to create the posterior samples $\bm{\theta}^s \sim p(\bm{\theta} | \mathcal{D}, \phi)$ efficiently, without having to evaluate the normalization constant. A common approach to this problem is known as __Markov chain Monte Carlo__ or __MCMC__. If we augment this algorithm with gradient-based information, derived from $\nabla \text{log\ } p(\bm{\theta}, \mathcal{D} | \phi)$, we can significantly speed up the method; this is called __Hamiltonian Monte Carlo__ or __HMC__.
