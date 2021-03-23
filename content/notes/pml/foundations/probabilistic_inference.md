+++
title = "Probabilistic Inference"
weight = 1
+++

# Bayesian Inference

__Inference__ is the process of arriving at generalizations using sample data. __Bayesian Inference__ uses _Bayes' Theorem_ to model the probability of different hypotheses.

$$p(H=h|Y=y) = \frac{p(H=h)p(Y=y|H=h)}{p(Y=y)}$$

- $p(H=h|Y=y)$ is the _posterior distribution_
- $p(H=h)$ is the _prior distribution_
- $p(Y=y|H=h)$ is the _likelihood_, this is not a probability distribution
- $p(Y=y)$ is the _marginal likelihood_

# Bayesian Concept Learning

We can model the distribution of the hidden quantity of interest $h \in H$ from a set of observations, $D = {y_n : n = 1 : N}$, the goal is to infer the _hidden patterns_ or _concept_ from the underlying data.

Humans can _generalize_ a sequence of numbers, based on whether they are all powers of 2, or whether they are even numbers and other similar hypotheses. How do we emulate such process in machines. One classic approach is __Induction__, here we move from a _hypotheses space_ $H$ of concepts to _version space_ based on the observed data $D$, as more data comes in, we become more certain and the version space shrinks. But the version space theory cannot explain why people choose  _powers of two_ when they see $D = \\{ 16, 8, 2, 64 \\}$ and not _all even numbers_ or _powers of 2 except 32_. Bayesian Inference can help explain this behavior.

## Likelihood

To explain why people go with $h_{two}$ and not $h_{even}$ we will have to understand that it will __suspiciously coincidental__ for all the examples in $D = \\{16, 8, 2, 64\\}$ to be powers of two if the true underlying hypothesis was $h_{even}$.

## Prior

Priori is usefull because, the hypothesis _powers of 2 except 32_ is more likely than _powers of 2_, but the former more likely hypothesis is _unnatural_ and we can eliminate such concepts by assigning low priors. Background knowledge or Domain knowledge can be brought into a problem using the prior values.

## Posterior

Posterior is proportional to likelihood times prior, find below an image that shows how both influence the posterior in identifying the most likely hypothesis for the observed $D$.

<div class="image-center">
{{ resize_image(path="notes/pml/foundations/pml_posterior.png", width=500, height=0 op="fit_width") }}
</div>

## Maximum a Posterior (MAP)

__MAP__ is defined as the hypothesis with the maximum posterior probability.

$$h_{map} \triangleq \argmax_h(h|D)$$

## Maximum Likelihood Estimate (MLE)

In MAP as the data size increases the prior term stays constant, hence it is reasonable to approximate MAP and just pick maximum likelihood estimate or __MLE__

$$h_{mle} \triangleq \argmax_{h}p(D|h) = \argmax_{h}\log p(D|h) = \argmax_{h}\sum_{n=1}^{N}\log p(y_n|h)$$

## Learning a continuous concept

The game is called __healthy levels__, we are tasked with identifying the healthy range for two continuous variables _cholestrol_ and _insulin_ from healthy patients, we will be provided with only positive examples. The hypotheses space will be axis parallel rectangles, it can be represented as $h = (l_1, l_2, s_1, s_2)$, where $l_j \in [-\infty, \infty]$ and represents the lower left corner of the rectangle, $s_j \in [0, \infty]$ are the lengths of the two sides.

### Likelihood

For 1d we will have $p(D|l,s) = (\frac{1}{s})^N$ if all the points are inside the interval. For 2d we assume the features are conditionally independent given the hypothesis.

$$p(D|h) = p(D_1|l_1,s_1)p(D_2|l_2,s_2)$$

### Prior

We will use uninformative priors of the form $p(h) \propto \frac{1}{s_1}\frac{1}{s_2}$.

### Posterior

Posterior is given by,

$$p(l_1, l_2, s_1, s_2|D) \propto p(D_1|l_1,s_1)p(D_2|l_2,s_2)\frac{1}{s_1}\frac{1}{s_2}$$

# Bayesian Machine Learning

In many applications along with each unknown output $\bold{y}$ we will have features $\bold{x} \in X$ associated with it, in such cases we want to use conditional probability distribution of the form $p(\bold{y}|\bold{x},D)$, where $D = \\{(\bold{x}_n,\bold{y}_n) : n = 1:N\\}$. If the output is from a low-dimensional space, such as a set of labels $y \in \\{1,...,C\\}$ or scalars $y \in \mathbb{R}$, then we call it __discriminative model__, since it discriminates between different possbile outputs. If the output is high dimensional like images or sentences, it is called a __conditinal generative model__. 

In these complex settings, the hypothesis or concept $h$ predictst the output given the input and set of real valued parameters $\theta \in \mathbb{R}^K$.

$$p(\bold{y}|\bold{x},\theta) = p(\bold{y}|f(\bold{x};\theta))$$

Where $f(\bold{x};\theta)$ maps the inputs to the parameters of the output distribution. To fully specify the model, we need to choose the output probability distribution and the form of $f$.

## Plugin Approximation

Here we fit a model to compute a point estimate $\hat{\theta}$ and then use it to make predictions. The posterior is represented using __Dirac delta function__, the point estimates of the posterior are computed using __MLE__ or __MAP__. The __sifting property__ of the dirac delta helps us arrive at the final form.

$$p(\bold{y}|D) = \int p(\bold{y}|\theta) p(\theta|D) d\theta \approx \int p(\bold{y}|\theta)\delta(\theta - \hat{\theta}) d\theta = p(\bold{y}|\hat{\theta})$$
