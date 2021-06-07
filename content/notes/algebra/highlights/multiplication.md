+++
title = "Multiplication"
weight = 1
+++

# Matrix-Vector multiplication 

Mutiplication $Ax$ using columns of $A$,

$$
\begin{bmatrix}
2 & 3 \\\\
2 & 4 \\\\
3 & 7
\end{bmatrix}
\begin{bmatrix}
x\_1 \\\\
x\_2
\end{bmatrix}
\=
x\_1
\begin{bmatrix}
2 \\\\
2 \\\\
3
\end{bmatrix}
+
x\_2
\begin{bmatrix}
3 \\\\
4 \\\\
7
\end{bmatrix}
$$

Multiplication using dot products/rows is low level and used for computing. Understanding is higher level, using vectors.

__Thus $Ax$ is linear combination of the columns of $A$. This is fundamental.__

__The combination of columns__ fill out the __column space__ of $A$. The column space of the above example is a plane.

- Three independent columns in $\mathbb{R}^3$ produce an __invertible matrix__.
- $Ax = \mathbf{0}$ requires $x = (0, 0, 0)$, then $Ax = b$ has exactly one solution.

__The rank of a matrix is the dimension of its column space.__

$$\mathbf{A} = \mathbf{CR}$$

$\mathbf{C}$ is the basis of $\mathbf{A}$, and $\mathbf{R}$ is the __row-reduced echelon form of $\mathbf{A}$__

The big factorization for data science is the "SVD" of $A$, where the first factor $C$ has $r$ orthogonal columns and the second factor $R$ has  $r$ orthogonal rows.

# Matrix-Matrix multiplication 

Two ways to arrive at matrix-matrix multiplication,

- Using inner products between rows and columns from $A$ and $B$ respectively
- Using the outer product of the columns of $A$ with the rows of $B$, and adding together all the outer products (rank one matrices)

Both involve $mnp$ multiplications.

## Insights from Column times Row

Outer product helps us look for the important part of matrix $A$, we do not usually want the biggest number in $A$, what we want is the largest piece of $A$. __And those pieces are the rank one matrices__.
