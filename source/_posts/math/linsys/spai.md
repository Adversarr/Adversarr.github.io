---
title: Sparse Approximate Inverse
date: '2024-06-19'
toc: true
tags:
  - Numeric Methods
---

# Sparse Approximate Inverse

Given non singular $A$ find:
$$
M \approx A^{-1}, \quad M \in \mathbb{R}^{n \times n} \text{ is sparse}
$$
and $S$ is the sparsity pattern of $M$.

## Motivation

SPAI is useful as a parallel preconditioner for iterative solvers. It is also used in the context of domain decomposition methods.

Apply the preconditioner is just a SpMV operation.

- static pattern: choose a fixed sparsity pattern
- dynamic pattern: choose a sparsity pattern during the computation of $M$

## Diagonal Block Method

Given $S$ find $M$ such that:

$$
(A M)_{ij} = (I)_{ij} \quad (i,j) \in S
$$

- Not requiring $AM$ to match $I$ in every entry, but only on the sparsity pattern $S$
- This problem decouples into $n$ subproblems on each column.
  - compute $M$ is also highly parallelizable

For column $j$ we have:
$$
(A m_j)_i = \delta_{ij} \quad i \in S_j
$$
where $S_j$ is the set of rows in the sparsity pattern of column $j$.

- is attractive because of its simplicity, parallelism and scalability

Each subproblem involves solving a linear system with a sparse matrix, but can be much 
smaller than the original system by only considering the block related to the sparsity pattern.
- If $A$ is SPD, then the block in subproblems are also SPD.

Question:
1. Is $M$ non singular? No!
2. If $A$ is SPD, is $M$ SPD? No!

*For CG, we need a symmetric and positive definite preconditioner!*

## Least Squares Sparse Inverse

Given $S$ find $M$ such that:

$$
\min_{M} \| A M - I \|_F^2
$$

Again, this computation decouples into independent subproblems.

- The least-squares problem is well-posed and has a unique solution.

However, even $A$ is symmetric, $M$ is not symmetric in general.

## Generalization (Koloblina & Yeremin, 1986)

Given $S$ find $M$ such that:

$$
\min F_W (G) = \| I - G A \|_W^2 = \mathrm{tr} (I-GA) W (I-GA)^T
$$
where $W$ is a symmetric positive definite (weight) matrix.

- If $W = I$, then we have the least squares problem.

take the derivative:
$$
\frac{\partial F_W}{\partial G_{ij}} = 0 \implies
(GAWA^T)_{ij} = (WA^T)_{ij} \quad (i,j) \in S
$$

the optimal value of minimum of $F_W(G)$ is $\mathrm{tr} (W) - \mathrm{tr} (GAW)$

To see this:

$$
F_W(G) = \mathrm{tr}(W) - 2 \mathrm{tr} (GAW) + \mathrm{tr} (GAWA^TG)
$$

### $W = A^{-T}$

If $W = A^{-T}$:
$$
(GA) _{ij} = (I)_{ij} \quad (i,j) \in S
$$

Optimal value is $\mathrm{tr} (A^{-T}) - \mathrm{tr} (G AA^{-T}) = n$

Further, if $A$ is symmetric, then optimal is $\mathrm{tr} (A^{-1}) - \mathrm{tr} (G)$

choose $S$ to maximize the $\mathrm{tr} (G)$

### $W = I$

$$
(GAA^T)_{ij} = (A^T)_{ij} \quad (i,j) \in S
$$

Optimal value is $n - \mathrm{tr} (GA)$

view as solving the normal equations.

### $W = (A^T A)^{-1}$

we have:

$$
G_{ij} = (A^{-1})_{ij} \quad (i,j) \in S
$$

not practical, we donot know how to compute it cheaply.

### Properties

Nonsingularity: If $\|I - GA\| = \epsilon < 1$,

1. $GA$ is nonsingular
2. $\kappa (GA) = (1+ \epsilon)/ (1-\epsilon)$ 
3. $GA$ is positive definite.

In practice, this condition may be expensive to obtain! (need $G$ to be dense.)


## Factorized Sparse Approximate Inverse

Given $A$ find $G$ with sparse pattern $S$ such that:
$$
G^T G \approx A^{-1}
$$

advantage of this form:

- if $A$ is spd, then we can guarantee that $G^T G$ is spd.
- $G^T G$ is "denser" than $G$, so it may approximate $A^{-1}$ better

We will choose $G$ as lower triangular. (non triangular is possible, but the performance is not as well.) All known methods for computing FSAI use $G$ triangular.

If $A$ is SPD, then $G$ approximates the inverse of Cholesky factor $L$ of $A = L L^T$.

$$
\min \| I - GL \| _ F^2
$$

However, we do not know $L$.

Similar to the previous case, we can derive:
$$
(G LL^T)_{ij} = (L^T)_{ij} \quad (i,j) \in S
$$

However, $L$ is lower triangular, and $S$ is also. we only need the Diagonal part of $L$ (still not known).

Solve for $\tilde G = D G$. (scaled version of G)

$$
(\tilde G A)_{ij} = (I)_{ij} \quad (i,j) \in S
$$

And now find $D$, such that
$$
G A G = I
$$
the diagonal of $\mathrm{diag}D^{-1} \tilde G A \tilde G^T D^{-1} = \mathrm{diag}(I)$









