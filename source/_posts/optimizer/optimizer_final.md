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

## Lecture 3: Convex Function

### Gradients & Hessians

**Gradient**:
$$
\lim_{p\to 0} \frac{f(x + p) - f(x)}{\|p\|} = \nabla f(x)
$$

**Hessian**:
$$
\nabla^2 f(x) = \begin{bmatrix}
\frac{\partial^2 f}{\partial x_1^2} & \frac{\partial^2 f}{\partial x_1 \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_1 \partial x_n} \\
\frac{\partial^2 f}{\partial x_2 \partial x_1} & \frac{\partial^2 f}{\partial x_2^2} & \cdots & \frac{\partial^2 f}{\partial x_2 \partial x_n} \\
\vdots & \vdots & \ddots & \vdots \\
\frac{\partial^2 f}{\partial x_n \partial x_1} & \frac{\partial^2 f}{\partial x_n \partial x_2} & \cdots & \frac{\partial^2 f}{\partial x_n^2}
\end{bmatrix}
$$

Gateaux derivative:
$$
\lim_{\alpha \to 0} \frac{f(x + \alpha d) - f(x) - t \langle g, d \rangle}{\alpha}
$$


Some important derivatives:
$$
\text{Linear: } \nabla_x \mathrm{tr} (A X^T B) = BA
$$

$$
\text{Quadratic: } \nabla_x x^T A x = (A + A^T) x
$$

$$
\nabla \ln \det X = X^{-1}
$$

### Definition

A function $f: \mathbb{R}^n \to \mathbb{R}$ is convex if:
$$
f(\theta x + (1-\theta)y) \leq \theta f(x) + (1-\theta)f(y), \forall x, y \in \text{dom} f, \theta \in [0, 1]
$$

Strict convex:
$$
f(\theta x + (1-\theta)y) < \theta f(x) + (1-\theta)f(y), \forall x, y \in \text{dom} f, \theta \in (0, 1)
$$

some important examples in 1D:
- Affines
- Exponentials
- Powers $x^p$, with $p \geq 1, x \in \mathbb R_{++}$
- Negative entropy $x \ln x$, with $x \in \mathbb R_{++}$

basic examples in $\mathbb{R}^n$:
- Affine functions
- Norm, with $p \geq 1$

In matrix space:
- $f(X) = \mathrm{tr} (AX) = \sum_{ij} A_{ij} X_{ij} + b$ is affine, convex.
- Matrix norms ($p=2$): $f(X) = \|X\|_2$ is convex.

### checking convexity

**Restrict to line**:
$g(t) = f(x + td)$ is always convex, then $f$ is convex.

**First order condition**: 
if $f$ is differentiable, then $f$ is convex if and only if $f(y) \geq f(x) + \nabla f(x)^T (y - x)$.

More on derivative:
if $f$ is differentiable, then $f$ is convex if and only if $\mathrm{dom} f$ is convex, and $\nabla f$ is monotonically increasing:
$$
(\nabla f(x) - \nabla f(y))^T (x - y) \geq 0, \forall x, y \in \text{dom} f
$$

**Second order condition**:
if $f$ is twice differentiable, then $f$ is convex if and only if $\nabla^2 f(x) \succeq 0, \forall x \in \text{dom} f$.

And if $\nabla^2 f \succ 0$, then $f$ is strictly convex.

**Jensen's Inequality**:
if $f$ is convex, then
1. $f(\theta x + (1-\theta)y) \leq \theta f(x) + (1-\theta)f(y)$
2. $f(\mathbb{E}[X]) \leq \mathbb{E}[f(X)]$

### Operations

**Nonnegative weighted sum**:
$$
f(x) = \sum_{i=1}^k \theta_i f_i(x), \theta_i \geq 0
$$

**Pointwise maximum**:
$$
f(x) = \max_{i=1}^k f_i(x)
$$

**Composition with affine transform**:
$$
f(x) = g(Ax + b)
$$

