---
title: "Lecture06 随机向量的分布(II)"
tags:
  - 概率论
  - 前半学期
  - 随机向量
  - 条件分布
  - 连续型
---

# Lecture06 随机向量的分布(II)

> [!ABSTRACT] 本讲概要
> 上一讲处理了离散型随机向量，这一讲把"联合—边缘—独立性"这套语言推广到**连续型随机向量**：联合密度取代分布列，积分取代求和。随后引入**条件分布**——已知一个变量的取值后，另一个变量的分布如何更新，这是后续条件期望、贝叶斯方法的地基。
>
> 参考教材：Bertsekas & Tsitsiklis Ch2 2.6, Ch3 3.4, 3.5。
>
> ---

## 一、连续型随机向量及其分布

### 1.1 复习：随机向量（定义3.1）

> [!NOTE] Review（定义 3.1，n维随机向量）
> 如果$X_1,\ldots,X_n$都是概率空间$(\Omega,\mathcal{F},\mathbb{P})$上的随机变量，称$\mathbf{X}=(X_1,\ldots,X_n)$是概率空间$(\Omega,\mathcal{F},\mathbb{P})$上的**n维随机向量**，简称随机向量。

**直觉**：随机向量就是"同一个样本点$\omega$同时输出$n$个数"，即从样本空间到$\mathbb{R}^n$的映射，各分量共用同一个随机性来源。

### 1.2 联合概率密度（定义1.1）

> [!IMPORTANT] 定义 1.1（连续型随机向量）
> 设$\mathbf{X}=(X_1,X_2,\ldots,X_n)$是随机向量。如果存在$\mathbb{R}^n$上的非负可积函数$f(x_1,\ldots,x_n)$（或记$f(\mathbf{x})$），使得对$\mathbb{R}^n$的任何子立方体
>
> $$D=\{(x_1,x_2,\ldots,x_n)\mid a_i<x_i\leq b_i,\ 1\leq i\leq n\}$$
>
> 有
>
> $$\mathbb{P}(\mathbf{X}\in D)=\int_D f(x_1,x_2,\ldots,x_n)dx_1 dx_2\cdots dx_n:=\int_D f(\mathbf{x})d\mathbf{x}$$
>
> 就称$\mathbf{X}$是**连续型随机向量**，并称$f(x_1,\ldots,x_n)$（或$f(\mathbf{x})$）是$\mathbf{X}$的**联合概率密度函数**，简称为联合密度或概率密度。

**直觉**：一维密度是"单位长度上的概率"，联合密度是"单位体积上的概率"——$\mathbf{X}$落在小立方体里的概率约等于密度乘以体积。

> [!IMPORTANT] 定理 1.1（常用）
> 对任意n维Borel集$B$有
>
> $$\mathbb{P}(\mathbf{X}\in B)=\int_B f(\mathbf{x})d\mathbf{x}$$

定义里只要求对"立方体"成立，定理把它升级到一切Borel集（直观上即一切"合理"的区域）。由于$\mathbb{R}^n$本身是Borel集，立刻得到**归一化**：

$$\int_{\mathbb{R}^n}f(\mathbf{x})d\mathbf{x}=\mathbb{P}(\mathbf{X}\in\mathbb{R}^n)=1$$

### 1.3 工具：Fubini定理（定理1.2，会使用、不要求证明）

> [!IMPORTANT] 定理 1.2（Fubini）
> 设$D$是$\mathbb{R}^n$上的子区域，$\varphi(\mathbf{x})$是$D$上的非负函数或绝对可积函数（指取绝对值后积分有限），则对区域$D$上的n重积分
>
> $$\int_D\varphi(\mathbf{x})d\mathbf{x}$$
>
> 可以进行累次积分计算，且积分的次序可以交换。

**直觉**：算体积时"先横切再竖切"和"先竖切再横切"答案一样——前提是被积函数非负或绝对可积。本讲所有"先对$y$积分再对$x$积分"的操作都靠它撑腰。

---

## 二、边缘密度

### 2.1 二维情形（例1.1）

> [!NOTE] 例 1.1（二维边缘密度公式，常用）
> 设$(X,Y)$有联合密度$f(x,y)$，则$X$与$Y$分别有概率密度
>
> $$f_X(x)=\int_{-\infty}^{\infty}f(x,y)dy,\quad f_Y(y)=\int_{-\infty}^{\infty}f(x,y)dx$$

**直觉**：把不关心的那个变量"积掉"。几何上（课件第9页图）：边缘密度$f_X(x)$的高度＝联合密度曲面在$x$处切片的面积。

### 2.2 一般情形（定义1.2、例1.2）

推导思路（课件第10页）：设$f(\mathbf{x})$是$\mathbf{X}$的概率密度，对$1\leq k<n$，令$\mathbb{R}^k$中的子立方体$D_k=\{(x_1,\ldots,x_k)\mid a_i<x_i\leq b_i,1\leq i\leq k\}$，定义

$$D_k\times\mathbb{R}^{n-k}=\{(x_1,\ldots,x_n)\mid(x_1,\ldots,x_k)\in D_k,\ (x_{k+1},\ldots,x_n)\in\mathbb{R}^{n-k}\}$$

则由定理1.1和Fubini定理：

$$\mathbb{P}\big((X_1,\ldots,X_k)\in D_k\big)=\mathbb{P}\big(\mathbf{X}\in D_k\times\mathbb{R}^{n-k}\big)=\int_{D_k}\left\{\int_{\mathbb{R}^{n-k}}f(x_1,\ldots,x_n)dx_{k+1}\cdots dx_n\right\}dx_1\cdots dx_k$$

花括号内的函数正好充当$(X_1,\ldots,X_k)$的密度，于是有：

> [!IMPORTANT] 定义 1.2（边缘密度、边际密度）
> 被积函数
>
> $$f_k(x_1,\ldots,x_k)=\int_{\mathbb{R}^{n-k}}f(x_1,\ldots,x_n)dx_{k+1}\cdots dx_n$$
>
> 是$(X_1,\ldots,X_k)$的联合密度，被称为$\mathbf{X}$的**边缘概率密度函数**，简称为边缘密度。

