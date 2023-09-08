---
title: 过一遍USTC-CG-2020 ppt
date: '2023-09-06 19:16:02'
updated: '2023-09-08 16:40:28'
comments: true
toc: true
---
# 过一遍USTC-CG-2020 ppt

## 2d图形光栅化

### 2d图像和光栅化显示器

图像是什么：rgb[][]

像素：图像的基本单元；

光栅：像素阵列；

像素构成的矩阵：

* 每个元素就是片元（Frag）可能包含很多信息
* 片元被赋予了颜色，称为像素

图像放缩的问题：插值、误差、SuperResolution

### 2d图形

有哪些呢：点、线、离散曲线、多边形区域

问题：如何光栅化几何图形？

### 光栅化2d图形

#### 线段光栅化

主要是：

1. dda算法：对于每个x画出最接近的y
2. bresenham：从一个像素，找出下一个可能的像素

#### 多边形区域的光栅化

一个问题是：如何决定封闭多边形的内外？

1. 奇偶检测法，也就是射线法；
2. 扫描线法

​![image](assets/image-20230906192323-r2ftj62.png)​

#### 光滑曲线光栅化

最简单的：圆的光栅化

具有八分对称性，因此只需要画出1/8的圆，然后镜像；

* 中点法、Bresenham算法
* 正负判定法 → 判断$F (x, y)$和0的大小关系，决定往哪个方向走

一般曲线呢？分段线性逼近

隐函数呢？Hard！

### 反走样 aa

走样 ⇒ 采样不足

Blur before sampling

使用低通滤波去除掉高频的信息

### 图形v.s.图像

## 数据拟合

### 拟合问题

输入：观察数据点

输出：泛影这些数据的函数

两个方法：逼近、插值

如何求解：

1. 用什么函数？（完备的函数空间）
2. 最小二乘拟合：L2、l2？选择什么函数空间？

    1. RBF（径向基函数）
3. Lagrange 插值函数
4. Overfitting问题？

联系Machine Learning：

1. 岭回归
2. 稀疏学习 - 冗余的基函数
3. 压缩感知

## 重心坐标

## 采样和网格划分

1d 曲线采样：分段线性逼近

2d 曲面：分片线性

平面区域：

1. 规则采样：网格
2. 不规则采样：三角化

### 2d delaunay triangulation

Voronoi图

DT 的性质：

1. 最大化最小角
2. 凸包
3. 最小化图拉普拉斯矩阵的谱范数

### Mesh Generation

如何采样？

CVT方法：centroidal voronoi tesselation

## Meshes: DS & Programming

### 三维曲面

#### 数学表达

1. 函数表达
2. 参数表达

如何画出曲面：离散化

多面体网格模型 - 每个面都是平面多边形

正多面体

#### Euler 公式

$$
V + F - E = 2
$$

#### 三角网格

基本元素：点、线、面

存储方法：Obj file

#### Topology

洞 ⇒ 建立连续可逆的映射？

### Mesh DS

渲染：Triangle List, Trip, Fan ...

几何：常见操作是加一个顶点、边，分裂顶点等

1. 存储上很难高效存储；
2. 时间上呢？

    1. 构建
    2. 查询：点相关的边、边相关的点……
    3. 更新

如何定义一个Mesh？

* Edge []
* Vertex - Edge Relation
* Vertex - Face Relation
* Combined...

#### Half edge

半边数据结构的核心思想：用两个有向半边来取代原先的边。

#### List of faces

好处：

1. 内存开销小
2. 可以表示非流形的网格

缺点：过于简陋，对于vf的操作复杂度高

#### 邻接矩阵

直接用图论的方法

1. 查找顶点相关的边：O(1)
2. 两个顶点是否相邻：O(1)
3. 哪些面和顶点相邻：遍历所有的面

缺点：面只和顶点保存联系，但与边不保存。

#### DCEL

本质上是HalfEdge DS

## Discrete Differential Coordinates

Laplacian Coordinates

