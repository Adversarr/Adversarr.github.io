---
title: 图形变换算法
date: '2023-08-09 11:01:58'
updated: '2023-08-29 15:46:09'
permalink: /post/graphic-transformation-algorithm-z10h0cf.html
comments: true
toc: true
---


> 包括视点变换、世界坐标变换、局部坐标变换等各种矩阵变换方法；

一般的，有如下几个坐标系之间需要相互转化：

1. 模型坐标系
2. 世界坐标系
3. Eye coordinates
4. Clip coordinates
5. NDC
6. Window coordinates.

## 齐次坐标

考虑两个坐标系之间的转化：

$$
\begin{bmatrix}u_1\\ u_2\\ u_3\end{bmatrix} = M \begin{bmatrix}\nu_1\\ \nu_2\\ \nu_3\end{bmatrix}
$$

如果一个向量表示为：

$$
w=\alpha_1\nu_1+\alpha_2\nu_2+\alpha_3\nu_3
$$

即在$\mathbf \nu$下的坐标为$\alpha$，那么在$u$下的坐标为

$$
\beta = T\alpha = M^{-T} \alpha
$$

‍

而为了用矩阵来方便的表示3d仿射变换，引入齐次坐标：

$$
P = P_0 + x \nu _1 + y\nu _2 + z \nu _3
$$

1. 对于点：$(x, y, z) \rightarrow (x, y, z, 1)$，并且认定$(kx, ky, kz, k)$等价于$(x, y, z, 1)$
2. 对于向量：$(x, y, z) \rightarrow (x, y, z, 0)$

这样：

1. 点 + 点 → 中点
2. 点 + 向量 → 点
3. 向量 + 向量 → 向量

对于两个标架：$(u, Q), (\nu, P)$，之间可以用矩阵来进行转换，即：

$$
\begin{bmatrix}u\\ Q\end{bmatrix}=M\begin{bmatrix}\nu\\ P\end{bmatrix}
$$

假设坐标为$\alpha$，求出另一标架下的坐标：

$$
\alpha^{\prime}\begin{bmatrix}u\\ Q\end{bmatrix}=\beta^{\prime}\begin{bmatrix}\nu\\ P\end{bmatrix}=\beta^{\prime}M\begin{bmatrix}u\\ Q\end{bmatrix}
$$

因此$\beta = M^{-T}\alpha$​

### 平移

$(x, y, z) \rightarrow (x + dx, y + dy, z + dz)$​

$$
M=\begin{bmatrix}1 & 0 & 0 & \mathrm{d}x\\ 0 & 1 & 0 & \mathrm{d}y\\ 0 & 0 & 1 & dz\\ 0 & 0 & 0 & 1\end{bmatrix}
$$

### 旋转

首先考虑二维的旋转，二维绕原点的旋转为：

$$
\begin{bmatrix}\cos\theta & -\sin\theta\\ \sin\theta & \cos\theta\end{bmatrix}
$$

可以看成是，三维中绕某一固定轴的旋转。

例如，绕z轴

$$
\begin{bmatrix}\cos\theta & -\sin\theta & 0 & 0\\ \sin\theta & \cos\theta & 0 & 0\\ 0 & 0 & 1 & 0\\ 0 & 0 & 0 & 1\end{bmatrix}
$$

需要注意的是，旋转矩阵一定满足$R^{-T} = R$​

### 缩放矩阵

$$
(x,y,z)\to\left(\beta_{x}x,\beta_{y}y,\beta_{z}z\right)
$$

$$
M=\mathrm{diag}(\beta_{x},\beta_{y},\beta_{z},1)
$$

### 复杂旋转

主要是考虑绕任意轴的旋转。

记绕$x$轴的旋转为$R_x(\theta)$，轴过点$p$，且对于$x, y$轴的角为$\theta_{x},\theta_{y}$，那么：

$$
M = T(p_0) R_x(-\theta_x) R_y(-\theta_y) R_z(\theta) R_y(\theta_y)R_x(\theta _x) T(-p_0)
$$

### 向量旋转公式

另外，考虑绕向量$u$的旋转，我们可以尝试将向量$v$分解到沿$u$的方向和垂直于$u$的方向。

先考虑垂直方向：

$$
\mathbf{v}^{\prime}=\cos\theta\mathbf{v}_{}+\sin\theta\left(u\times\mathbf{v}\right)
$$

整合垂直方向和平行方向：

$$
v^{\prime}=\cos\theta\left(v-\left(u\cdot v\right)u\right)+\sin\theta\left(u\times v\right)+\left(u\cdot v\right)u
$$

## 四元数、光滑旋转

