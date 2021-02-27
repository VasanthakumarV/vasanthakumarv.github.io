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