**Composition with perspective transform**:
$$
g(x, t) = t f(x / t)
$$

**Conjugate function**:
$$
f^*(y) = \sup_{x \in \text{dom} f} \langle x, y \rangle - f(x)
$$

- [ ] Connection to proximal operator, Moreau decomposition.

## Lecture 4: Convex Problems

**Definition of Convex Optimization Problem**:
$$
\begin{aligned}
       \min \quad &f_0(x) \\
\text{s.t.} \quad &f_i(x) \leq 0, i = 1, ..., m \\
                  &h_i(x) = 0, i = 1, ..., p
\end{aligned}
$$

basic property: the feasible set is convex.

**Theorem**: Any local minimum of a convex problem is a global minimum.

**Linear Programming**:
$$
\min c^Tx \quad \text{s.t.} \quad Ax = b, G x \leq e
$$
and fractional linear programming, is also equivalent to linear programming.

**Quadratic Programming**:
$$
\min \frac{1}{2} x^T P x + q^T x + r \quad \text{s.t.} \quad Ax = b, G x \leq e
$$

some examples:
- Least squares
- Stotasitc Linear Programming

**QCQP**:
$$
\min x^T P_0 x + q_0^T x + r_0 \quad \text{s.t.} \quad x^T P_i x + q_i^T x + r_i \leq 0, i = 1, ..., m
$$

**SOCP**:
$$
\begin{aligned}
       \min \quad &c^Tx \\
\text{s.t.} \quad &\|A_i x + b_i\|_2 \leq c_i^T x + d_i, i = 1, ..., m
                  &Fx = g
\end{aligned}
$$

**Convex Relaxation**: max-cut:
$$
\begin{aligned}
       \max \quad &\frac{1}{2} \sum_{i < j} (1 - x_i x_j) w_{ij} \\
\text{s.t.} \quad &x_i \in \{-1, 1\}
\end{aligned}
$$

relaxation: let $W = (w_{ij}) \in S^n$, $C = -\frac{1}{4} (\mathrm{diag} (W 1) - W)$ (graph laplacian):
$$
\begin{aligned}
       \max \quad &\frac{1}{4} x^T C x \\
\text{s.t.} \quad &x_i \in \{-1, 1\}
\end{aligned}
$$

Let $X = xx^T$, and use $x_i^2 = 1$, we have:
$$
\begin{aligned}
       \max \quad &\frac{1}{4} \mathrm{tr} (CX) \\
\text{s.t.} \quad &X \succeq 0, X_{ii} = 1, X\preceq 0, \mathrm{rank} X = 1
\end{aligned}
$$

## Lecture 5: Optimal conditions

### First Order Condition and Second Order Condition

**First order**: Suppose $f$ is differentiable, then $x$ is optimal must satisfies
$$
\nabla f(x) = 0
$$
This is only a necessary condition generally. But for convex function, it is also sufficient.

**Second order**: Suppose $f$ is twice differentiable,
1. necessary condition: $\nabla f(x) = 0, \nabla^2 f \preceq 0$
2. sufficient condition: $\nabla f(x) = 0, \nabla^2 f \prec 0$

### Duality

**Lagrange Dual Function**: for a convex optimization problem
$$
\begin{aligned}
       \min \quad &f_0(x) \\
\text{s.t.} \quad &f_i(x) \leq 0, i = 1, ..., m \\
                  &h_i(x) = 0, i = 1, ..., p
\end{aligned}
$$
the Lagrange dual function is
$$
L(x, \lambda, \nu) = f_0(x) + \sum_{i=1}^m \lambda_i f_i(x) + \sum_{i=1}^p \nu_i h_i(x)
$$

**Weak Duality**: for any feasible $x$ and $\lambda, \nu$,
$$
g(\lambda, \nu) = \inf_x L(x, \lambda, \nu)
$$
and, if $\lambda \ge 0$, we have:
$$
g(\lambda, \nu) \leq p^*
$$

