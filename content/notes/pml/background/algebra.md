+++
title = "Linear Algebra"
+++

# Introduction

## Vector spaces

The span of set of vectors ${\textbf{x}_1,\textbf{x}_2,...,\textbf{x}_n}$ is the set of all the vectors that can be expressed as a linear combination of the vectors,

$$\text{span}(\textbf{x}\_1,\ldots,\textbf{x}\_n) \triangleq \Bigg\\{ \textbf{v} : \textbf{v} =\sum_{i=1}^{n}  \alpha_i \textbf{x}_i, \alpha_i \in \mathbb{R} \Bigg\\}$$

If $\\{\textbf{x}_1, ..., \textbf{x}_2\\}$ is a set of linearly independent vectors, where $\textbf{x}_i \in \mathbb{R}^n$, then the span of that set is $\mathbb{R}^n$.

A __basis__ $\mathcal{B}$ is a set of linearly independent vectors that span the whole space. There are often multiple basis to choose from. The _standard basis_ uses the coordinate vectors $\textbf{e}_1 = (1,0,\ldots,0)$, up to $\textbf{e}_n = (0,0,\ldots,1)$.

## Range and nullspace of a matrix

The __range__ or the __column space__ of a matrix $\textbf{A} \in \mathbb{R}^{m \times n}$ is the span of the columns of $\textbf{A}$,

$$\text{range}(\textbf{A}) \triangleq \\{ \textbf{v} \in \mathbb{R}^m : \textbf{v} = \textbf{Ax}, \textbf{x} \in \mathbb{R}^n \\}$$

The __nullspace__ of a matrix is the set of all vectors that get mapped to the null vector when multiplied,

$$\text{nullspace}(\textbf{A}) \triangleq \\{ \textbf{x} \in \mathbb{R}^n : \textbf{Ax} = 0 \\}$$

## Linear projection

The projection of a vector $\textbf{y} \in \mathbb{R}^m$ onto the span of $\\{ \textbf{x}_1, \ldots, \textbf{x}_n \\}$ (here we assume $\textbf{x}_i \in \mathbb{R}^m$) is the vector $\textbf{v} \in \text{span}(\\{ \textbf{x}_1, \ldots, \textbf{x}_n \\})$, such that $\textbf{v}$ is as close as possible to $\textbf{y}$, as measured by the Euclidean norm $||\textbf{v} - \textbf{y}||_2$.

$$\text{Proj}(\textbf{y}; \textbf{A}) = \textbf{A}(\textbf{A}^\mathsf{T}\textbf{A})^{-1}\textbf{A}^\mathsf{T}\textbf{y}$$

## Norms of vector and matrix

The norm of a vector $||\textbf{x}||$ is informally, a measure of the length of the vector.

__p-norm__ $||\textbf{x}||_p = (\sum\_{i=1}^{n} |x_i|^p)^{1/p}$, for $p \ge 1$.

__Max-norm__ $||\textbf{x}||_{\infty} = \text{max}_i|x_i|$.

The induced norm of matrix $\textbf{A}$ as the maximum amount by which a linear function $f(\textbf{x}) = \textbf{Ax}$ can lengthen any unit-norm input.

## Properties of a matrix

__Trace__

The __trace__ of a square matrix $\textbf{A} \in \mathbb{R}^{n \times n}$, denoted by $\text{tr}(\textbf{A})$, is the sum of the diagonal elements in the matrix:

$$\text{tr}(\textbf{A}) \triangleq \sum_{i=1}^n A_{ii}$$

Some properties of trace of a matrix,

$$\text{tr}(\textbf{A}) = \sum_{i=1}^{n} \lambda_i\ \text{where}\ \lambda_i\ \text{are\ the\ eigenvalues}$$

__Determinant__

The __determinant__ of a matrix, denoted by $\text{det}(\textbf{A})$ or $|\textbf{A}|$, is a measure of how much it changes a unit volume when viewed as a linear transformation.

Some properties of determinants,

