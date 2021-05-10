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