> [!NOTE] 例 1.2（任意子向量的边缘密度）
> 设$f(\mathbf{x})$是$\mathbf{X}$的概率密度，则任意子向量$(X_{j_1},X_{j_2},\ldots,X_{j_k})$的边缘密度为
>
> $$g_k(x_{j_1},x_{j_2},\ldots,x_{j_k})=\int_{\mathbb{R}^{n-k}}f(x_1,\ldots,x_n)dx_{j_{k+1}}\cdots dx_{j_n}$$
>
> 即对不保留的那$n-k$个分量积分，分量不必是"前$k$个"。

> [!EXAMPLE]- 例题 1.3：单位圆内均匀分布的边缘密度
> 设$(X,Y)$在单位圆$D=\{(x,y)\mid x^2+y^2\leq 1\}$内均匀分布，求$X$、$Y$的概率密度。
>
> **解**　$(X,Y)$的联合密度为
>
> $$f(x,y)=\frac{1}{\pi}I_D(x,y)$$
>
> （注：此步补全了归一化常数的来源——单位圆面积为$\pi$，均匀分布密度＝$1/$面积。）
>
> $X$只在$[-1,1]$中取值。对$|x|\leq 1$：
>
> $$f_X(x)=\int_{-\infty}^{\infty}f(x,y)dy=\frac{1}{\pi}\int_{-\infty}^{\infty}I_{\{x^2+y^2\leq 1\}}dy=\frac{1}{\pi}\int_{-\infty}^{\infty}I_{\{|y|\leq\sqrt{1-x^2}\}}dy$$
>
> 内层是长度为$2\sqrt{1-x^2}$的区间上的积分（注：此步补全了——固定$x$时$y$的取值范围是$[-\sqrt{1-x^2},\sqrt{1-x^2}\,]$），故
>
> $$f_X(x)=\frac{2}{\pi}\sqrt{1-x^2},\quad |x|\leq 1$$
>
> 同理可得$Y$的密度$f_Y(y)=\dfrac{2}{\pi}\sqrt{1-y^2}$，$|y|\leq 1$。

> [!WARNING] 易错
> 二维均匀分布的边缘**不一定**是均匀分布——本例中$X$的边缘密度是半圆形的，中间高两边低。"联合均匀"只保证概率与面积成正比，切片长度随$x$变化时边缘就不均匀了。

---

## 三、连续型随机向量的独立性

### 3.1 二维判别（定理1.3）

> [!IMPORTANT] 定理 1.3（二维独立性判别，常用）
> 设随机变量$X,Y$分别有概率密度$f_X(x),f_Y(y)$，则$X,Y$相互独立的充分必要条件是随机向量$(X,Y)$有联合密度
>
> $$f_X(x)f_Y(y),\quad (x,y)\in\mathbb{R}^2$$

**直觉**：独立＝联合密度可以"按变量拆成乘积"，两个方向互不干涉。

**证明思路**：
- （$\Leftarrow$）若$f_X(x)f_Y(y)$是联合密度，对任意$(x,y)\in\mathbb{R}^2$，用Fubini把二重积分拆开：

$$\mathbb{P}(X\leq x,Y\leq y)=\int_{-\infty}^{y}\int_{-\infty}^{x}f_X(t_1)f_Y(t_2)dt_1dt_2=\int_{-\infty}^{x}f_X(t_1)dt_1\int_{-\infty}^{y}f_Y(t_2)dt_2=\mathbb{P}(X\leq x)\mathbb{P}(Y\leq y)$$

故$X,Y$相互独立。
- （$\Rightarrow$）若$X,Y$相互独立，对$\mathbb{R}^2$的任何长方形$D=\{(x,y)\mid a_1<x\leq b_1,a_2<y\leq b_2\}$，利用Fubini定理：

$$\mathbb{P}((X,Y)\in D)=\mathbb{P}(a_1<X\leq b_1)\mathbb{P}(a_2<Y\leq b_2)=\int_{a_1}^{b_1}f_X(t_1)dt_1\int_{a_2}^{b_2}f_Y(t_2)dt_2=\int_D f_X(t_1)f_Y(t_2)dt_1dt_2$$

这正是联合密度的定义式，因此$f_X(x)f_Y(y)$是$(X,Y)$的联合密度。

### 3.2 n维判别（定理1.3的一般形式）

> [!IMPORTANT] 定理 1.3（n维独立性判别）
> 设对每个$i$（$1\leq i\leq n$），随机变量$X_i$有概率密度$f_i(x_i)$，则$X_1,X_2,\ldots,X_n$相互独立的充分必要条件是随机向量$\mathbf{X}=(X_1,X_2,\ldots,X_n)$有联合密度
>
> $$f_1(x_1)f_2(x_2)\cdots f_n(x_n),\quad(x_1,x_2,\ldots,x_n)\in\mathbb{R}^n$$

**证明思路**（与二维平行）：
- （$\Leftarrow$）对任意$(x_1,\ldots,x_n)\in\mathbb{R}^n$：

$$\mathbb{P}(X_1\leq x_1,\ldots,X_n\leq x_n)=\int_{-\infty}^{x_1}\cdots\int_{-\infty}^{x_n}\prod_{i=1}^{n}f_i(t_i)dt_1\cdots dt_n=\prod_{i=1}^{n}\int_{-\infty}^{x_i}f_i(t_i)dt_i=\prod_{i=1}^{n}\mathbb{P}(X_i\leq x_i)$$

- （$\Rightarrow$）对任何子立方体$D$，独立性给出$\mathbb{P}(\mathbf{X}\in D)=\prod_i\mathbb{P}(a_i<X_i\leq b_i)=\int_D f_1(t_1)\cdots f_n(t_n)dt_1\cdots dt_n$，故乘积函数是联合密度。

> [!TIP] 方法（密度的快速拆解，常用）
> 拿到联合密度$f(x,y)$判独立时，先看它能否写成"只含$x$的函数$\times$只含$y$的函数"，且**取值区域是矩形**（无相互牵制）。能拆即独立，归一化常数怎么分配不影响结论。

---

## 四、经典例：二元正态分布

### 4.1 标准情形：密度可拆 → 独立

考虑

$$f(x,y)=\frac{1}{2\pi}\exp\left\{-\frac{1}{2}[x^2+y^2]\right\}$$

求边缘密度（课件第19、20页）：

