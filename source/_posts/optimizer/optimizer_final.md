---
title: A short summary to Optimization Theory.
date: 2024-06-21
---

# Optimization

## Lecture 2: Convex Set

### Common Convex Sets

- **Hyperplane**: $H = \{x \in \mathbb{R}^n \mid a^Tx = b\}$.
- **Halfspace**: $H = \{x \in \mathbb{R}^n \mid a^Tx \leq b\}$.
- **Polyhedron**: $P = \{x \in \mathbb{R}^n \mid Ax \leq b\}$.
- **Euclidean Ball**: $B = \{x \in \mathbb{R}^n \mid \|x - x_c\|_2 \leq r\}$.
- **Ellipsoid**: $E = \{x \in \mathbb{R}^n \mid (x - x_c)^T P^{-1} (x - x_c) \leq 1\}$.
- **Norm Ball**: $B = \{x \in \mathbb{R}^n \mid \|x - x_c\|_p \leq r\}$.
- **Norm Cone**: $C = \{x \in \mathbb{R}^n \mid \|x\|_p \leq t\}$.

Some special matrices:

- Symmetric matrix set: $S^n = \{X \in \mathbb{R}^{n \times n} \mid X = X^T\}$.
- Semi-positive definite matrix set: $S_+^n = \{X \in \mathbb{R}^{n \times n} \mid X = X^T, \lambda_{\min}(X) \geq 0\}$.
- Positive definite matrix set: $S_{++}^n = \{X \in \mathbb{R}^{n \times n} \mid X = X^T, \lambda_{\min}(X) > 0\}$.

Actually, SPD matrix set is a cone.


### Property of `conv`

Convex combination:
$$
x = \theta_1 x_1 + ... + \theta_k x_k, \theta_i \geq 0, \sum_{i=1}^k \theta_i = 1.
$$

$\mathbf{conv} S$ is the smallest convex set that contains $S$.
- Also the intersection of all convex sets that contain $S$.

`aff`: The smallest affine set that contains $S$.
- The smallest affine set that contains $S$.
- Containing all the affine combinations of points in $S$.

Cone: 
$$
C = \{x \in \mathbb{R}^n \mid \lambda x \in C, \forall \lambda \geq 0\}
$$

Cone combination:
$$
x = \theta_1 x_1 + ... + \theta_k x_k, \theta_i \geq 0, x_i \in C.
$$

- If all the cone combinations of $x_1, ..., x_k$ are in $C$, then $C$ is a convex cone.

### Operations on Convex Sets

Affine transform keeps convexity.

Perspective transform $P: R^{n+1} \to R^n$
$$
P(x, t) = \frac{x}{t}, \text{dom} P = \{(x, t) \mid t > 0\}
$$
Perspective transform keeps convexity.

Therefore:
$$
f(x)  = \frac{Ax + b}{c^Tx + d}, \text{dom} f = \{x \mid c^Tx + d > 0\}
$$
keeps convexity.

### Dual Cone & Generalized Inequalities

**Proper cone**:
- Closed
- $\text{int} K$ is nonempty
- $K$ is pointed: $K \cap -K = \{0\}$

For example:
1. Nonnegative orthant: $K = \mathbb{R}_+^n$
2. Semi-PD matrix cone: $K = S_{+}^n$

**Generalized Inequalities**: For proper cone $K$,
$$
x \preceq_K y \Leftrightarrow y - x \in K
$$
Strict inequality:
$$
x \prec_K y \Leftrightarrow y - x \in \text{int} K
$$

**Dual Cone**: For $K$, the dual cone is
$$
K^* = \{y \mid x^Ty \geq 0, \forall x \in K\}
$$

There are many properties for dual cone

- $K^*$ is a cone, and a closed convex set.
- if $\mathrm{int} K$ is nonempty, then $K^*$ is pointed
- ... (see slide page 36.)

One important property is: if $K$ is proper, then $K^*$ is also proper.

There is dual generalized inequalities:
$$
x \preceq_K y \iff y - x \in K^*
$$
it satisfies:
- $x \preceq_K y \implies z^Tx \leq z^Ty, \forall z \succeq_{K^*} 0$

> The advantage of dual generalized inequalities is that, the dual cone is always closed and convex, and it converts a partial order to a full order problem.

> Reference: 02-convex-set-ustc.pdf, page 37

### Separating Hyperplane Theorem

For two disjoint convex sets $C$ and $D$, there exists a hyperplane that separates them.

**Supporting Hyperplane**: For a convex set $C$, and a point $x_0 \in \partial C$, there exists a hyperplane $a^Tx = b$ such that $a^Tx \leq b, \forall x \in C$.

## Convex Function

### Definition


