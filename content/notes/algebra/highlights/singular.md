+++
title = "Singular Value Decomposition (SVD)"
weight = 3
+++

# Introduction

The Singular Value Decomposition of $A$ is:

$$A = U \Sigma V^{\text{T}} = \sigma\_1 u\_1 v\_1^{\text{T}} + \ldots + \sigma\_r u\_r v\_r^{\text{T}}$$

Reduced form of SVD, has $r$ $v$'s and $u$'s and $\sigma$'s. We can reduce $AV = U\Sigma$ to $AV\_r = U\_r \Sigma\_r$ by removing parts that are sure to produce zeros ($r$ is the rank of the matrix). Now $\Sigma\_r$ is square.