$$f_X(x)=\int_{-\infty}^{\infty}f(x,y)dy=\int_{-\infty}^{\infty}\frac{1}{2\pi}\exp\left\{-\frac{1}{2}[x^2+y^2]\right\}dy=\frac{1}{\sqrt{2\pi}}\exp\left\{-\frac{x^2}{2}\right\}\cdot\int_{-\infty}^{\infty}\frac{1}{\sqrt{2\pi}}\exp\left\{-\frac{y^2}{2}\right\}dy=\frac{1}{\sqrt{2\pi}}\exp\left\{-\frac{x^2}{2}\right\}$$

（最后一步用了标准正态密度的归一化，积分为1。）故$X\sim N(0,1)$；同理$f_Y(y)=\frac{1}{\sqrt{2\pi}}\exp\{-\frac{y^2}{2}\}$，$Y\sim N(0,1)$。且

$$f(x,y)=\frac{1}{\sqrt{2\pi}}\exp\left\{-\frac{x^2}{2}\right\}\cdot\frac{1}{\sqrt{2\pi}}\exp\left\{-\frac{y^2}{2}\right\}=f_X(x)\cdot f_Y(y)$$

由定理1.3，此时$X$与$Y$独立。

### 4.2 由标准化变换到一般情形

> [!NOTE] 例 2.2（Review：一元正态的标准化）
> 设$X\sim N(\mu,\sigma^2)$，密度$f(x)=\dfrac{1}{\sqrt{2\pi\sigma^2}}\exp\left\{-\dfrac{(x-\mu)^2}{2\sigma^2}\right\}$，则$Y=\dfrac{X-\mu}{\sigma}\sim N(0,1)$。

二维同理（课件第22、23页）：设$X_0\sim N(0,1)$，$Y_0\sim N(0,1)$，标准化关系

$$\begin{pmatrix}\dfrac{X_1-\mu_1}{\sigma_1}\\ \dfrac{Y_1-\mu_2}{\sigma_2}\end{pmatrix}=\begin{pmatrix}X_0\\ Y_0\end{pmatrix}\iff\begin{pmatrix}X_1\\ Y_1\end{pmatrix}=\begin{pmatrix}\sigma_1&\\ &\sigma_2\end{pmatrix}\begin{pmatrix}X_0\\ Y_0\end{pmatrix}+\begin{pmatrix}\mu_1\\ \mu_2\end{pmatrix}$$

则$X_1\sim N(\mu_1,\sigma_1^2)$，$Y_1\sim N(\mu_2,\sigma_2^2)$。**直觉**：一般二元正态＝标准二元正态经过"拉伸（乘对角阵，更一般地乘任意矩阵）＋平移"得到；课件第23页用占位符$\begin{pmatrix}***&**\\ **&***\end{pmatrix}$提示，把对角阵换成一般矩阵就得到带相关性的二元正态。

### 4.3 矩阵简写形式

二元正态密度的简写：

$$f(\mathbf{x})=\frac{1}{\sqrt{(2\pi)^2|\Sigma|}}\exp\left\{-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})'\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu})\right\}$$

其中$\mathbf{x}=(x,y)'$，$\boldsymbol{\mu}=(\mu_1,\mu_2)'$，$\Sigma=\begin{pmatrix}\sigma_1^2&\rho\sigma_1\sigma_2\\ \rho\sigma_1\sigma_2&\sigma_2^2\end{pmatrix}$，$|\Sigma|$是$\Sigma$的行列式。

对比一元正态$f(x)=\dfrac{1}{\sqrt{2\pi\sigma^2}}\exp\left\{-\dfrac{(x-\mu)^2}{2\sigma^2}\right\}$：$(x-\mu)^2/\sigma^2$被推广成二次型$(\mathbf{x}-\boldsymbol{\mu})'\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu})$，$\sigma^2$的角色由协方差矩阵$\Sigma$接管。

p维一般形式（课件第25页）：

