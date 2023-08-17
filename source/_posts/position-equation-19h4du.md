---
title: 06. 位势方程
date: 2023-08-07T10:35:26Z
lastmod: 2023-08-09T11:48:17Z
---



位势方程：

$$
-\Delta u=f\left(x\right)
$$

是椭圆形方程的代表：

* $f\equiv 0$：**Laplace 方程，**​**** 称为调和函数；
* 否则称为 **Poisson 方程**

类似于下解、上解，引入：

$$
-\Delta u\le0
$$

为下调和函数。

## 基本解

### 基本解、Green 公式

固定球心，对于球坐标系，$\Delta u$ 可以写作：

$$
\Delta u=u''(r)+\frac{n-1}{r}u^{\prime}\left(r\right)
$$

解 Laplace 方程，得到：

$$
u=\begin{cases}\frac{c}{2-n}r^{2-n} & n>2\\ c\ln r & n=2\end{cases}
$$

其中 $r=\left|x-y\right|$。其满足 Laplace 方程。取常数 $c=\frac{1}{n\omega_{n}}$，定义调和方程的基本解 $k(x-y)$。

* $\omega_2 = \pi$​
* $\omega_3=\frac43\pi$

#### 调和函数的基本积分公式

> Green 第二公式: Integration by parts，（[PDE.pdf - p134 - PDE-P134-20230807144704](assets/PDE-20230804142154-8fruti8.pdf?p=134)）
>
> ​![](assets/PDE-P134-20230807144704-20230807144941-o7y8zpr.png)​

对于 $y\in \Omega$，作球 $B_\rho (y) \sub \Omega$，在区域 $\Omega-\bar {B}_{\rho}$ 中用调和函数的基本解，代入 Green 第二公式，

$$
\int_{\Omega-B_{\rho}}^{}k\left(x-y\right)\Delta u\mathrm{d}x=\int_{\partial\Omega}^{}\left(k\frac{\partial u}{\partial\nu}-u\frac{\partial k}{\partial\nu}\right)\mathrm{d}S_{x}+\int_{\partial B_{\rho}}^{}\left(k\frac{\partial u}{\partial\nu}-u\frac{\partial k}{\partial\nu}\right)
$$

对于第二个积分

$$
\int_{\partial B}^{}k\frac{\partial u}{\partial\nu}dS_{x}\to0\quad\int_{\partial B}^{}u\frac{\partial k}{\partial\nu}dS_{x}→-u(y)\quad(\rho\to0)
$$

因此，有 $u$ 的 Green 表示：

$$
u(y)=\int_{\partial\Omega}^{}\left(u\frac{\partial k}{\partial\nu}-k\frac{\partial u}{\partial\nu}\right)\mathrm{d}S_{x}+\int_{\Omega}^{}k\Delta u\mathrm{d}x
$$

[PDE.pdf - p135 - PDE-P135-20230807151753](assets/PDE-20230804142154-8fruti8.pdf?p=135)
​![](assets/PDE-P135-20230807151753-20230807151755-u1uhjc3.png)​

> 基本积分公式：
>
> $$
> u(y)=\int_{\partial\Omega}^{}\left(u\frac{\partial k\left(x-y\right)}{\partial\nu}-k\left(x-y\right)\frac{\partial u}{\partial\nu}\right)\mathrm{d}S_{x}
> $$

### 平均值等式

设 $u\in C^2$，在 $\Omega$ 中满足

$$
-\Delta u=0(\le 0)
$$

那么对于任何一个球 $B_R(y)\sub \Omega$，都有：

$$
u(y)=(\le)\frac{1}{n\omega_{n}R^{n-1}}\int_{\partial B_{n}}^{}udS
$$

和

$$
u(y)=(\le)\frac{1}{\omega_{n}R^{n}}\int_{B_{R}}^{}u\mathrm{d}x
$$

等号成立时，称为平均值定理。

### 最大、最小值原理

**下调和函数的强最大值原理**：设 $u$ 是 $\Omega$ 内的下调和函数，且存在 $y\in \Omega$ 使得

$$
u(y) = \sup_{\Omega} u
$$

那么 $u$ 是常数。

**下调和函数的弱最大值原理**：设 $u$ 是 $\Omega$ 内的下调和函数，且 $\Omega$ 有界，那么

$$
\max _{\bar \Omega} u= \max _{\partial \Omega} u
$$

由此可以直接得到调和函数的最大值/最小值原理、调和函数的比较定理

[PDE.pdf - p137 - PDE-P137-20230807155201](assets/PDE-20230804142154-8fruti8.pdf?p=137)
​![](assets/PDE-P137-20230807155201-20230807155203-u6jpn05.png)​

[PDE.pdf - p138 - PDE-P138-20230807155210](assets/PDE-20230804142154-8fruti8.pdf?p=138)
​![](assets/PDE-P138-20230807155210-20230807155212-8h7op8n.png)​

通过最大最小值原理，可以轻松得到：

