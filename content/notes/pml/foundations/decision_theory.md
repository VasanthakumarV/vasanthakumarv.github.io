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

# Classification problems

In this section, we use Bayesian decision theory to decide optimal class label to predict given an observed input $x \in \mathcal{X}$.

## Zero-one loss

Suppose the states of nature correspond to class labels, os $\mathcal{H} = \mathcal{Y} = \\{ 1, \ldots, C \\}$. Furthermore, suppose the actions also correspond to class labels, os $\mathcal{A} = \mathcal{Y}$. In this setting, a very commonly used loss function is the zero-one loss.

Hence the action that minimizes the expected loss is to choose the most probable label:

$$\pi(\mathbf{x}) = \underset{y \in \mathcal{Y}}{\text{argmax}}\ p(y|\mathbf{x})$$

This corresponds to the mode of the posterior distribution, also known as the maximum a posteriori or MAP estimate.

## Reject option

In some cases, we may be able to say "I don't know" instead of returning an answer that we don't really trust, this is particulary important in risk averse domains.

$$
l(h, a) = 
\begin{cases}
0 & if\ h = a\ and\ a \in \\{ 1, \ldots, C \\} \\\\
\lambda\_r & if\ a = 0 \\\\
\lambda\_e & otherwise
\end{cases}
$$

where $\lambda\_r$ is the cost of reject action, and $\lambda\_e$ is the cost of classification error.

# ROC curves

We showed that we can pick the optimal lable in binary classification by thresholding the probability using a value derived from the relative cost of a false positive and false negative. Instead of picking a single threshold, we can instead consider using a set of different thresholds, and comparing the resulting performance.

## Class confusion matrices

For any fixed threshold $\tau$, we can compute the empirical number of false positives (FP), false negatives (FN), true positives (TP), and true negatives (TN). We can store these results in a $2 \times 2$ class confusion matrix $C$, where $C\_{ij}$ is the number of times an item with true class label $i$ was (mis)classified as having lable $j$. We can now plot TPR vs FPR as an implicit function of $\tau$. This is called a __receiver operation characteristic__ or __ROC__ curve.

The quality of the ROC curve is often summarized as a single number using the __area under the curve__ or __AUC__ score, higher AUC scores are better. Another summary statistic that is used is the __equal error rate__ or __EER__ as called the __cross-over rate__, defined as the value which satisfies FPR = FNR. Since FNR = 1-TPR, we can compute EER by drawing a line from top left to the bottom right and seeing where it intersects the ROC curve, lower EER scores are better.

## Class imbalance

In some problems, there is severe class imbalance. For example, the set of negatives is usually much larger than the set of positives. The usefulness of the ROC curve may be reduced in such cases, since a large change in the absolute number of false positives will not change the false positive rate very much, since FPR is divided by FP + TN. Thus all action happens in the extreme left part of the curve. In such cases, we may choose other ways of summarizing the class confusion matrix, such as precision-recall curves.
