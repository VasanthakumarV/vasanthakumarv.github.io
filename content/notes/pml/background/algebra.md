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

The induced norm of matrix $\textbf{A}$ as the maximum amount by which a linear function $f(\textbf{x}) = \textbf{Ax}$ can lengthen any unit-norm input.

# Properties of a matrix

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

# Special types of matrices

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
