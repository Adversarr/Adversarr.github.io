---
title: 内积空间
date: 2023-08-17T10:46:04Z
lastmod: 2023-08-17T15:52:09Z
---



## 内积空间

### 基本定义和性质

#### 共轭双线性函数、内积、内积空间

* 定义：共轭对称、正定的共轭双线性函数
* 例：

  * $l^2$ 空间 $L^2$ 空间
  * $C^k(\bar \Omega)$ 中，按照 $(u,v)=\sum_{\left|\alpha\right|\le k}^{}\int_{\Omega}^{}\partial^{\alpha}u\overline{\partial^{\alpha}v}dx$ 是内积空间
* Cauchy-Schwarz 不等式：$|(x, y) | \le \| x \| \|y\|$，等号成立当且仅当 $x, y$ 线性相关

内积空间按照 $\|x\|=(x, x)$ 定义范数，构成 B*空间：

* 内积 $(\cdot, \cdot)$ 是关于 $\|\cdot \|$ 的连续函数
* 内积空间是严格凸的 B*空间

反过来，一个 $\|\cdot \|$ 也有可能构成一个内积空间：

* 如果 $\|\cdot \|$ 满足平行四边形等式：

  $$
  \|x-y\|^2+\|x+y\|^2=2\left(\|x\|+\|y\|\right)
  $$

#### Hilbert 空间

* 完备的内积空间

> 在 PDE 中，常用的一个 Hilbert 空间是 $H^m_0$，
>
> 设 $C_0^m$ 是有界开区域上一切 $m$ 次连续可微、在边界的某个邻域内为 0 的函数集合，那么：
>
> $$
> \forall u\in C_{0^{}}^{m},\sum_{\left|\alpha\right|<m}^{}\int_{\Omega}^{}\left|\partial^{\alpha}u\left(x\right)\right|^2dx\le C\sum_{\left|\alpha\right|=m}^{}\int_\Omega\left|\partial^{\alpha}u(x)\right|^2dx
> $$
>
> ‍
>
> 从而，在 $C^m_0$ 上引入范数：
>
> $$
> \|u\|_{m}=\left(\sum_{\alpha=m}^{}\int_{\Omega}^{}\left|\partial^{\alpha}u\left(x\right)\right|^2dx\right)^{\frac12}
> $$
>
> 完备化后得到 $H^m_0$，它是 $H^m$ 的一个闭子空间

### 正交和正交基

#### 正交、正交补

* 定义？
* 性质：

  * 勾股定理
  * 若 $x\perp y_n$，且 $y_n \to y$，那么 $x \perp y$​
  * 若 $x \perp M$ 那么 $x \perp span(M)$​
  * $M^\perp$ 是一个闭线性子空间

#### 正交集、正交规范集、完备正交集

* 定义？
* 非平凡的内积空间一定有完备正交集

> Zorn 引理

有正交规范集，可以考虑：

#### 基、Fourier 系数

* Bessel 不等式：$\sum_{\alpha \in A} |(x, e_\alpha)|^2\le \| x \| ^ 2$
* 假设 $X$ 是 Hilbert 空间，并且 $e_\alpha$ 是正交规范集，那么对于任意的 $x\in X$，都有 $\sum _{\alpha \in A }(x, e_\alpha) e_\alpha \in X$，并且

  $$
  \|x-\sum_{\alpha\in A}^{}\left(x,e_{\alpha}\right)e_{\alpha}\|^2=\|x\|^2-\sum_{\alpha\in A}^{}\left|(x,e_{\alpha})\right|^2
  $$

问：何时 Bessel 不等式取等号？

* Theorem：设 X 是 Hilbert 空间，若 $S=\left\lbrace e_{\alpha}\,\vert\alpha\in A\,\right\rbrace$ 是其中的正交规范集，那么下面三条等价：

  1. S 封闭
  2. S 完备
  3. Parseval 等式成立

例如：

1. $L^2 [0, 2\pi]$ 上 $e_{n}(t)=\frac{1}{\sqrt{2\pi}}e^{\mathrm{i}nt}$ 是正交规范基
2. $l^2$ 上，$e_n = ( 0, ...., 0, 1, 0, ... )$ 是正交规范基
3. 令 $D$ 是 $C$ 中的单位开圆域，$H^2(D)$ 表示其中 L2 可积的解析函数组成的全体构成的空间，规定内积为：$(u,v)=\iint_{D}u\bar{v}dxdy$，那么 $\varphi_n = \sqrt{ n / \pi } z ^ {n - 1}$ 是正交规范基

### 正交化和 Hilbert 空间的同构

Gram-Schmidt 正交化过程可以在Hilbert空间中直接实施。

#### 同构

* 定义
* 为了Hilbert空间可分，必须且仅须它有至多可数的正交规范基S；

  * 如果S中元素个数$N < \infty$，那么同构于$K^N$​
  * 否则同构于$l^n$​

### 最佳逼近问题-ext

最佳逼近问题中我们将其看成求空间中一点到它的线性子空间的距离问题。当时我们要求了，子空间是**有穷维**的，并不知道**无穷维**的情况。

在Hilbert空间中，答案是肯定的，并且可以用更为一般的闭凸子集来替代原本考虑的闭子空间。

Theorem：如果$C$是Hilbert空间中的一个闭凸子集，那么$C$上**存在唯一**元素取最小模

* 思路：首先找到下确界$\inf \| z\|$，然后逐步逼近，注意到平行四边形不等式成立即可；
* 推论：对于任意元素$x_0 \in X$，和闭凸子集$C$，C中的最佳逼近是存在且唯一的

我们还需要考虑，这样的最佳逼近元有什么样的性质：

Theorem：设$C$是内积空间$X$中的一个闭凸子集，为了$x_0$是$y$的最佳逼近，当且仅当：

$$
\operatorname{Re}\left(y-x_0,x_0-x\right)\ge0
$$

* 思路：考察函数$\varphi _ x (t) = \| y - tx - (1-t) x _ 0\|^2$​
* 推论：**（正交分解）**设M是Hilbert空间上的一个闭线性子空间，对于任意的$x \in X$​**存在唯一的**正交分解$x = y + z, ( y \in M , z \in M ^ \perp)$​

### 应用

#### 最小二乘法

1. 实际观测问题（线性拟合）
2. 平方平均逼近：类似与NPDE求解？
3. 最佳估计问题

#### 曲线光顺和样条函数（Spline）

> TODO？