1. 将虚数推广到3d
2. 一个实部、三个虚部$q = q_0 + q_1 i + q_2 j + q_3 k = (q_0, Q)$
3. $i^2=j^2=k^2=ijk=-1$

$$
pq = (p_0 q_0 - P\cdot Q, q_0 P + p_0 Q + P \times Q)
$$

$$
pq=\begin{bmatrix}p_0 & -p_1 & -p_2 & -p_3\\ p_1 & p_0 & -p_3 & p_2\\ p_2 & p_3 & p_0 & -p_1\\ p_3 & -p_2 & p_1 & p_0\end{bmatrix}q
$$

共轭四元数可以用于求逆：

$$
qq^{*}=\|q\|^2\Rightarrow q^{-1}=\frac{q}{\|q\|^2}
$$

‍

### 四元数表示旋转

空间中的点表示为：

$$
p = (0, Q)
$$

定义：

$$
r=\left(\cos\frac{\theta}{2},\sin\frac{\theta}{2}\mathbf{u}\right)
$$

其中的$\mathbf u$是一个单位向量。

那么$r p r^{-1}$也是一个点，是$Q$绕方向$v$旋转$\theta$角的位置。

我们考虑纯四元数$v = (0, \mathbf v)$​

通过之前的公式，假设它垂直于我们的旋转轴$u$，旋转后四元数应为：

$$
v' = (0, \cos\theta\mathbf{v}_{}+\sin\theta\left(u\times\mathbf{v}\right))
$$

对比乘法公式，不难得到：

$$
v' = (\cos \theta , u \sin \theta )v
$$

因此，一般情况下：

$$
v' = v_\|+qv_{\perp}
$$

进一步化简需要用到如下的公式：

> $$
> \left(\cos\theta,u\sin\theta\right)^2=\left(\cos2\theta,u\sin2\theta\right)
> $$

从而，令$p=\left(\cos\frac{\theta}{2},u\sin\frac{\theta}{2}\right)$，我们可以对于原本的公式进行变形：

$$
v^{\prime}=pp^{-1}v_{\parallel}+ppv_{\perp}
$$

但考虑到

1. $v_\parallel$平行于$u$，因此$pv_\parallel = v_\parallel p$
2. $v_\perp$垂直于$u$，因此$q v_\perp = v_\perp q^{-1}$​

交换两个顺序：

$$
v' = p v p^* = p v p ^{-1}
$$

因此，如果单位四元数 $q = [a, \mathbf b]$，那么可以通过：

$$
\cos\frac{\theta}{2}=a,u\sin\theta=b
$$

来反求出转轴和转动角。

#### 旋转复合

如上定义的旋转也满足复合，可以通过旋转的复合，等价于四元数的乘法。 

#### 双倍覆盖

任意的单位四元数，$q$和$-q$代表的是同一个旋转。$-q$可以看作是沿着转轴$-u$旋转$2\pi - \theta$。

#### 指数形式

类似于复数的欧拉公式，四元数有类似的公式。只考虑单位纯四元数的情况：

$$
u=[0,\mathbf{u}]\implies\exp u\theta=\cos\theta+u\sin\theta
$$

因此，沿着$u$轴的旋转可以写作：

$$
v^{\prime}=e^{u\frac{\theta}{2}}ve^{-u\frac{\theta}{2}}
$$

### 四元数旋转插值

假设有两个旋转变换，$q_0$和$q_1$，希望找到一些中间的变换$q_t$。它可以将$v_0 \rightarrow v_1$按照旋转插值到$v_t$。

​![image](assets/image-20230811161310-dt508l5.png)​

显然：

$$
q_1vq_1^{*}=\Delta qq_0vq_0^{\ast}\left(\Delta q\right)^{*}\implies \Delta q = q_1 q_0 ^{*}
$$

因此：

$$
q_ t = (q_1 q_0 ^*)^t q_0
$$

在本质上，$q_0, q_1$仅能张成一个4d空间内的2d的超平面，因此可以在圆上考虑旋转差值：

​![image](assets/image-20230811162708-mw83uf9.png)​

其中的$\theta$可以通过 $q_0\cdot q_1$ 计算得到。而恰巧的是，该角度刚刚好是$\Delta q$对应的旋转角度的一半。

### Lerp Nlerp Slerp

#### Lerp

​![image](assets/image-20230811163152-e03be6w.png)​

$$
Lerp(v_0, v_1, t) = v_t = (1-t) v_0 + tv_1
$$

#### NLerp

​![image](assets/image-20230811163148-4thudqd.png)​

$$
Nlerp(v_0, v_1, t) = Normalize(Lerp(v_0, v_1, t))
$$

#### Slerp

球面线性插值

