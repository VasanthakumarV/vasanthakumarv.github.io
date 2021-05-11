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
