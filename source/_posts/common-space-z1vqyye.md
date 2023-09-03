---
title: 共轭空间
date: '2023-08-23 10:29:57'
updated: '2023-09-03 14:35:16'
comments: true
toc: true
---


# 共轭空间

## 共轭空间的表示和应用

### 共轭空间

* 定义：连续线性泛函全体，按照算子范数构成B空间；
* Note：不要求原本的空间是B空间，仅仅是B*空间

例如：

1. $L^p$的共轭空间是$L^q$：首先因为Holder不等式成立，因此可以定义积分变换为连续线性泛函，另外，这样的变换构成了连续线性泛函全体；
2. $C[ 0, 1]$的共轭空间$BV[0,1]$（有界变差函数）

回顾Riesz定理，有更加一般的情况：

Theorem（Riesz表示定理）：设$M$是一个Hausdorff紧空间，则$\forall f \in C(M)^*$，存在唯一的复值Baire测度（即一个完全可加的集函数）$\mu$，满足$\mu(M)< \infty$，并

$$
\langle f, \varphi \rangle = \int_M \varphi(m) d\mu
$$

作为Riesz定理和Theorem（Hahn-Banach）的应用：

Theorem（Runge）：设$K$是复平面上的一个紧子集，令$C_\infty = C \cup \{ \infty \}$，并且$E$是$C_\infty \backslash K$中的一个子集，它与$C_\infty \backslash K$中的每一个分量都相交，如果$f$是$K$的一个邻域内的任意解析函数，则一定存在有理函数列$f_n$，其极点都在$E$内，并且$f_n$在$K$上一致收敛到$f$.

### 第二共轭空间、自反空间

因为B*空间的共轭空间是B空间，我们考虑共轭空间的共轭空间，即$X^{ ** }$。对于任意的$x\in X$定义：

$$
X(f) = \langle f, x\rangle
$$

不难验证 $X$ 是$X^*$上的连续线性泛函，这是因为 $|X(f)|=|f(x)|\le \| f\| \cdot \| x\|$​

令这样的从$X$到$X^{**}$的映射为**自然映射**​$T$，它是从$X$到$X^{**}$的连续嵌入，并且这个映射是一个线性同构。

应用Theorem（Hahn-Banach），存在$f\in X^*$使得$\| f \| = 1$且$\langle f, x\rangle = \| x \|$，因此

$$
X(f) = \|x \|
$$

从而$\| X \| = \|x\|$，这表明了$T$还是等距的。

Theorem：B*空间$X$与它的第二共轭空间的一个子空间等距线性同构。

> 因此，有时我们不区分$x$和$X$，并简单写成$X \subset X^{**}$​

Definition（自反空间）：如果$X$到$X^{**}$的自然映射是满的

## 共轭算子

> 共轭算子的概念可以看作有穷维空间中，转置矩阵的推广。

这要利用：

$$
\langle y, Ax \rangle = \langle A ^ * y, x\rangle
$$

我们用共轭空间来定义共轭算子。

* 定义：对于B\*空间$X$和$Y$以及算子$T : X \to Y$，共轭算子定义为$T^*: Y ^ * \to X ^ *$：

  $$
  f(Tx) = (T^*f)(x)
  $$
* 这样：$\langle f , Tx \rangle =\langle T^* f, x\rangle$
* 这样的共轭运算$T \rightarrowtail T^*$是一个等距同构；

对于这样的共轭，我们参考前一节，再考察$T^{**}$：（假设自然映射$U:X \to X^{**}$，以及$V : Y \to Y^{**}$）

$$
\langle T^{**} U x, f\rangle = \langle U x, T^* f\rangle =\langle T^* f, x\rangle = \langle f, Tx\rangle = \langle V Tx, f\rangle
$$

因此 $T ^ {**} U = VT$，即$T ^ {**}$是$T$在$X^ {**}$上的扩张。

Theorem：设$X, Y$是B*空间，$T$是连续线性算子，那么$T^ { * *}$是$T$在$X^{**}$上的咽唾，并满足$\| T^{**} \| = \| T \|$  

