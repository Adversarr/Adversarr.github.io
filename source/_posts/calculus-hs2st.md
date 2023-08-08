---
title: ' Calculus'
updated: '2023-08-08'
excerpt: ''
permalink: /post/calculus-hs2st.html
comments: true
toc: true
---

# 00. Calculus

## Gauss-Green Theorem

### Divergence Theorem

Suppose $u \in C^1$,

$$
\int_{U}^{}u_{x_{i}}\mathrm{d}x=\int_{\partial U}^{}u\nu^{i}\mathrm{d}S
$$

where $\nu$ is the normal vector of $\partial U$. Therefore, we have**​ (Divergence Theorem)**

$$
\int_U \mathrm{div}\mathbf u \mathrm dx = \int_{\partial U} \mathbf u \cdot \nu \mathrm dS
$$

for each vector field.

### Integration by parts

Let $u, v\in C^1$, then

$$
\int_{U}^{}u_{x_i} vdx = - \int_U u v_{x_i} dx + \int_{\partial U} u v \nu ^i dS
$$

> Apply Divergence Theorem.

### Green's Formulas

Let $u, v\in C^2$, then

$$
\begin{cases}\int_{U}^{_{}}\Delta udx=\int_{\partial U}^{}\frac{\partial u}{\partial\nu}dS\\ \int_{U}^{}Dv\cdot Du\ \mathrm{d}x=-\int_{U}^{}u\Delta vdx+\int_{\partial U}^{}\frac{\partial v}{\partial\nu}udS\\ \int_{U}^{}u\Delta v-v\Delta udx=\int_{\partial U}^{}u\cdot\frac{\partial v}{\partial\nu}-v\cdot\frac{\partial u}{\partial\nu}dS\end{cases}
$$

‍
