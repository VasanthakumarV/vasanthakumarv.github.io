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

Consider a function that maps a vector to another vector, $\bold{\text{f}} : \mathbb{R}^n \rightarrow \mathbb{R}^m$, the jacobian matrix of this function is $$m \cross n$ matrix of partial derivatives (we lay out the results in numerator layout):

$$\bold{\text{J}} \triangleq
\begin{pmatrix}
\frac{\partial f_1}{\partial x_1} & \ldots & \frac{\partial f_1}{\partial x_n} \\\\
\vdots & \ddots & \vdots \\\\
\frac{\partial f_m}{\partial x_1} & \ldots & \frac{\partial f_m}{\partial x_n}
\end{pmatrix}
$$
