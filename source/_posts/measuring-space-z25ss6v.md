---
title: 度量空间
date: 2023-02-22T19:02:05Z
lastmod: 2023-08-17T10:27:20Z
---



## 压缩映像原理

**距离**

* 定义：**三个条件**
* 例：$C([a, b])$，按照 $\max |x - y|$
* 目的：引入“收敛”

**收敛、闭集、基本列、完备空间**

* $R^n,||_2$ 是完备的；
* $C([a, b])$，按照 $\max |x - y|$ 是完备的；

**连续映射、压缩映射、不动点**

* 定义：$T:(X,\rho)\to\left(X,\rho\right)\quad\rho\left(Tx,Ty\right)\le\alpha\rho\left(x,y\right),0<\alpha<1$

**Banach 不动点定理、压缩映射原理**

* 完备距离空间到自身的压缩映射的不动点存在且唯一
* 应用：隐函数存在定理

> ODE 的初值问题
>
> $$
> \begin{cases}\dot{x}=F\left(t,x\right)\\ x\left(0\right)=\xi\end{cases}
> $$
>
> 等价于求解积分方程问题：
>
> $$
> x(t)=\xi+\int_0^{t}F\left(\tau,x\left(\tau\right)\right)\mathrm{d}\tau
> $$
>
> 定义映射：
>
> $$
> (Tx)(t)=\xi+\int_0^{t}F\left(\tau,x\left(\tau\right)\right)\mathrm{d}\tau
> $$
>
> 考虑如何使得 $T$ 为压缩映射？（距离定义为 $\max|x-y|$）
>
> 假设 $F$ 对 $x$ 关于 $t$ 一致满足局部 L 条件即可。

Theorem：假设函数 $F$ 在 $[-h, h]\times [\xi - \delta, \xi + \delta]$ 上有定义、连续、满足条件

$$
|F(t, x_1) - F(t, x_2)| \le L|x_1 - x_2|
$$

则当 $h<\min\left\lbrace\frac{\delta}{M},\frac{1}{L}\right\rbrace$ 时，初值问题在 $[-h, h]$ 上存在唯一解。

## 完备化

一般而言，距离空间是不完备的。例如全体有理数组成的空间，或 $C[a,b]$ 对 $L_1$ 范数。

**等距同构、等距同构映射、嵌入**

* 定义？
* 目的：存在等距同构的空间的性质都是一样的，不加以区分

**稠密子集、完备化空间**

* Theorem：每个空间都有其完备化空间
* 例如：$P[a,b]$ 在 $C[a, b]$ 内稠密，以 $C[a,b]$ 为其完备化空间

## 列紧集

> **Compactness** is a [topological](https://brilliant.org/wiki/topology/ "topological") property that is fundamental in [real analysis](https://brilliant.org/wiki/real-analysis/ "real analysis"), [algebraic geometry](https://brilliant.org/wiki/algebraic-geometry/ "algebraic geometry"), and many other mathematical fields. In ��**R**n (with the standard topology), the compact sets are precisely the sets which are [closed](https://brilliant.org/wiki/closed-sets/ "closed") and bounded. Compactness can be thought of a generalization of these properties to more abstract topological spaces.
>
> Compact sets are well-behaved with respect to [continuous functions](https://brilliant.org/wiki/continuous-functions/ "continuous functions"); in particular, the continuous image of a compact function is compact, so a continuous function from a compact set to �**R** must have a finite minimum and maximum, and must attain each of these at some point in the domain (the [extreme value theorem](https://brilliant.org/wiki/extreme-value-theorem/ "extreme value theorem")). This is quite useful in applications to [optimization](https://brilliant.org/wiki/optimization-problems/ "optimization") and other related areas.

**有界：**

* 在 Rn 中，有界无穷集中可以找到收敛子列
* 一般的距离空间不满足

**列紧、自列紧、列紧空间**

* 定义：任意点列都有一个收敛子列；进一步，收敛到原本空间中的点；进一步，自身是列紧的
* 例如：Rn 中的有界集合是列紧的、有界闭集是自列紧的
* 列紧空间的任意的子集都是列紧的、任意闭子集都是自列紧的；（反证法）
* 列紧空间是完备的

$\epsilon$** **网、有穷** **** **网、完全有界、Hausdorff 定理**

* 定义？
* Hausdorff：
  为了距离空间中的集合是列紧的，必须要求其是完全有界的；
  为了完备距离空间中的集合是列紧的，必须且仅须其是完全有界的；

**可分**

* 定义？
* Theorem：完全有界的距离空间是可分的.

**紧集**

* **Z** is compact if every open cover has a finite subcover.
* Theorem：距离空间中的紧集，当且仅当其是自列紧的

​![image](http://127.0.0.1:6806/assets/image-20230816114201-eupnfg5.png)​

> [怎么通俗的理解有界闭集，紧集，列紧集？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/58904993)

考察紧的距离空间 $M$，和其上的连续映射全体 $C(M)$，定义：

$$
d(u, v) = \max_{x\in M} |u - v|
$$

* $C, d$ 是距离空间、完备
* 一致有界、等度连续、Arzela-Ascoli：为了 $F \subset C(M)$ 列紧，当且仅当，$F$ 一致有界且等度连续.

  * 刻画了连续函数空间上的列紧集

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