$$|\textbf{A}| = 0\ \text{iff}\ \textbf{A}\ \text{is\ singular}$$
$$\textbf{A}| = \prod_{i=1}^{n} \lambda_i\ \text{where}\ \lambda_i\ \text{are\ the\ eigen\ values\ of}\ \textbf{A}$$

__Rank__

The __column rank__ of a matrix $\textbf{A}$ is the dimension of the space spanned by its column, and the __row rank__ is the dimension of the space spanned by its rows. For any matrix $\textbf{A}$ $\text{columnrank}(\textbf{A}) = \text{rowrank}(\textbf{A})$, and so this quantity is simply referred to as the __rank__ of $\textbf{A}$.

__Condition numbers__

The __condition number__ of a matrix $\textbf{A}$ is a measure of how numerically stable any computation involving $\textbf{A}$ will be, it is defined as follows:

$$\kappa(\textbf{A}) \triangleq ||\textbf{A}||.||\textbf{A}^{-1}||$$

We say $\textbf{A}$ is well-conditioned if $\kappa(\textbf{A})$ is close to 1, and ill-conditioned if it is large.

## Special types of matrices

__Diagonal matrix__

A __diagonal matrix__ is a matrix where all non-diagonal elements are 0.

The __identity matrix__ is a square matrix, denoted $\textbf{I} \in \mathbb{R}^{n \times n}$, with ones on the diagonal and zeros everywhere else.

A __block diagonal__ matrix is one which contains matrices on the main diagonal, and is 0 everywhere else.

A __band diagonal__ matrix only has non-zero entries along the diagonal, and on $k$ sides of the diagonal, where $k$ is the bandwidth.

__Triangular matrix__

 An __uppper triangular matrix__ only has non-zero entries on and above the diagnonal. A __lower triangular matrix__ only has non-zero entries on and below the diagonal. Triangular matrices have the useful property that the diagonal entries of $\textbf{A}$ are the eigenvalues.

__Positive definite matrix__

A symmetric matrix $\textbf{A} \in \mathbb{S}^n$ is __positive definite__ iff for all non-zero vectors $\textbf{x} \in \mathbb{R}^n$, $\textbf{x}^\mathsf{T}\textbf{A}\textbf{x} > 0$. If it is possible that $\textbf{x}^\mathsf{T}\textbf{A}\textbf{x} = 0$, we say the matrix is __positive semidefinite__. We denote the set of all positive definite matrices by $\mathbb{S}_{++}^n$.

There is one type of positive definite matrix that deserves special mention. Given any matrix $\textbf{A} \in \mathbb{R}^{m \times n}$, the __Gram matrix__ $\textbf{G} = \textbf{A}^\mathsf{T}\textbf{A}$ is always positive semidefinite. Further, if $m \ge n$ (and we assume for convenience that $\textbf{A}$ is full rank), then $\textbf{G} = \textbf{A}^\mathsf{T}\textbf{A}$ is positive definite.

__Orthogonal matrix__

A set of vectors that is pairwise orthogonal and normalized is called __orthonormal__. A square matrix $\textbf{U} \in \mathbb{R}^{n \times n}$ is orthogonal if all of its columns are orthonormal.

$$\textbf{U}^{\mathsf{T}}\textbf{U} = \textbf{I} = \textbf{U}\textbf{U}^\mathsf{T}$$

__Gram Schmidt orthogonalization__ is a way to make any square matrix orthogonal.

# Matrix multiplication

## Kronecker products

If $\textbf{B}$ is an $m \times n$ matrix and $\textbf{B}$ is a $p \times q$ matrix, then the __Kronecker product__ $\textbf{A} \otimes \textbf{B}$ is the $mp \times nq$ block matrix

$$\textbf{A} \otimes \textbf{B} =
\begin{bmatrix}
a_{11}\textbf{B} \ldots a_{1n}\textbf{B} \\\\
\vdots \ddots \vdots \\\\
a_{m1}\textbf{B} \ldots a_{mn}\textbf{B}
\end{bmatrix}
$$

## Einstein summation

