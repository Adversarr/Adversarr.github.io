# Day2

## Optimization Time Integration for Solids and Fluids
by Minchen Li, CMU, AP

基于数值优化的物理仿真框架。

主要是Fundamental Theory.

**Computer Graphics: Creating Realistic Visual Effect via Computing**

离散集合体(Geometry) -> 材质（Appearance）-> 动画（Animation）

这里用的是 DOT 的图片。

**Animation**：
1. Key Frame Animation：关键帧、插值
2. Skining Animation：蒙皮，给出关键位置，方便艺术家创作
3. Physics Based Animation：直接通过PDE，计算受力、然后做时间积分。自动化程度更高。

> 这里PBA用的是IPC、CIPC、SPH的几张插图。
> 1. SPH: A Contact Proxy ...

**Physics Based Animation**：
依然有很多不同的现象。

1. 刚体、cloth、弹性体
2. 沙子、水：这里用的是SPH

**Optimization Time Integration**: Reliable Simulation Approach based on Numerical Optimization

> 用的是DOT的图片，拉伸一个Armadillo

### Distortion Minimization
Minimize 新的形状和旧的形状的差别。得到更加smooth的形状。

**Spatial Discretization**: 离散化
1. Tetrahedralize. 四面体网格、八面体网格、六面体
2. 然后表达成一个 $x\in \mathbb R^{3n}$

> 这里用的是 Minchen 博士论文的图片。

**Measure Distortion Locally**：

Rest Pose -> Deformed Space
1. Deformation Gradient：得到 3x3 的 Transformation 矩阵（Affine 矩阵的左上三角）
2. Distortion Energy：这里展示的ARAP能量，Isometric ARAP，做SVD矩阵，然后找Fro norm

然后做积分（对应离散的就是求和），加权为体积。

**Mesh deformation via Distortion Minimization**：

假设需要进行局部的形变。

Move the anchors to the target and only optimize for free variables => Unconstrained Optimization.

**Newton's Method for Distortion Minimization**:
$$
g(x) = \nabla E(x)
$$

> 这边放的图应该是他在CMU的手写课件。

Higher Dimensions:
$$
x^{i+1} \leftarrow (\nabla g(x^i))^{-1} x^i
$$

问题：需要初始解接近真实解，Overshooting Problem -> Numerical Explosion

需要一个鲁棒的方法
1. Line search
2. Projected Newton，投影Hessian 到 SPD

Pseudo-code:
```python
x = x0
while not converged:
  P = make_spd(Hessian(E(x)))
  p = solve(P, gradient(E(x)))
  x = linesearch(x, p)
```

> 其实是很经典的Pipeline：Refer to "Dynamic Deformables: ..."

**Examples**: 展示了几个2D和3D的例子。

### Elasto dynamics Simulation via OTI

**Adding Dynamics**：

1. Distortion Minimization：Distortion Only
2. Elastodynamic Simulation：Distortion + Inertia term

**Governing Equation**：

Spatial Discrete，Generally Continuous Term（半离散格式）
$$dx/dt = v \quad M dv/ dt = f$$

For now, assume mass matrix is *Lumped*, i.e. Diagonal. (incorrect for FEM apps.)

**时间离散化**：Forward Difference(Explicit RK1, Forward Euler)

隐式方程：Backward in time.
$$
x^{n+1} = x^n + \Delta t v^{n} + \Delta t^2 M^{-1} f^{n+1}
$$

Solve for $x^{n+1}$

Why not explicit?
1. explicit：Require Time step size very small, 或者直接不稳定。
2. Symplectic Euler
3. Implicit Euler: 稳定性，添加Damping，看起来没有很大的扰动。

**Optimziation Time Integration**：minimize the incremental potential.

把解方程变成解一个Optimization Problelem.

### Case Study: Mass Spring System

**Mass spring Representation of Solids**：Mass particles connected by springs.

这个很basic。

**Incremental Potential**: 
1. Inertial，Mass Matrix：无论是Lumped的形式，还是原本FEM的形式，都是SPD的。
2. Elasticity：

$$
l^2 \frac12 k \left( \|x_1 - x_2\| / l - 1 \right)^2
$$

avoid computing square root.

$$
P_e(x) = l^2 \frac k 2 \left( \|x_1 - x_2\|^2 / l^2 - 1 \right)^2
$$

果然还是推广了一下和蒋老师的book：https://github.com/phys-sim-book/phys-sim-book.github.io

### More Topics on Optimization Time Integration

Self-Contact：Incremental Potential Contact, 2020.
- 内点法+Barrier

Thin Objects: Codimensional IPC
- Stretch + Bend, Surface Mesh.

Nearly Rigid Effects: Rigid IPC/ABD
- Not care about tiny deformations: Simply track rotation/affine transformation $Q$.
- ABD: Translation is linear, Rotation is non-linear.

Fluid: SPH, MLS, "A Contact Proxy Splitting Method for Lagrangian Solid-Fluid Coupling"
- Penalize the volume.
- Weakly compressible.

Summary: Opt Time Integration. reliable and versatile Phys based Simulation.

1. Improving efficiency scalabiltiy
2. Incorporating path dependent effects.
3. Applications to down stream applications, RL, etc.

## Deep Learning for Physics Simulation
By Tao Du, Tsinghua Univ IIIS

The complexity in simulation physical systems.

水渑在水面上，通过动量传输向前跳。CG、计算物理，CFD中，计算设计，仿真机器人。

翅果。Passive 无人机，单叶片无人机。


物理现象比较难建模。技术上的挑战。

几个想法：
1. 第一性原理出发，FEM、F = ma，直接建模
2. 不一定能直接建模，但是参数很难做，NS很准，但是参数等等都需要测量、准确 -> Learning, Data Driven.

