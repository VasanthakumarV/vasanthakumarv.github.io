+++
title = "Bayesian reasoning"
weight = 1
+++

# Overview

Beliefs start with our existing experience of the world, $X$. When we observe data, $D$, it either aligns with our experience, $P(D | X)$ = very high, or it surprises us, $P(D | X)$ = very low. To understand the world, we rely on beliefs we have about what we observe, or hypotheses, $H$. Oftentimes a new hypothesis can help explain the data that surprises us, $P(D | H, X) \gg P(D | X)$. When we gather new data or come up with new ideas, we can create more hypotheses, $H\_1, H\_2, H\_3, \ldots$. We update our beliefs when a new hypothesis explains our data much better than our old hypothesis:

$$\frac{P( D | H\_2, X )}{P( D | H\_1, X )} = \text{large\ number}$$

Finally we should be far more concerned with data changing our beliefs than with ensuring that the data supports our beliefs, $P(H | D)$.

A full Bayesian analysis involves the following,

- Observing data
- Forming hypotheses
- Updating beliefs based on new data and ideas
