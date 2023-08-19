---
title: 度量空间、压缩映射、列紧集
date: 2023-08-18T10:47:53Z
lastmod: 2023-08-18T10:48:27Z
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

​![image](assets/image-20230816114201-eupnfg5.png)​

> [怎么通俗的理解有界闭集，紧集，列紧集？ - 知乎 (zhihu.com)](https://www.zhihu.com/question/58904993)

考察紧的距离空间 $M$，和其上的连续映射全体 $C(M)$，定义：

$$
d(u, v) = \max_{x\in M} |u - v|
$$

* $C, d$ 是距离空间、完备
* 一致有界、等度连续、Arzela-Ascoli：为了 $F \subset C(M)$ 列紧，当且仅当，$F$ 一致有界且等度连续.

  * 刻画了连续函数空间上的列紧集
