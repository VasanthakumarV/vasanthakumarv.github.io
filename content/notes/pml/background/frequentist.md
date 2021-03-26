+++
title = "Frequentist statistics"
weight = 4
+++

# Introduction

Bayesian statistics treats parameters of models just like any other random variable, and applies the rules of probability theory to infer them from data. Attempts have been made to devise approaches to statistical inference that avoid treating parameters like random variables, and which avoid the use of priors and Bayes rule. The alternative appraoch is known as __frequentist statistics__, __classical statistics__ or __orthodox statistics__.

The basic idea is to represent uncertainty by calculating how a quantity estimated from data would change if the data were changed. By contrast the Bayesian approach views probability in terms of information rather than repeated trials.

# Fisher information matrix (FIM)

In this section we discuss an important quantity called the Fisher information matrix, which is related to the curvature of the log-likelihood function.

The __score function__ is defined as the gradient of the log-likelihood:

$$\mathbf{s(\boldsymbol{\theta})} \triangleq \text{log}\ p(\mathbf{x}|\boldsymbol{\theta})$$

FIM is defined as the covariance of the score function.

## Connection between FIM and the Hessian of the NLL

__Lemma__ _The expected value of the score function is zero i.e.,_

$$\mathbb{E}_{p(\bm{x | \theta})} [\nabla \text{log}\ p(\mathbf{x|\bm{\theta}})] = \bm{0}$$

__Theorem__ _If $\text{log}\ p(\mathbf{x}\bm{\theta})$ is twice differentiable, and under certain regularity conditions, the FIM is equal to the expected Hessian of the NLL, i.e.,_

$$\mathbf{F}(\bm{\theta})_{ij} = -\mathbb{E}\_{\mathbf{x} \sim \bm{\theta}} \left[ \frac{\partial^2}{\partial\theta_i \theta_j} \text{log}\ p(\mathbf{x}|\bm{\theta}) \right]$$

Since Hessian measure the curvature of the likelihood, we see that the FIM tells us how well thelikelihood function can identify the best set of parameters.

## Connection between FIM and KL divergence

The FIM can be viewed as an approximation of the KL divergence between two similar distribution.

Let $p_{\theta} (\mathbf{x})$ and $p_{\theta\prime}(\mathbf{x})$ be two distributions, where $\bm{\theta^\prime} = \bm{\theta} + \bm{\delta}$. We can measure how close the second distribution is to the first in terms of their predictive distribution as follows:

$$\mathbb{KL}(p_\theta || p_{\theta\prime}) = \mathbb{E}[ \text{log}\ p_{\theta}(\mathbf{x}) -\text{log}\ p_{\theta\prime}(\mathbf{x}) ]$$

Let us approximate this with a second order Taylor series expansion:

$$\mathbb{KL}(p_{\theta} || p_{\theta\prime}) \approx -\bm{\delta}^\top \mathbb{E}[\nabla \text{log}\ p_\theta (\mathbf{x})] - \frac{1}{2} \bm{\delta}^\top \mathbb{e}[ \nabla^2 \text{log}\ p_\theta (\mathbf{x}) ]\bm{\delta}$$

Since the expected score function is zero, the first term vanishes,

$$\mathbb{KL} \approx \frac{1}{2}\bm{\delta}^\top \mathbf{F}(\bm{\theta}) \bm{\delta}$$

# Sampling distributions

In frequentist statistics, uncertainty is not represented by the posterior distribution of a random variable, but instead by the __sampling distribution__ of an __estimator__.

An estimator is a decision procedure that specifies what action to take given some observed data. In the context of parameter estimation, where the action space is to return a parameter vector, we will denote this by $\hat{\bm{\theta}} = \pi(\mathcal{D})$, $\hat{\bm{\theta}}$ could be MLE estimate, MAP estimate, or the method of moments estimate. 

The sampling distribution of an estimator is the distribution of the results we would see if we applied the estimator multiple times to different datasets sampled from some distribution; in the context of parameter estimation, it is the distribution $\hat{\theta}$, viewed as a random variable that depends on the random sample $\mathcal{D}$.

## Bootstrap approximation

In cases where estimator is a complex function of the data, we can approximate its sampling distribution using a Monte Carlo technique known as the boostrap.

The idea is simple. If we knew the true parameters $\bm{\theta}^\*$, we could generate many fake datasets, each of size $N$, from the true distribution. We could then compute our estimator from each sample and use the empirical distribution as our estimate of the sampling distribution. Since $\bm{\theta}^\*$ is unknown, the idea of __parametric bootstrap__ is to generate each sampled dataset using $\hat{\bm{\theta}}$ instead. This is a plug-in approximation to the sampling distribution.

## Confidence intervals

In frequentist statistics, we use the variability induced by the sampling distribution as a way to estimate uncertainty of a parameter estimate. More precisely, we define a $100(1 - \alpha)$% confidence interval for a parameter estimate $\theta$ as any interval $I(\tilde{\mathcal{D}}) = (\mathcal{l(\widetilde{D})}, \mathcal{u(\widetilde{D})})$ derived from a hypothetical dataset $\widetilde{\mathcal{D}}$ such that