Einsum summation is a notational shortcut for working with tensors. In einsum notation, we write $L_{nc} = S_{ntk}W_{kd}V_{dc}$. We sum over $k$ and $d$ because those indices occur twice on the RHS. We sum over $t$ because the index does not occur on the LHS.

# Matrix inversion

 The inverse of a square matrix $\textbf{A} \in \mathbb{R}^{n \times n}$ is denoted $\textbf{A}^{-1}$, the inverse exists if and only if $\text{det}(\textbf{A})$ is not $0$. If the $\text{det}(\textbf{A}) = 0$ it is called a singular matrix.

# Eigenvalue decomposition (EVD)

Give a square matrix $\textbf{A} \in \mathbb{R}^{n \times n}$, we say that $\lambda \in \mathbb{R}$ of $\textbf{A}$ and $\textbf{u} \in \mathbb{R}^n$ is the corresponding eigenvector if,

$$\textbf{A}\textbf{u} = \lambda\textbf{u},\ \textbf{u}\text{\ not\ equal\ }0$$

This definition means that multiplying $\textbf{A}$ by the vector $\textbf{u}$ results in a new vector that points in the same direction as $\textbf{u}$, but scaled by a factor $\lambda$. We assume that the eigenvector is normalized to have length 1.

$$(\lambda \textbf{I} - \textbf{A})\textbf{u} = \textbf{0}$$

Now the equation has a non-zero solution to $\textbf{u}$ if and only if $(\lambda \textbf{I} - \textbf{A})$ has a non-empty nullspace. The $n$ solutions to this equation are the $n$ (possibly complex-valued) eigenvalues $\lambda_i$, and $\textbf{u}_i$ are the corresponding eigenvectors. It is standard to sort the eigenvectors in order of their eigenvalues, with the largest magnitude ones first.

We can write all of the eigenvector equations simultaneously as

$$\textbf{A}\textbf{U} = \textbf{U} \boldsymbol{\Lambda}$$

Where the columns of $\textbf{U} \in \mathbb{R}^{n \times n}$ are the eigenvectors of $\textbf{A}$ and $\boldsymbol{\Lambda}$ is a diagonal matrix whose entries are the eigenvalues of $\textbf{A}$.

If the eigenvectors of $\textbf{A}$ are linearly independent, then the matrix $\textbf{U}$ will be invertible, so

$$\textbf{A} = \textbf{U}\boldsymbol{\Lambda}\textbf{U}^{-1}$$

A matrix that can be written in this form is called diagonalizable.

## Standardizing and whitening data

Suppose we have a dataset $\textbf{X} \in \mathbb{R}^{N \times D}$. It is common to preprocess the data so that each column has zero mean and unit variance. This is called standardizing the data. Although standardizing forces the variance to be 1, it does not remove the correlation between the columns. To do that, we must whiten the data.

## Power method

We now describe a simple iterative method for computing the eigenvector corresponding to the largest eigenvalue of a real symmetric matrix; this is called the power method.

Let $\textbf{A}$ be a matrix with orthonormal eigenvectors, so $\textbf{A} = \textbf{U}\boldsymbol{\Lambda}\textbf{U}^{\mathsf{T}}$. Let $\textbf{v}\_{(0)}$ be an arbitrary vector in the range of $\textbf{A}$, so $\textbf{A}\textbf{x} = \textbf{v}_{(0)}$ for some $\textbf{x}$. Hence we can write $\textbf{v}\_{(0)}$ as

$$\textbf{v}_0 = \textbf{U}(\boldsymbol{\Lambda}\textbf{U}^{\mathsf{T}}\textbf{x}) = a_1 \textbf{v}_1 + \ldots + a_m\textbf{u}_m$$

for some constants $a_i$. We can now repeatedly multiply $\textbf{v}$ by $\textbf{A}$ and renormalize:

$$\textbf{v}\_{t} \propto \textbf{A} \textbf{v}_{t - 1}$$

Since $\textbf{v}_t$ is a multiple of $\textbf{A}^t \textbf{v}_0$, we have

