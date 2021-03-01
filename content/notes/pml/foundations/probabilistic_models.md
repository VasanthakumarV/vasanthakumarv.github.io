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