> 例如，我们考虑卷积算子以及它的共轭算子：
>
> * $(K  * f)(x) = \int _{-\infty}^{\infty} K(x - y) f(y ) dy$
> * 首先$K ^*$是$L^p$到自身的游街线性算子；
> * 令 $\hat K (x) = K(-x)$，由Fubini定理，$T=K*$的共轭算子是$T^* = \hat K *$​

## 弱收敛和弱*收敛

有穷维和无穷维的B空间的根本区别之一是：

* 有穷维B空间中的任意有界点列一定存在收敛子列，
* 无穷维则不一定

我们可以考虑弱收敛和弱*收敛，作为这条定理的推广

### 弱收敛

* 定义：弱收敛$x_{n}\rightharpoonup x$是指，对于任意的$f$，都有$\lim _{n \to \infty} f(x_n) = f(x)$成立
* Prop：如果弱极限存在，那么弱极限是唯一的，强极限如果存在，那么弱极限存在且就是强极限

Theorem（Mazur）设$X$是一个B*空间，并且$x_n$弱收敛到$x$，那么

$$
\forall\varepsilon>0,\exists\lambda_{i}\ge0,\sum_{i}\lambda_{i}=1,s.t.\left\|x_0-\sum_{i}\lambda_{i}x_{i}\right\|\le\varepsilon
$$

> 若不然，那么$x_0$不属于$x_i$构成的凸包的闭包。考虑Ascoli 定理可知，$\exists f,\alpha, f(x)<\alpha < f(x _ 0), \forall x$，即与弱收敛矛盾。

既然X\*也是B空间，那么X\*上自然也有两种收敛性。所谓的弱收敛$f_n \rightharpoonup f$是指，

$$
\forall x^{**} \in X^{**}\quad x^{**} (f_n)\rightharpoonup x^{**}(f)
$$

为了避免讨论$X^{**}$定义**弱*收敛**为：

* 定义：设$X$是B\*空间，$f_n , f \in X^*$，称$f_n$弱\*收敛到$f$记作$w ^ * - \lim_{n\to \infty} f_n = f$，是指对于所有的$f \in X$，$\lim_{n \to \infty} f_n(x) = f(x)$，称$f$是泛函序列$\{ f_n \}$的弱*极限。
* 如果X是一个自反空间，那么弱*收敛和弱收敛是等价的

Theorem：设$X$是B\*空间，设$x_n, x\in X$，那么$x_{n}\rightharpoonup x$，当且仅当

1. $\| x_n \|$有界；
2. 对$X^*$中的一个稠密子集$M^*$上的一切泛函$f$都有$\lim_{n \to \infty} f(x_n) = f(x)$​

> 应用Theorem（Banach-Steinhaus定理）将$x_n$看作$X^*$上的连续线性泛函。

Theorem：设$X$是一个B空间，以及$f_n, f\in X^*$，为了$f_n$弱*收敛到$f$，当且仅当

1. $\| f_ n\|$有界；
2. 对$X$中的某个稠密子集$M$上的一切$x$，都有$f_n(x) \to f(x)$​

此外，类似于连续线性泛函序列，对于连续线性算子序列，我们也考虑各种收敛性：

定义：设$X, Y$是B*空间，以及其上的$f_n, f \in L(X, Y)$

1. 一致收敛是指$\| T_n - T\| \rightarrow 0$（考虑算子范数的定义）
2. 强收敛是指$\| (T_n - T)x\| \to 0, \forall x\in X$（对于每一个$x$，点点收敛）
3. 弱收敛是指$\forall x \in X$，以及$\forall f \in Y^*$都有 $f(T_n x) \to f(Tx)$​

显然的是 一致收敛 ⇒ 强收敛 ⇒ 弱收敛，下面的例子说明了反过来的箭头是错误的：

* 考察$l^2$上的左移动算子$T$，定义$T_n = T^n$，是有界线性算子，其强收敛到$0$，但并不一致收敛到$0$​
* 考察$l^2$上的右移动算子$T$，定义$T_n = T^n$，是有界线性算子，其弱收敛到$0$，但不强收敛到$0$​

‍
