+++
title = "Sets, functions and relations"
+++

# Sets

A set is collection of objects, it can be finite, or countably infinite, or uncountably infinite, it can be empty (denoted by $\phi$). The size of a set is denoted by $|\mathcal{X}|$

# Functions

A function $f : \mathcal{X} \longrightarrow \mathcal{Y}$ is a mapping from a set of points known _domain_ to another set of points known as _codomain_. For example, $y = x^2$ is a function mapping $X = \mathbb{R}$ to $\mathcal{Y} = \mathbb{R}_+$. 

# Continuous functions

$$\forall\epsilon > 0.\ \exists\ \delta > 0.\ \text{s.t.}\ ||\bold{x} - \bold{a}|| < \delta \Longrightarrow ||f(\bold{x}) - f(\bold{a})|| < \epsilon$$

If we move small distance in the input space, then the function's response should only change a little bit.

# Lipschitz constants

Lipschitz constant of a function measures how much the function changes as we vary its input. In 1d case, this is defined as a constant $C \ge 0$, we have

$$|f(x_1) - f(x_2)| \le C|x_1 - x_2|$$

For a given constant $C$, the function output cannot change by more than $C$ if we change the input by 1 unit.

# Jacobian

Consider a function that maps a vector to another vector, $\bold{f} : \mathbb{R}^n \rightarrow \mathbb{R}^m$, the jacobian matrix of this function is $m \times n$ matrix of partial derivatives (we lay out the results in numerator layout):

$$\bold{J} \triangleq
\begin{pmatrix}
\frac{\partial f_1}{\partial x_1} & \ldots & \frac{\partial f_1}{\partial x_n} \\\\
\vdots & \ddots & \vdots \\\\
\frac{\partial f_m}{\partial x_1} & \ldots & \frac{\partial f_m}{\partial x_n}
\end{pmatrix}
$$

__Jacobian vector product__ is multiplying the Jacobian matrix $\bold{J} \in \mathbb{R}^{m \times n}$ by a vector $\bold{v} \in \mathbb{R}^n$. __Vector Jacobian product__ is left-multiplying the Jacobian matrix by a vector. JVP is efficient if $m \ge n$, and VJP is efficient when $m \le n$.

# Hessian

For a function $f : \mathbb{R}^n \rightarrow \mathbb{R}$ that is twice differentiable, we define Hessian matrix as $n \times n$ matrix of second partial derivativess:

$$\bold{H} = \frac{\partial^2 f}{\partial \bold{x}^2} = \nabla^2 f =
\begin{pmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \ldots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\\\
 & \vdots & \\\\
\frac{\partial^2 f}{\partial x_n \partial x_1} & \ldots & \frac{\partial^2}{\partial x_n^2}
\end{pmatrix}
$$

# Convexity

__Convex set__

We say $\mathcal{s}$ is a __convex set__ if, for any $\bold{x}, \bold{x}\prime \in \mathcal{S}$, we have,

$$\lambda \bold{x} + (1 - \lambda)\bold{x}\prime, \forall \lambda \in [0, 1]$$

That is, if we draw a line from $\bold{x}$ to $\bold{x}\prime$, all points on the line lie inside the set.

__Convex function__

We say a function $f$ is convex if its __epigraph__ (the set of points above the function) defines a convex set.

A function $f$ is convex iff $\bold{H} = \nabla^2f(\bold{x})$ is _positive semi definite_ for all $\bold{x} \in \text{dom}(f)$, $f$ is strictly convex if $\bold{H}$ is _positive definite_.