1. Poisson 方程的 Dirichlet **内**问题具有**唯一性和稳定性**；
2. Poisson 方程的 Dirichlet **外**问题具有**唯一性和稳定性**；

## Green 函数

### Green 函数的导出与性质

我们试图求用：

>> 基本积分公式：
>>
>> $$
>> u(y)=\int_{\partial\Omega}^{}\left(u\frac{\partial k\left(x-y\right)}{\partial\nu}-k\left(x-y\right)\frac{\partial u}{\partial\nu}\right)\mathrm{d}S_{x}
>> $$
>>

解调和方程、或 Poisson 方程的 Dirichlet 问题，

$$
\begin{cases}-\Delta u=f\\ u\left|_{\partial\Omega}\right.=\varphi\left(x\right)\end{cases}
$$

显然，边界上的 $\partial u/\partial \nu$ 是未知的，不能直接求解，我们设法消去这一项。

考察一个调和函数 $h(x;y)$，满足 $\Delta h=0$，对 $h, u$ 应用 Green 第二公式，先考虑 $f\equiv 0$ 的情况：

$$
\int_{\partial\Omega}^{}u\frac{\partial h}{\partial\nu}-h\frac{\partial u}{\partial\nu}dS=0
$$

要求 $G|_{\partial \Omega}=0$，可得：

$$
u(y)=\int_{\partial\Omega}^{}\varphi\left(x\right)\frac{\partial G}{\partial\nu}dS
$$

一般的：[PDE.pdf - p140 - PDE-P140-20230808110623](assets/PDE-20230804142154-8fruti8.pdf?p=140)
​![](assets/PDE-P140-20230808110623-20230808110627-mq87mq1.png)​

因此，问题转换为求解一个的 Dirichlet 问题，即求出特定区域上的 Green 函数。

[PDE.pdf - p141 - PDE-P141-20230808105512](assets/PDE-20230804142154-8fruti8.pdf?p=141)
​![](assets/PDE-P141-20230808105512-20230808105516-dtv2fn4.png)​

### 球上的 Green 函数、Poisson 积分公式

当区域为球时，可以使用**镜像法**来求 Green 函数。[PDE.pdf - p142 - PDE-P142-20230808111049](assets/PDE-20230804142154-8fruti8.pdf?p=142)
​![](assets/PDE-P142-20230808111049-20230808111051-ejdecbp.png)​

分两种情况：

1. $y\ne 0$, $G(x,y)=k\left(\left|x-y\right|\right)-k\left(\frac{\left|y\right|}{R}\left|x-\bar{y}\right|\right)$​
2. $y=0$, $G(x,y) = k(|x|) - k(R)$

直接得到 Poisson 公式：

三维情况：[PDE.pdf - p143 - PDE-P143-20230808111834](assets/PDE-20230804142154-8fruti8.pdf?p=143)
​![](assets/PDE-P143-20230808111834-20230808111836-xx6o93c.png)​

二维情况：[PDE.pdf - p144 - PDE-P144-20230808111855](assets/PDE-20230804142154-8fruti8.pdf?p=144)
​![](assets/PDE-P144-20230808111855-20230808111857-2vbip2i.png)​

### 上半空间的 Green 函数

[PDE.pdf - p144 - PDE-P144-20230808111411](assets/PDE-20230804142154-8fruti8.pdf?p=144)
​![](assets/PDE-P144-20230808111411-20230808111413-rb45wia.png)​

定义 Green 函数为

$$
G(x, y) = k (x-y) - k (x - y^*)
$$

Poisson 公式：[PDE.pdf - p145 - PDE-P145-20230808112021](assets/PDE-20230804142154-8fruti8.pdf?p=145)
​![](assets/PDE-P145-20230808112021-20230808112023-fz9y67m.png)​

### 能量法

用能量法，也能得到解的存在性和唯一性。

1. 唯一性：通过 Green 公式可以直接得到。$0=\int_{\Omega}^{}w\Delta w\mathrm{d}x=\int_{\Omega}^{}\left|Dw\right|^2\mathrm{d}x$

Dirichlet 原理：能量泛函定义为

$$
I[w]=\int_{\Omega}^{}\left(\frac12\left|Dw\right|^2-wf\right)\mathrm{d}x
$$

其中的 $w\in A=\left\lbrace w|_{\partial\Omega}=\varphi\right\rbrace$，假设 $u$ 是 Dirichlet 问题的解，那么 $u$ 满足 $I[u]=\min I[w]$，反之亦然。

> [PDE.pdf - p148 - PDE-P148-20230808112645](assets/PDE-20230804142154-8fruti8.pdf?p=148)
> ​![](assets/PDE-P148-20230808112645-20230808112648-hzjesmv.png)​

## 调和函数的基本性质

### 逆平均值性质

从之前的讨论中知道，调和函数具有平均值性质：