### Mesh Surface

本质上就是2d区域在三维中的“嵌入”

#### Cardinal Coordinates

欧式坐标，类似obj文件中的`v`​部分

#### Laplace Coord

Detail = Surface - SmoothedSurface

= 自己的坐标 - 1ring neighbour的加权平均

几种可能：

1. Uniform weight：所有1ring的权重相同，这个不考虑几何信息
2. Cotangent weight：考虑了几何信息

为什么Laplace Coordinate重要：保持了变化率信息！

联想Poisson Image Editing。

$$
L = I - D^{-1} A
$$

​![image](assets/image-20230908100237-zm1uiip.png)​

重建：从相对坐标重建绝对坐标。

本质是什么：好的$w$能算出平均曲率！

​![image](assets/image-20230908101238-erhx5pm.png)​

注意下面那个公式左边就直接取到$\delta _i$​

$$
\frac{1}{d}\sum_{v\in N}^{}\left(v_{i}-v\right)\approx H\left(v_{i}\right)n_{i}
$$

### 极小曲面

平均曲率处处为0

如何生成？

## 曲面参数化

问题是什么？给定3d中的曲面，嵌入到2d中

应用落地：纹理映射

> TODO

## 几何建模与处理

几个需求：

1. 几何建模
2. 曲面重建
3. 曲面光顺
4. 曲面简化
5. 曲面编辑
6. 曲面动画插值
7. ……

我看crj的课件里面似乎没有这些东西，但还是记录一下

### 曲面重建

输入：电晕

输出：2d manifold

主要两种方法：

1. Explicit - 直接构建三角网格

    1. voronoi diagram
    2. delaunay trianglation
2. Implicit - 找某个函数的等值面，例如

    1. sdf、rbf重建
    2. Poisson重建

隐式函数拟合方法 - 联系marching cube

### 曲面光顺

从三维重建的物体通常是Noisy的 -- 去除高频分量

Laplace Operator：1ring 的 Uniform weight

​![image](assets/image-20230908104738-237suzq.png)​

Laplacian Smoothing Flow：

$$
P_{new}\leftarrow P_{old}+\lambda L\left(P_{old}\right)
$$

* 相当于Box Filter，（信号处理领域）
* 应用到所有顶点上
* 重复多次
* 可以被描述为Energy Minimization

当然，也可以用Mean Curvature做Flow

​![image](assets/image-20230908105331-rju2yfm.png)

### 网格简化

策略：删掉不重要的点、面、边，比如曲率的顶点等

### 曲面编辑

如何生成满足用户交互的形变？

#### Free-Form Deformation

把物体嵌入到更加容易参数化的一个空间里面，然后对空间做形变

​![image](assets/image-20230908105713-t1xzina.png)​

#### Axial Deformation

沿着某个轴做形变

#### Detail Preserving

几何细节是什么：Laplacian Coordinates

1. Laplacian Mesh Editing：$L x = \delta, x_j = c_j$​
2. Poisson Mesh Editing
3. Linear Rotation-Invariant Coordinates

### Mesh Morphing

生成动画，没咋讲啊。。

## 计算机动画

关键帧动画 - Morphing

两个子问题：

1. 匹配：两个关键帧之间的曲面如何相互映射？

    1. vertex matching
    2. component matching
2. 插值：如何建立动画

    1. 线性插值？
    2. 非线性- 小波插值？

## 仿真算法

太熟悉了，果断不看，列个提纲：

1. 牛顿第二定律
2. 柔性物体：自身如何仿真、交互如何仿真，种类（布料、流体、刚体、弹性体……）
3. 弹簧质点模型和隐式积分、Local-Global
4. FEM：这玩意就看着很复杂，直接套公式代码还是简单的
5. 流体：FVM还是主流、还有SPH
6. IK、骨骼动画、数据驱动

## 渲染

### 三维物体的显示

Render = 渲染和绘制

区分：光栅化图像、矢量图形

三维物体渲染？

成像原理：