**Lagrange Dual Problem**: the dual problem is:
$$
\begin{aligned}
       \max \quad &g(\lambda, \nu) = \inf_x L(x, \lambda, \nu) \\
\text{s.t.} \quad &\lambda \succeq 0
\end{aligned}
$$
and duality gap is $p^* - d^* \ge 0$, where $p^*$ is the primal optimal value, and $d^*$ is the dual optimal value.

Duality feasible:
$$
\mathrm{dom} g = \{(\lambda, \nu) \mid \lambda \succeq 0, g(\lambda, \nu) > -\infty\}
$$

Examples:
- LP -> LP
- QP -> QP

**Connection to conjugate function**: if the constraint is linear,
$$
g(\lambda, \nu) = -f_0^*(-A^T \lambda - C^T \nu) - b^T \lambda - d^T \nu
$$
When conjugate function is known, we can directly solve the dual problem.

**Change of variables**:
$$
\min f_0 (Ax + b)
$$
can be changed to:
$$
\min f_0(y) \quad \text{s.t.} \quad y = Ax + b
$$

**Bound constrainted LP**:
$$
\begin{aligned}
        \min &c^T x \\
\text{s.t.} &A x = b, -1 \le x \le 1
\end{aligned}
$$

Implicit boundary constraint:
$$
\begin{aligned}
        \min &f_0(x) = \begin{cases}
        c^T x &\text{if } -1 \le x \le 1 \\
        +\infty &\text{otherwise}
    \end{cases} \\
\text{s.t.} &A x = b, -1 \le x \le 1
\end{aligned}
$$
the dual function:
$$
g(\nu) = -b^T \nu - \| A^T \nu + c \|_1
$$

**Cones**: How to deal with cone constraint?
$$
\begin{aligned}
       \min & f(x) \\
\text{s.t.} & c_i(x) \succeq_{K_i} 0\\
            & d_i(x) = 0
\end{aligned}
$$
the Lagrange dual function is:
$$
L(x, \lambda, \nu) = f(x) + \sum_i \langle \lambda_i, c_i(x)\rangle + \sum_i \nu_i^T d_i(x)
$$

### Optimal condition: Slater, KKT, LICQ

Why we need slater's condition: wish to find the optimal condition for a constrainted optimization problem, as if we are solving an unconstrainted problem.

**Slater's Condition**: if there exists a feasible $x \in \mathrm{relint} \mathcal D$ such that $f_i(x) < 0, h_i(x) = 0$, then we say slate's condition holds.

For convex problem, Slater's condition is sufficient for **strong duality**(zero duality gap).

**KKT condition**, also the **First order sufficient and necessary condition**:
For a convex optimization problem, if Slater's condition holds, then the KKT condition is necessary and sufficient for optimality:
1. stationary: $0 \in \partial f(x^*) + \sum \lambda_i \partial f_i(x^*) + \sum \nu_i \partial h_i(x^*)$
2. primal feasibility: $f_i(x^*) \le 0, h_i(x^*) = 0$
3. duality feasibility: $\lambda_i \ge 0$
4. complementary slackness: $\lambda_i f_i(x^*) = 0$

#### General KKT condition

**LICQ**(Linear Independence Constraint Qualification): for a point $x$, if the gradients of active constraints are linearly independent, then we say LICQ holds.

For a general problem, we need LICQ condition to ensure the KKT condition is necessary and sufficient.

> TODO: More on LICQ

- Analytic solution for some basic problems.

## Lecture 6: Gradient Descent

For a quadratic problem:
$$
\| x_k - x^* \|^2 \le \left(\frac{\lambda_{\max} - \lambda_{\min}}{\lambda_{\max} + \lambda_{\min}}\right) \|x_0 - x^*\|^2
$$

Therefore, we consider the Lipschitz constant:
$$
\| \nabla f(x) - \nabla f(y) \| \le L \|x - y\|
$$
the Lipschitz constant also gives us:
$$
\begin{aligned}
    f(y) &\le f(x) + \nabla f(x)^T (y - x) + \frac{L}{2} \|y - x\|^2 \\
    f(x) &\ge f(y) + \nabla f(y)^T (x - y) + \frac{L}{2} \|x - y\|^2
