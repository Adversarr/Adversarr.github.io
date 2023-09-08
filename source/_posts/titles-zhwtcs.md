---
title: 题目整理
date: '2023-09-06 11:12:44'
updated: '2023-09-08 20:23:21'
comments: true
toc: true
---
# 题目整理

## 二阶线性方程分类

### 求解特征线方程

> 例题类型：给定方程，求解特征线方程。
>
> 1. 写出特征线方程、判别式；
> 2. 观察是否有实的特征线，如果有就尝试解出来；

### 化为标准型

> 题型：给定方程，化标准型
>
> 1. 先按判别式定义域分类
> 2. 在每一类中，找出变换，然后化成标准型
>
> 导数计算很复杂

### 传输方程

‍

## 一阶拟线性

### 初值问题的求解 - 特征线法

> 解$au_{x} +bu_{y}=0$，初值条件为$u(0, y) = e^y$.
>
> Ans：$u(x, y) = \exp(y- \frac{b}{a}x)$

> 解$u_{x} + yu_{y} = y^{2}$，初值条件为$u(0, y) = \sin y$.
>
> Ans：$u =\sin ye^{-x} + \frac{1}{2} y^{2} -\frac{1}{2} y^{2}e^{-2x}$

步骤：

1. 考察给定初值是否是特征方向，也就是$J \ne 0$​
2. 解特征方程组的初值问题，认定参数$\tau = 0$时为初值
3. 消去解中的参数（用$x,y$表示参数，并且代入$u=z$的表达式中）

## 波动方程

### 求解初值问题

直接应用 d'Alembert 公式即可

d'Alembert 公式

### 反射法 求解初边值问题

如果遇到$x$的定义域是$\mathbb R^+$的情况，可以考虑是否能进行奇偶延拓。

比如书上的例题：

$$
\begin{cases}\square u=0\\ u\left(x,0\right)=g,u_{t}\left(x,0\right)=h,x\in\mathbb{R}^{+}\\ u\left(0,t\right)=0,t\ge0\end{cases}
$$

对$u, g, h$进行奇延拓

### Kirchhoff 公式

* 主要就是背诵公式，也没啥好说的；
* 用于求初边值问题解；

我个人觉得这一块好的概率特别特别低，因为真的就只有公式。

### 非齐次方程的求解：Duhamel 原理

之前考虑的方程本身是齐次的，这次我们考虑非齐次的线性方程；

主要就是将函数换到$w_t|_{t = \tau}$上，其余没有什么问题；

### 能量等式的证明

能量定义是什么:

$$
E\left(t\right)=\iint_{\Omega}|u_{t}|^2+a^2|\Delta u|^2\mathrm{d}x
$$

题目是真的会很难搞，因为你对Green公式、分部积分公式不熟悉。

书上基本的证明要会，关键是看懂分部积分、Green公式的步骤。

博资考的题目：利用输入的函数具有紧支集、从而分部积分+Green公式得到的：

$$
\int _{\partial \Omega} (u_i u_t)\nu^i\mathrm dS = 0
$$

原因是当$\Omega$充分大时，由波动方程解的有限传播速度特性有$u \equiv 0$

这也提示我们要注意各个方程解的一些物理性质！

### 能量不等式

主要观察的是$u$的2norm：

$$
E_0(t) = \iint_\Omega u^2\mathrm dx
$$

其目的是考察初边值问题对于初值的稳定性，因为：

$$
\dot E_0(t) \le 2 [E_0(t)]^{1/2} \cdot [\frac 2 \rho E(t)]^{1/2}
$$

表明了$E_0(t) \le 2 E_0(0) + 4t^2/\rho E(0)$.

### 高维波动方程解

如何求解？如何推导？看Evans的书上有完整过程！

## 热传导方程

### 初值问题 Fourier方法

书上Fourier变换的定义是：

$$
\int f(x)e^{-ix\cdot\xi}dx
$$

Fourier逆变换：