1. 小孔成像
2. 相机离散均匀采样

像平面实际上没必要是真实的相机平面，可以虚拟到对称的平面上

#### 相机的指定

外部参数：位置、旋转（6Dof刚体）

内部参数：焦距、胶卷尺寸

确定好参数后，可以定义一个透视投影，进行3d物体可视化

#### 3d物体渲染

基本的操作流程：

* 输入：顶点
* 变换 T：顶点
* 光栅化：像素

计算某个点到成像平面的位置

​![image](assets/image-20230908112645-7eyqiw4.png)​

涉及到不同的坐标系，相互之间如何转化？

矩阵 + 齐次坐标

## 渲染管线

CPU - GPU - Framebuffer

两个最重要的阶段：

1. 几何

    1. 3d模型投影变换到图像平面上
    2. 决定可见的图元
2. 光栅化

    1. 决定可见的片元
    2. 决定片元的颜色，就是像素

基本的图元：点、线、三角（3d）

渲染管线：渲染的流水线

​![image](assets/image-20230908113151-p4x8a9r.png)​

Vertex Shader - 顶点变换

Fragment Shader - 片元处理

​​![image](assets/image-20230908113418-znadcmf.png)​

MVP变换分别：

1. MV：Object → Eye
2. P：Eye → NDC

并不是每一个都单独做的。

### 顶点处理

3d → 2d

拿opengl举例子，输出的是一个`gl_Position`​，但是vec4

* 前俩坐标是 xy，基本就对应了2d的坐标
* 第三个坐标是z，表示深度坐标 - zbuffer
* 第四个坐标是齐次的系数，目的是用来处理透视投影的

需要做什么的裁剪？

1. 视锥体裁剪
2. 窗口裁剪
3. 隐藏面消除

屏幕空间变换：NDC到Screen，这个是机器自己做

### 光栅化

逐顶点计算屏幕坐标：

* 模型 → 图元 → 片元

真正的“着色”器开始发挥作用，计算光照等信息

### 着色

信息从顶点插值。

1. Flat shading - 对每个三角形着色
2. Gourand Shading - 对每个 vertex 着色
3. Phong Shading - 对每个Fragment着色

其实也可以在Vertex Shader中做着色，本质上是算出了每一个Vertex 的颜色。

## Opengl

两种管线：可编程、不可编程

这个图的2和3步是不是反掉了，

