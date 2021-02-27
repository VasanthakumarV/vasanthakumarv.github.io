+++
title = "Probabilistic Models"
+++

Here we concentrate on the output probability distribution $p(y|\theta)$, we will go through the building blocks used to construct probabilistic models.

# Bernoulli and Binomial distribution

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
