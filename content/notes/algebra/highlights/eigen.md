+++
title = "Eigenvalues and Eigenvectors"
weight = 2
+++

# Eigenvalues and Eigenvectors 

The eigenvectors of $A$ do not change direction when you multiply them by $A$. The output $Ax$ is on the same line as the input vector $x$.

$$Ax = \lambda x$$

Multiply again by $A$, to see that __$x$ is also an eigenvector of $A^2$__:

$$A^k x = \lambda^k x$$

- Sum of eigenvalues will be the trace of $A$
- Product of eigenvalues will be the determinant of $A$
- Symmetric matrices will have real eigenvalues

__The eigenvalues of any triangular matrix is its main diagonal elements.__

# Symmetric positive definite matrices

- All $n$ eigenvalues $\lambda$ of a symmetric matrix $S$ are real numbers
- The $n$ eigenvectors $q$ can be chosen orthogonal (perpendicular to each other)

__Spectral theorem: Every real symmetric matrix has the form $S = Q \Lambda Q^\text{T}.$__

# Positive definite matrices

__A positive definite matrix has all positive eigenvalues__.

If $\lambda \geq 0$ but not $\lambda \gt 0$ then it is __positive semidefinite__.

__Elimation factors every positive definite $S$ into $A^\text{T}A$ (A is upper triangular)__

This is Cholesky factorization $S = A^{\text{T}}A$ with $\sqrt{\text{pivots}}$ on the main diagonal of $A$.