$$\text{Pr}(\theta \in I(\widetilde{\mathcal{D}})|\widetilde{\mathcal{D}} \approx \theta) = 1 - \alpha$$

It is common to set $\alpha = 0.05$, which yields 95% CI. This means that, if we repeatedly sampled data, and compute $I(\widetilde{\mathcal{D}})$ for each dataset, then 95% of such intervals contain the true parameter $\theta$.

# Bias and variance

An estimator is a procedure applied to data which returns an estimand. Let $\hat{\bm{\theta}}()$ be the estimator, and $\hat{\bm{\theta}}(\mathcal{D})$ be  the estimand. In frequentist statistics, we treat the data as a random variable, drawn from some true but unknown distribution, $p^*(\mathcal{D})$; this induces a distribution over the estimand, $p^\*({\hat{\bm{\theta}}}(\mathcal{D}))$, known as the sampling distribution. In this section, we discuss two key properties of this distribution, its bias and variance.

## Bias of an estimator

The bias of an estimator is defined as

$$\text{bias}(\hat{\theta}(.)) \triangleq \mathbb{E}[\hat{\theta}(\mathcal{D})] - \theta^*$$

If the bias is zero, the estimator is called unbiased.

## Variance of an estimator

Being unbiased is not enough, for e.g., suppose we want to estimate the mean of a Gaussian from $\mathcal{D} = \{ x_1, \ldots, x_N \}$. The estimator that just looks at the first data point is an unbiased estimator, but will generally be further from $\theta^*$ than the empirical mean $\overline{x}$. So the variance of an estimator is also important.

__The Cramer-Rao lower bound__

How low can the variance go? A famous result called the Cramer-Rao lower bound, provides a lower bound on the variance of any unbiased estimator.

$$\mathbb{V}[\hat{\theta}] = \frac{1}{N F(\theta^*)}$$

## The bias-variance tradeoff

 There is a fundamental tradeoff that needs to be made when picking a method for parameter estimation, assuming our goal is to minimize mean squared error of our estimate $\hat{\theta}$.

$$
\begin{aligned}
\mathbb{E}[\hat{\theta} - \theta^\*] &= \mathbb{E}\[ [(\hat{\theta} - \overline{\theta}) + (\overline{\theta} - \theta^*)]^2 \] \\\\
&= \mathbb{V}[\hat{\theta}] + \text{bias}^2(\hat{\theta})
\end{aligned}
$$

What it means is that it might be wise to use a biased estimator, so long as it reduces our variance by more than the square of the bias, assuming our goal is to minimize squared error.

## Jacknife

The jacknife is an approach to estimate the variability of an estimator based on resampling the data. Unlike bootstrap it cannot be used to approximate the full sampling distribution, but it can estimate the bias and variance of many well-behaved estimators.

The approach is based on computing $N$ estimates, by leaving out one data point at a time, i.e, we compute $\bm{\hat{\theta}}\_n = \pi (\mathcal{D}_{-n})$, where $\mathcal{D}\_{-n}$ is the full dataset omitting the $n$'th point. The mean of these estimates is $\overline{\bm{\theta}} = \frac{1}{N} \sum\_{n=1}^{N} \hat{\bm{\theta}}\_n$

We can now estimate the bias using

$$\hat{\text{bias}}(\hat{\bm{\theta}}) = (N - 1)(\overline{\bm{\theta}} - \hat{\bm{\theta}})$$

We can also estimate the variance as follows:

$$\mathbb{V}[\hat{\bm{\theta}}] = \frac{N - 1}{N} \sum_{n=1}^{N} (\hat{\bm{\theta}}_n - \overline{\bm{\theta}})^2$$

# Hypothesis testing

Suppose we have two hypotheses, known as null hypothesis $H_0$ and an alternative hypothesis $H_1$, and we want to choose the one we think is correct on the basis of a dataset $\mathcal{D}$.

## Null hypothesis significance testing (NHST)

The decision rule is designed on __type I error rate__ of (the probability of accidentally rejecting the null hypothesis) $\alpha$. The error rate $\alpha$ is called the significance of the test. The type II error rate is the probability we accidentally accept the null when the alternative is true.

### t-test

Suppose we have two sets of paired samples $y_i^1$ and $y_i^2$ for $i = 1:N$. For example, $y_i^1$ might be the blood pressure of person $i$ before taking a drug, and $y_i^2$ might be the blood pressure of the same person after taking the drug. Let $x_i = y_i^1 - y_i^2$. If is often reasonable to assume that $x_i \sim \mathcal{N}(\mu, \sigma^2)$, where $\mu$ is the unknown effect of the drug on blood pressure.

Suppose we want to test the point null hypothesis $H_0 : \mu = 0$ (i.e., the drug has no effect) given samples $\mathbf{x} = (x_1, \ldots, x_N)$. Let $\overline{x} = \frac{1}{N} \sum\_{i=1}^{N}x_i$ be the test statistic. One can show that the sampling distribution of $\overline{x}$ under the null hypothesis is given by

$$p(\overline{x}|\mu) = \mathcal{T}(\overline{x} | \mu, s^2/N, N-1)$$

