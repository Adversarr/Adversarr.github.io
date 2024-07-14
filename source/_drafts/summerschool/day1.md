## Day 1: AIGC

### 基于 AIGC 的三维建模

三维模型
: 离散/连续的数学表达 -> 静态或者动态的三维物体/场景

1. 离散：点线面
2. 连续：参数表达、隐式表达
3. 动态：骨骼蒙皮
4. ……

**应用**

1. 渲染、可视化
2. 游戏、影视
3. 设计
4. XR：教育、交互

**建模的常见方式**

1. 手工、扫描重建：多视图重建（算法：SFM、MVS）
2. CAD建模+网格建模： 常见的软件，例如Solidworks、Blender，从简单形体进行网格变形和交并补差
3. 雕刻建模：例如 ZBrush，很复杂，基于网格细分。
4. 动态建模：例如 Daz3D，XGen，Simulation
5. 草图建模：CATIA、BendSketch，可以通过图像的勾勒然后映射到3D。（类比素描），Google Tilt Brush（VR）

**文字、图像驱动的三维建模**

1. 文字驱动：Dream Diffusion，语义很难做，比如人骑在马上，合理的建模是需要按Part，而不是直接输出一个大的网格。
2. 图像驱动：输入是图像（One-2-3-45++ CVPR 2024）

**数据驱动的微结构建模**

**发展趋势**：

1. 真实世界->虚拟建模
2. 几何建模->结合物理特性、仿真
3. 复杂的交互->简单的（VR、草图、语言）
4. 严重依赖于创造者的丰富经验->结合人工智能和机器学习

**什么是好的建模？**

1. 交互：简化原有的交互方式、精确控制和及时反馈
2. 质量：对齐原有的建模标准，兼容常见的建模流程、新的工作流、解决现有的困难问题

**数据：非常重要**

- 图像数据：10^10 级别进行训练
- 文本数据：10^12 级别

三维物体，10^7，仍然在扩充，必要性。

数据：（例如ABC）

1. 简单的：类型、几何、纹理、结构、多视图（深度图、法向图、……）
2. 网格拓扑：规则性
3. 运动方式，(PartNet Mobility)
4. 文字描述
5. Brep（边界表示）信息：点、曲线、曲面片
6. 构造信息：CAD的构造序列。
7. 特征信息：特征线、离散化、网格

### Introduction to Generative Model.

Task 1: Image Classifier

1. Linear Classifier：CIFAR10,~90%
2. Neural Network：MLP

#### Auto Regressive

Explicit Density Estimation.

目标：$p(x) = f(x, W)$

极大似然估计：$\max \sum_i \log p(x_i)$

假设$x = (x_1, ..., x_T)$，用链式法则。

$$
p(x) = p(x_1) p(x_2 | x_1) ...
$$

如果是图像生成：每次生成一个pixel。

例如，Casual CNN, RNN

Pixel CNN/RNN.

ImageGPT: 图像->序列->分类/回归

#### VAE

Auto Encoder. Not a generative model:

Reparameterization trick: $z = \mu_x + \sigma_x + \delta$, 可能会带来退化问题，需要进行正则化

VAE: KL Loss

VAE: Auto Encoder + latent space has good properties that enable generative process.

In diffusion: 将Input Image压缩到低维空间

#### GAN

Generate uniform random numbers. 传统的计算机：

$$
U_n = (a U_{n-1} + c) \mod m
$$

生成别的分布：$X = F^{-1}(U)$

- 其中的$F$ 是累积概率分布函数。

我们希望得到图片的分布。

$$G: U \to X$$

就是这样的$F^{-1}$。

但是$F^{-1}$是未知的，只能得到其中的采样。于是添加一个判别 $D$，然后相互对抗。

常用的：DCGAN、StyleGAN

#### Diffusion

扩散模型：经典的是DPPM

1. 前向：添加噪声，得到搞死
2. 反向：去噪声