> ### 平均值等式
>
> 设 $u\in C^2$，在 $\Omega$ 中满足
>
> $$
> -\Delta u=0(\le 0)
> $$
>
> 那么对于任何一个球 $B_R(y)\sub \Omega$，都有：
>
> $$
> u(y)=(\le)\frac{1}{n\omega_{n}R^{n-1}}\int_{\partial B_{n}}^{}udS
> $$
>
> 和
>
> $$
> u(y)=(\le)\frac{1}{\omega_{n}R^{n}}\int_{B_{R}}^{}u\mathrm{d}x
> $$
>
> 等号成立时，称为平均值定理。

但是并没有给出其逆定理。

**逆平均值定理**：设 $u$ 连续，且对于任意一个 $B = B_R(y) \subset \Omega$，都满足平均值等式，那么 $u$ 在 $\Omega$ 内调和。

另外，假设调和函数列 $u_n\rightarrow u$ 一致收敛，那么 $u$ 是调和函数。

[PDE.pdf - p150 - PDE-P150-20230808145235](assets/PDE-20230804142154-8fruti8.pdf?p=150)  
​![](assets/PDE-P150-20230808145235-20230808145236-0epamw2.png)

### Harnack不等式

> 一个非负调和函数在其调和区域内一个紧子域上的最大值，可以被其最小值乘以一个与函数无关的常数界定。

[PDE.pdf - p150 - PDE-P150-20230808145422](assets/PDE-20230804142154-8fruti8.pdf?p=150)  
​![](assets/PDE-P150-20230808145422-20230808145423-q5b5g8h.png)​

### Liouville 定理

**Liouville 定理**：全空间$\mathbb{R}^{n}$上的有界调和函数一定是常数。

### 奇点可去性

假设$u$在$\Omega-\left\lbrace x_0\right\rbrace$调和，在$x_0$有：

$$
\lim_{x\to x_0}\left|x-x_0\right|^{n-2}u\left(x\right)=0,n>2
$$

那么可以重新定义$u$在$x_0$的值，使得$u$在$\Omega$中调和。

### 正则性

调和函数是无穷次可微的。

### 局部微商估计

对于每个球$B_r$，满足$|\alpha|=k$的多重指标，

$$
\left|D^{\alpha}u\left(x_0\right)\right|\le\frac{C_{k}}{r^{n+k}}\|u\|_{L^1}
$$

### 解析性

调和函数都是解析的。

## Hopf最大值原理及其应用

### Hopf最大值原理

调和方程描述的稳定的温度分布，通过最大值/最小值原理可知，温度的最高点和最低点一定在边界上取得。

**Hopf引理**：设$B_R(y)\subset R^n$，在其中$-\Delta u \le 0$，假设有边界点$x_0$，以及

1. $u\in C(\bar B_R)$
2. $\forall x \in B_R, u(x_0) > u(x)$

若$u$在$x_0$沿着外法向的微商存在，那么$\frac{\partial u}{\partial\nu}>0$

**Hopf最大最小值原理**：设在$\Omega$中$-\Delta u \le 0$，$x_0 \in \partial \Omega$且：

1. $u$在$x_0$连续
2. 对所有的$x$，有$u(x_0) > u(x)$​
3. $\Omega$在$x_0$满足内部球条件

那么$u$在$x_0$的外法向微商若存在，则满足$\frac{\partial u}{\partial\nu}>0$  

### Hopf原理应用

[PDE.pdf - p163 - PDE-P163-20230809111748](assets/PDE-20230804142154-8fruti8.pdf?p=163)  
​![](assets/PDE-P163-20230809111748-20230809111751-ui0lq8w.png)​

第二边值问题的解，除去一个常数是唯一的

## 位势方程的弱解

### 伴随微分算子

考察齐次边界的函数类：$D = C_0^2(\Omega)$

$L_2$内积：

$$
(u, v) = \int _ {\Omega} uv \mathrm dx
$$

伴随微分算子：对于任意的$u, v$都有：

$$
(L u , v)  = (u, L^*v)
$$

一般的二阶偏微分算子：

[PDE.pdf - p164 - PDE-P164-20230809112250](assets/PDE-20230804142154-8fruti8.pdf?p=164)  
​![](assets/PDE-P164-20230809112250-20230809112252-djc45ds.png)​

Laplace 算子、波动算子都是自伴随微分算子。

### 弱微商

设$u, \psi \in L^1_{loc}$，等式

$$
\int_{\Omega}^{}uD^{\alpha}\varphi dx=\left(-1\right)^{\left|\alpha\right|}\int_{\Omega}^{}\psi\varphi dx
$$

对任意的$\varphi \in C_0 ^{|\alpha|}(\Omega)$成立，那么称$\psi$为$u$的$\alpha$弱微商。

[PDE.pdf - p166 - PDE-P166-20230809114813](assets/PDE-20230804142154-8fruti8.pdf?p=166)  
​![](assets/PDE-P166-20230809114813-20230809114815-1jleqeg.png)​

‍
