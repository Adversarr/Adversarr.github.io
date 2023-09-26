---
title: 2-Model Equations
date: '2023-09-22 09:49:41'
updated: '2023-09-26 09:02:27'
comments: true
toc: true
---

# 2-Model Equations

## First order wave-equation, convergence, stability

$$
\begin{cases}
  u_t = u_x\\
  u(x, 0) = f(x)
\end{cases}
$$

其中$f$是周期函数，周期为$2\pi$，那么解也是以$2 \pi$为周期的函数。

Follow 上一章，考虑

$$
f(x) = \frac{1}{\sqrt{2\pi}} e^{i \omega x} \hat f(\omega)
$$

我们考虑找到相同类型的解：

$$
u = \frac{1}{\sqrt{2 \pi}} e^{i \omega x} \hat u(\omega, t)
$$

显然：

$$
u(x, t) = f(x + t)
$$

因此还有Parseval等式成立，即$\| u(\cdot, t) \|$不变，为$\| f\|$​

数值解是指：进行空间和时间划分：

$$
u_j^n = u(x_j, t^n) = u(jh, nk)
$$

求出近似解。

$$
\begin{cases}
 v_j ^{n+1} = (I+kD_0)v_j^n\\
v_j^0 = f_j
\end{cases}
$$

假设$v_j^n$是某个谐波解，即

$$
v_j^n = \frac{1}{\sqrt{2 \pi}} \hat v^n (\omega) e^{i \omega x_j}
$$

我们考虑这个解的Fourier系数会如何变化！

其实我的理解是，

* 原本空间域上的$E$算子
* 在频率域空间就是简单的数乘

推导：令$\lambda = dt / dx$ 以及 $\xi = \omega h$，那么：

$$
y_j = E x_j\implies 

\hat y = e^{i\omega h} \hat x
$$

对应的$D\sim (e^{i \omega h} - 1)/ h$

从而对于格式：

$$
y= x + dt/ dh(Ex - E^{-1}x)
$$

有：

$$
\hat y = (1 + \lambda(e^{i\omega h} - e^{-i\omega h}))\hat x
$$

所谓的$\hat Q$就是**放大因子**

简单说，这个系统将$\omega$的频率分量放大了$\hat Q$倍。

​![image](assets/image-20230922103339-4808cmb.png)

有这个结论，我们还能知道，这个算法是逐点收敛的。

### stablity

实际上就是考虑 $\hat Q$ 的性质。

方法：固定 $T$，$n \sim T / dt$，考察$|\hat Q|^n$是否有界。

FTCS格式的结论：

* if $\lambda$ fixed, $| \hat Q |^n\to \infty$
* if $dx / dt^2$ fixed, then $|\hat Q|^n < e^{c T}$

FTCS方法不常用的原因：

1. 要求 $dx/dt^2$固定，复杂度问题
2. 就算是这种情况，上面这个不等式的界也很大

### 数值粘性

$$
v^{n+1} = (I + k D_0) v_j + \sigma k h D_+ D_- v_j
$$

这是：

$$
u_t = u_x + \sigma h u_{xx}
$$

* 类比流体粘性项，$\Delta u$​

那么：

$$
\begin{aligned}
\hat Q = 1 + \lambda (e^{i \omega h} - e^{-i \omega h})/2 +
\sigma\lambda (e^{i \omega h}-1)(1-e^{-i \omega h})\\ = 1 + i \lambda \sin \xi - 4 \sigma \lambda \sin^2 \xi/2
\end{aligned}
$$

两种方式：

1. $0 < \lambda \le 2 \sigma \le 1$​
2. $1 \le 2 \sigma, 2 \sigma \lambda \le 1$​

​![image](assets/image-20230922104907-gw4p43v.png)​

> Theorem：设有格式如上定义，假设：
>
> 1. 初值条件的Fourier级数收敛到原函数、并且能量有限
> 2. 初值条件等距采样后的DFT收敛到原本的函数
> 3. 方法Stable：$\sup |\hat Q^n| \le K(s)$​
> 4. 方法Consistent：$\lim_{k, h \to 0} \sup | \hat Q^n - e^{i \omega t_n}| = 0$
>
> 那么，三角插值 $Int_N v$收敛到原本方程的解。

## Leap frog scheme

[Time Dependent Problems and____ Difference Methods.pdf - p65 - Time Dependent Problems and____ Difference Methods-P65-20230922195151](assets/Time Dependent Problems and____ Difference Methods-20230922195106-20cq141.pdf?p=65)  
​![](assets/Time Dependent Problems and____ Difference Methods-P65-20230922195151-20230922195155-i3shy9y.png)​

$$
v_j^{n+1} = v_j^{n-1} + \lambda (v_{j+1} ^ n - v_{j-1}^n)
$$

分析困难一些；

$$
\hat v^{n+2} = \hat v^n + (2i\lambda \sin \omega h)\hat v^{n+1}
$$

写成等比数列和的形式：

$$
\hat v^n = C_1 z_1^n + C_2 z_2 ^n
$$

$z_{1,2}$是特征方程的解。

​![image](assets/image-20230922191135-c0xr1vh.png)​

### CFL条件

Domain of Dependence of `difference approximation`​  **must include ​**Domain of Dependence of PDE.

[Time Dependent Problems and____ Difference Methods.pdf - p69 - Time Dependent Problems and____ Difference Methods-P69-20230922195539](assets/Time Dependent Problems and____ Difference Methods-20230922195106-20cq141.pdf?p=69)  
​![](assets/Time Dependent Problems and____ Difference Methods-P69-20230922195539-20230926090128-y2lyi05.png)​

## Implicit Methods

‍