\end{aligned}
$$
To ensure convergence, we must set $\alpha_k < \frac{1}{L}$.

Moreover, if $f$ is twice differentiable, then $f$ is $m$-strong convex, and $L$-continuously differentiable, if:
$$
m I \preceq \nabla^2 f(x) \preceq L I
$$

The convergence rate of GD is given by:
$$
f(x_k) - f(x^*) \le \frac{L \|x_0 - x^*\|^2}{2k}
$$

Convergence rate under strong convexity:
$$
f(x^k) - f^* \le c^k \frac{L}{2} \| x^0 - x^* \|_2^2
$$
where $c = L / m < 1$.

### More on convex functions

For a differentiable function, tfae:
1. $\nabla f$ is Lipschitz continuous with constant $L$,
2. $g(x) := L/2 \|x\|_2^2 - f(x)$ is convex,
3. $\nabla f$ has: $(\nabla f(x) - \nabla f(y))^T (x - y) \ge L \|x - y\|^2$, for all $x, y$

### Line searching

**Armijo rule**, checking for sufficient decrease:
$$
f(x_k + \alpha_k d_k) \le f(x_k) + \alpha_k c_1 \nabla f(x_k)^T d_k
$$

**Wolfe conditions**, checking for curvature:
$$
\begin{aligned}
    f(x_k + \alpha_k d_k) &\le f(x_k) + \alpha_k c_1 \nabla f(x_k)^T d_k \\
    \nabla f(x_k + \alpha_k d_k)^T d_k &\ge c_2 \nabla f(x_k)^T d_k
\end{aligned}
$$
we need $0 < c_1 < c_2 < 1$.

**Goldstein conditions**, a compromise between Armijo and Wolfe:
$$
\begin{aligned}
    f(x_k + \alpha_k d_k) &\le f(x_k) + \alpha_k c_1 \nabla f(x_k)^T d_k \\
    f(x_k + \alpha_k d_k) &\ge f(x_k) + \alpha_k (1-c) \nabla f(x_k)^T d_k
\end{aligned}
$$
we need $0 < c < 1/2$

### Non smooth problems

Convergence rate for gd:
$$
\min _{k = 0, 1, ..., T} \| \nabla f (x_k) \|^2 \le \frac{2 L (f(x_0) - f^*)}{T}
$$

TODO: Check for the convergency proof.

## Lecture 7: Subgradients

### Definition of Subgradients & Subdifferential

**Subgradient**:
$$
\partial f(x) = \{ g \mid f(y) \ge f(x) + g^T (y - x), \forall y \}
$$

For a convex function, $x \in \mathrm{int~dom} f$, the subgradient is always nonempty.

### Computing Subgradients & Subdifferential

differentiable function: equivalent to strong derivative.

Non-negative weighted sum.

Composition with affine transform.

Pointwise maximum:
$$
f(x) = \max \{ f_1(x), f_2(x) \}
\implies
\partial f(x) = \mathbf{conv} \partial f_1(x) \cap \partial f_2(x)
$$

Examples:
- Piecewise linear function 
- L1 norm.

### Optimal condition

**First order condition**(unconstrainted): $x^*$ is local minimum, if and only if,
$$
0 \in \partial f
$$

**First order condition**(constrainted): $x^*$ is local minimum, if and only if,
$$
0 \in \partial f(x^*) + \sum \lambda_i \partial f_i(x^*)
$$
where $\lambda_i \ge 0$ is the optimal dual variable.

### Subgradient methods

$$
x^{k+1}\larr x^k - \alpha_k g^k
$$
we have many choices for $\alpha_k$:
1. constant step size: does not guarantee convergency
2. constant $\|x^{k+1} - x^k\|$: does not guarantee convergency
3. diminishing step size: ok, a typical choice is $\alpha_k = 1/k$
4. line search: ok, but expensive.

