---
title: Hahn-Banach定理
date: '2023-08-22 09:12:19'
updated: '2023-08-23 10:29:44'
permalink: /post/hahnbanach-theorem-1gjror.html
comments: true
toc: true
---


 给定无穷维的线性赋范空间，问：

* 是否存在不恒等于0的连续线性泛函？
* 是否这样的连续线性泛函是足够多的？（能够用于区分每一个元素）

## 线性泛函的延拓定理

我们考虑均衡吸收的凸集，由它可以决定一个空间上的半模$p$，我们试图从$p$来产生$X$上的非零连续线性泛函：

$$
X_0 = \{ \lambda x_0 : \lambda \in K\}, f_0(\lambda x_0) = \lambda p(x_0)
$$

那么，$f_0$是$X_0$上的连续线性泛函，并且满足有界性条件

$$
| f(x_0) | \le | \lambda p(x_0)| = p(\lambda x_0)
$$

**Theorem（实数域上的Hahn-Banach定理）**设$X$是实线性空间，$p$是定义在$X$上的线性泛函，$X_0$是$X$的实线性子空间，$f_0$是$X_0$上的实线性泛函，并满足$f_0 < p\forall x \in X_0$，那么$X$上一定有一个实线性泛函$f$满足：

1. 受$p$控制：$f(x) \le p(x) \forall x\in X$​
2. 延拓条件：$f|_{X_0} = f_0$

**Theorem（复数域上的Hahn-Banach定理）**设$X$是复线性空间，$p$是定义在$X$上的半模，$X_0$是$X$的线性子空间，$f_0$是$X_0$上的线性泛函，并满足$|f_0| < p\forall x \in X_0$，那么$X$上一定有一个实线性泛函$f$满足：

1. 受$p$控制：$|f(x)| \le p(x) \forall x\in X$
2. 延拓条件：$f|_{X_0} = f_0$

从这两个定理可以得到：

* 为了复线性空间上至少有一个非零的线性泛函，只要$X$中有一个均衡、吸收的凸集

在B*空间上，可以更进一步：

**Theorem（Hahn-Banach）**设$X$是B*空间，$X_0$是$X$的线性子空间，$f$是$X_0$上的有界线性泛函，则在$X$上有$f$的保范延拓。

推论：

1. 每个B*空间都有足够多的连续线性泛函；
2. 对于B*空间，对于一切非零元$x$一定存在函数$f\in X ^ *$，使得$f(x_0) = \| x _ 0 \|$ 且 $\| f \| = 1$​

回顾Hilbert空间，对于任意的连续线性泛函，有Riesz表示定理成立。现在我们考虑是否可能可以扩展到B*空间上：

**Theorem**：设$X$是B*空间，$M$是$X$的线性子空间，若$x_0 \in X$，且$d = \rho (x_0 ,M ) >0$，则存在$f \in X ^ *$适合：

1. $f(x) = 0 \forall x \in M$​
2. $f(x_0) = d$​
3. $\| f\| = 1$​

推论为：设$M$是B*空间的一个子集，设$x_0$是$X$中的任一个非零元素，那么$x_0 \in \overline{spanM}$当且仅当$\forall f \in X^ * ,f(x) = 0(\forall x\in M)$蕴含了$f(x_0) = 0$

## 几何形式 —— 凸集分离定理

在$R^n$中，有凸集分离定理显然成立。

对应于$n-1$维超平面的概念：

### 极大线性子空间、极大线性流形、超平面

* 定义：以$M$为真子集的线性子空间只有$X$​
* 充要条件：$M$是线性真子空间，并且对于任意的$x_0\in X \backslash M$有$X=\{\lambda x_0\|\lambda\in R^1\}\oplus M$​

Note：超平面是平面上一般直线的推广：直线可以由一个线性函数$a x + by = c$表示，超平面可以由线性泛函$f(x) = r$来表示。

**Theorem**：为了$L$是线性空间上的一个闭超平面，必须其仅须存在非零的线性泛函$f$和$r \in R$，使得$L = H_f^r = \{ f(x) = r \}$.

### 超平面分离定理

* 超平面分离的定义？$f(E) \le r \le f(F)$
* 思路：先考虑可以分离凸集和空间中的一固定点$x_0$  

  * 若$E$是$X$中以$\theta$为内点的真凸子集，那么其Minkowski泛函$p(x)$是一个非零的连续次线性泛函
  * 空间中不在凸集内的点都满足$p(x) \ge 1$，因此在一维线性空间$\{ \lambda x_0 \}$上定义连续线性泛函$f_0 (\lambda x_0 ) = \lambda p(x_0)$，根据Theorem（Hahn-Banach）可知，存在$X$上的连续线性泛函，使得$f(x_0) = f_0(x_0) = p(x_0) \ge 1, f(x) \le p(x)$​

**Theorem（Hahn-Banach定理-几何形式）**：设$E$是实B*空间上以$\theta$为内点的真凸子集，设$x_0 \bar \in E$那么存在超平面$H _ f ^r$分离$x_0$和$E$​

**Theorem（凸集分离定理）**：设$E_1, E_2$为B*空间中互不相交的非空凸集，其中 $E_1$ 有内点，则存在超平面$H_f ^ s$分离$E_1, E_2$.

该定理有一系列推论：

1. Ascoli 定理：设$E$是实B*空间中的一个闭凸集，$\forall x \in X \backslash E$存在$f$和$a$适合$f(x) < a < f(x_0) \quad \forall x \in E$​
2. Mazur 定理：设$E$是B*空间$X$上的一个有内点的闭凸集，$F$是$X$上的一个线性流形，设$\r{E}\cap F=\emptyset$，那么存在一个包含$F$ 的闭超平面，使得$E$在$L$的一侧

## 应用

### 抽象可微函数的中值定理

微商

* 定义：$\lim_{\delta\to0}\left(\frac{f\left(t+\delta\right)-f\left(t\right)}{\delta}\right)$

**Theorem：**抽象函数$f$若在$(a, b)$内可微，那么对于任意的$t_1, t_2 \in (a, b)$存在$0 < \theta < 1$使得中值定理成立：

$$
\| f(t_2) - f(t_1) \|\le \| f'(\theta t_2 + (1-\theta) t_1 )\| | t_2 - t_1|
$$

### 凸优化问题的Lagrange乘子

**Theorem（Kuhn-Tuncker）**：设$X$是一个线性空间，$C$是$X$的一个凸子集，$f, g_1, g_2, ..., g_n$是$C$上的凸泛函，若$x_0$是问题：

$$
\min f(x)\quad s.t.\ g_i (x) \le 0
$$

的解，那么一定存在非负实数$\lambda_1, ..., \lambda _n$：

$$
f(x_0)=\min\left\lbrace f\left(x\right)+\sum_{i=1}^{n}\lambda_{i}g_{i}\left(x\right), x\in C\right\rbrace\quad \lambda_i g_i(x_0) = 0
$$

###
