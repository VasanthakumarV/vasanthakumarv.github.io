+++
title = "Linear Algebra"
+++

# Vector spaces

The span of set of vectors ${\textbf{x}_1,\textbf{x}_2,...,\textbf{x}_n}$ is the set of all the vectors that can be expressed as a linear combination of the vectors,

$$\text{span}(\textbf{x}\_1,\ldots,\textbf{x}\_n) \triangleq \Bigg\\{ \textbf{v} : \textbf{v} =\sum_{i=1}^{n}  \alpha_i \textbf{x}_i, \alpha_i \in \mathbb{R} \Bigg\\}$$

If $\\{\textbf{x}_1, ..., \textbf{x}_2\\}$ is a set of linearly independent vectors, where $\textbf{x}_i \in \mathbb{R}^n$, then the span of that set is $\mathbb{R}^n$.

A __basis \mathcal{B}__ is a set of linearly independent vectors that span the whole space. There are often multiple basis to choose from. The _standard basis_ uses the coordinate vectors $\textbf{e}_1 = (1,0,\ldots,0)$, up to $\textbf{e}_n = (0,0,\ldots,1)$.