## Lecture 8: projected gradient descent, conditional gradient descent

Now consider constrainted problems.

**Optimal condition**:
$$
\langle \nabla f(x^*), x^* - y\rangle = 0,\quad \forall y in C
$$

**Projected Gradient Descent**:
$$
x_{k+1} = \Pi_C (x_k - \alpha_k \nabla f(x_k))
$$

**Non expansion property of projection**: if $C$ is convex,
$$
\| \Pi_C(x) - \Pi_C(y) \| \le \|x - y\|
$$

The convergency result under strong convex assumption:
$$
\|x_k - x^*\|^2 \leq \left(1 - \frac{m}{L}\right)^k \|x_0 - x^*\|^2
$$
if we choose $\alpha_k = 1/L$

### Conditional Gradient Descent

also called Frank-Wolfe algorithm.

Why we need conditional gradient descent: Projection is expensive

**Conditional Gradient Descent**:
$$
\begin{aligned}
    x_k &= \arg\min_{x \in C} \langle \nabla f(x_{k-1}), x \rangle, \\
    y_k &= x_{k-1} + \alpha_k (x_k - x_{k-1})
\end{aligned}
$$
might be easier, if the linear programming is easy in $C$

Choices for $\alpha_k$:
- diminishing step size: $\alpha_k = 2/(k+1)$
- or via exact line search

## Lecture 9: Prox Mapping

### Definition of Proximal Mapping

**Proximal Mapping**:
$$
\text{prox}_{\alpha f}(x) = \arg\min_y \left( f(y) + \frac{1}{2} \|y - x\|^2 \right)
$$

**Relation to subgradient**:
$$
u = \text{prox}_{f}(x) \iff x - u \in \partial f(u)
$$

**Relation to projection**:
$$
\text{prox}_{I_C}(x) = \Pi_C(x)
$$

### Moreau decomposition

$$
x = \mathrm{prox}_{h}(x) + \mathrm{prox}_{h^*}(x)
$$
Generally:
$$
x = \mathrm{prox}_{\lambda h}(x) + \lambda\mathrm{prox}_{\lambda^{-1}h^*}(x)
$$

we can use Moreau decomposition to compute many proximal mappings.

**Norm Ball**:
The conjugate of $\| \cdot \|$ is the indicator function of the unit ball under the dual norm.

### Proximal Gradient Descent

**Proximal Gradient Descent**:
$$
x_{k+1} = \text{prox}_{\alpha h}(x_k - \alpha \nabla f(x_k))
$$

due to the optimal condition, we have:
$$
x = \text{prox}_{\alpha h}(x - \alpha \nabla f(x)) \iff -\nabla f(x) \in \partial h(x)
$$

#### Convergency

Define the gradient mapping:
$$
G_t (x) = \frac{1}{t} (x - \text{prox}_{t h}(x - t \nabla f(x)))
$$

The proximal gradient descent can be written as:
$$
x_{k+1} = x_k - t G_{\alpha} (x_k)
$$

Convergency for constant step size $\alpha < 1/L$:
$$
f(x_k) - f(x^*) \le \frac{2 L}{k}\|x_0 - x^*\|^2
$$

Convergency for backtracking, similar.
$$
f(x_k) - f(x^*) \le \frac{1}{2k \min\{ \hat{t}, \beta/L \}} \|x_0 - x^*\|^2
$$

### Moreau Envelope

**Moreau Envelope**:
$$
h_\alpha (x) = \min_y h(y) + \frac{1}{2\alpha} \|x - y\|^2
$$

Moreau envelop can be viewed as an approximation to non smooth $h$.

For any proper, closed, convex function, the Moreau envelop $h_\alpha$ is differentiable, and the gradient is given by:
$$
\nabla h_\alpha (x) = \frac{1}{\alpha} (x - \text{prox}_{\alpha h}(x))
$$






