To derive a hypothesis test, we will use the following decision rule: accept $H_0$ iff $\overline{x} \le x^\*$, where $x^*$ is chosen so that $p(\overline{x} \ge x^\* | \mu) = 1 - \alpha$, where $\alpha = 0.05$ is the significance level. This procedure is called a (one-sample) t-test.

### $\mathcal{X}^2$ test

Suppose we have two sets of unpaired samples, $\mathcal{X} = \\{ \mathbf{x}_1, \ldots, \mathbf{x}_N \\}$ sampled from $P$ and $\mathcal{X}\prime = \\{ \hat{\mathbf{x}}_1, \dots, \hat{\mathbf{x}}_M \\}$ sampled from $Q$, and we want to test the hypothesis $H_0 : P = Q$. This is called a two-sample test.

To test this hypothesis, we need some kind of summary statistic, in the context of contingency tables, it is common to use chi-squared statistic, which is a function of the difference between the observed counts, $O_{ij}$, and the counts we would expect if the row and column variables were independent $E_{ij}$.

$$\mathcal{x}^2(\mathcal{D}) \triangleq \sum_{i=1}^{I} \sum_{j=1}^{J} \frac{(O_{ij} - E_{ij})^2}{E_{ij}}$$

where $I$ is the number of rows and $J$ is the number of columns.

One can show that the chi-squared statistic of a contingency table $\widetilde{\mathcal{D}}$ sampled from the null distribution has a chi-squared distribution,

$$\mathcal{X}^2(\widetilde{\mathcal{D}}) | H_0 \sim \mathcal{X_v}^2(.)$$

where $\mathcal{v} = (I - 1)(J - 1)$ is the number of degrees of freedom. The critical value $c^*$ to reject the null hypothesis at level $\alpha = 0.95$ is given by solving

$$\alpha = \text{Pr}( \mathcal{X}^2(\widetilde{\mathcal{D}}) > c^*|\widetilde{\mathcal{D}} \sim H_0 )$$

If $\mathcal{X}^2(D) < c^*$, we do not reject the null hypothesis.

### p-values

p-value is defined as the probability, under the null hypothesis, of observing a test statistic that is large or larger than the actually observed. IF we only accept hypotheses where p-value is less than $\alpha = 0.05$, then 95% of the time we will correctly reject the null hypothesis. However, this does not mean that the alternative hypothesis $H_1$ is true with probability 0.95.

# Pathologies of frequentist statistics

## Confidence intervals

A 95% frequentist confidence interval for a parameter $\theta$ is defined as any interval $I(\widetilde{\mathcal{D}})$ such that $\text{Pr}(\theta \in I(\widetilde{\mathcal{D}}) | \widetilde{\mathcal{D}} \ approx \theta)$. This does not mean that the parameter is 95% likely to live inside this interval given the observed data. That quantity - which is usually what we want to compute - is instead fiven by the Bayesian credible interval $p(\theta \in I | \mathcal{D})$.

In frequentist approach, $\theta$ is treated as an unknown fixed constant, and the data is treated as random. In the Bayesian approach, we treat the data as fixed (since it is known) and the parameter as random (since it is unknown).

## p-values confuse deduction with induction

A p-value is often interpreted as the likelihood of the data under the null hypothesis, so small values are interpreted to mean that $H_0$ is unlikely, and therefore that $H_1$ is likely. The reasoning is roughly as follows:

> If $H_0$ is true, then this test statistic would probably not occur. This statistic did occur. Therefore $H_0$ is probably false.

However, this invalid reasoning. To see why, consider the following example:

> If a person is an American, then he is probably not a member of Congress. This person is a member of Congress. Therefore he is probably not an American.

This is obviously fallacious reasoning. By contrast, the following logical argument is valid reasoning:

> If a person is a Martian, then he is not a member of Congress. This person is a member of Congress. Therefore he is not a Martian.

The difference between these two cases is that the Martian example is using __deduction__, that is, reasoning forward from logical definitions to their consequences. By contrast the American example concerns __induction__, that is, reasoning backwards from observed evidence to probable (but not necessarily true) causes using statistical regularities not logical definitions.

To perform induction, we need to use probabilistic inference. In particular to compute the probability of the null hypothesis, we should use Bayes rule.

In the American Congress example, $\mathcal{D}$ is the observation that the person is a member of Congress. The null hypothesis $H_0$ is that the person is American, and the alternative hypothesis $H_1$ is that the person is not American. We assume $p(\mathcal{D}|H_0)$ is low, since most Americans are not members of Congress. However $p(\mathcal{D}|H_1}$ is 0, so $p(H_0|\mathcal{D}) = 1.0$ as intuition suggests. However, NHST ignores $p(\mathcal{D}|H_1)$ as well as the prior $p(H_0)$, so it gives the wrong results.

## p-values overstate evidence against the null hypothesis

In general there can be huge difference between p-values and $p(H_0|\mathcal{D})$. We should distrust claims of statistical significance if they violate our prior knowledge.

## p-values depend on the stopping rule

Another problem with p-values is that their computation depends on decisions you make about when to stop collecting data, even if these decisions don't change the data you actually observed.