$$\textbf{v}_t \propto a_1\lambda_1^t\textbf{u}_1 + \ldots + a_m\lambda_m^t\textbf{u}_m \rightarrow \lambda_1^ta_1\textbf{U}_1$$

since $\frac{|\lambda_k|}{|\lambda_1|} < 1$ for $k > 1$ (assuming the eigenvalues are sorted in descending order). So we can see that this converges to $\textbf{u}_1$. 

We can now discuss how to compute the corresponding eigenvalue $\lambda_1$. Define the Rayleigh quotient to be,

$$R(\textbf{A}, \textbf{x}) \triangleq \frac{\textbf{x}^{\mathsf{T}} \textbf{A} \textbf{x}}{\textbf{x}^\mathsf{T} \textbf{x}}$$

Hence,

$$R(\textbf{A}, \textbf{u}_i) = \frac{\textbf{u}_i^{\mathsf{T}}\textbf{A}\textbf{u}_i}{\textbf{u}_i^{\mathsf{T}}} = \lambda_i$$

Thus we can easily compute $\lambda_i$ from $\textbf{u}_i$ and $\textbf{A}$.

## Deflation

We now describe how to compute subsequent eignevectors and values. Since the eigenvectors are orthonormal, and the eigenvalues are real, we can project out the $\textbf{u}_1$ component from the matrix as follows,

$$\textbf{A}^{(2)} = \textbf{A}^{(1)} - \lambda_1 \textbf{u}_1 \textbf{u}_1^{\mathsf{T}}$$

This is called deflation. We can then apply the power method to find the largest eigenvector and value in the subspace orthogonal to $\textbf{u}_1$.

# Singular value decomposition (SVD)

SVD generalizes EVD to rectangular matrices.

$$\textbf{A} = \textbf{U}\textbf{S}\textbf{V}^\mathsf{T} = \sigma_1
\begin{pmatrix}
| \\\\
\textbf{u}_1 \\\\
|
\end{pmatrix}
\begin{pmatrix}
\- & \textbf{v}_1^{\mathsf{T}} & \-
\end{pmatrix}
+
\ldots
+
\sigma_r
\begin{pmatrix}
| \\\\
\textbf{u}_r \\\\
|
\end{pmatrix}
\begin{pmatrix}
\- & \textbf{v}_r^{\mathsf{T}} & \-
\end{pmatrix}
$$

Where $\textbf{U}$ is an $m \times m$ whose columns are orthonormal (so $\textbf{U} \textbf{U}^\mathsf{T} = \textbf{I}_m$), $\textbf{V}$ is $n \times n$ matrix whose rows and columns are orthonormal (so $\textbf{V}^\mathsf{T} \textbf{V} = \textbf{V} \textbf{V}^\mathsf{T} = \textbf{I}_n$), and $\textbf{S}$ is a $m \times n$ matrix containing the $r = min(m, n)$ __singular values__ $\sigma_i \ge 0$ on the main diagonal, with 0s filling the rest of the matrix. The columns of $\textbf{U}$ are left singular vectors, and the columns of $\textbf{V}$ are right singular vectors.

## Pseudo inverse

The __Moore-Penrose pseudo-inverse__ of $\textbf{A}$, pseudo inverse denoted $\textbf{A}^{\dagger}$, is defined as the unique matrix that satisfies the following four properties:

$$\mathbf{A} \mathbf{A}^\dagger \mathbf{A} = \mathbf{A}, \mathbf{A}^\dagger \mathbf{A} \mathbf{A}^\dagger = \mathbf{A}^\dagger, (\mathbf{A}^\dagger \mathbf{A})^\top = \mathbf{A}^\dagger \mathbf{A}, (\mathbf{A} \mathbf{A}^\dagger)^\top = \mathbf{A} \mathbf{A}^\dagger$$

If $\mathbf{A}$ is square and non-singular, then $\mathbf{A}^\dagger = \mathbf{A}^{-1}$.

If $m > n$ (tall, skinny) and the columns of $\mathbf{A}$ are linearly independent (so $\mathbf{A}$ is full rank), then

