+++
title = "Bayesian reasoning and Probability"
weight = 1
+++

# Bayesian reasoning 

Beliefs start with our existing experience of the world, $X$. When we observe data, $D$, it either aligns with our experience, $P(D | X)$ = very high, or it surprises us, $P(D | X)$ = very low. To understand the world, we rely on beliefs we have about what we observe, or hypotheses, $H$. Oftentimes a new hypothesis can help explain the data that surprises us, $P(D | H, X) \gg P(D | X)$. When we gather new data or come up with new ideas, we can create more hypotheses, $H\_1, H\_2, H\_3, \ldots$. We update our beliefs when a new hypothesis explains our data much better than our old hypothesis:

$$\frac{P( D | H\_2, X )}{P( D | H\_1, X )} = \text{large\ number}$$

Finally we should be far more concerned with data changing our beliefs than with ensuring that the data supports our beliefs, $P(H | D)$.

A full Bayesian analysis involves the following,

- Observing data
- Forming hypotheses
- Updating beliefs based on new data and ideas

# Probability

We have two different types of probabilities; those of events and those of beliefs. We define probability as the ratio of the outcome(s) we care about to the number of all possible. While this is the most common definition of probability is difficult to apply to beliefs, because most practical, everyday probability problems do not have clear-cut outcomes and so aren't intuitively assigned discrete numbers.

$$P(H) = \frac{Number\ of\ favorable\ outcomes}{Total\ number\ of\ possible\ outcomes}$$

To calculate the probability of beliefs, we need to establish how many times more we believe in one hypothesis over another. One good test of this is how much you would be willing to bet on your belief.

$$P(H) = \frac{ O(H) }{ 1 + O(H) }$$

Where $O(H)$ is the odds.

## Combining probabilities

Calculating the probability of two events occuring together using product rule

$$P(A, B) = P(A) \times P(B)$$

Sum rule for combining probabilities, to solve for overcounting in non-mutually exclusive events, sum rule uses the product rule

$$P(A\ OR\ B) = P(A) + P(B) - P(A, B)$$
