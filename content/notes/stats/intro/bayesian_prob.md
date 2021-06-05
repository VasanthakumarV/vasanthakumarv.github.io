+++
title = "Bayesian probability and prior probabilities"
weight = 3
+++

# Conditional probabilities

Conditional probabilities are essential part of statistics because they allow us to demonstrate how information changes our beliefs.

$$P(A, B) = P(A) \times P(B | A)$$

# Bayes' theorem

One of the most amazing things we can do with conditional probabilities is reversing the condition to calculate the probability of the event we are conditioning on, we can use $P(A|B)$ to arrive at $P(B|A)$.

$$P(A|B) = \frac{ P(A)P(B|A) }{ P(B) }$$

Our beliefs describe the world we know, so when we observe something, its conditional probability represents _the likelihood of what we have seen given what we believe_:

$$P(\text{observed} | \text{belief})$$

Bayes' theorem allows us to reverse $P(\text{observed} | \text{belief})$, this is fundamental to understanding how we can use data to update what we believe about the world.

- $P(\text{belief | data})$ is the __posterior probability__
- $P(\text{data | belief})$ is the __likelihood__
- $P(\text{belief})$ is the __prior probability__

If both the likelihood and prior are represented using beta distribution, it is really easy to calculate normalized posterior,

$$\text{Beta}(\alpha_{\text{posterior}}, \beta_{\text{posterior}}) = \text{Beta}( \alpha\_{\text{likelihood}} + \alpha\_{\text{prior}}, \beta\_{\text{likelihood}} + \beta\_{\text{prior}} )$$
