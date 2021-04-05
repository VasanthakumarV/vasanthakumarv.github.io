+++
title = "Probabilistic Models"
weight = 2
+++

Here we concentrate on the output probability distribution $p(y|\theta)$, we will go through the building blocks used to construct probabilistic models.

# Bernoulli and Binomial distributions

__Bernoulli distribution__ is used to model binary events.

$$\text{Ber}(y|\theta) \triangleq \theta^y(1 - \theta)^{1-y} = 
\begin{cases}
	1 - \theta & \text{if } y = 0 \\\\
	\theta & \text{if } y = 1
\end{cases}$$

where $0 \le \theta \le 1$ is the probability that $y = 1$.

On tossing a coin $N$ times, if $s$ denotes the number of heads, the distribution of $s$ is given by the binomial distribution:

$$\text{Bin}(s|N,\theta) \triangleq \binom{N}{s} \theta^s (1-\theta)^{N-s}$$

where,

$$\binom{N}{s} \triangleq \frac{N!}{(N-s)!s!}$$

is the __binomial coefficient__.

# Categorical and Multinomial distributions

In __categorical distribution__ the parameters are constrained so that $0 \le \theta_c \le 1$ and they sum up to 1. $\bold{y}$ is a _one-hot vector_, the distribution is given by:

$$\text{Cat}(\bold{y}|\mu) \triangleq \prod_{c=1}^{C} \theta_c^{y_c}$$

On rolling a C-sided dice $N$ times, $\bold{s}$ denotes the number of times each face showed up, the __multinomial distribution__ is given by:

$$\text{Mu}(\bold{s}|N,\bold{\mu}) \triangleq \binom{N}{s_1...s_C} \prod_{c=1}^{C} \theta_c^{s_c}$$

where $\theta_c$ is the probability that $c$ shows up, and

$$\binom{N}{s_1..s_C} \triangleq \frac{N!}{s_1!s_2!...s_C!}$$

is the __multinomial coefficient__, which is the number of ways to divide a set of size $N$ in subsets.

## Log-sum-exp trick

In softmax distribution, the normalized probability is given by:

$$p_c = \frac{e^{a_c}}{Z(\bold{a})} = \frac{e^{a_c}}{\sum_{c^\`=1}^C e^{a_{c^\`}}}$$

where $\bold{a}$ are the logits, we might encounter numerical problems when computing $Z$, like $\text{np.exp(1000)=inf}$ and also $\text{np.exp(-1000)=0}$, to avoid numerical problems, we can use the following:

$$\text{log} \sum_{c=1}^C \text{exp}(a_c) = m + \text{log} \sum_{c=1}^C \text{exp}(a_c - m)$$

It is common to use $m = max_c a_c$, which ensures that the largest value being exponentiated will be zero.

# Univariate Gaussian (Normal) distribution

## Cumulative distribution function

We represent the cumulative distribution function (cdf) of a random variable $Y$ as:

$$P(y) \triangleq \text{Pr}(Y \le y)$$

The capital $P$ represents cdf, the probability in an interval is as follows:

$$\text{Pr}(a < Y \le b) = P(b) - P(a)$$

The cdf of gaussian is defined as,

$$\phi(y;\mu,\sigma^2) \triangleq \int_{-\infty}^{y}\mathcal{N}(z|\mu,\sigma^2)dz$$

where $z = (y-\mu) / \sigma$

## Probability density function

Probability density function or pdf is the derivative of the cdf:

$$p(y) \triangleq \frac{d}{dy}P(y)$$

The pdf of the Gaussian is given by:

$$\mathcal{N}(y|\mu,\sigma^2) \triangleq \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{1}{2\sigma^2}(y-\mu)^2}$$

Using pdf to compute the mean or expected value of the distribution:

$$\mathbb{E}[Y] \triangleq \int_y yp(y)dy$$

Using pdf to compute the variance of the distribution:

$$\mathbb{V}[Y] \triangleq \mathbb{E}[(Y - \mu)^2] = \mathbb{E}[Y^2] - \mu^2$$

# Regression

We have considered unconditional gaussian distribution so far, sometimes it is useful to make the parameters functions of some input variables.

$$p(y|x;\theta) = \mathcal{N}(y|f_{\mu}(x;\theta), f_{\sigma}(x;\theta)^2)$$

If we assume the variance to be fixed and independent of the input, it is called __homoscedastic regresion__. Furthermore it is common to assume the mean to be a linear function of the input, the resulting model is called __linear regression__:

$$p(y|x;\theta) = \mathcal{N}(y|\bold{w}_{\mu}^\mathsf{T}\bold{x} + b, \sigma^2)$$

## Popularity of Gaussian

The Gaussian distribution is the most widely used distribution in statistics and machine learning. The two parameters (mean and variance) are easy to interpret. Central limit theorem states that the sums of independent random variables have an approximately Gaussian distribution. Makes fewer assumptions. Easy to implement, but highly effective.

# Other common univariate distributions

## Student t distribution

Gaussian distribution is sensitive to outliers, a robust alternative to Gaussian is Student distribution. Its pdf is as follows:

$$\mathcal{T}(y|\mu,\sigma^2,\gamma) \propto \left[ 1 + \frac{1}{\gamma} \left( \frac{y-\mu}{\sigma}^2 \right) \right]^{-(\frac{\gamma+1}{2})}$$

where $\mu$ is the mean, $\sigma > 0$ is the scale parameter (not the standard deviation), and $\gamma > 0$ is callled the degrees of freedom (better term would be _degree of normality_, since large values of $\gamma$ make the distribution act like a Gaussian).

Student distribution has heavy tails, which makes it robust to outliers.

## Cauchy distribution

If $\gamma = 1$, the Student distribution is known as Cauchy or Lorentz distribution. It has heavy tails compared to Gaussian. Its pdf is defined by:

$$\mathcal{C}(x|\mu,\gamma) = \frac{1}{\gamma \pi} \left[ 1 + \left( \frac{x-\mu}{\gamma} \right)^2 \right]^{-1}$$

## Laplace distribution

Another distribution with heavy tails, also known as the double sided exponential distribution. It has the following pdf:

$$\text{Lap}(y|\mu,b) \triangleq \frac{1}{2b} \text{exp} \left( - \frac{|y-\mu|}{b} \right)$$

## Beta distribution

Beta distribution has support over the interval $[0,1]$ and is defined as follows:

$$\text{Beta}(x|a,b) = \frac{1}{B(a,b)} x^{a-1} (1-x)^{b-1}$$

where $B(a,b)$ is the beta function, defined by:

$$B(a,b) \triangleq \frac{\Gamma(a)\Gamma(b)}{\Gamma(a+b)}$$

where $\Gamma(a)$ is the Gamma function defined by:

$$\Gamma(a) \triangleq \int_0^{\infty} x^{a-1} e^{-x} dx$$

We require $a,b > 0$ to ensure the distribution is integrable. If $a = b = 1$ we get uniform distribution; if $a$ and $b$ are both less than 1, we get a bimodal distribution; if $a$ and $b$ are both greater than 1, we get unimodal distribution.

## Gamma distribution

Gamma distribution is a flexible distribution for positive real valued random variables, $x > 0$. It is defined in terms of two parameters, called the shape $a>0$ and the rate $b>0$:

$$\text{Ga}(x|a,b) \triangleq \frac{b^a}{\Gamma(a)} x^{a-1} e^{-xb}$$

Sometimes the distribution is parameterized in terms of the shape $a$ and the scale $s=1/b$.

There are several distributions which are special cases of Gamma distribution.

### Exponential distribution

The distribution describes the time between events in a Poisson process (a process in which events occur continuously and independently at a constant average rate $\lambda$).

$$\text{Expon}(x|\lambda) \triangleq \text{Ga}(x|a=1,b=\lambda)$$

### Chi-squared distribution

This is the distribution of the sum of squared Gaussian random variables.

### Inverse Gamma distribution

This is the distribution of $Y = 1/X$ assuming $X \sim \text{Ga}(a,b)$.

# Multivariate Gausssian (Normal) distribution

The multivariate normal density is defined as:

$$\mathcal{N}(\bold{y}|\boldsymbol{\mu},\bold{\Sigma}) \triangleq \frac{1}{(2\pi)^{D/2} |\bold{\Sigma}|^{1/2}} \text{exp} \left[ -\frac{1}{2} (\bold{y}-\boldsymbol{\mu})^\mathsf{T} \bold{\Sigma}^{-1} (\bold{y}-\boldsymbol{\mu}) \right]$$

where $\boldsymbol{\mu} = \mathbb{E}[\bold{y}] \in \mathbb{R}^D$ is the mean vector, $\bold{\Sigma} = \text{Cov}[\bold{y}]$ is the $D\ \times\ D$ covariance matrix, it is defined as:

$$\text{Cov}[\bold{y}] \triangleq \mathbb{E}\left[ (\bold{y} - \mathbb{E}[\bold{y}])(\bold{y}-\mathbb{E}[\bold{y}])^\mathsf{T} \right]$$

$$
\=
\begin{pmatrix}
\mathbb{V}[Y_1] & \text{Cov}[Y_1,Y_2] & ... & \text{Cov}[Y_1,Y_D] \\\\
\text{Cov}[Y_2,Y_1] & \mathbb{V}[Y_2] & ... & \text{Cov}[Y_2,Y_D] \\\\
\text{Cov}[Y_D,Y_1] & \text{Cov}[Y_D,Y_2] & ... & \mathbb{V}[Y_D]
\end{pmatrix}
$$

where
$$\text{Cov}[Y_i,Y_j] \triangleq \mathbb{E}[(Y_i-\mathbb{E}[Y_i])(Y_j-\mathbb{E}[Y_j])] = \mathbb{E}[Y_iY_j] - \mathbb{E}[Y_i]\mathbb{E}[Y_j]$$

$$\mathbb{V}[Y_i] = \text{Cov}[Y_i,Y_i]$$

Another important result,

$$\mathbb{E}[\bold{y}\bold{y}^\mathsf{T}] = \bold{\Sigma} + \boldsymbol{\mu}\boldsymbol{\mu}^\mathsf{T}$$

In 2d MVN is known as __bivariate Gaussian__ distribution. Its pdf can be expressed as $\bold{y} \sim \mathcal{N}(\boldsymbol{\mu}\bold{\Sigma})$, where $\bold{y} \in \mathbb{R}^2$, $\boldsymbol{\mu} \in \mathbb{R}^2$ and

$$\bold{\Sigma} = 
\begin{pmatrix}
\sigma_1^2 & \sigma_{12}^2 \\\\
\sigma_{21}^2 & \sigma_2^2
\end{pmatrix}
\=
\begin{pmatrix}
\sigma_1^2 & \rho\sigma_1\sigma_2 \\\\
\rho\sigma_1\sigma_2 & \sigma_2^2
\end{pmatrix}
$$

where $\rho$ is the __correlation coefficient__, it is defined by:

$$\text{corr}[X,Y] \triangleq \frac{\sigma_{12}^2}{\sigma_1\sigma_2}$$

We can show that $-1 \le \text{corr}[X,Y] \le 1$, using _Cauchy-Schwarz inequality_ and independence of random variables.

## Marginals and conditionals of MVN

Consider two vectors of random variables $\mathbf{y}_1$ and $\mathbf{y}_2$, where $\mathbf{y}_2$ are the variables of interest, and $\mathbf{y}_1$ are called nuisance variables. The marginal distribution of $\mathbf{y}_2$ can be computed by integrating out $\mathbf{y}_1$ as follows:

$$p(\mathbf{y}\_2) = \int \mathcal{N} (\mathbf{y} | \bm{\mu, \Sigma}) d\mathbf{y}\_1 = \mathcal{N}( \mathbf{y}\_2 | \bm{\mu}\_2, \bm{\Sigma}\_{22} )$$

Now suppose we observe the value of $\mathbf{y}\_2$, and we want to predict the value of $\mathbf{y}_1$ conditional on this observation. That is, we want to transform the prior distribution $p(\mathbf{y}_1)$, which represents our beliefs about the values of $\mathbf{y}_1$ before we have seen any obervations, into the posterior distribution $p(\mathbf{y}_1 | \mathbf{y}_2)$, which represents our beliefs about the values of $\mathbf{y}_1$ after (posterior to) seeing $\mathbf{y}_2$.

$$p(\mathbf{y}\_1 | \mathbf{y}\_2) = \mathcal{N}( \mathbf{y}_1 | \bm{\mu}\_1 + \bm{\Sigma}\_{12}\bm{\Sigma}\_{22}^{-1}(\mathbf{y}\_2 - \bm{\mu}\_2), \bm{\Sigma}\_{11} - \bm{\Sigma}\_{12}\bm{\Sigma}\_{22}^{-1}\bm{\Sigma}\_{21} )$$

Note that the posterior mean is a linear function of $\mathbf{y}_2$, but the posterior covariance is independent of $\mathbf{y}_2$.

# Linear Gaussian systems

Let $\mathbf{z} \in \mathbb{R}^D$ be the vector of unknown values, $\mathbf{y} \in \mathbb{R}^K$ be its noisy observation, we assume these variables are related by the following joint distribution:

$$p(\mathbf{z}) = \mathcal{N}(\mathbf{z} | \bm{\mu_z, \Sigma_z})$$
$$p(\mathbf{y | z}) = \mathcal{N}(\mathbf{y} | \mathbf{Wz + b, \Sigma_y})$$

The corresponding joint distribution $p(\mathbf{z}, \mathbf{y}) = p(\mathbf{z})p(\mathbf{y | z})$, is a $D + K$ dimensional Gaussian.

By conditioning on $\mathbf{y}$, we can compute the posterior $p(\mathbf{z|y})$ using Bayes' rule for Gaussians, which is as follows:

$$p(\mathbf{z|y}) = \frac{p(\mathbf{y|z}) p(\mathbf{z})}{p(\mathbf{y})} = \mathcal{N}(\mathbf{z}| \bm{\mu}\_{z|y}, \bm{\Sigma}_{z|y})$$

# Mixture models

One way to create more complex probability model is to take a convex combination of simple distributions. This is called mixture models. This has the form:

$$p(\mathbf{y} | \bm{\theta}) = \sum\_{k=1}^{K} \pi\_k p\_k (\mathbf{y})$$

## Gaussian mixture models

A __Gaussian mixture model__ or __GMM__, is defined as follows:

$$p(\mathbf{y}) = \sum\_{k=1}^{K} \pi\_k \mathcal{N}( \mathbf{y} | \bm{\mu}_k, \bm{\Sigma}_k )$$

GMMs are often used for unsupervised clustering of real-valued data samples $\mathbf{y}_n \in \mathbb{R}^D$. This works in two stages. First we fit the model e.g., by computing the MLE $\hat{\bm{\theta}} = \text{argmax}\ \text{log}\ p(\mathcal{D}|\bm{\theta})$, where $\mathcal{D} = \\{\mathbf{y}_n : n = 1 : N\\}$. Then we associate each data point $\mathbf{y}_n$ with discrete latent or hidden variable $z_n \in \\{ 1, \ldots, K \\}$ which specifies the identity of the mixture component or cluster which was used to generate $\mathbf{y}_n$. These latent identities are unknown, but we can compute a posterior over them using Bayes rule:

$$r\_{nk} \triangleq p(z\_n = k|\mathbf{x}_n, \bm{\theta}) = \frac{p(z\_n = k | \bm{\theta}) p(\mathbf{x}\_n | z\_n = k, \bm{\theta})}{\sum\_{k^{\prime}=1}^{K} p(z\_n = k^{\prime}|\bm{\theta}) p(\mathbf{x}\_n | z\_n = k^{\prime}, \bm{\theta})}$$

The quantity $r_{nk}$ is called the __responsibility__ of cluster $k$ for data point $n$. Given the responsibilities, we can compute the most probable cluster assignment. This is known as __hard clustering__. (If we use the responsibilities to fractionally assign each data point to different clusters, it is called __soft clustering__).

## Gaussian scale mixtures

A __Gaussian scale mixtures__ __GSM__ is like an "infinite" mixture of Gaussians, each with a different scale (variance). More precisely, let $x = \epsilon z$, where $z \sim \mathcal{N}(0, \sigma_0^2)$ and $\epsilon \sim p(\epsilon)$. We can think of this as multiplicative noise being applied to the Gaussian rv $z$. We have $x | \epsilon \sim \mathcal{N}(0, \epsilon^2\sigma_0^2)$. Marginalizing out the scale $\epsilon$ gives:

$$p(x) = \int \mathcal{N} (x | 0, \sigma_0^2 \epsilon^2) p(\epsilon^2) d\epsilon$$

# Probabilistic graphical models

Joint distributions over sets of many random variables can be defined, with the key assumption that some variables are conditionally independent. We will represent our CI assumption using graphs.

A __probabilistic graphical model__ or __PGM__ is a joint probability distribution that uses a graph structure to encode conditional assumptions. When the graph is directed acyclic graph, the model is sometimes called a Bayesian network, although there is nothing inherently Bayesian about such models.

The basic idea in PGMs is that each node in the graph represents a random variable, and each edge represents a direct dependency. More precisely, each lack of edge represents a conditional independency.

$$Y\_i \perp \mathbf{Y}\_{\text{pred}(i) \backslash \text{pa}(i)} | \mathbf{Y}\_{\text{pa}(i)}$$

where $\text{pa}(i)$ are the parents of node $i$, and $\text{pred}(i)$ are the predecessors of node $i$ in the ordering. (This is called the ordered Markov property). Consequently we represent the joint distribution as follows:

$$p(\mathbf{Y}\_{1:V}) = \prod\_{i=1}^{V} p(Y\_i | \mathbf{Y}\_{\text{pa}(i)})$$

where $V$ is the number of nodes in the graph.

## Inference

A PGM defines a joint probabiity distribution. We can therefore use the rules of marginalization and conditioning to compute $p(\mathbf{Y}_i | \mathbf{Y}_j = y_j)$ for any sets of variables $i$ and $j$.