Stable Diffusion.

### 三维表示和三位编码

#### 背景

1. CG-GC.
2. 关键因素：REAL:
  1. Photo Realistic
  2. Efficient
  3. Scalable
  4. Low cost

主要的技术手段：重建、创作。

发展趋势：
样条--点云--三角网格--Implicit Field--NERF--Gauss Splatting.

局限性：
- 经典图形：几何、物理
- 神经：加上数据。

#### 神经辐射场

核心：给定位置，预测某个属性，用某种方式渲染。

基本原理：

- 体渲染。
- 多视角一致性

NeRFactor: 建立NeRF到BRDF的关系。

- 但是几何仍然不可靠。

SDF：符号距离场。 -> NeuS

DE-NeRF 推广到整个场景上。

#### Gauss Splatting

Mip-Splatting：滤波器，采样定理。

#### Future work

透明物体、复杂拓扑。

重建、增强。

挑战：加速、空间时间、设备。

## Day 1 Afternoon

### Tiantian Liu ：基于二维先验的生成模型。

#### 路径分叉：原生三维方法/二维升维方法

原生：替换2D pipeline，重用。

- 表达：Pixel->voxel/point cloud/occupancy grid (with Octree) etc.

**原生的2D->3D**

3D Gan(by MIT csail)

**3D Data**：数据数量差距悬殊

- Objaverse: 800K, XL 10M
- 但是：ImageNet: 1.3M, LAION 5B

*数据质量：也是一言难尽。*

同时期，2D/3D Diffusion 模型差距很大。

Idea：2D很强，能不能用在3D里面。

**升维**：3D 重建就是2->3升维
- 2D 模型具有一定的 3D 能力。

基本框架：
- Differentiable Representation + Renderer -> 2D Diffusion
- 然后修正得到

问题：如何从一个清晰的输入中拿到演化梯度。

> 找到连接不同维度网络的适配器来进行梯度回传

#### 分数蒸馏采样（Score Distillation Sampling, SDS）：连接扩散模型的适配器

DreamFusion

后续：

1. Magic3D
2. ProlificDrimer
3. LucidDrimer：利用DDIM Inversion加噪，而不是 $z_t = \alpha_t z + \sigma_t \epsilon$
4. DreamGaussian
5. GSGen：使用SDS同时连接 SD 和 Shape-E 的扩散网络

衍生工作的问题：

1. 多脸问题：视角控制
2. 速度问题：
  1. 可微表达不够快
  2. 优化迭代数目要求高

#### 消除二面怪：视角一致性

**Zero-1-to-3[Liu 2023]**

- 基于 Pretrained SD 来进行 Finetune
- 基于图片和相机信息进行conditioning
- Objaverse
- SDS

**MVDream[Shi 2024]**

问题：表面破洞

#### 二位中的三维信息：2.5D 先验的应用

> 例如 Normal Map/Depth Map

Canonical Coordinate Maps(CCM)：在二维图片上提供3D信息。

例如：**SweetDreamer[Qiu et al. 2024]**

**Rich Dreamer[Qiu et al. 2024]**：

- 重新train了text conditioned Normal Depth Diffusion model.

**Wonder3D[Long et al. 2024]**：

- LVIS finetune出生成 normal 的能力

### 一把梭哈行不行：从优化模型到前馈模型

**Large Reconstruction Model(LRM) [Hong et al. 2024]**

Image -> Triplane Forward Model.

力大砖飞。

- 正面很好，但是背面不一定。

**Large Multi-view Gaussian Model (LGM) [Tang et al. 2024]**

- 不需要拼一个NeRF，可以做Gaussian

**Mesh LRM[Wei et al. 2024]**

- 输入不再是单视角，改为多视角图片。

**Instant Mesh[Xu et al. 2024]**

- 和 MeshLRM 相似的流水线，利用多视角进行。

> meshy.ai