> ​![Rendering Pipeline Flowchart](https://www.khronos.org/opengl/wiki_opengl/images/RenderingPipeline.png)
>
> [https://www.khronos.org/opengl/wiki/File:RenderingPipeline.png](https://www.khronos.org/opengl/wiki/File:RenderingPipeline.png)

​![image](assets/image-20230908140825-xihblgg.png)​

需要注意看清楚各个阶段都是啥。

1. buffer：position、attributes

    1. 也有 uniform buffer：存储全局数据
2. vertex shader：投影计算，法向量变换、归一化、逐顶点的光照

    按照Opengl的流水线，后面还有两个可能的，可编程的着色器：

    1. Tessellation：曲面细分
    2. Geometry Shader：输出更多图元
3. 图元装配：之前的计算都只是对于顶点操作的，不设计到点之间的拓扑关系

    > 其实OpenGL 网站上写的很清楚：Primitive assembly takes the vertex stream and converts it into a sequence of primitives, in accord with the [Primitive](https://www.khronos.org/opengl/wiki/Primitive "Primitive") type specified in the rendering command. Primitives can also be discarded at this point, to allow transform feedback without rendering anything.
    >

    1. 生成图元，点、线、三角面都在这里生成
    2. 面剔除在这个阶段发生
    3. 其实OpenGL的Culling是分阶段的，现在是认为装配后再进行culling，这里的culling主要是上面提到的面剔除和这里的视锥体对应的剔除
    4. Viewport Transform：ndc ⇒ viewport，这个是通过`glViewport`​指定的
    5. Perspective Divide：透视除法
4. 光栅化（Rasterization）没啥好说的，这个是硬件实现的，它的英文也很简单易懂

    所有的数值都是线性插值出来的

    输入是图元，输出是片元

    **Rasterization** is the process whereby each individual ****​**​ is broken down into discrete elements called** [Fragments](https://www.khronos.org/opengl/wiki/Fragment "Fragment"), based on the sample coverage of the primitive.
5. 片元着色器，从片元输出颜色

    它的输出不是直接的像素，因为一个像素可能会有多个fragment决定（Blending）
6. Framebuffer，也就是OpenGL的Per-Sample Processing：

    这里实际上就直接要从片元数据决定像素了

    这里也进行纹理映射 -- sampler，纹理坐标是从buffer中一路传过来的

    1. [Scissor Test](https://www.khronos.org/opengl/wiki/Scissor_Test "Scissor Test")
    2. [Stencil Test](https://www.khronos.org/opengl/wiki/Stencil_Test "Stencil Test")
    3. [Depth Test](https://www.khronos.org/opengl/wiki/Depth_Test "Depth Test")
    4. [Blending](https://www.khronos.org/opengl/wiki/Blending "Blending")
    5. [Logical Operation](https://www.khronos.org/opengl/wiki/Logical_Operation "Logical Operation")
    6. [Write Mask](https://www.khronos.org/opengl/wiki/Write_Mask "Write Mask")

其实也没有很复杂对吧！但你要注意每个阶段的输入输出是啥，例如像素是在最后阶段才被决定的，并不是从fragment shader出来就是像素。

其实这里ppt讲的就不太对了，后面的混合啥的都是不可编程的阶段，和FS无关了。

逐片元操作的一些应用：

1. 隐藏面消除、阴影绘制
2. 模版缓存 - multipass
3. 混合 -- 透明物体
4. 多重采样、MSAA之类的

下面我们主要讲一下光照模型

## 光照

其实就是fragment shader怎么写

Phong 模型：三部分，其中前两个还需要注意距离光源远近

1. diffuse：漫反射只需要考虑这个物体接受了光源多少光，所以是$\langle l, n\rangle$
2. specular：高光是和$\langle reflect(l,n), v\rangle$相关的，通常还需要变成$\alpha$次方的操作；
3. ambient：没啥好说的，固定值 * 材质

看下答案：

$$
\begin{cases}I_{d}=kI_{l}\langle l,n\rangle\\ I_{s}=k_{s}I_{l}\langle r,n\rangle\\ I_{a}=k_{a}I_{a}\end{cases}
$$

​![image](assets/image-20230908150342-c71tr0z.png)​

Blinn-Phong：其中比较难算的是$r$向量，可以用

$$
n \cdot h \approx v\cdot r,\quad h = \mathrm{norm}(l+v)
$$

来近似。

不难观察出$r\cdot v$得到的角和$n \cdot h$得到的角是两倍的关系。

## 纹理映射

三种映射方法：

1. 纹理映射
2. 环境贴图
3. 凹凸贴图

参数坐标-纹理坐标-世界坐标-屏幕坐标

​![image](assets/image-20230908151612-wofd1fq.png)​

基本问题：如何定义映射

### MipMap

产生摩尔纹：

* 远处的一个像素覆盖纹理上的一个很大的区域，不能直接采样一个点的颜色。
* 近处呢？

### OpenGL中的纹理

三个步骤：

1. 指定纹理
2. 每个顶点赋予纹理坐标
3. 纹理参数

gl自带了mipmap的生成。

### 环境映射

球面映射、立方体映射

### 凹凸贴图

​![image](assets/image-20230908153320-pcftm3n.png)​

## 真实感渲染

终于到RayTracing了。

### 复习：Local Shading Model

不足：

1. 过于简化的反射模型 -- 复杂材质怎么办？
2. 间接反射光？
3. 阴影？

### 全局光照

#### BRDF

几个参数？3+2+2

描述了啥？某个位置上，从入射方向打来光，对给定方向射出多少

#### Radiance - 辐射率

5d函数，描述了物体$x$位置，向$w$射出的能量

#### 渲染方程

Out = Emit + Reflect

$$
L(x, w) = L_e(x, w)+\int_{w_i} L_i (x, w_i) f(x, w_i \to w)\langle n_x, w_i \rangle dw_i
$$

Really Important!

### 求解渲染方程

递归过程！

## Ray Tracing

反向追踪：从像素透射出光线

### Ray casting

假设光线只反弹一次。

打出去一条线，找chit，然后看是否被遮挡。

这个只能处理阴影！

### （Whitted-Style）Ray Tracing

这个是递归的，打到的时候做两件事：

1. 看光源，如果不被遮挡就做Shading
2. 在镜面反射方向继续打出一条光，递归该过程

终止条件：

1. rmiss → 背景光强
2. 递归步数限制

来默写一下这个算法：

```python
def rtrace(ray, step):
  if step > max_step:
    return zero
  r = scene.query(ray)
  if rmiss:
    return bg_color
  elif light:
    return light_color
  else: # chit
    local = phong_model()
    reflect = trace(reflect_ray, step + 1)
    transmit = trace(transmit_ray, step + 1)
    return local + reflect + transmit
```

效率：

1. 求交 - 空间数据结构加速

## Path Tracing

上面并没有求解渲染方程。

1. 只算了至多三条光路：直接到光源的、镜面反射、折射
2. 就算考虑多条光路呢？没用，phong模型要换

如何求，直接给出最终算法！

Path Tracing：蒙特卡洛积分！

* 一个像素 → N个光线
* 每个光线生成1条光路，着色
* N条平均

像是光的粒子性，我们考虑一个光的粒子是如何来到眼睛里的。它撞到表面上就会随机得向一个方向反射。

蒙特卡洛积分的原理是：设计一个随机变量$X$，概率密度为$p$：

$$
E[I] = E[f/p] = \int f/p \cdot pdx=I
$$

### PT 的具体算法

先把这个算法简单实现一下：

```py
def shade(p, wo):
  direction = random_direction(wi_PDF)
  trace(p, direction)
  if light:
    return L_i * fr * cosine / pdf(wi)
  elif chit:
    return shade(hit, -wi) * f_r * cos / pdf(wi)
```

never stop？

1. RR，注意添加存活概率为$p$的RR后，要让输出都除以$p$，保持期望不变
2. 添加最大递归次数

最后一个问题！直接采样效率太低了，光源要单独拿出来采样。

分开直接光照和间接光照，直接光照不用递归。

本质上`shade(p, wo)`​只是在求解给定点`p`​对方向`wo`​的出射光的密度

关键是，这里需要在光源x'采样和球面x采样上做一个转换：

$$
\cos\theta\mathrm{d}A=\|x-x^{\prime}\|^2dw
$$

```py
def light_sample(p, wo):
  Uniformly sample the light, pdf = 1/A
  L_dir = L_i * f_r * cos theta cos theta2 / |x - p|**2 / pdf_light

def trace(p, wo):
  RR()
  L = light_sample(p, wo)
  ray = random(pdf)
  query(ray)
  if rhit:
    L += shade(q, -wi) * f_r * cos / pdf(wi) / P_RR
  return L
```

## Radiosity 辐射度渲染法

假设大家都是理想的漫反射表面，Render Eq：

$$
L = L_e + K L
$$

K是一个积分算子，线性，那么就是稀疏矩阵

$$
(I-K)L=L_e \implies L = (I-K)^{-1}L_e =(I + K + K^2+ \cdots) L_e
$$

好处：快

缺点：不是漫反射咋办。

## Real time Rendering

主要都是些前沿的技术了

1. 光照贴图
2. 阴影贴图
3. 预计算

原理上都是以存代算

## 变换

没啥好说的，道理我都懂，但是我选择背书。

## CAGD

Nurbs
