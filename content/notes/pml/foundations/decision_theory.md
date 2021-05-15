+++
title = "Bayesian decision theory"
weight = 5
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

# Precision-recall curves

In some problems, the notion of a "negative" is not well-defined. In these kinds of situations, we may choose to use a __precision-recall curve__ to summarize the performance of the system.

The key idea is to replace FPR with __precision__. __Recall__ is same as TPR. If $\widehat{y}\_n \in \\{ 0, 1 \\}$ is the predicted label, and $y\_n \in \\{ 0, 1 \\}$ is the true label, we can estimate precision and recall using

$$\mathcal{P}(\tau) =  \frac{\sum\_n y\_n \widehat{y}\_n}{\sum\_n \widehat{y}\_n}$$
$$\mathcal{R}(\tau) =  \frac{\sum\_n y\_n \widehat{y}\_n}{\sum\_n y\_n}$$

We can now plot precision vs recall as we vary the threshold $\tau$. Hugging the top right is the best we can do.

## F-scores

For a fixed threshold, corresponding to a single point on the PR curve, we can compute a single precision and recall value, which will be denoted by $\mathcal{P}$ and $\mathcal{R}$. These are often combined into a single statistic called the $F\_{\beta}$, which weights recall as $\beta > 0$ more important than precision.

$$\frac{1}{F\_\beta} = \frac{1}{1 + \beta^2} \frac{1}{\mathcal{P}} + \frac{\beta^2}{1 + \beta^2} \frac{1}{\mathcal{R}}$$

or equivalently

$$F\_\beta \triangleq (1 + \beta^2) \frac{\mathcal{P . R}}{\beta^2\mathcal{P + R}}$$

If we set $\beta = 1$, we get the harmonic mean of precision and recall:

$$F\_1 = 2 \frac{\mathcal{P . R}}{\mathcal{P + R}}$$

Using $F\_1$ score weights precision and recall equally. However, if recall is more important, we may use $\beta = 2$, and if precision is more important, we may use $\beta = 0.5$.

# Regression problems

So far, we have considered the case where there are a finite number of actions $A$ and states of nature $H$. In this section, we consider the case where the set of actions and states are both equal to the real line.

## L2 loss

Also called __squared error__ or __quadratic loss__, which is defined as follows:

$$l\_2 (h, a) = (h - a)^2$$

## L1 loss

The $l\_2$ loss penalizes deviations from the truth quadratically, and thus is sensitive to outliers. A more robust alternative is the absolute or $l\_1$ loss

$$l\_1(h, a) = |h - a|$$

## Huber loss

Another robust loss function is the __Huber loss__, defined as follows:

$$l\_{\delta}(h, a) = 
\begin{cases}
r^2/2 & if |r| \leq \delta \\\\
\delta|r| - \delta^2/2 & if |r| \gt \delta
\end{cases}
$$

where $r = h - a$. This is equivalent to $l\_2$ for errors that are smaller than $\delta$, and is equivalent to $l\_1$ for larger errors.

# Probabilistic prediction problems

In this section, we assume the set of possible actions is to pick a __probability distribution__ over some value of interest. That is, we want to perform __probabilistic prediction__ or __probabilistic forecasting__ rather than predicting a specific value. More precisely, we assume the true "state of nature" is a distribution, $h = p(Y | x)$, the action is another distribution, $a = q(Y | x)$, and we want to pick $q$ to minimize $\mathbb{E}[l(p, q)]$ for a given $x$.

## KL, cross-entropy and log-loss

A common form of loss functions for comparing two distributions is the __Kullback Leibler divergence__ or __KL divergence__, which is defined as follows:

$$\mathbb{KL}(p || q) \triangleq \sum\_{y \in \mathcal{Y}} p(y) \text{log} \frac{p(y)}{q(y)}$$

We can expand the KL as folows:

$$
\begin{aligned}
\mathbb{KL}(p || q) & = \sum\_{y \in \mathcal{Y}} p(y)\ log\ p(y) - \sum\_{y \in \mathcal{Y}} p(y)\ \text{log}\ q(y) \\\\
\mathbb{H}(p) & \triangleq - \sum\_y p(y)\ \text{log}\ p(y) \\\\
\mathbb{H}(p, q) & \triangleq - \sum\_y p(y)\ \text{log}\ q(y)
\end{aligned}
$$

$\mathbb{H}(p)$ is known as the __entropy__. This is a measure of uncertainty or variance of $p$, it is maximal if $p$ is uniform, and is 0 if $p$ is a degenerate or deterministic delta function. The $\mathbb{H}(p, q)$ is known as the __cross-entropy__.

Now consider a special case in which the true state of nature is a degenerate distribution, which puts all its mass on a single outcome, say $c$, i.e., $h = p(Y|x) = \mathbb{I}(Y = c)$.

$$\mathbb{H}(\delta(Y = c), q) = - \sum\_{y \in \mathcal{Y}} \delta(y = c)\ \text{log}\ q(y) = -\text{log}\ q(c)$$

This is known as the __log loss__ of the predictive distribution $q$ when given given target label $c$.

## Brier score

$$l(p, q) = \triangleq \frac{1}{C} \sum\_{c=1}^{C} (q(y = c | x) - p(y =c | x))^2$$

This is just the squared error of the predictive distribution compared to the true distribution, when viewed as vectors. Since it is based on squared error, the Brier score is less sensitive to extremely rare or extremely common classes.

# A/B testing

Suppose you are trying to decide which version of a product is likely to sell more, or which version of a drug is likely to work better. Let us call the versions you are choosing between A and B, sometimes version A is called the __treatment__, and version B is called the __control__. To simplify the notation, we will refer to picking version A as choosing action 1, and picking version B as choosing action 0. We will call the resulting outcome from each action that you want to maximize the __reward__.

A very common approach to such problems is to use an __A/B test__, in which you try both actions out for a while, by randomly assigning a different action to different subsets of the publication, and then you measure the results and pick the winner. This is sometimes called a "__test and roll__" problem, since you test which method is best, and then roll it out for the rest of the population.

A key problem in A/B testing is to come up with a decision rule, or policy, for deciding which action is best, after obtaining potentially noisy results during the test phase. Another problem is to choose how many people to assign to the treat, $n\_1$, and how many to the control, $n\_0$.

## A Bayesian approach

We assume the $i$'th reward for action $j$ is given by $Y\_{ij} \sim \mathcal{N} (\mu\_j, \sigma\_j^2)$ for $i = 1:n\_j$ nad $j = 0:1$, where $j=1$ corresponds to the treatment (action !) and $j = 0$ corresponds to the control (action B). For simplicity we assume $\sigma^2$ are known. For the unknown $\mu\_j$ parameters (expected reward), we will use Gausian priors, $\mu\_j \sim \mathcal{N}(m\_j, \tau\_j^2)$. If we assign $n\_1$ people to the treatment and $n\_0$ to the control, then the expected reward in the testing phase is given by

$$\mathbb{E}[R\_{test}] = n\_0m\_0 + n\_1m\_1$$

The expected reward in the roll phase depends on the decision rule $\pi(\mathbf{y}\_1, \mathbf{y}\_0)$, which specifies which action to deploy, where $\mathbf{y}\_j = (y\_{1j}, \dots, y\_{n\_j, j})$ is the data from action $j$. We derive the opimal policy below, and then discuss some of its properties.

### Optimal policy

The optimal policy is to choose the action with the greater expected posterior mean reward. Applying Bayes' rule for Gaussians, we find that the corresponding posterior is given by

$$p(\mu\_j | \mathbf{y}\_j, n\_j) = \mathcal{N}(\mu\_j | \widehat{m}\_j, \widehat{\tau}\_j^2)$$

The optimal policy is given is

$$\pi^*(\mathbf{y}\_1, \mathbf{y}\_0) = 
\begin{cases}
1 & \text{if\ } \mathbb{E}[\mu\_1 | \mathbf{y}\_1] \geq \mathbb{E}[\mu\_0 | \mathbf{y}\_0] \\\\
0 & \text{if\ } \mathbb{E}[\mu\_1 | \mathbf{y}\_1] \lt \mathbb{E}[\mu\_0 | \mathbf{y}\_0]
\end{cases}$$

