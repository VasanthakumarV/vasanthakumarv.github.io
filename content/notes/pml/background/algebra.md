+++
title = "Linear Algebra"
+++

# Vector spaces

The span of set of vectors ${\textbf{x}_1,\textbf{x}_2,...,\textbf{x}_n}$ is the set of all the vectors that can be expressed as a linear combination of the vectors,

$$\text{span}(\textbf{x}\_1,\ldots,\textbf{x}\_n) \triangleq \Bigg\\{ \textbf{v} : \textbf{v} =\sum_{i=1}^{n}  \alpha_i \textbf{x}_i, \alpha_i \in \mathbb{R} \Bigg\\}$$

If $\\{\textbf{x}_1, ..., \textbf{x}_2\\}$ is a set of linearly independent vectors, where $\textbf{x}_i \in \mathbb{R}^n$, then the span of that set is $\mathbb{R}^n$.

A __basis__ $\mathcal{B}$ is a set of linearly independent vectors that span the whole space. There are often multiple basis to choose from. The _standard basis_ uses the coordinate vectors $\textbf{e}_1 = (1,0,\ldots,0)$, up to $\textbf{e}_n = (0,0,\ldots,1)$.

# Range and nullspace of a matrix

The __range__ or the __column space__ of a matrix $\textbf{A} \in \mathbb{R}^{m \times n}$ is the span of the columns of $\textbf{A}$,

$$\text{range}(\textbf{A}) \triangleq \\{ \textbf{v} \in \mathbb{R}^m : \textbf{v} = \textbf{Ax}, \textbf{x} \in \mathbb{R}^n \\}$$

The __nullspace__ of a matrix is the set of all vectors that get mapped to the null vector when multiplied,

$$\text{nullspace}(\textbf{A}) \triangleq \\{ \textbf{x} \in \mathbb{R}^n : \textbf{Ax} = 0 \\}$$

# Linear projection

The projection of a vector $\textbf{y} \in \mathbb{R}^m$ onto the span of $\\{ \textbf{x}_1, \ldots, \textbf{x}_n \\}$ (here we assume $\textbf{x}_i \in \mathbb{R}^m$) is the vector $\textbf{v} \in \text{span}(\\{ \textbf{x}_1, \ldots, \textbf{x}_n \\})$, such that $\textbf{v}$ is as close as possible to $\textbf{y}$, as measured by the Euclidean norm $||\textbf{v} - \textbf{y}||_2$.

$$\text{Proj}(\textbf{y}; \textbf{A}) = \textbf{A}(\textbf{A}^\mathsf{T}\textbf{A})^{-1}\textbf{A}^\mathsf{T}\textbf{y}$$

# Norms of vector and matrix

The norm of a vector $||\textbf{x}||$ is informally, a measure of the length of the vector.

__p-norm__ $||\textbf{x}||_p = (\sum\_{i=1}^{n} |x_i|^p)^{1/p}$, for $p \ge 1$.

__Max-norm__ $||\textbf{x}||_{\infty} = \text{max}_i|x_i|$.


