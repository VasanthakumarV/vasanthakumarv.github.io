+++
title = "Probability distributions"
weight = 2
+++

# Introdution

Probability distributions are a way of describing all possible events and probability of each one happening. Probability distributions are useful for asking questions about ranges of possible values.

# Binomial distribution

Binomial distribution is used to calculate the probability of a certain number of successful outcones, and it involves three parameters:

- The number of outcomes we care about $k$
- The total number of trials $n$
- The probability of the event happening $p$

Probability Mass Function (pmf) for binomial distribution:

$$\text{B}(k; n, p) = \binom{n}{k} \times p^k \times (1 - p)^{n - k}$$

# Beta distribution

Beta distribution is used to estimate the probability of an event for which we have already observed a number of trials and the number of successful outcomes. For example, we would use it to estimate the probability of heads, when so far we have observed 100 tosses of a coin and 40 of those were heads.

Probability density function of beta distribution:

$$\text{Beta}(p, \alpha, \beta) = \frac{ p^{\alpha - 1} \times (1 - p)^{\beta-1} }{ \text{beta}(\alpha, \beta) }$$
