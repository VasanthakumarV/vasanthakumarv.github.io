+++
title = "Probabilistic Models"
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
