+++
title = "Singular Value Decomposition (SVD)"
weight = 3
+++

# Singular Value Decomposition (SVD)

The Singular Value Decomposition of $A$ is:

$$A = U \Sigma V^{\text{T}} = \sigma\_1 u\_1 v\_1^{\text{T}} + \ldots + \sigma\_r u\_r v\_r^{\text{T}}$$

Reduced form of SVD, has $r$ $v$'s and $u$'s and $\sigma$'s. We can reduce $AV = U\Sigma$ to $AV\_r = U\_r \Sigma\_r$ by removing parts that are sure to produce zeros ($r$ is the rank of the matrix). Now $\Sigma\_r$ is square.

# Principal Components

The principal components of $A$ are its singular vectors, the columns $u\_j$ and $v\_j$ of the orthogonal matrices $U$ and $V$. __Principal Component Analysis (PCA)__ uses the largest $\sigma$'s connected to the first $u$'s and $v$'s to understand the information in a matrix of data. We are given a matrix $A$, and we extract its most important part $A\_k$,

$$A\_k = \sigma\_1 u\_1 v\_1^{\text{T}} + \ldots + \sigma\_k u\_k v\_k^{\text{T}}$$
