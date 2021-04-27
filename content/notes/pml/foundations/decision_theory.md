+++
title = "Bayesian Decision Theory"
weight = 4
+++

# Introduction

Bayesian inference provides the optimal way to update our beliefs about hidden quantities $H$ given observed data $X = x$ by computing the posterior $p(H|x)$. However, at the end of the day, we need to turn our beliefs into actions that we can perform in the world. How can we decide which action is best? This is where __Bayesian decision theory__ comes in.

In decision theory, we assume the decision maker, or agent, has a set of possible actions $\mathcal{A}$, to choose from. Each of these actions have costs and benefits, which will depend on the underlying __state of nature__ $H \in \mathcal{H}$. We can encode this information into a loss function $l(h, a)$, that specifies the loss we incur if we take action $a \in \mathcal{A}$ when the state of nature is $h \in \mathcal{H}$.

For example, suppose the state is defined by the age of the patient (young vs old), and whether they have COVID-19 or not. Note that the age can observed directly, but the disease state must be inferred from noisy observations, thus the state is partially observed.

Let us assume that the cost of administering the drug is the same, no matter what the state of the patient is. However the benefits will differ. If the patient is young, we expect them to live a long time, so the cost of not giving the drug if they have COVID-19 is high; but if the patient is old, they have fewer years to live, os the cost of not giving the drug is arguably less. In medical circles, a common unit of cost is quality-adjusted life years or QALY. Suppose that the expected QALY for a young person is 60, and for an old person is 10. Let us assume the drug costs the equivalent of 8 QALY, due to induced pain and suffering from side effects.

Once we have specified the loss function, we can compute the __posterior expected loss__ or __risk__ for each possible action:

$$R(a|x) \triangleq \mathbb{E}\_{p(h|x)} [l(h, a)] = \sum\_{h \in \mathcal{H}} l(h, a) p(h|x)$$

The __optimal policy__ (also called the __Bayes estimator__) specifies what action to take for each possible observation so as to minimize risk:

$$\pi^* (\mathbf{x}) = \underset{a \in \mathcal{A}}{\text{argmin}}\ \mathbb{E}\_{p(h|\mathbf{x})} [l(h, a)]$$