​![image](assets/image-20230811163200-9qseiro.png)​

$$
Slerp=\frac{\sin\left(1-t\right)\theta}{\sin\theta}v_0+\frac{\sin t\theta}{\sin\theta}v_1
$$

## 图形变换

重新回到我们研究的图形变换问题上。

### 观察（Viewing）

#### 平行投影

1. 正投影：不改变距离和角度，距离和形状都没有失真；
2. 轴测投影：投影线仍然垂直于投影面，但是投影平面相对于物体的方向是任意的；
3. 斜投影：普通的平行投影

#### 透视

尺寸会变化，同时分为：

1. 三点透视
2. 两点透视
3. 一点透视

### 定位照相机

我们一般直接使用模-视变换，而非单独的的Model, View变换。初始的矩阵为Identity Mat，即照相机标架和对象标架重合。而且，MV变换是相对于相机标架的，作用在图元上。

一种可能的API是基于：

1. 相机的位置 $p$
2. 相机的朝向 $u$
3. 相机的上方向（Up） $n$

来确定view变换。

通过$v = n \times u$来确定左方向，因此从$uvn$到$xyz$标架的矩阵为：

$$
R=\begin{bmatrix}u_{x} & v_{x} & n_{x} & 0\\ u_{y} & v_{y} & n_{y} & 0\\ u_{z} & v_{z} & n_{z} & 0\\ 0 & 0 & 0 & 1\end{bmatrix}
$$

同时，考虑到相机的平移为$T^{-1} = T(x, y, z)$，组合出mv矩阵为$V=RT$​

另一种api可以基于俯仰角、滚转角、偏航角来确定。

### 简单投影

#### 透视投影

考虑点$(x, y, z)$投影到平面$z = d$上：

$$
\left(x,y,z\right)\rightarrowtail\left(\frac{xd}{z},\frac{yd}{z},d\right)
$$

不难看出，这不是一个仿射变换。但是考虑齐次坐标：

$$
\left(x,y,z,1)\equiv\left(xd,\right.yd,zd,d\right)
$$

我们可以定义变换：

$$
M=\begin{bmatrix}1 & 0 & 0 & 0\\ 0 & 1 & 0 & 0\\ 0 & 0 & 1 & 0\\ 0 & 0 & \frac{1}{d} & 0\end{bmatrix}
$$

可以得到：

$$
(x,y,z,1)\to\left(x,y,z,\frac{z}{d}\right)\equiv\left(\frac{xd}{z},\frac{yd}{z},d,1\right)
$$

即为所求的透视变换。

### Opengl 投影

定义为：

```cpp
glFrustum(l, r, b, t, n ,f)
```

### 投影矩阵

#### 平行投影

​![image](assets/image-20230814155754-rxl0joz.png)​

$$
x,y,z\to x,y,0
$$

OpenGL 中的平行投影API为：

```cpp
mat4 Ortho(GLfloat left, GLfloat right, GLfloat bottom, GLfloat top, GLfloat near, GLfloat far)
```

​![image](assets/image-20230814155859-6eh5pu0.png)​

#### 投影规范化

​![image](assets/image-20230814160341-5s5oknr.png)​

‍

1. 在4d空间中计算
2. 尽可能保留深度信息，然后进行深度测试
3. 执行投影规范化，使得需要的投影变成一个固定的正交投影

#### 正交投影

​![image](assets/image-20230814161642-59uzx5m.png)​

​![image](assets/image-20230814161648-z4qawdx.png)​

#### 斜投影

类似于正投影，但涵盖一个切变变换：

​![image](assets/image-20230814173621-iknmmdr.png)​​

![image](assets/image-20230814173626-llgwro5.png)​

### 透视投影

考察如下的透视投影问题：

​![image](assets/image-20230814173745-5qx890u.png)​

现在我们考虑：$z=-near\to-1$，$z=-far\to1$，即：

​![image](assets/image-20230815101557-jmiuyum.png)​

只考虑z轴，矩阵为

$$
M=\begin{bmatrix}1 & 0 & 0 & 0\\ 0 & 1 & 0 & 0\\ 0 & 0 & \alpha & \beta\\ 0 & 0 & -1 & 0\end{bmatrix}
$$

其中的：

$$
\begin{cases}\alpha=-\frac{n+f}{n-f}\\ \beta=-\frac{2nf}{n-f}\end{cases}
$$

‍

​![image](assets/image-20230815105743-9ecc72j.png)​

## 隐藏面消除

两大类：

1. 对象空间算法：将场景中的对象表面排序
2. 图像空间算法：确定每一条投影线于对象表面所有交点的关系，例如 z-buffer

‍

‍