$$\mathbf{A}^{\dagger} = (\mathbf{A}^{\top}\mathbf{A})^{-1} \mathbf{A}^{\top}$$

We can compute pseudo inverse using SVD decomposition,

$$\mathbf{A}^\dagger = \mathbf{A}^{-1} = \mathbf{V} \mathbf{S}^{-1} \mathbf{U}^\top$$

# Other matrix decompositions

__LU factorization__

We can factorize any square matrix $\mathbf{A}$ into a product of lower triangular matrix $\mathbf{L}$ and an upper triangular matrix $\mathbf{U}$.

__QR decomposition__

Suppose we have $\mathbf{A} \in \mathbb{R}^{m \times n}$ representing a set of linearly independent basis vectors (so $m \ge n$), and we want to find a series of orthonormal vectors $\mathbf{q}_1, \mathbf{q}_2, \ldots$ that span the successive subspaces of $\text{span}(\mathbf{a_1}), \text{span}(\mathbf{a}_1, \mathbf{a}_2), \text{etc}$. QR decomposition is commonly used to solve systems of linear equations.

__Cholesky decomposition__

Any symmetric positive definite matrix can be factorized as $\mathbf{A} = \mathbf{R}^\top \mathbf{R}$, where $\mathbf{R}$ is upper triangular with real, positive diagonal elements.

# Solving systems of linear equations

If we have $m$ equations and $n$ unknowns then $\mathbf{A}$ will be a $m \times n$ matrix, $\mathbf{b}$ will be a $m \times 1$ vector. If $m = n$ (and $\mathbf{A}$ is full rank), there is a single unique solution. If $m < n$ the system is underdetermined, so there is no unique solution. If $m > n$, the system is overdetermined, since there are more constraints than unknowns, and not all lines intersect at the same point.

## Solving square systems

In the case where $m = n$, we can solve for $\mathbf{x}$ by computing an LU decomposition, $\mathbf{A} = \mathbf{L}\mathbf{U}$, and then proceeding as follows:

$$\begin{aligned}
\mathbf{Ax} &= \mathbf{b} \\\\
\mathbf{LUx} &= \mathbf{b} \\\\
\mathbf{Ux} &= \mathbf{L}^{-1} \mathbf{b} \triangleq \mathbf{y} \\\\
\mathbf{x} &= \mathbf{U}^{-1} \mathbf{y}
\end{aligned}
$$
The crucial point is that $\mathbf{L}$ and $\mathbf{U}$ are both triangular matrices, so we can avoid taking matrix inverses, and use a method known as __backsubstituion__ instead.

## Solving underconstrained systems

Here we consider underconstrained setting, where $m < n$. We assume the rows are linearly independent, so $\mathbf{A}$ is full rank. When $m < n$, there are multiple possible solutions, which have the form

$$\\{ \mathbf{x} : \mathbf{Ax} = \mathbf{b} \\} = \\{ \mathbf{x}_p + \mathbf{z : z} \in \text{nullspace}(\mathbf{A}) \\}$$

Where $\mathbf{x}_p$ is any particular solution. It is standard to pick the particular solution with minimal $l_2$ norm.

## Solving overconstrained systems

If $m > n$, we have an overdetermined solution, which typically does not have an exact solution, but we will try to fidn the solution that gets as close as possible to satisfying all of the constraints specified by $\mathbf{Ax = b}$. We can do this by minimizing the following cost function, known as the __least squares objective__:

$$f(\mathbf{x}) = \frac{1}{2} || \mathbf{Ax - b} ||_2^2$$

Using matrix calculus, we can find its gradient,

$$g(\mathbf{x}) = \frac{\partial(f(\mathbf{x}))}{\partial \mathbf{x}} = \mathbf{A^\top A x} - \mathbf{A^\top b}$$

The optimum can be found by setting the gradient to 0, the corresponding $\mathbf{\hat{x}}$ is the __ordinary least squares (OLS)__ solution, which is given by,

$$\mathbf{\hat{x}} = \mathbf{(A^\top A)}^{-1} \mathbf{A^\top b}$$
