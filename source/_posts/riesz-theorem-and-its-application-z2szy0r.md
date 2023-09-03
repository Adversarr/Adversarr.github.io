---
title: Riesz定理及其应用
date: '2023-08-20 10:10:49'
updated: '2023-09-03 14:36:06'
comments: true
toc: true
---


# Riesz定理及其应用

## Riesz定理

对于Hilbert 空间 $X$，定义线性算子：

$$
f_{y}:x\rightarrowtail\left(x,y\right)
$$

那么$f_y \in X^*$，并且是有界的（Cauchy Schwartz不等式）。这个结论反过来也是对的：

**Theorem（Riesz）**：设$f$是Hilbert空间$X$上的一个连续线性泛函，则必存在唯一的$y_f \in X$使得

$$
f(x) = (x, y_f)
$$

> 1. 几何意义：Hilbert空间中的连续线性泛函的等值面都是相互平行的超平面
> 2. $\|f\|=\|y_f\|$​

**Theorem: ​**设$X$是Hilbert空间，$a(x, y)$是X上的共轭双线性函数，并且$\exists M > 0$使得

$$
|a(x, y) | \le M \| x \| \| y\|
$$

则存在唯一的$A \in L(X)$使得

$$
a(x, y) = (x, Ay)
$$

并且

$$
\|A\|=\sup_{(x,y)\in X\times X,x,y\ne\theta}\frac{|a|}{\|x\|\|y\|}
$$

## 应用

### Laplace 方程的Dirichlet边值问题的弱解

对于Laplace方程的D边值问题：

$$
\begin{cases}-\Delta u=f\\ u\left|_{\partial\Omega}\right.=0\end{cases}
$$

弱解是指：

$$
-\int_{\Omega}\nabla u\cdot\nabla vdx=\int_{\Omega}^{}fvdx\quad \forall v\in H_0^1(\Omega)
$$

**Theorem: ​**对于任意的L2可积函数，该问题的弱解存在且唯一。

* Idea：定义$(u, v) = \int_\Omega \nabla u \cdot \nabla v dx$ 为Hilbert空间上的内积

### 变分不等式

**Theorem：**设$C$是$H_0^1$中的闭凸子集，若$f\in L^2(\Omega)$，则下面的不等式存在唯一解：

$$
\int_{\Omega}^{}\nabla u_0^{\ast}\cdot\nabla\left(v-u_0^{\ast}\right)\mathrm{d}x\ge\int_{\Omega}f\cdot\left(v-u_0^{\ast}\right)\mathrm{d}x
$$

‍