## Expected reward

If the total population size is $N$, and we cannot reuse people from the testing phase, the expected reward from the roll stage is

$$\mathbb{E}[R\_{roll}] = (N - n\_1 - n\_0) \left( m\_1 + e\Phi(\frac{e}{v}) + v \phi (\frac{e}{v}) \right)$$

where $\phi$ is the Gaussian pdf, $\Phi$ is the Gaussian cdf, $e = m\_0 - m\_1$ and

$$v = \sqrt{ \frac{\tau\_1^4}{\tau\_1^2 + \sigma\_1^2 / n\_1}  + \frac{\tau\_0^4}{ \tau\_0^2 + \sigma\_0^2 / n\_0 }}$$

# Bandit problems

In A/B testing the decision maker tries two different actions a fixed number of times and then pciks the best action. We can obviously generalize this beyond two actions. More importantly, we can generalize this beyond a one-stage decision problem. In particular, suppose we allow the decision maker to try an action $a\_t$, observe the reward $r\_t$, and then decide what to do at time step $t + 1$, rather than waiting until $n\_1 + n\_0$ experiments are finished. This immediate feedback allows for adaptive policies that can result in much higher expected reward (lower regret). We have converted a one-stage decision problem into a __sequential decision problem__. There are many kinds of sequential decision problems, but here we consider the simplest kind, known as a __bandit problem__.

In a bandit problem, there is an agent (decision maker) which gets to see some __state of nature__, which it uses to choose an __action__ from some __policy__, and then it finally receives a __reward__ sampled from the environment. In the finite horizon formulation, the goal is to maximize the expected cumulative reward.

## Contextual bandits

In the basic bandit problem, the state of nature $s\_t$ is fixed, meaning that the world does not change. However, the agent's internal model of the world does change, as it learns about which actions have highest reward. If we allow the state of the environment $s\_t$ to vary randomly over time, the model is known as __contextual bandit__, which is more flexible model.

## Markov decision processes

We can consider a generalization of the contextual bandit model, in which the next state $s\_{t+1}$ depends on $s\_t$ and the agent's action $a\_t$; this is called a __Markov decision process__ or __MDP__. This defines a __controlled Markov chain__.

$$p(s\_{0:T} | a\_{0:T-1}) = p(s\_0) \prod\_{t=1}^{T} p(s\_t | s\_{t-1}, a\_{t-1})$$

where $p(s\_t | s\_{t-1}, a\_{t-1})$ is known as the __state transition model__.

## Exploration-exploitation tradeoff

The fundamental difficulty in solving bandit problems is known as the __exploration--exploitation tradeoff__. This refers to the fact that the agent needs to try new state/action combinations (this is known as exploration) in order to learn the reward function $R(s, a)$ before it can exploit its knowledge by picking the predicted the predicted best action for each state.



# Bayesian hypothesis testing

Suppose we have two hypotheses or models, commonly called the __null hypothesis__, $M\_0$, and the __alternative hypothesis__, $M\_1$, and we want to know which one is more likely to be true. This is called __hypothesis testing__.

If we use 0-1 loss, the optimal decision is to pick the alternate hypothesis iff $p(M\_1 | \mathcal{D}) / p(M\_0 | \mathcal{D}) \gt 1$. If we use uniform prior, the decision rule becomes: select $M\_1$ iff $p(\mathcal{D} | M\_1) / p(\mathcal{D} | M\_0) \gt 1$. This quantity, which is the ratio of marginal likelihoods of the two models, is known as __Bayes factor__:

$$B\_{1,0} \triangleq \frac{ p(\mathcal{D} | M\_1) }{ p(\mathcal{D} | M\_0) }$$

This is the likelihood ratio, except we integrate out the parameters, which allows us to compare models of different complexity, due to the Bayesian Occam's razor effect.
