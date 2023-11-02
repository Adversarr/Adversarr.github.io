## B-Spline Curve

### Definition

Use repleated linear interpolation.
$$
N_i^1(t) = \begin{cases}
	1 & i \le t < i + 1\\
	0& \text{otherwise}
\end{cases}
$$
and,
$$
N_i^k(t) = \frac{t-i}{(i+k-1) -i} N_i^{k-1} (t) + \frac{(i+k) - t}{(i+k)- (i+1)}N_{i+1}^{k-1}(t)
$$
Generalize: replace $i$ with $t_i$

Then, the curve is defined: Given $n+1$ control points $\vec p_i$, Knot vector $T = (t_0, …, t_{n+k})$:
$$
\vec r(t) = \sum_{i = 0}^n \vec p_i N_{i}^k (t)
$$

- $\vec p_i$ is **de Boor points**
- Curve is defined on interval $[t_{k-1}, t_{n+1}]$

### Properties

1. Local support: For given $i, k$, support is $(t_i, t_{i+k})$

2. Non-negtivity

3. Unitary: $\sum N_i (t) = 1$ inside the domain of definition.

   ⇒ Convex

4. For $t_i \le t_j \le t_{i+k}$, $N$ is $C^{k-2}$ at $t_j$

5. Repeat at $t_i$ for $j$ times, the continuity goes down $j$ order.

### Relation to Bezier

$$
T=(0, 0, ..., 0, 1, 1, ..., 1)
$$

$k$-times on two ending ⇒ Bernstein polynomial.

## B-Spline

### Definition

Given special knot vector: (Repaat at ends)
$$
T = (t_0= t_1=\cdots= t_{k-1}, t_k, t_1, ..., t_n, t_{n+1} = \cdots = t_{n+k})
$$

- de Boor polygon: $d_0, …, d_n$
- also defined on $[t_{k-1}, t_{n+1}]$, but endings are repeated.

### Properties

1. Endpoint interpolation
2. Tangent direction at $d_0$
3. $n-k+2$ polynomial curve segments of degree $k-1$

Multiple inner knots ⇒ Reduction of continuity of $x(t)$

- $l$-times ⇒ $C^{k-l-1}$ cont.

Local impact, $d_i$ ⇒ impact $[t_i, t_{i+k}]$

### Evaluation: de Boor algorithm

1. evaluate B-Spline Functions
2. (or) de Boor algorithm

```python
def deBoor(d, T, t):
  r = t[r] < t < t[r+1]
  for i in range(r-k+1, r+1):
    d[0][i] = d[i]
  for j in 1, ..., k-1:
    for i = r-k+1, ..., r:
      d[j][i] = (1 - alpha) d[j-1][i-1] + alpha d[j-1][i]
	return d[k-1][r]
```

### Interpolation using b-spline

Input:

- control points (not de boor points) $k_0,...,k_n$
- knot vector $s_0, … s_n$

Output: curve interpolates $k_i$ at $s_i$

Key: find deboor points $d_0, …, d_{n+k-2}$

- Domain: $t_{k-1} \to t_{N+1}$ has $N-k+3$ “points”
- therefore $N-k+3 = n+1 \implies N = n+k-2$

Formulation:

1. Interpolation: $x(s_i) = k_i$
2. Ending condition

## Relationships

### Bezier → B-Spline

Input:

- control points of bezier curve
- knot vector
- $b_0, …, b_{3n}$, Bezier points interpolating the curve.
- ending conditions

Output:

- curve in b-spline form

Key:

- deboor points, and knot for b-spline

Algorithm:
$$
\begin{aligned}
d_0 &= b_0\quad d_1 = b_1 \\
d_i &= b_{3i-4} + \Delta_{i-1}/ \Delta_{i-2} (b_{3i-4}-b_{3i-5})\\
d_{n+1} &= b_{3n - 1}\quad d_{n} = b_{3n}
\end{aligned}
$$