Today：结合的套路是什么？

### A standard physics simulation pipeline: No Learning

**Step 1: Identifying the physical model.**
Identify continuous PDEs.

Cauchy Momentum Equation:
$$\rho a(X, t) = \nabla^X \cdot P(X, t) + \rho g(X, t)$$

**Step 2: Numerical Discretization**

Transfering them to discretized PDEs.

通常，不是ODE（Rigid body simulation的情况），弹性体，最常见的是FEM

**Step 3: Time Integration**
Solving discretized PDE along the time axis.

和 Minchen 的一样的。

But, How can ML be of help?

Today: Focus on Physical Model / Time Integration.

### Physical Model

#### NCLaw

Building digital twins is important: VR/AR, Autonomous Vehicles, Game, ...

Previous Solutions: *Motion capture*
1. pros: simple & precise
2. cons: expensive, non-physical

*System Identification* (System Id)
1. Pros: Data driven, physics based
2. Cons: domain knowledge, single physics：模型选择的错误会导致最终结果很差

*Graph NN*
1. Pros: Data-driven, General
2. Cons: Expensive training, non-physical

**Example**: 面团，有弹塑性形变。

**Technical Overview**：挑战在于，不知道本构模型。

于是：Neural Elastic Law，

- 很多内容，已经被刻画很好，比如 $F=ma$，不需要用Learning来学，（不需要从一个MLP+数据学出来）
- 建模困难的点：上数据，从数据中获得。

**Physics Aware Network Architecture**：
1. Rotation Equivariance：Polar Decomposition.
2. Undeformed State Equilibrium

#### Fast Aquatic Swimmer ...

Motivation: Fast differentiable simulator for fluid and soft-body coupling.

机器鱼。

Main Idea：固体很简单，但流体算的很慢。

Hydro Net -> Fluid Simulation

Idea：不需要非常非常准，但是需要定性的视角下是可靠的。

### Time Integration

#### Learning Preconditioners for Conjugate Gradients

Our focus: Sparse SPD matrices.

Numerical Optimization. 

Mature solutions:
1. Cholesky,
2. CG or GMRES, ...

Time decomp:
1. CG solver ~ 60%
2. Linesearch ~ 20%
3. Hessian Projection, ~ 15 %
4. Other...

**Nerual Network**: Mesh Graph Net.

特色：Fast but Inexact

**CG, Cholesky**：hmm，解10000次，但10001次也不会更好。

**First Inspiration: Preconditioning.**

A good preconditioner give *fast approximations of solutions*：比较像原本的东西，但是很快，不用很准，NN!

that is: An end-to-end NN gives fast approximation of solutions!

**Examples**：Heat, Wave, Poisson.

Summary: Understand the strength of NN to use them with a reason.

**Discussion**:
1. when should we use physics?
2. when should we use ML?

应用层面上讲，到底多在乎准/快，还是其他的指标，这决定了最终的算法。

My question:
1. data is important
2. scalability law. higher DOF, demands more data, larger Neural Network
3. Any Trick?

## Forward and Inverse problems in Fluid Animation

Stress and Strain.

Compressibility.

Non-Newtonian Fluids

Frame of reference: Lagrangian or Eulerian.

Lagrangian Method for CFD:
1. FEM: Remeshing strategy & Noticeable Artifact
2. SPH: Complex Boundary Dynamics & Multiple phase flows.

Eulerian Specification.
- divide into volume cells.
- large deformations such as those occurring in fluid motion.

Hybrid method:
1. ALE: Arbitary Lagrangian-Eulerian Method
2. PIC, FLIP.
3. MPM

混合SPH和Level Set、LBM

Gas Condensation with heat transfer.

Unified simulation framework. 同时处理材料不同的情况


### Inverse Modeling

Fluid Control, PDE correction.

# Day2：Afternoon

## 徐昆：基于物理的可微渲染

可微渲染的定义：给定场景参数$\theta$，包括几何、材质、光源参数，生成对应的渲染图像 $y$。
$$y = f(\theta)$$

导数是*存在的*。

拼成一个向量。

- 内部导数：比较好算，比如用重心坐标；
- 边界导数：难算一些


Application:
1. 逆向渲染：输入目标渲染图像，找$\theta$
2. AI+图形学：场景参数可以是显式表示，甚至是Neural

分类：
1. 可微光栅化
2. 可微的光线追踪：Mitsuba, PBRT, LusiaRender(By tsing hua)
3. 神经渲染：NeRF, 3DGS

主要挑战：
1. 边界不连续性：边界导数
  - 很多时候真正有用的是边界导数而不是内部导数！

解决方法：模糊化，
1. Soft Rasterizer, PyTorch3d：设置透明度
2. N3MR：后处理模糊化
3. Nvdiffrast：在抗锯齿阶段进行边界位置判断。

### 可微 光线追踪

可微光栅化，可微分光线追踪：提高生成质量。

Trival Idea：交换积分和导数的顺序。Not Correct. 因为f不连续。

不连续函数求导：雷诺传输定理。

更多内容：Dr.Jit, Mitsuba 3，高效采样，信息复用。

失败情况：边界导数是稀疏的，且是局部、间接的。

### 拉格朗日视角

光栅化：借鉴流体模拟。最优传输匹配。更加鲁棒一些。

Loss: L2 -> Optimal Transport Loss.

光线追踪：类似的，但是要考虑复杂光路。

光子映射

值得研究的问题：
1. 计算效率
2. Optimization的鲁棒性：初始值要比较好。 

Idea：
1. Far away from you solution: the "simulator" can have large error.
2. Near solution, must have small error!

## PKU 李胜：真实感渲染的路径

Background：全局的光照渲染

基本原理：路径积分。


