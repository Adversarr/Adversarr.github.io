---
title: 纲和开映像定理
date: '2023-08-20 10:57:28'
updated: '2023-09-03 14:36:18'
comments: true
toc: true
---


# 纲和开映像定理

## 纲和开映像定理

有一大类方程求解问题，从泛函分析上看是，对于给定的 $T$ 算子，求得：

$$
Tx = y
$$

那么：

1. 解的存在性等同于算子存在右逆；
2. 解的唯一性等同于算子存在左逆；

> 如果存在右逆：$T(T_r^{-1} y)=y$ 那么 $T_r^{-1} y$ 是一个解
>
> 如果存在左逆：$T_l^{-1}T(x-z)=0\implies x=z$，那么解是唯一的

在都存在的情况下，我们一般还需要考虑解的稳定性：

> 稳定性：在定解条件作微小的变动时，相应的定解问题也只作微小的变动

也就是 $T^{-1}$ 是连续的。$T$ ​将开集映射为开集。

### 纲和纲推理

和稠密子集、完备化空间的定义相联系，引入：

#### 疏集、第一纲、第二纲

* 定义：

  * $E \subset X, \bar{E}$ 的内点是空的
  * 第一纲：疏集的至多可数并
  * 第二纲：其他
* 例如：

  * 有穷点集是疏集
  * Cantor 集是疏集
* Prop：设有度量空间，为了 $E$ 是疏集，当且仅当，$\forall B(x_0, r_0), \exists B(x_1, r_1) \subset B(x_0, r_0),\bar E \cap \bar B (x_1, r_1) = \emptyset$​

Theorem（Baire）：完备度量空间是第二纲的

* 应用：在 $C[0, 1]$ 中处处不可微的函数集合 $E$ 是非空的，并且 $E$ 的补集是第一纲的。

### 开映像定理

假设有 B 空间 $X, Y$，并且 $T\in L(X,Y)$，T 可能满足一些性质：

1. 单射
2. 满射
3. 一一映射

在是一一映射的情况下，我们自然要问 $T^{-1}$ 是否是有界线性算子。

Theorem：

1. Banach 逆算子定理：设 $X,Y$ 是 B 空间，并且存在**一一的有界线性算子** $T$，那么 $T^{-1}$ 也是有界线性算子；
2. （更一般的结论是）

   开映像定理：设 $X, Y$ 是 B 空间，若**有界线性算子** $T$ 是满射，那么 $T$ 是开映像（将开集映射为开集）

考虑第二个定理的证明方法：

1. 开映射 <=> 对于开球 $B$，存在 $\delta > 0$，使得 $U(\theta, \delta) \subset TB(\theta, 1)$

   （Proof is easy，转化为只要证明，若 $T$ 是满射，那么 $\theta$ 在 TB 中是内点）
2. 证明：$\exists \delta > 0, \overline{TB}\supset U(\theta, 3\delta)$

   1. $Y$ 是完备的，因此至少有一个 $n\in \mathbb N$ 使得 $TB$ 非疏（$TB$ 存在内点）
   2. 记内点以及闭球为 $U(y_0, r)$，由于 $T$ 线性，因此 $U(-y_0, r) \subset TB$
   3. 因此 $U(\theta , r) \subset TB$​
3. 证明，$TB(\theta, 1) \supset U(\theta, \delta)$

分析该证明过程，不难发现，线性算子的连续性可以减弱为

#### 闭算子

* 定义：对于定义域中的$\{ x_n \}$，$x_n \in x$（$x$可以不在定义域中）以及$T x _ n \rightarrow y$，可以得到$y = Tx, x\in D$​
* Theorem：假设$X, Y$是B空间，$T$是一个闭线性算子，$R(T)$是$Y$中的第二纲集，那么：$R(T) = Y$并且$\forall \epsilon > 0, \exists \delta = \delta ( \epsilon ) > 0$使得$\forall y \in Y, \| y \| < \delta$，必有$x \in D(T)$，适合$\| x \| < \epsilon$且$y = Tx$​

### 闭图像定理

对于线性算子而言，我们观察其连续性和闭算子之间的关系：

> 一个有界线性算子 $T:D\rightarrow Y$总能延拓到$\bar D$上

Theorem（B. L. T）：设$T$是B*空间$X$到B空间$Y$的连续线性算子，那么$T$能够唯一的延拓到$\bar D(T)$上，成为连续线性算子，并且保持其算子范数；

* Proof is eazy
* 意义：可以认为，每一个连续线性算子都有闭的定义域。因此，可以认为，一切连续线性算子都是闭算子。

以下是一些推论：

1. 等价范数定理：假设线性空间上有两个范数，$\| \cdot \| _1$和$\| \cdot \| _2$，在这两个范数意义下都构成B空间，并且1比2强，那么1和2等价

    * Proof：考虑恒等映射
2. 闭图像定理：设$X, Y$是B空间，若$T$是一个闭线性算子，并且$D(T)$是闭的，那么$T$是连续的；

    * 集合$G\left(T\right)=\left\lbrace\left(x,Tx\right)\vert x\in D(T)\right\rbrace$称为算子$T$的图像，因此$\| \cdot \|_G$被称为图模，算子是闭的，实际上就是$G(T)$按图模是闭的

### 共鸣定理

Theorem（共鸣定理、一致有界定理）：设$X$是B空间，$Y$是B*空间，若：

$$
W\subset L(X, Y)\quad s.t.\ \sup_{A \in W}\| Ax\|< \infty (\forall x\in X)
$$

那么存在常数$M$使得$\| A \| \le M, \forall A \in W$.

* 注意区分条件和结论中的有界性；
* 反过来：$\sup _{A \in W} \| A \| = \infty \implies \exists x_0 \in X, \sup \| A x _ 0 \| = \infty$（“共鸣”的由来）
* 定理给出条件，算子族$W$如果对于$x$点点有界，那么$W$一致有界；

另外：

**Theorem（Banach-Steinhaus定理）**：设$X$是B空间，$Y$是B*空间，$M$是$X$的某个稠密子集，若$A_n,A$是有界线性算子，则对于任意的$x \in X$都有，$\lim A_n x = Ax$，的充要条件是：

1. $\| A_n \|$有界
2. $\lim A_n x = Ax$对每一个$x\in M$都成立

### 应用

#### Lax-Milgram定理

‍
