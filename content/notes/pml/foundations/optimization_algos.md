+++
title = "Optimization algorithms"
weight = 7
+++

# Introduction

The core problem in machine learning is parameter estimation, this requires solving an __optimization problem__, where we try to find the values for a set of variables $\bm{\theta} \in \Theta$, that minimizes a scalar-valued loss function or cost function $\mathcal{L} : \Theta \rightarrow \mathbb{R}$

We will assume that the parameter space is given by $\Theta \subseteq \mathbb{R}^D$, where $D$ is the number of variables being optimized over. Thus we are focusing on __continuous optimization__, rather than __discrete optimization__.

If we want to maximize a score function or reward function $R(\bm{\theta})$, we can equivalently minimize $-R$. We will use the term __objective function__ to refer generically to a function we want to maximize or minimize. An algorithm that can find an optimum of an objective function is called a __solver__.

## Local vs global optimization

Finding global optima for the objective function is intractable. In such cases, we will just try to find a local optimum. For continuous problems, this is defined to be a point $\bm{\theta}^*$ which has lower (or equal) cost than nearby points.

A local minimum could be surrounded by other local minima with the same objective value; this is known as a __flat local minimum__. A point is said to be __strict local minimum__ if its cost is strictly lower than those of neighboring points.

If an algorithm is guaranteed to converge to a stationary point from any starting point, it is called __globally convergent__. However this does not mean that it will converge to global optimum, it just means it will converge to some stationary point.

### Optimality conditions for local vs global optima

For continuous, twice differentiable functions, we can precisely characterize the points which correspond to local minima. Let $g(\bm{\theta}) = \nabla \mathcal{L}(\bm{\theta})$ be the gradient vector, and $H(\bm{\theta}) = \nabla^2 \mathcal{L}(\bm{\theta})$ be the hessian matrix. Consider a point $\bm{\theta}^\* \in \mathbb{R}^D$, and let $g^\*$ be the gradient at that point, and $H^*$ be the corresponding Hessian. One can show that the following conditions characterize every local minimum:

- Necessary condition: If $\bm{\theta}^\*$ is a local minimum, then we must have $g^* = 0$ (i.e., $\bm{\theta}^\*$ must be a stationary point), and $H^*$ must be positive semi-definite
- Sufficient condition: If $g^\* = 0$ and $H^\*$ is positive definite, then $\bm{\theta}^\*$ is a local optimum

## Constrained vs unconstrained optimization

In __unconstrained optimization__, we define the optimization task as finding any value in the parameter space $\Theta$ that minimizes the loss. However, we often have a set of __constraints__ on the allowable values. It is standard to partition the set of constraints $\mathcal{C}$ into __inequality constraints__, $g\_j(\bm{\theta}) \leq 0$ for $j \in \mathcal{I}$ and __equality constraints__, $h\_k (\bm{\theta}) = 0$ for $k \in \mathcal{E}$. For example, we can represent a sum-to-one constraint as a nequality constraint $h(\bm{\theta}) = (1 - \sum\_{i=1}^{D} \theta\_i) = 0$, and we can represent a non-negativity constraint on the parameters by using $D$ inequality constraints of the form $g\_i(\bm{\theta}) = -\theta\_i \leq 0$.

We define __feasible set__ as the subset of parameter space that satisfies the constraints:

$$\mathcal{C} = \\{ \bm{\theta} : g\_j(\bm{\theta}) \leq 0 : j \in \mathcal{I}, h\_k(\bm{\theta}) = 0 : k \in \mathcal{E} \\} \subseteq \mathbb{R}^D$$

Out __constrained optimization__ problem now becomes

$$\bm{\theta}^\* \in \underset{\bm{\theta}\ \in\ \mathcal{C}}{\text{argmin}}\ \mathcal{L}(\bm{\theta})$$

If $\mathcal{C} = \mathbb{R}^D$, it is called __unconstrained optimization__.

A common strategy for solving constrained problems is to create penalty terms that measure how much we violate each constraint. We then add these terms to the objective and solve an unconstrained optimization problem. The __Lagrangian__ is a special case of such a combined objective.

## Convex vs nonconvex optimization

In convex optimization, we require the objective to be a convex function defined over a convex set. In such problems, every local minimum is also the global minimum. If $\mathcal{L}$ is a strictly convex function, then the optimal solution is unique. Furthermore, we can usually devise methods to efficiently find such minima. Thus many models are designed so that their training objectives are convex.

## Smooth vs non smooth optimization

In smooth optimization, the objective and constraints are continuously differentiable functions, whereas in nonsmooth optimization, there are aat least some points where the gradient of the objective function or the constraints is not well-defined.

In some optimization problems, we can partition the objective into a part that only contains smooth terms, and a part that contains the nonsmooth terms:

$$\mathcal{L}(\bm{\theta}) = \mathcal{L}\_s(\bm{\theta}) + \mathcal{L}\_r(\bm{\theta})$$

where $\mathcal{L}\_s$ is usually the training set loss, and $\mathcal{L}\_r$ is a regularizer. This composite structure can be exploited by various algorithms.

# First-order methods

We consider optimization methods that leverage first order derivative of the objective function, i.e., they compute which direction point downhill, but they ignore curvature information. All of these algorithms require that the user specify a starting point $\bm{\theta}\_0$. Then at each iteration $t$, they perform an update of the following form:

$$\bm{\theta}\_{t + 1} = \bm{\theta}\_t + \eta\_{t}\mathbf{d}\_t$$

where $\eta\_{t}$ is known as the step size or learning rate, and $\mathbf{d}\_t$ is a descent direction, such as the negative of the gradient, given by $\mathbf{g}\_t = \nabla\_{\bm{\theta}} \mathcal{L}(\bm{\theta}) | \_{\bm{\theta}\_t}$

## Step size (learning rate)

In machine learning, the sequence of step sizes $\\{ \eta\_t \\}$ is called the __learning rate schedule__.

### Constant step size

The simplest method is constant step size. However, if it is too large, the method may fail to converge, and if it is too small, the method will converge but very slowly.

### Line search

The optimal step size can be found by finding the value that maximally decreases the objective along the chosen direction by solving the 1d minimization problem

$$\eta\_t = \underset{\eta \gt 0}{\text{argmin}}\ \phi\_t(\eta) = \underset{\eta \gt 0}{\text{argmin}}\ \mathcal{L}(\bm{\theta}\_t + \eta \mathbf{d}\_t)$$

This is known as line search, since we are searching along the line defined by $\mathbf{d}\_t$

### Convergence rates

We want to find optimization algorithms that converge quickly to a local optimum. For certain convex problems with bounded Lipschitz constant, one can show that gradient descent converges at a linear rate.

# Momentum methods

Gradient descent can move very slowly along flat regions of the loss landscape, momentum methods can offer a solution for this.

## Momentum