$$f(\mathbf{x})=\frac{1}{(2\pi)^{p/2}|\Sigma|^{1/2}}\exp\left\{-\frac{(\mathbf{x}-\boldsymbol{\mu})'\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu})}{2}\right\}$$

**几何直观**：等高线是椭圆$(\mathbf{x}-\boldsymbol{\mu})'\Sigma^{-1}(\mathbf{x}-\boldsymbol{\mu})=c^2$；课件第27、28页展示了$\sigma_{11}=\sigma_{22}$时$\rho=0$（圆形等高线、对称钟形）与$\rho=0.75$（沿对角线拉长的椭圆）的曲面与等高线对比，$\rho$越接近$\pm 1$椭圆越扁。

### 4.4 二元正态的正式定义（定义1.3）

> [!IMPORTANT] 定义 1.3（二元正态分布）
> 设$\mu_1,\mu_2$是常数，$\sigma_1,\sigma_2$是正常数，$\rho\in(-1,1)$中的常数。如果随机向量$(X,Y)$有概率密度
>
> $$f(x,y)=\frac{1}{2\pi\sigma_1\sigma_2\sqrt{1-\rho^2}}\exp\left\{-\frac{1}{2(1-\rho^2)}\left[\frac{(x-\mu_1)^2}{\sigma_1^2}-\frac{2\rho(x-\mu_1)(y-\mu_2)}{\sigma_1\sigma_2}+\frac{(y-\mu_2)^2}{\sigma_2^2}\right]\right\}$$
>
> 则称$(X,Y)$服从**二元正态分布**，记作$(X,Y)\sim N(\mu_1,\mu_2,\sigma_1^2,\sigma_2^2,\rho)$。

**直觉**：五个参数各司其职——$\mu_1,\mu_2$定中心，$\sigma_1,\sigma_2$定两个方向的展幅，$\rho$定"倾斜程度"（相关性）。

### 4.5 独立 ⟺ ρ=0（定理1.4）

> [!IMPORTANT] 定理 1.4（常用）
> 设$(X,Y)\sim N(\mu_1,\mu_2,\sigma_1^2,\sigma_2^2,\rho)$，则$X,Y$独立的充分必要条件是$\rho=0$。

**证明**　不失一般性，假设$(X,Y)\sim N(0,0,1,1,\rho)$。先算边缘：

$$f_X(x)=\int_{\mathbb{R}}f(x,y)dy=\frac{1}{\sqrt{2\pi}}\exp(-x^2/2),\quad f_Y(y)=\int_{\mathbb{R}}f(x,y)dx=\frac{1}{\sqrt{2\pi}}\exp(-y^2/2)$$

（注：此步补全了——对$y$配方$\frac{x^2-2\rho xy+y^2}{1-\rho^2}=x^2+\frac{(y-\rho x)^2}{1-\rho^2}$，关于$y$的高斯积分贡献$\sqrt{2\pi(1-\rho^2)}$，恰好消去系数中的$\sqrt{1-\rho^2}$，所以**无论$\rho$取何值边缘都是标准正态**。）

因此由定理1.3，$X,Y$独立$\iff f_X(x)f_Y(y)=f(x,y)$。
- 当$\rho=0$时，直接代入有$f_X(x)f_Y(y)=f(x,y)$，故$X,Y$独立。
- 当$X,Y$独立时，在$f_X(x)f_Y(y)=f(x,y)$中取$(x,y)=(0,0)$：左边$=\frac{1}{2\pi}$，右边$=\frac{1}{2\pi\sqrt{1-\rho^2}}$，得

$$\sqrt{1-\rho^2}=1\ \Rightarrow\ \rho=0$$

> [!WARNING] 辨析
> "$\rho=0\Rightarrow$独立"是**二元正态的专属福利**。对一般分布，不相关（$\rho=0$）远弱于独立。另外，该定理要求的是$(X,Y)$**联合**服从二元正态——只有"$X,Y$各自边缘是正态"并不够。

---

## 五、联合分布与联合密度的互化

### 5.1 已知密度求分布

设$f(x,y)$是$(X,Y)$的联合密度，则联合分布函数

$$F(x,y)=\int_{-\infty}^{x}\int_{-\infty}^{y}f(u,v)du\,dv$$

当$f(x,y)$连续时，两者有关系

$$f(x,y)=\frac{\partial^2 F(x,y)}{\partial x\partial y}$$

> [!NOTE] 备注
> 随机向量$(X,Y)$的联合概率密度**不必唯一**——在零测集（如有限条曲线）上修改密度的值，不影响任何概率。

### 5.2 已知分布求密度（课件"例1.3"，编号与单位圆例重复，按课件保留）

> [!NOTE] 例 1.3（由分布函数恢复密度）
> 如果在$(x,y)$的邻域内，$\dfrac{\partial F(x,y)}{\partial x}$、$\dfrac{\partial F(x,y)}{\partial y}$、$\dfrac{\partial^2F(x,y)}{\partial x\partial y}$、$\dfrac{\partial^2F(x,y)}{\partial y\partial x}$连续，则
>
> $$\lim_{\substack{\Delta x\downarrow 0\\ \Delta y\downarrow 0}}\frac{\mathbb{P}(x-\Delta x<X\leq x,\ y-\Delta y<Y\leq y)}{\Delta x\Delta y}=\frac{\partial^2F(x,y)}{\partial x\partial y}=\frac{\partial^2F(x,y)}{\partial y\partial x}:=f(x,y)$$
>
> 即此$f(x,y)$为$(X,Y)$的联合密度函数。

**直觉**：混合偏导就是"小矩形上的概率÷小矩形面积"的极限，正是密度的本义。

### 5.3 一般化定理与反例（不要求掌握）

> [!IMPORTANT] 定理 1.5（不要求掌握）
> 设$(X,Y)$有连续的分布函数$F(x,y)$，定义
>
> $$f(x,y)=\begin{cases}\dfrac{\partial^2F(x,y)}{\partial x\partial y}, & \text{当该混合偏导数存在}\\ 0, & \text{其它}\end{cases}$$
>
> 如果
>
> $$\int_{\mathbb{R}^2}f(x,y)dxdy=1$$
>
> 则$f(x,y)$是$(X,Y)$的联合密度。

下面两个例子是更细致的讨论（课件标注非重点）。

> [!NOTE] 例 1.4（不要求掌握，略述）
> **结论**：如果$X,Y$的分布函数都连续，则它们的联合分布$F(x,y)$连续。
> **证明思路**：对$\forall(x_0,y_0)$与$\forall\epsilon>0$，取$\delta$使$|x-x_0|<\delta,|y-y_0|<\delta$时$|F_X(x)-F_X(x_0)|<\epsilon/2$，$|F_Y(y)-F_Y(y_0)|<\epsilon/2$；再用三角不等式拆分
>
> $$|F(x,y)-F(x_0,y_0)|\leq|F(x,y)-F(x_0,y)|+|F(x_0,y)-F(x_0,y_0)|\leq\mathbb{P}(x\wedge x_0<X\leq x\vee x_0)+\mathbb{P}(y\wedge y_0<Y\leq y\vee y_0)=|F_X(x)-F_X(x_0)|+|F_Y(y)-F_Y(y_0)|<\epsilon$$

> [!EXAMPLE]- 例题 1.5：联合分布连续，却不是连续型随机向量
> **结论**：存在随机向量$(X,Y)$，它有连续的联合分布，但不是连续型随机向量。
>
> **解（构造与证明）**　设$X\sim\mathcal{U}(0,1)$，$Y=X$。则$(X,Y)$有连续的联合分布函数：
>
> $$F(x,y)=\mathbb{P}(X\leq\min\{x,y\})=\begin{cases}0, & \min\{x,y\}\leq 0\\ \min\{x,y\}, & \min\{x,y\}\in(0,1]\\ 1, & \min\{x,y\}>1\end{cases}$$
>
> （注：此步补全了——$\{X\leq x,Y\leq y\}=\{X\leq x,X\leq y\}=\{X\leq\min\{x,y\}\}$，再代入$\mathcal{U}(0,1)$的分布函数。）
>
> 反设$(X,Y)$有联合密度$f(x,y)$。用$D$表示直线$y=x$上点的全体，则一方面$\mathbb{P}(X=Y)=1$，另一方面
>
> $$1=\mathbb{P}(X=Y)=\mathbb{P}((X,Y)\in D)=\int_D f(x,y)dxdy=0$$
>
> （直线是二维零测集，任何函数在其上的二重积分为0。）矛盾！因此$(X,Y)$没有联合密度，从而不是连续型随机向量。

> [!NOTE] 备注（课件第35页）
> 在例1.5中，$F(x,y)$连续，且除去有限条直线外偏导数$\frac{\partial^2F(x,y)}{\partial x\partial y}$存在且连续。这说明：**"$F$连续＋混合偏导几乎处处存在且连续"仍不能保证$(X,Y)$有联合密度**（定理1.5中归一化条件$\int f=1$不可省）。

> [!WARNING] 辨析
> "联合分布函数连续"$\neq$"是连续型随机向量"。连续型要求**存在联合密度**，这是更强的条件；例1.5中全部概率质量挤在一条直线（零面积集）上，密度无处安放。

### 5.4 思考题（课件第36页）

- Marginal $\Rightarrow$ Joint？需考虑**存在性**与**唯一性**两个层面。
- 连续型：两个连续型随机变量$X_1,X_2$拼成的$(X_1,X_2)$是否一定是连续型随机向量（存在Joint PDF）？——**不一定**（例1.5即反例：$X_2=X_1$）。
- 若$(X_1,X_2)$存在联合密度但未知，仅知道各自的边缘密度，能否恢复联合密度？——**不能**，边缘不含"两个变量如何搭配"的信息（例如不同$\rho$的二元正态有完全相同的边缘）。

---

## 六、条件分布和条件密度

### 6.1 离散型条件分布（定义2.1）

设$(X,Y)$是离散型随机向量，有概率分布（joint PMF）$p_{ij}=\mathbb{P}(X=x_i,Y=y_j)>0$，$i,j=1,2,\ldots$，则$X,Y$分别有边缘分布（marginal PMF）

$$p_i=\mathbb{P}(X=x_i),\quad q_j=\mathbb{P}(Y=y_j),\quad i,j=1,2,\ldots$$

> [!IMPORTANT] 定义 2.1（条件概率分布）
> 对每个固定的$j$，称
>
> $$\mathbb{P}(X=x_i\mid Y=y_j)=\frac{\mathbb{P}(X=x_i,Y=y_j)}{\mathbb{P}(Y=y_j)}=\frac{p_{ij}}{q_j},\quad i=1,2,\ldots$$
>
> 为给定条件$Y=y_j$下，$X$的**条件分布列**（conditional PMF）。

**直觉**：知道$Y=y_j$后，样本空间收缩到第$j$"行"，把这一行的联合概率除以行总和（重新归一化），就得到$X$的新分布。

> [!EXAMPLE]- 例题（Review）：两个四面骰子
> 同时抛掷两个4面的骰子（一红一黑），记$X$、$Y$分别为红、黑骰子的点数，联合分布列由表格给出（非均匀）。求$\mathbb{P}(X=3\mid Y=2)$。
>
> **解**　课件表格中$Y=2$这一行的取值为：$\mathbb{P}(X=2,Y=2)=\frac{1}{20}$，$\mathbb{P}(X=3,Y=2)=\frac{3}{20}$，$\mathbb{P}(X=4,Y=2)=\frac{1}{20}$。
>
> 先求边缘（注：此步补全了行求和）：
>
> $$\mathbb{P}(Y=2)=\frac{1}{20}+\frac{3}{20}+\frac{1}{20}=\frac{5}{20}=\frac{1}{4}$$
>
> 于是
>
> $$\mathbb{P}(X=3\mid Y=2)=\frac{\mathbb{P}(X=3,Y=2)}{\mathbb{P}(Y=2)}=\frac{3/20}{5/20}=\frac{3}{5}$$

### 6.2 离散型独立性判别（定理2.1）

> [!IMPORTANT] 定理 2.1（常用）
> $X,Y$独立的充分必要条件是对任何$i,j\geq 1$，
>
> $$\mathbb{P}(X=x_i\mid Y=y_j)=\mathbb{P}(X=x_i)$$
>
> 等价于
>
> $$\mathbb{P}(X=x_i,Y=y_j)=\mathbb{P}(X=x_i)\mathbb{P}(Y=y_j),\quad i,j\geq 1$$

**直觉**：独立＝"打听$Y$的取值对预测$X$毫无帮助"，条件分布与无条件分布完全一样。

> [!EXAMPLE]- 例题 2.1：射击问题——前两次击中时刻的联合、边缘与条件分布
> 甲向一个目标射击，用$S_n$表示第$n$次击中目标时的射击次数。如果甲每次击中目标的概率是$p=1-q$，则$(X,Y)=(S_1,S_2)$的联合分布为
>
> $$\mathbb{P}(X=i,Y=j)=p^2q^{j-2},\quad j>i\geq 1$$
>
> 求边缘分布与两个方向的条件分布。
>
> **解**
> **第一步：联合分布列的来历**（注：此步补全了课件直接给出的公式）。事件$\{X=i,Y=j\}$表示：前$i-1$次未中、第$i$次中、第$i+1$到$j-1$次未中、第$j$次中，各次射击独立，故
>
> $$\mathbb{P}(X=i,Y=j)=q^{i-1}p\cdot q^{j-i-1}p=p^2q^{j-2},\quad j>i\geq 1$$
>
> 注意它只依赖$j$，不依赖$i$。
>
> **第二步：边缘分布**。对$X$（对$j$求和，几何级数）：
>
> $$\mathbb{P}(X=i)=\sum_{j=i+1}^{\infty}\mathbb{P}(X=i,Y=j)=\sum_{j=i+1}^{\infty}p^2q^{j-2}=p^2\cdot\frac{q^{i-1}}{1-q}=pq^{i-1}$$
>
> （注：此步补全了求和细节——首项$j=i+1$时为$p^2q^{i-1}$，公比$q$，和为首项除以$1-q=p$。）即$X\sim G(p)$，符合"第一次成功等待时间"的直觉。对$Y$（对$i$求和，共$j-1$项相同）：
>
> $$\mathbb{P}(Y=j)=\sum_{i=1}^{j-1}\mathbb{P}(X=i,Y=j)=\sum_{i=1}^{j-1}p^2q^{j-2}=(j-1)p^2q^{j-2},\quad j=2,3,\ldots$$
>
> （这是Pascal分布／负二项分布$m=2$的情形。）
>
> **第三步：条件分布**。对确定的$i$，得$Y$的条件分布：
>
> $$\mathbb{P}(Y=j\mid X=i)=\frac{p^2q^{j-2}}{pq^{i-1}}=pq^{j-i-1},\quad j>i$$
>
> 即已知$S_1=i$后，$Y-i$（还需等待的次数）仍是$G(p)$——几何分布的无记忆性再现。对确定的$j$（$j\geq 2$），得$X$的条件分布：
>
> $$\mathbb{P}(X=i\mid Y=j)=\frac{p^2q^{j-2}}{(j-1)p^2q^{j-2}}=\frac{1}{j-1},\quad 1\leq i<j$$
>
> 上式表明：已知$S_2=j$时，$S_1$在$\{1,2,\ldots,j-1\}$中的取值是**等可能**的。
>
> **第四步：增量独立**。若令$X_1=S_1$，$X_2=S_2-S_1,\ldots$，则
>
> $$\mathbb{P}(X_1=i,X_2=j)=\mathbb{P}(X=i,Y=i+j)=p^2q^{i+j-2}=pq^{i-1}\cdot pq^{j-1}=\mathbb{P}(X_1=i)\mathbb{P}(X_2=j)$$
>
> 可见随机变量$X_1,X_2,\ldots$是**独立同分布**的（都服从$G(p)$）。

### 6.3 随机变量序列的独立性（Lecture 3讲义末尾的回顾）

> [!NOTE] 定义（独立序列）
> 如果对任意的$n$，$X_1,\ldots,X_n$相互独立，则称随机变量序列$\{X_i\}$相互独立，此时称$\{X_i\}$为**独立序列**。

> [!NOTE] 定义（独立同分布序列）
> 如果随机变量$X_1,X_2,\ldots$是相互独立并且有相同的分布函数，则称$X_1,X_2,\ldots$**独立同分布**（independent and identically distributed, i.i.d.）。

### 6.4 连续型条件分布：动机与困难

**情景**（课件第44页）：用$Y$表示身高、$X$表示体重，$(X,Y)$是连续型随机向量，有联合密度$f(x,y)$。我们常关心：已知身高$Y=y$的条件下，体重$X$的概率分布如何？用$\mathbb{P}(X\leq x\mid Y=y)$表示该条件下$X$的分布函数，称为**条件分布函数**。记

$$f_X(x)=\int_{-\infty}^{\infty}f(x,y)dy,\quad f_Y(y)=\int_{-\infty}^{\infty}f(x,y)dx$$

**困难**：$\mathbb{P}(Y=y)=0$，不能直接套条件概率公式$\mathbb{P}(A\mid B)=\mathbb{P}(AB)/\mathbb{P}(B)$——分母为零！

**几何直观**（课件第45页）：把联合密度曲面在$Y=y$处切一刀，得到关于$x$的切片曲线；切片本身面积不为1，**重新归一化**（除以切片面积$f_Y(y)$）之后就是条件密度。对任意固定的$y$，$f_{X\mid Y}(x\mid y)$确实是一个合格的概率密度函数。

**极限推导**（课件第46页）：对于充分小的$\varepsilon>0$，可以理解

$$\mathbb{P}(X\leq x\mid y-\varepsilon<Y\leq y)\approx\mathbb{P}(X\leq x\mid Y=y)$$

进一步，如果$f_Y(y)$在$y$处连续，$f_Y(y)>0$，并且$\partial F(x,y)/\partial y$存在，就有

$$\begin{align}
\lim_{\varepsilon\to 0}\mathbb{P}(X\leq x\mid y-\varepsilon<Y\leq y)&=\lim_{\varepsilon\to 0}\frac{\mathbb{P}(X\leq x,\ y-\varepsilon<Y\leq y)}{\mathbb{P}(y-\varepsilon<Y\leq y)}\\
&=\lim_{\varepsilon\to 0}\frac{F(x,y)-F(x,y-\varepsilon)}{F_Y(y)-F_Y(y-\varepsilon)}\\
&=\frac{\displaystyle\lim_{\varepsilon\to 0}\frac{F(x,y)-F(x,y-\varepsilon)}{\varepsilon}}{\displaystyle\lim_{\varepsilon\to 0}\frac{F_Y(y)-F_Y(y-\varepsilon)}{\varepsilon}}\\
&=\frac{\dfrac{\partial}{\partial y}\displaystyle\int_{-\infty}^{y}\int_{-\infty}^{x}f(s,t)ds\,dt}{f_Y(y)}=\frac{\displaystyle\int_{-\infty}^{x}f(s,y)ds}{f_Y(y)}
\end{align}$$

这就把"条件在零概率事件上"安全地定义成了极限。

### 6.5 条件分布与条件密度（定义2.2）

> [!IMPORTANT] 定义 2.2（条件分布函数、条件密度）
> 设随机向量$(X,Y)$有联合密度$f(x,y)$，$Y$有边缘密度$f_Y(y)$。若在（确定的）$y$处$f_Y(y)>0$，则称
>
> $$\mathbb{P}(X\leq x\mid Y=y)=\frac{\int_{-\infty}^{x}f(s,y)ds}{f_Y(y)},\quad x\in\mathbb{R}$$
>
> 为给定条件$Y=y$下，$X$的**条件分布函数**，简称条件分布，记作$F_{X\mid Y}(x\mid y)$。称
>
> $$f_{X\mid Y}(x\mid y)=\frac{f(x,y)}{f_Y(y)}=\frac{f(x,y)}{\int_{-\infty}^{\infty}f(x,y)dx},\quad x\in\mathbb{R}$$
>
> 为给定条件$Y=y$下，$X$的**条件概率密度**，简称条件密度。

立刻得到**乘法公式**（常用）：

$$f(x,y)=f_Y(y)f_{X\mid Y}(x\mid y)$$

**直觉**：条件密度＝联合密度的"切片÷切片面积"，形式上与离散的$p_{ij}/q_j$完全平行——把求和换成积分而已。

**条件密度与条件分布的关系**（课件第48页）：对使得$f_Y(y)>0$的$y$，
1. $F_{X\mid Y}(x\mid y)=\mathbb{P}(X\leq x\mid Y=y)=\displaystyle\int_{-\infty}^{x}f_{X\mid Y}(s\mid y)ds$，$x\in\mathbb{R}$；
2. 如果$F_{X\mid Y}(x\mid y)$关于$x$连续，且除去至多可列个点外有连续的导数，则

$$f_{X\mid Y}(x\mid y)=\begin{cases}\dfrac{\partial F_{X\mid Y}(x\mid y)}{\partial x}, & \text{当偏导数存在}\\ 0, & \text{其它}\end{cases}$$

是给定条件$Y=y$下$X$的条件密度。即条件分布与条件密度之间的"积分—求导"关系与普通一维情形完全一样。

### 6.6 连续型独立性判别（定理2.2）

> [!IMPORTANT] 定理 2.2（常用）
> $X,Y$独立的充分必要条件是对$y\in\{y\mid f_Y(y)>0\}$，
>
> $$f_{X\mid Y}(x\mid y)=f_X(x),\quad x\in\mathbb{R}$$
>
> 等价于$f(x,y)=f_X(x)f_Y(y)$，$x,y\in\mathbb{R}$。

**直觉**：与离散版定理2.1一字平行——条件密度不随条件变化＝独立。

> [!EXAMPLE]- 例题 2.2：二元正态的条件分布
> 设$(X,Y)\sim N(\mu_1,\mu_2,\sigma_1^2,\sigma_2^2,\rho)$，已知$X=x$时，求$Y$的条件密度。
>
> **解**　由4.5节证明中的事实，$X\sim N(\mu_1,\sigma_1^2)$。按定义
>
> $$f_{Y\mid X}(y\mid x)=\frac{f(x,y)}{f_X(x)}$$
>
> 代入二元正态密度与一元正态密度相除（注：此步补全了化简过程——分子指数中关于$y$配方：
>
> $$-\frac{1}{2(1-\rho^2)}\left[\frac{(x-\mu_1)^2}{\sigma_1^2}-\frac{2\rho(x-\mu_1)(y-\mu_2)}{\sigma_1\sigma_2}+\frac{(y-\mu_2)^2}{\sigma_2^2}\right]=-\frac{\left(y-\mu_2-\rho\frac{\sigma_2}{\sigma_1}(x-\mu_1)\right)^2}{2(1-\rho^2)\sigma_2^2}-\frac{(x-\mu_1)^2}{2\sigma_1^2}$$
>
> 第二项与$f_X(x)$的指数恰好相消，系数$\frac{1}{2\pi\sigma_1\sigma_2\sqrt{1-\rho^2}}\div\frac{1}{\sqrt{2\pi}\sigma_1}=\frac{1}{\sigma_2\sqrt{2\pi(1-\rho^2)}}$），得
>
> $$f_{Y\mid X}(y\mid x)=\frac{1}{\sigma_2\sqrt{2\pi(1-\rho^2)}}\exp\left(-\frac{(y-\mu_x)^2}{2(1-\rho^2)\sigma_2^2}\right),\quad\text{其中 }\mu_x=\mu_2+\rho\frac{\sigma_2}{\sigma_1}(x-\mu_1)$$
>
> 此说明
>
> $$Y\mid_{X=x}\sim N\left(\mu_2+\rho\frac{\sigma_2}{\sigma_1}(x-\mu_1),\ (1-\rho^2)\sigma_2^2\right)$$
>
> 同理，
>
> $$X\mid_{Y=y}\sim N\left(\mu_1+\rho\frac{\sigma_1}{\sigma_2}(y-\mu_2),\ (1-\rho^2)\sigma_1^2\right)$$
>
> 当$X$和$Y$独立时，$\rho=0$，于是$f_{Y\mid X}(y\mid x)=f_Y(y)$，与定理2.2一致。
>
> **直觉**：二元正态的条件分布仍是正态；条件均值随$x$**线性**变化（这正是线性回归的概率原型），条件方差$(1-\rho^2)\sigma_2^2$比无条件方差$\sigma_2^2$小——信息使不确定性收缩，$|\rho|$越大收缩越多。

> [!EXAMPLE]- 例题 2.3：随机环境下的软件寿命（Gamma 混合指数）
> 设计算机使用的环境指标$Y\sim\Gamma(\alpha,\beta)$，概率密度是
>
> $$f_Y(y)=\frac{\beta^{\alpha}}{\Gamma(\alpha)}y^{\alpha-1}e^{-\beta y},\quad y>0$$
>
> 已知$Y=y$时，软件的使用寿命$X\mid Y=y\sim\mathcal{E}(y)$。求$X$的分布。
>
> **解**
> **第一步：写出联合密度**。$X$的条件密度$f_{X\mid Y}(x\mid y)=ye^{-xy}$，$x>0$。于是由乘法公式，$(X,Y)$的联合密度为
>
> $$f(x,y)=f_{X\mid Y}(x\mid y)f_Y(y)=ye^{-xy}\cdot\frac{\beta^{\alpha}}{\Gamma(\alpha)}y^{\alpha-1}e^{-\beta y}=\frac{\beta^{\alpha}}{\Gamma(\alpha)}y^{\alpha}e^{-y(x+\beta)},\quad x,y>0$$
>
> **第二步：积掉$y$求边缘**。对$x>0$，
>
> $$f_X(x)=\int_0^{\infty}f(x,y)dy=\int_0^{\infty}\frac{\beta^{\alpha}}{\Gamma(\alpha)}y^{\alpha}e^{-y(x+\beta)}dy$$
>
> 作换元$t=y(x+\beta)$，则$y=\frac{t}{x+\beta}$，$dy=\frac{dt}{x+\beta}$（注：此步补全了换元细节），得
>
> $$f_X(x)=\frac{\beta^{\alpha}}{\Gamma(\alpha)}\cdot\frac{1}{(x+\beta)^{\alpha+1}}\int_0^{\infty}t^{\alpha}e^{-t}dt=\frac{\beta^{\alpha}}{\Gamma(\alpha)}\cdot\frac{\Gamma(\alpha+1)}{(x+\beta)^{\alpha+1}}$$
>
> 利用$\Gamma(\alpha+1)=\alpha\Gamma(\alpha)$：
>
> $$f_X(x)=\frac{\alpha\beta^{\alpha}}{(x+\beta)^{\alpha+1}},\quad x>0$$
>
> 这是一个**幂律尾**（Pareto型）密度——条件上是轻尾的指数分布，把随机环境平均之后边缘变成了重尾分布。
>
> **附（课件框注）Gamma 分布$\Gamma(\alpha,\lambda)$**：设$\alpha,\lambda$是正常数，如果$X$的密度是
>
> $$f(x)=\frac{\lambda^{\alpha}}{\Gamma(\alpha)}x^{\alpha-1}e^{-\lambda x},\quad x\geq 0$$
>
> 则称$X\sim\Gamma(\alpha,\lambda)$。

### 6.7 随机向量的条件分布（定义2.3）（不要求掌握）

> [!NOTE] 定义 2.3（不要求掌握，略述）
> 设$\mathbf{X}=(X_1,\ldots,X_n)$和$\mathbf{Y}=(Y_1,\ldots,Y_m)$是随机向量，$f(\mathbf{x},\mathbf{y})$是$(\mathbf{X},\mathbf{Y})$的联合密度，此时$\mathbf{Y}$有边缘密度
>
> $$f_{\mathbf{Y}}(\mathbf{y})=\int_{\mathbb{R}^n}f(\mathbf{x},\mathbf{y})d\mathbf{x}$$
>
> 若在（确定的）$\mathbf{y}$处$f_{\mathbf{Y}}(\mathbf{y})>0$，则称
>
> $$\mathbb{P}(\mathbf{X}\leq\mathbf{x}\mid\mathbf{Y}=\mathbf{y})=\frac{\int_{\mathbf{s}\leq\mathbf{x}}f(\mathbf{s},\mathbf{y})d\mathbf{s}}{f_{\mathbf{Y}}(\mathbf{y})}$$
>
> 为给定条件$\mathbf{Y}=\mathbf{y}$下$\mathbf{X}$的条件分布函数，记作$F_{\mathbf{X}\mid\mathbf{Y}}(\mathbf{x}\mid\mathbf{y})$；称
>
> $$f_{\mathbf{X}\mid\mathbf{Y}}(\mathbf{x}\mid\mathbf{y})=\frac{f(\mathbf{x},\mathbf{y})}{f_{\mathbf{Y}}(\mathbf{y})}$$
>
> 为给定条件$\mathbf{Y}=\mathbf{y}$下$\mathbf{X}$的条件概率密度，简称条件密度。形式与二维情形完全一致。

---

## 七、小结（课件第55、56页）

**概念**（含理解其意义）：
- 连续型随机向量：核心知识是联合PDF、边缘PDF、独立性的判定；经典例子——离散型：多项分布；连续型：多元正态分布。
- 条件分布：离散型随机变（向）量的条件分布列（conditional PMF）、连续型随机变（向）量的条件密度（conditional PDF）、累积条件分布（conditional CDF）。

**能力**：
- 条件CDF/PDF/PMF与联合、边缘之间的转换运算；
- 基于多种工具（条件、联合）判定独立性。

**技巧**：
- 密度与分布间的转换（e.g. 理解条件密度的定义）；
- 蕴含独立性的联合概率密度的快速拆解（归一化）；
- 条件在随机变量上时，可赋予其固定取值进行计算推演和理解（$\mathbb{P}(X\mid Y=y)$，$f(X\mid Y=y)$）。

**思考**：条件概率的形式？相应的乘法法则、全概率公式、贝叶斯法则？（提示：$f(x,y)=f_Y(y)f_{X\mid Y}(x\mid y)$是乘法法则；$f_X(x)=\int f_{X\mid Y}(x\mid y)f_Y(y)dy$是全概率公式的密度版，例2.3正是其应用；两者相除即得密度版贝叶斯公式。）

主要公式速查：

| 对象 | 离散型 | 连续型 |
| ---- | ---- | ---- |
| 联合 | $p_{ij}=\mathbb{P}(X=x_i,Y=y_j)$ | $f(x,y)$ |
| 边缘 | $p_i=\sum_j p_{ij}$ | $f_X(x)=\int_{-\infty}^{\infty}f(x,y)dy$ |
| 条件 | $\mathbb{P}(X=x_i\mid Y=y_j)=p_{ij}/q_j$ | $f_{X\mid Y}(x\mid y)=f(x,y)/f_Y(y)$ |
| 独立判别 | $p_{ij}=p_iq_j$，$\forall i,j$ | $f(x,y)=f_X(x)f_Y(y)$ |
| 独立判别（条件版） | $\mathbb{P}(X=x_i\mid Y=y_j)=\mathbb{P}(X=x_i)$ | $f_{X\mid Y}(x\mid y)=f_X(x)$ |
| 乘法公式 | $p_{ij}=q_j\cdot\mathbb{P}(X=x_i\mid Y=y_j)$ | $f(x,y)=f_Y(y)f_{X\mid Y}(x\mid y)$ |

---

## 本讲方法/题型清单

- 求$\mathbb{P}(\mathbf{X}\in B)$（已知联合密度）→ 定理1.1＋Fubini → 写出区域$B$，化为累次积分，注意内层积分限随外层变量变化。
- 求边缘密度（已知联合密度）→ 定义1.2 → 把不要的变量从$-\infty$到$\infty$积掉；关键是先画清取值区域、确定固定一个变量时另一变量的积分范围（如例1.3单位圆）。
- 判定连续型$X,Y$（或$X_1,\ldots,X_n$）独立 → 定理1.3 → 检查联合密度能否拆成单变量函数之积且支撑集为矩形（立方体）；或用定理2.2检查条件密度是否等于边缘密度。
- 判定二元正态的两个分量独立 → 定理1.4 → 只看$\rho$是否为0，不必积分。
- 已知联合密度求联合分布（或反向）→ $F(x,y)=\int_{-\infty}^{x}\int_{-\infty}^{y}f$；反向在偏导连续处用$f=\partial^2F/\partial x\partial y$（例1.3第二个）。
- 求离散型条件分布列 → 定义2.1 → 三步：写联合分布列、对条件变量求和得边缘、相除归一化（例2.1、四面骰子例）。
- 求连续型条件密度 → 定义2.2 → 切片再归一化：$f_{X\mid Y}(x\mid y)=f(x,y)/f_Y(y)$，把$y$当常数看。
- 求二元正态条件分布 → 例2.2结论直接套用 → $Y\mid_{X=x}\sim N\big(\mu_2+\rho\frac{\sigma_2}{\sigma_1}(x-\mu_1),(1-\rho^2)\sigma_2^2\big)$；记忆口诀"条件均值线性修正、条件方差乘$(1-\rho^2)$"。
- 由"条件密度＋边缘密度"反求另一变量的边缘（分层/混合模型）→ 乘法公式＋积分 → 先$f(x,y)=f_{X\mid Y}(x\mid y)f_Y(y)$，再对条件变量积分；积分常用换元配出$\Gamma$函数（例2.3）。
- 证明某随机向量**不是**连续型 → 反证法 → 假设密度存在，找一个零测集（如直线$y=x$）使其概率为正，与$\int_{\text{零测集}}f=0$矛盾（例1.5）。