$$
\frac 1 {(2\pi )^n} \int \hat f(\xi)e^{ix\cdot \xi}dx
$$

用道德Fourier变换的性质：微分、卷积、幂乘

求解的基本思路是：对于方程和初值都进行Fourier变换，然后解ODE，再反过来进行Fourier逆变换即可。

如果用之前的基本解来表达：

> $$
> u(x,t)=\left(4\pi\right)^{-\frac{n}{2}}\int_{\mathbb{R}^{n}}^{}E\left(x-y,t\right)\varphi\left(y\right)\mathrm{d}y
> $$

解核也有一些性质：

1. 恒正、无穷次可微
2. 满足方程
3. 积分为1

### 非齐次方程的初值问题的求解

利用叠加原理。

$$
u_t - \Delta u = f, u(x,0) = 0
$$

将非齐次项转化到初值上

$$
w_t -\Delta _ x  w=0, w(x, \tau; \tau)= f(x, \tau)
$$

那么$\int_0^t w\mathrm d \tau$是非齐次方程的解。

### 均值性质

[偏微分方程(七)——热方程的均值性质](https://zhuanlan.zhihu.com/p/400672316)

这一部分书上没有，但看着挺简单的。

$$
u(x,t)=\frac{1}{4r^{n}}\int_{E\left(x,t;\tau\right)}^{}u\left(y,s\right)\frac{\left|x-y\right|^2}{\left(t-s\right)^2}\mathrm{d}yds
$$

其中的$E$是热球。

### 最大值原理

主要是偏向于结论性的内容。

要注意抛物边界的定义：不包含顶部（$t = T$）

结合物理意义来理解：

1. 如果内部没有热源：那么最大**模**能在抛物边界上取到，但不一定只在边界上取到
2. 如果内部有冷源：那么最大值能且只能在抛物边界上取到；热源是同理的

比较原理是说对于同一个方程控制的两个现象，如果在边界上一个比另一个大，那么在内部也是；

## 位势方程

椭圆型方程的典型代表，主要还是考虑调和方程的解的特点。

这一类方程更加侧重解的性质，而不是如何求解。

### 基本解、Green公式

Green第二积分公式；

调和函数的基本积分公式：

> $$
> u(y)=\int_{\partial\Omega}^{}\left(u\frac{\partial k\left(x-y\right)}{\partial\nu}-k\left(x-y\right)\frac{\partial u}{\partial\nu}\right)\mathrm{d}S_{x}
> $$

可以用来导出一些性质

### 调和函数的性质

所谓调和函数就是Laplace方程的解。

1. 证明平均值等式：最基本的性质，可以导出很多其他有用的性质
2. 证明最大、最小值原理：温度分布不可能在内部有最高、最低点。

需要注意的是，平均值等式是一个本质的结论：

* 对于$C^2$函数，平均值等式 $\iff$ 调和
* 更强的结论：对于$C^1$函数，满足平均值等式，则其调和

最大最小值定理就是调和函数的强极值原理。

其他的性质：

1. 局部估计：用来估计$|\partial _\alpha u|$
2. Liouville's Theorem：有界的无穷区间上的调和函数只有常数
3. 解析

### Green函数法 - Poisson方程和Laplace方程的Dirichlet问题

简单说就是边值问题。

工具是调和函数的基本积分公式。

假设我们已知了给定区域的Green函数，那么：

$$
u(x) = \int _{\partial U}\varphi(y) \frac{\partial G}{\partial \nu} dS_y+\int_U G(x, y) \Delta udy
$$

格林函数具有的性质：

1. $k < G$
2. 对称性：$G(x, y) = G(y, x)$

要记住几个常用的Green函数：

1. 球上的Green函数：关于球的“对称点”放置一个点电荷

### 球上Dirichlet问题解的存在性

暂时不看了

### 能量法

考察

$$
\int_\Omega | Dw| ^2\mathrm dx
$$

## 广义解

‍
