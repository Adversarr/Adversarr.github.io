---
title: 内积空间
date: 2023-08-17T10:46:04Z
lastmod: 2023-08-17T11:15:58Z
---



## 内积空间

### 基本定义和性质

**共轭双线性函数、内积、内积空间**

* 定义：共轭对称、正定的共轭双线性函数
* 例：

  * $l^2$空间$L^2$空间
  * $C^k(\bar \Omega)$中，按照$(u,v)=\sum_{\left|\alpha\right|\le k}^{}\int_{\Omega}^{}\partial^{\alpha}u\overline{\partial^{\alpha}v}dx$ 是内积空间
* Cauchy-Schwarz不等式：$|(x, y) | \le \| x \| \|y\|$，等号成立当且仅当$x, y$线性相关

内积空间按照$\|x\|=(x, x)$定义范数，构成B*空间：

* 内积$(\cdot, \cdot)$是关于$\|\cdot \|$的连续函数
* 内积空间是严格凸的B*空间

反过来，一个$\|\cdot \|$也有可能构成一个内积空间：

* 如果$\|\cdot \|$ 满足平行四边形等式：

  $$
  \|x-y\|^2+\|x+y\|^2=2\left(\|x\|+\|y\|\right)
  $$

**Hilbert空间**

* 完备的内积空间

> 在PDE中，常用的一个Hilbert空间是$H^m_0$，
>
> 设$C_0^m$是有界开区域上一切$m$次连续可微、在边界的某个邻域内为0的函数集合，那么：
>
> $$
> \forall u\in C_{0^{}}^{m},\sum_{\left|\alpha\right|<m}^{}\int_{\Omega}^{}\left|\partial^{\alpha}u\left(x\right)\right|^2dx\le C\sum_{\left|\alpha\right|=m}^{}\int_\Omega\left|\partial^{\alpha}u(x)\right|^2dx
> $$
>
> ‍

‍
