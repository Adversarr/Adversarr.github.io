---
title: 线性赋范空间、Banach空间
date: 2023-02-22T19:02:05Z
lastmod: 2023-08-18T16:14:37Z
---



## 线性赋范空间

之前我们的讨论只涉及了“距离”，其只包含拓扑结构，我们还需要考虑其代数结构。

### 线性空间

**线性空间、线性同构、线性子空间、线性流形、线性相关、线性基、维数、线性包、线性和和直和**

### 线性空间上的距离

结合距离和线性运算，我们要求这个距离具有如下性质：

1. 平移不变性：$\rho (x, y) = \rho (x+ z, y+z) \forall z$
2. 数乘连续性：$\rho\left(x_{n},y\right)\to0\Rightarrow\rho\left(\alpha x_{n,}\alpha x\right)\to0,\alpha_{n}\to\alpha\Rightarrow\rho\left(\alpha_{n}x,\alpha x\right)\to0$

从而可以将其公理化为某一函数 $p$ 的条件，因为 $\rho (x, y) = \rho (x-y, 0)=p(x - y)$

**准范数（准模）、F*空间、F 空间（Frechet）**

* 定义？（四个条件）
* 例如：

  * $C(M)$，按 $\max |x- y|$ ​是 $F$ 空间
  * Euclid 空间是 F 空间
  * 数列，按照 $\|x\|=\sum_{n=1}^{\infty}\frac{1}{2^{n}}\frac{|x_{n}|}{1+\left|x_{n}\right|}$ 是 F 空间

### 范数、Banach 空间

**范数、线性赋范空间（B*空间）、Banach 空间**

* 定义？（三个性质）
* 例如：

  * $L^p(1\le p < \infty)$ 是 B 空间，三角形不等式由 Minkowski 不等式给出
  * $L^\infty$ 是 B 空间
  * $C^k(M)$ 按照 $\| u \| = \max_{|\alpha |< k, x \in \bar \Omega}| \partial^\alpha u|$ 是 B 空间
  * $C^k(M)$ 按照 $\|u\|_{m,p}=\left(\sum_{\left|\alpha\right|\le m}^{}\int_{\Omega}^{}\left|\partial^{\alpha}u\left(x\right)\right|^{p}dx\right)^{\frac{1}{p}}$ 是 B*空间，其完备化记作 $H^{m, p}$，是 B 空间
  * 当 $p=2$ 时，$H^{m, 2}$ 简单地记为 $H^m(\Omega)$

### 线性赋范空间中的模等价

**（范数的）强、等价**

* 定义？
* 为了 $\|\cdot\|_2$ 比 $\|\cdot\|_1$ 强，当且仅当存在常数 $C$，使得 $\|\cdot\|_1 \le C\|\cdot\|_2$

有穷维线性空间：任意两个有相同维数的线性空间等价，我们想知道，其拓扑之间有什么联系？（思路：写出每一个点的坐标，然后将原先的范数用 $K^n$ 中的 L2 范数建立联系）

* 有穷维线性空间上的范数之间时相互等价的
* 有穷维 B*空间一定是 B 空间

**次线性泛函**

* 定义？（次可加性、正齐次性）
* Theorem：设有穷维 B*空间上的次线性泛函 $P$，若 $P(x) \ge 0, P(x) = 0 \iff x = 0$，那么存在正常数 $c_1, c_2$ 使得 $c_1 \| x\| \le P(x) \le c_2\|x\|$

### 最佳逼近问题

逼近论的一个基本问题是：给定一组函数 $\phi_1 ... \phi_n$，和函数 $f$，尝试用 $\phi$ 的线性组合去逼近 $f$，问是否有最佳逼近存在？

换成 B* 空间：给定 B*空间，和其中的有穷个向量 $e_i$，对于给定向量，求一组系数，使得按照空间中的范数而言误差最小。

首先，最小值是存在的，定义：

$$
F(a)=\left\|x-\sum_{i=1}^{n}a_{i}e_{i}\right\|
$$

$F$ 是连续函数，且 $F(a) > \| \sum a_i e_i \| - \| x\|\ge c_1 |a| - \| x\|$

> ???

* Theorem：这样的最佳逼近系数是存在的
* 问题：唯一性？

**严格凸**

* 定义：$\forall x\ne y,\|x\|=\|y\|=1\implies\|\alpha x+\beta y\|<1$
* Theorem：严格凸的 B*空间中的最佳逼近系数是存在且唯一的；

Summary：有穷个向量的情况下，

* 普通B*空间，最佳逼近存在；
* 严格凸的B*空间，最佳逼近存在，并且唯一
* 例如：

  * 习题 1.4.7：用不超过$n$次的多项式逼近$C[ a, b]$上的函数，存在唯一的最佳逼近元

### 有穷维 B*空间的刻画

1. 为了 B*空间是有穷维的，当且仅当其单位球面是列紧的
2. 定义：有界
3. 为了 B*空间是有穷维的，当且仅当其中的任意有界集是列紧的

Riesz 引理：

* 如果 $X_0$ 是 $X$ 的一个真闭子空间，那么对于 $\forall 0 < \varepsilon < 1, \exists y \in X, \| y \| = 1 , \| y - x\| \ge 1-\varepsilon$

## 凸集和不动点

### 定义和基本性质

**凸集、凸包、凸组合**

1. 定义？
2. 凸集的任意并集也是凸集
3. 凸包：集合中元素的任意凸组合的全体

**Minkowski泛函**

* 定义：$P(x) = \inf \{ \lambda > 0| x/\lambda \in C , x \in X\}$（其中$C \subset X$是凸集）
* 性质：正齐次性、次可加性、$P(x) \in [0, \infty], P(\theta) = 0$
* 问：何时$P(x)$成为函数，即何时$P < \infty$？

**（实线性空间上、凸集的）吸收性、对称性、（复线性空间）均衡**

* 定义：吸收是指$P$是函数，即$\forall x, \exists \lambda x/ \lambda \in C$；对称是指，$x \in C \iff -x \in C$​
* Prop：吸收$\iff P$是函数、对称$\Rightarrow P$是齐次的；
* 均衡的定义：$x \in C \Rightarrow \alpha x \in C, \forall |\alpha | = 1$​
* Prop：复线性空间上的一个均衡吸收凸集$C$决定了一个半模（Minkowski泛函）

对于线性赋范空间中的凸集，有更强的结果：

* 设$X$是一个B*空间，$C$是一个含有$\theta$点的闭凸集，$P$是下半连续的，并且

  $$
  C=\left\lbrace x\in X{|}P\left(x\right)\le1\right\rbrace
  $$

  如果$C$还是有界的，那么$P= 0 \iff x = \theta$  

  如果$C$还以$\theta$为内点，那么$C$是吸收的、并且$P$一致连续
* 若$C$ 是$R^n$中的一个紧凸子集，那么存在一个正整数$m\le n$，使得$C$同胚于$R^m$中的单位球

‍

‍
