---
title: "Lecture07 随机向量函数的分布、次序统计量、p分位数"
tags:
  - 概率论
  - 前半学期
  - Jacobian
  - 次序统计量
  - p分位数
---

# Lecture07 随机向量函数的分布、次序统计量、p分位数

> [!ABSTRACT] 本讲概要
> 上一讲我们会求单个随机变量函数 $g(X)$ 的分布，这一讲把问题升级为**随机向量的函数** $g(\boldsymbol{X})$：和、差、商、多对多变换（Jacobian 方法）。在此基础上引出两类极重要的"函数"：**次序统计量**（把样本从小到大排）与**分位数函数 $F^{-1}(p)$**（CDF 的"广义反函数"，是生成随机数的理论基础）。
>
> ---

## 一、预备知识：与正态相关的三大统计分布

本讲开头补完常见连续分布家族中与 $\mathcal{N}(0,1)$ 紧密相关的三个分布（统计推断的三大核心分布），它们本质上都是**正态随机向量的函数的分布**，正好呼应本讲主题。

### 1.1 卡方分布 $\chi^2_v$（Chi-squared distribution）

设 $v>0$，如果 $X$ 的密度是

$$
f(x)=\frac{1}{2^{v/2}\Gamma(v/2)}x^{\frac{v}{2}-1}e^{-\frac{x}{2}},\quad x\ge 0,
$$

称 $X$ 服从参数为 $v$ 的 $\chi^2_v$ 分布，记作 $X\sim\chi^2_v$。

**直觉**：$\chi^2_n$ 就是 $n$ 个独立标准正态的"平方和能量"的分布。

- 设有独立同分布 (i.i.d.) 的 $Z_j\sim\mathcal{N}(0,1)$，$j=1,\ldots,n$，令 $X=Z_1^2+\cdots+Z_n^2$，则 $X\sim\chi^2_n$。
- 可以验证 $\chi^2_1=\Gamma\left(\frac{1}{2},\frac{1}{2}\right)$。于是由 Gamma 分布的性质（以后会证明）有 $\chi^2_n=\Gamma\left(\frac{n}{2},\frac{1}{2}\right)$。

> [!NOTE] 备注
> $\chi^2$ 分布由 Karl Pearson 于 1900 年提出 $\chi^2$ 检验时引入。

### 1.2 Student's $t_v$ 分布

设 $v>0$，如果 $X$ 的密度是

$$
f(x)=\frac{\Gamma\left(\frac{v+1}{2}\right)}{\sqrt{v\pi}\,\Gamma\left(\frac{v}{2}\right)}\left(1+\frac{x^2}{v}\right)^{-\frac{v+1}{2}},\quad x\in\mathbb{R},
$$

称 $X$ 服从参数为 $v$ 的 Student's t 分布，简称 t 分布，记作 $X\sim t_v$。

**直觉**：t 分布是"用样本估计的标准差去标准化正态"产生的分布，形状像正态但尾巴更厚。

性质（逐条）：

| 性质 | 内容 | 标注 |
| --- | --- | --- |
| 构造 | 设 $Z\sim\mathcal{N}(0,1)$，$X\sim\chi^2_n$，且 $X$ 与 $Z$ 独立，令 $T=\dfrac{Z}{\sqrt{X/n}}$，则 $T\sim t_n$ | 常用 |
| 对称性 | 若 $T\sim t_v$，则 $-T\sim t_v$ | 常用 |
| 重尾 | 比正态分布重尾 | 了解即可 |
| 大自由度极限 | 当 $v$ 很大时，$t_v$ 分布和标准正态分布很像（以后用大数定律证明） | 了解即可 |
| 特例 | $v=1$ 时性质特殊，亦称为 **Cauchy 分布** | 常用 |

> [!NOTE] 备注
> t 分布由 William Sealy Gosset 于 1908 年以笔名 "Student" 发表。

### 1.3 F 分布 $F(m,n)$（Fisher–Snedecor distribution）

设 $m,n$ 是正整数，如果 $X$ 的密度是

$$
f(x)=\frac{\Gamma\left(\frac{m+n}{2}\right)}{\Gamma\left(\frac{m}{2}\right)\Gamma\left(\frac{n}{2}\right)}\cdot\frac{m^{m/2}\,n^{n/2}\,x^{\frac{m}{2}-1}}{(mx+n)^{\frac{m+n}{2}}},\quad x\ge 0,
$$

称 $X$ 服从参数为 $(m,n)$ 的 $F$ 分布，记作 $X\sim F(m,n)$。

**直觉**：F 分布是"两组独立正态平方和的（平均）比值"的分布，用来比较两个方差的大小。

- 设有 i.i.d. 的 $X_j\sim\mathcal{N}(0,1)$，$j=1,\ldots,m$ 和 $Y_j\sim\mathcal{N}(0,1)$，$j=1,\ldots,n$，令

$$
F=\frac{\sum_{i=1}^{m}X_i^2/m}{\sum_{i=1}^{n}Y_i^2/n},
$$

则 $F\sim F(m,n)$。

> [!NOTE] 备注
> 1924 年英国统计学家 R.A. Fisher 提出，因此命名 F 分布。在方差分析、线性回归中有重要应用。

### 1.4 常见分布关系图（课件手绘图）

> [!NOTE] 备注：常见分布之间的关系网
> - $B(n,p)\xrightarrow{np\to\lambda,\ n\to+\infty}\mathcal{P}(\lambda)$（二项收敛到 Poisson）；
> - $HG(n,M,N)\xrightarrow{M/N\to p,\ N\to+\infty}B(n,p)$（无放回 → 有放回）；$NHG(r,M,N)\xrightarrow{N\to\infty}NB(r,p)$；
> - $B(p)$（两点分布）独立和 → $B(n,p)$；$G(p)$ 独立和 → $NB(r,p)$（Pascal 分布）；
> - $\mathcal{E}(\lambda)$ 与 $G(p)$ 同为**无记忆 (memoryless)** 分布（连续/离散对应）；$\mathcal{E}(\lambda)$ 独立和 → $\Gamma(n,\lambda)$；
> - $\mathcal{N}(\mu,\sigma^2)$ 派生出 $\chi^2_n$、$t_n$、$F(m,n)$；$\mathcal{U}(a,b)$ 自成一类。

---

## 二、随机向量函数的分布

### 2.1 Review：刻画 $g(\boldsymbol{X})$ 分布的两条路

随机变量（向量）的三件套：CDF、PMF/PDF。CDF 与 PMF 互相可以确定；CDF 与 PDF 之间，PDF 可确定 CDF，CDF 不能唯一确定 PDF（只能"几乎处处"确定）。

由此我们得到两条路去刻画 $g(\vec{X})$ 的分布：
1. **general 通用方法**：从 $\vec{X}$ 的 CDF/PDF 出发，直接求 $g(\vec{X})$ 的 **CDF**，再根据需要求导得 PDF（或读出 PMF）；
2. **特殊情形**：当 $g$ 具有良好结构（如一维单调函数、和差、可逆多对多变换）时，可以**从 PDF 直接得到 PDF**（公式法）。

### 2.2 一般情形：CDF 曲线法

**方法**：直接求分布函数 $F_Z(z)=\mathbb{P}(g(\vec{X})\le z)$（一个区域上的积分/求和），再根据需要求 PDF 或 PMF。（常用）

> [!EXAMPLE]- 例题 1.1：单位正方形上均匀分布，求商 $Z=Y/X$ 的密度
> 设 $(X,Y)$ 为单位正方形上的均匀分布，有联合密度 $f(x,y)$。可验证 $X,Y$ 独立。求 $Z=g(X,Y)=Y/X$ 的概率密度函数。
> 
> **解**：$f(x,y)=1$（$0<x<1,0<y<1$）。对固定 $z$，事件 $\{Y/X\le z\}=\{Y\le zX\}$ 是单位正方形与直线 $y=zx$ 下方区域的交集。
> 
> - 当 $0\le z\le 1$ 时，直线 $y=zx$ 在正方形内从 $(0,0)$ 到 $(1,z)$，下方是一个直角三角形，面积为 $\frac{1}{2}\cdot 1\cdot z$，故
> 
> $$
> F_Z(z)=\mathbb{P}\left(\frac{Y}{X}\le z\right)=\frac{z}{2},\quad 0\le z\le 1.
> $$
> 
> - 当 $z>1$ 时，看补集 $\{Y>zX\}$：它是直线上方的三角形，顶点 $(0,0),(0,1),(1/z,1)$，面积 $\frac{1}{2}\cdot\frac{1}{z}\cdot 1=\frac{1}{2z}$（注：此步补全了"为何是 $1-\frac{1}{2z}$"的几何理由），故
> 
> $$
> F_Z(z)=\mathbb{P}\left(\frac{Y}{X}\le z\right)=1-\frac{1}{2z},\quad z>1.
> $$
> 
> - $F_Z(z)=0$，$z<0$。
> 
> 求导即得密度（注：此步补全了课件略去的求导）：
> 
> $$
> f_Z(z)=\begin{cases}\dfrac{1}{2}, & 0<z<1,\\[4pt] \dfrac{1}{2z^2}, & z>1,\\[4pt] 0, & \text{其它}.\end{cases}
> $$

> [!EXAMPLE]- 例题 1.2：两个独立标准正态的模长——Rayleigh 分布
> 设 $X,Y$ 独立且都服从 $\mathcal{N}(0,1)$，求 $Z=\sqrt{X^2+Y^2}$ 的分布。
> 
> **解**：$(X,Y)$ 有联合密度
> 
> $$
> f(x,y)=\frac{1}{2\pi}\exp\left(-\frac{x^2+y^2}{2}\right).
> $$
> 
> 对 $z\ge 0$，有
> 
> $$
> F_Z(z)=\mathbb{P}\left(\sqrt{X^2+Y^2}\le z\right)=\int_{\{\sqrt{x^2+y^2}\le z\}}\frac{1}{2\pi}\exp\left(-\frac{x^2+y^2}{2}\right)dxdy.
> $$
> 
> 作极坐标换元 $x=r\cos\theta$，$y=r\sin\theta$（依据：积分区域是圆盘，被积函数只依赖 $x^2+y^2=r^2$；面积元 $dxdy=r\,drd\theta$，即换元的 Jacobian 为 $r$）：
> 
> $$
> F_Z(z)=\frac{1}{2\pi}\int_0^{2\pi}d\theta\int_0^z re^{-r^2/2}\,dr=\int_0^z re^{-r^2/2}\,dr.
> $$
> 
> 求导可得 $Z$ 的密度函数
> 
> $$
> f_Z(z)=ze^{-z^2/2},\quad z\ge 0.
> $$
> 
> 此分布称为 **Rayleigh 分布**。
> 
> **背景**：向坐标 $(0,0)$ 射击时，弹落点 $(X,Y)$ 服从二元正态分布，$R=Z=\sqrt{X^2+Y^2}$ 为弹落点到目标的距离，被称为**脱靶量**。

### 2.3 特殊情形 (i)：和 $Z=X+Y$（卷积）

> [!EXAMPLE]- 例题 1.3：离散情形——分布列的卷积
> 设 $(X,Y)$ 有联合分布列，求 $Z=X+Y$ 的分布列。
> 
> **解**：把事件 $\{X+Y=z\}$ 按 $X$ 的取值分拆（全概率分解，互斥并）：
> 
> $$
> P_Z(z)=\mathbb{P}(X+Y=z)=\sum_x\mathbb{P}(X=x,Y=z-x).
> $$
> 
> 特别地，当 $X,Y$ 独立时，$Z=X+Y$ 有分布列
> 
> $$
> P_Z(z)=\sum_x\mathbb{P}(X=x)\mathbb{P}(Y=z-x)=\sum_x P_X(x)P_Y(z-x),
> $$
> 
> 此时 $Z$ 的分布列为 $X$ 和 $Y$ 的分布列的**卷积 (convolution)**。
> 
> **Review**：$X\sim B(n,p)$，$Y\sim B(m,p)$，独立 $\Rightarrow X+Y\sim B(m+n,p)$（直观：$n$ 次试验加 $m$ 次试验就是 $m+n$ 次试验）。

> [!NOTE] 备注
> 课件冷笑话：此卷 (convolution) 非彼卷 (involution)。

> [!IMPORTANT] 例 1.4（卷积公式，连续情形）（常用）
> 设 $(X,Y)$ 有联合密度 $f(x,y)$，则 $Z=X+Y$ 有密度函数
> 
> $$
> f_Z(z)=\int_{-\infty}^{\infty}f(x,z-x)\,dx.
> $$
> 
> 特别地，当 $X,Y$ 独立时，$Z=X+Y$ 有密度函数
> 
> $$
> f_Z(z)=\int_{-\infty}^{\infty}f_X(x)f_Y(z-x)\,dx.
> $$

**证明**：对任意 $a<b$，有

$$
\mathbb{P}(a<Z\le b)=\mathbb{P}(a<X+Y\le b)=\int_{\mathbb{R}^2}I_{\{a<x+y\le b\}}f(x,y)\,dxdy=\int_{\mathbb{R}}\left(\int_{a-x}^{b-x}f(x,y)\,dy\right)dx.
$$

对内层积分作换元 $y=z-x$（固定 $x$，$dy=dz$；当 $y$ 从 $a-x$ 到 $b-x$ 时 $z$ 从 $a$ 到 $b$），再用 Fubini 定理交换积分次序：

$$
=\int_{\mathbb{R}}\left(\int_a^b f(x,z-x)\,dz\right)dx=\int_a^b\left(\int_{\mathbb{R}}f(x,z-x)\,dx\right)dz.
$$

由 $a,b$ 任意，$Z=X+Y$ 的密度函数为 $f_Z(z)=\int_{-\infty}^{\infty}f(x,z-x)\,dx$。易见，$Z$ 的密度函数也可以写为（对称地按 $y$ 分拆）

$$
f_Z(z)=\int_{-\infty}^{\infty}f(z-y,y)\,dy.
$$

> [!EXAMPLE]- 例题 1.5：两个独立 $\mathcal{U}(0,1)$ 之和——三角分布
> 设 $X,Y$ 独立，且服从 $\mathcal{U}(0,1)$。求 $Z=X+Y$ 的概率密度。
> 
> **解**：显然 $Z\in(0,2)$，且
> 
> $$
> f_X(x)=f_Y(y)=I_{\{0<x<1\}}.
> $$
> 
> 于是由卷积公式
> 
> $$
> f_Z(z)=\int_{-\infty}^{\infty}f_X(x)f_Y(z-x)\,dx=\int_0^1 I_{\{0<z-x<1\}}\,dx.
> $$
> 
> 作换元 $t=z-x$（依据：$dt=-dx$，$x$ 从 $0$ 到 $1$ 时 $t$ 从 $z$ 降到 $z-1$，交换上下限消去负号）：
> 
> $$
> f_Z(z)=\int_{z-1}^{z}I_{\{0<t<1\}}\,dt=\text{区间}(z-1,z)\cap(0,1)\text{的长度}.
> $$
> 
> 分段讨论（注：此步补全了区间交集长度的计算）：当 $z\in[0,1)$ 时交集为 $(0,z)$，长度 $z$；当 $z\in[1,2]$ 时交集为 $(z-1,1)$，长度 $2-z$；其余为 0。故
> 
> $$
> f_Z(z)=\begin{cases}z, & \text{if } z\in[0,1),\\ 2-z, & \text{if } z\in[1,2],\\ 0, & \text{others}.\end{cases}
> $$
> 
> 密度图像是 $[0,2]$ 上以 $z=1$ 为顶点的三角形（课件"例2.5 结论图"）。

> [!EXAMPLE]- 例题 1.6：$n$ 个独立 $\mathcal{U}(-1,1)$ 之和
> 设 $X_1,X_2,\ldots,X_n$ 独立同分布，且服从 $\mathcal{U}(-1,1)$。则
> 
> 1) $X_1+X_2$ 的密度函数为
> 
> $$
> f_{X_1+X_2}(x)=\begin{cases}\dfrac{2-|x|}{4}, & \text{if } |x|\le 2,\\[4pt] 0, & \text{if } |x|>2.\end{cases}
> $$
> 
> （注：此步补全推导——$f_{X_i}(x)=\frac{1}{2}I_{\{|x|<1\}}$，卷积 $f_{X_1+X_2}(x)=\int\frac{1}{4}I_{\{|t|<1\}}I_{\{|x-t|<1\}}dt=\frac{1}{4}\times$区间 $(-1,1)\cap(x-1,x+1)$ 的长度 $=\frac{2-|x|}{4}$。）
> 
> 2) $X_1+X_2+X_3$ 的密度函数为（对 1) 的结果再卷一次 $\mathcal{U}(-1,1)$，分段积分可得）
> 
> $$
> f_{X_1+X_2+X_3}(x)=\begin{cases}\dfrac{(3-|x|)^2}{16}, & \text{if } 1\le|x|\le 3,\\[4pt] \dfrac{3-x^2}{8}, & \text{if } 0\le|x|\le 1,\\[4pt] 0, & \text{if } |x|>3.\end{cases}
> $$
> 
> 3) $S_n=X_1+X_2+\cdots+X_n$ 的密度函数为（归纳卷积的一般公式，了解即可）
> 
> $$
> f_{S_n}(x)=\begin{cases}\dfrac{1}{2^n(n-1)!}\displaystyle\sum_{k=0}^{[\frac{n+x}{2}]}(-1)^k\binom{n}{k}(n+x-2k)^{n-1}, & \text{if } |x|\le n,\\[4pt] 0, & \text{if } |x|>n,\end{cases}
> $$
> 
> 此处 $[a]$ 表示 $a$ 的整数部分。
> 
> **观察**（课件"例2.6 结论图"）：把 $f_{S_n}$ 与对应的正态密度（approximation）画在一起，$n=2$ 时已接近，$n\ge 5$ 后几乎重合——**多个独立变量叠加趋近正态**，这是中心极限定理的直观预览。

### 2.4 特殊情形 (ii)：差 $V=X-Y$（类似 (i)）

> [!EXAMPLE]- 例题 1.7：差的密度公式
> 设 $(X,Y)$ 有联合密度 $f(x,y)$，则 $V=X-Y$ 有密度函数
> 
> $$
> f_V(v)=\int_{-\infty}^{\infty}f(x,x-v)\,dx.
> $$
> 
> 特别地，当 $X,Y$ 独立时，$V=X-Y$ 有密度函数
> 
> $$
> f_V(v)=\int_{-\infty}^{\infty}f_X(x)f_Y(x-v)\,dx.
> $$
> 
> **解（思路）**：与例 1.4 同法。$\mathbb{P}(a<V\le b)=\int_{\mathbb{R}^2}I_{\{a<x-y\le b\}}f(x,y)dxdy$，固定 $x$ 对 $y$ 作换元 $v=x-y$（即 $y=x-v$，$|dy|=|dv|$），再用 Fubini 交换次序即得（注：此步补全了换元依据；也可把减法转化为加法 $V=X+(-Y)$ 套用卷积公式）。

> [!WARNING] 易错
> 差的公式里第二个密度的宗量是 $f_Y(x-v)$（即 $y=x-v$），**不是** $f_Y(v-x)$。和的卷积是 $f_Y(z-x)$。两者来源都是"解出另一变量"：$X+Y=z\Rightarrow y=z-x$；$X-Y=v\Rightarrow y=x-v$。死记容易混，建议每次现场解方程。

### 2.5 多个函数的联合密度（Jacobian 变换法）

设 $\vec{X}=(X_1,X_2,\ldots,X_n)$ 有联合密度 $f(\vec{x})$，$Y_1=g_1(\vec{X}),\ldots,Y_n=g_n(\vec{X})$ 是 $n$ 个 $\vec{X}$ 的函数。$\vec{Y}=(Y_1,Y_2,\ldots,Y_n)$ 的联合密度是什么？

> [!NOTE] 回忆（Lecture05/06 定理 2.1：一维随机变量函数的密度）
> 设 $X$ 有概率密度 $f(x)$，$D\subset\mathbb{R}$，$Y=g(X)$，$\mathbb{P}(Y\in D)=1$。如果
> 1. 对 $y\in D$，$\{Y=y\}=\bigcup_{i=1}^{n}\{X=h_i(y)\}$；
> 2. 每个 $h_i(y)$ 在 $D$ 上有连续导数，且诸 $h_i(D)$ 互不相交（各反函数分支的值域内有连续的导数）；
> 
> 则 $Y$ 有密度
> 
> $$
> g_Y(y)=\begin{cases}\displaystyle\sum_{i=1}^{n}f(h_i(y))\,|h_i'(y)|, & y\in D,\\ 0, & y\in D^c.\end{cases}
> $$
> 
> 本节的定理就是它的多维版本：$|h_i'(y)|$ 升级为 Jacobian 行列式的绝对值。

> [!IMPORTANT] 定理 1.1（2 维变量变换，2-dim）（常用）
> 设 $(X,Y)$ 有联合密度 $f(x,y)$，$U=u(X,Y)$，$V=v(X,Y)$ 是 $(X,Y)$ 的函数，$D$ 是平面上的区域使得 $\mathbb{P}((U,V)\in D)=1$。如果存在 $D$ 上的函数 $x_i=x_i(u,v)$，$y_i=y_i(u,v)$，$i=1,2,\ldots,n$，使得
> 1. 对 $(u,v)\in D$，有 $\{U=u,V=v\}=\bigcup_{i=1}^{n}\{X=x_i,Y=y_i\}$（反解出全部分支）；
> 2. $\Delta_i:x_i=x_i(u,v),\ y_i=y_i(u,v)$ 是 $D$ 到其值域 $D_i$ 的可逆映射，有连续的偏导数，并且雅克比 (Jacobian) 行列式的绝对值 $\left|\frac{\partial(x_i,y_i)}{\partial(u,v)}\right|\neq 0$，$(u,v)\in D$，$i=1,\ldots,n$；
> 3. $D_1,\ldots,D_n$ 互不相交；
> 
> 则 $(U,V)$ 有联合密度
> 
> $$
> g(u,v)=\begin{cases}\displaystyle\sum_{i=1}^{n}f\big(x_i(u,v),y_i(u,v)\big)\left|\frac{\partial(x_i,y_i)}{\partial(u,v)}\right|, & (u,v)\in D,\\ 0, & (u,v)\in D^c.\end{cases}
> $$

**直觉**：新密度 = 旧密度在原像点的值 × 面积缩放因子（Jacobian 绝对值），多个反解分支则把各分支的贡献加起来。**定理 1.1 可以直接从 2 维推广到 n 维**。

#### Aside: Vector and matrix calculus（Jacobian 的记号约定）

向量对向量求导有两种排版约定：

- **Numerator-layout（分子布局）**：$\frac{\partial y}{\partial x}$ 按 $y$ 和 $x'$ 排，如

$$
\frac{\partial(x,y)}{\partial(u,v)}=\begin{pmatrix}\dfrac{\partial x}{\partial u} & \dfrac{\partial x}{\partial v}\\[4pt] \dfrac{\partial y}{\partial u} & \dfrac{\partial y}{\partial v}\end{pmatrix};
$$

- **Denominator-layout（分母布局）**：按 $y'$ 和 $x$ 排，即上述矩阵的转置

$$
\frac{\partial(x,y)}{\partial(u,v)}=\begin{pmatrix}\dfrac{\partial x}{\partial u} & \dfrac{\partial y}{\partial u}\\[4pt] \dfrac{\partial x}{\partial v} & \dfrac{\partial y}{\partial v}\end{pmatrix};
$$

相应地，$\frac{\partial(x,y)}{\partial u}=\left(\frac{\partial x}{\partial u},\frac{\partial y}{\partial u}\right)'$（一列），$\frac{\partial x}{\partial(u,v)}=\left(\frac{\partial x}{\partial u},\frac{\partial x}{\partial v}\right)'$。

> [!NOTE] 备注
> 由于矩阵转置不改变行列式，$\left|\frac{\partial(x,y)}{\partial(u,v)}\right|$ 在两种布局下相同——所以定理 1.1 中的 Jacobian 绝对值不依赖布局约定，放心算。

> [!EXAMPLE]- 例题 1.8：极坐标变换——$(R,\Theta)$ 的联合密度
> 设 $X,Y$ 独立，$X,Y\sim\mathcal{N}(0,1)$，$(R,\Theta)$ 由极坐标变换
> 
> $$
> \begin{cases}X=R\cos\Theta\\ Y=R\sin\Theta\end{cases}
> $$
> 
> 决定，求 $(R,\Theta)$ 的联合密度。
> 
> **解**：$(X,Y)$ 有联合密度
> 
> $$
> f(x,y)=\frac{1}{2\pi}\exp\left(-\frac{x^2+y^2}{2}\right).
> $$
> 
> 定义 $D=\{(r,\theta)\mid r>0,\ \theta\in[0,2\pi)\}$，则 $\mathbb{P}((R,\Theta)\in D)=1$。变换
> 
> $$
> \Delta:\begin{cases}x=r\cos\theta\\ y=r\sin\theta\end{cases}
> $$
> 
> 建立了 $D$ 到 $D_1=\{(x,y)\mid(x,y)\neq 0\}$ 的可逆变换（单分支，$n=1$）。对 $(r,\theta)\in D$，利用
> 
> $$
> \{R=r,\Theta=\theta\}=\{X=x,Y=y\},\qquad \frac{\partial(x,y)}{\partial(r,\theta)}=\det\begin{pmatrix}\cos\theta & -r\sin\theta\\ \sin\theta & r\cos\theta\end{pmatrix}=r>0,
> $$
> 
> （注：此步补全了 Jacobian 行列式的展开：$r\cos^2\theta+r\sin^2\theta=r$。）由定理 1.1 得 $(R,\Theta)$ 的联合密度
> 
> $$
> g(r,\theta)=f(r\cos\theta,r\sin\theta)\cdot r=\frac{1}{2\pi}\cdot r\cdot\exp\left(-\frac{r^2}{2}\right),\quad(r,\theta)\in D.
> $$
> 
> 从中可以看出 $R$ 和 $\Theta$ **独立**（联合密度可分离变量为 $r$ 的函数乘 $\theta$ 的函数，且定义域是乘积形），分别有概率密度
> 
> $$
> g_R(r)=r\exp\left(-\frac{r^2}{2}\right),\ r\ge 0;\qquad g_\Theta(\theta)=\frac{1}{2\pi}I_{[0,2\pi)}(\theta).
> $$
> 
> 即 $R$ 是 Rayleigh 分布（脱靶量，呼应例 1.2），$\Theta\sim\mathcal{U}[0,2\pi)$。

> [!TIP] 方法：蕴含独立性的联合密度快速拆解（归一化）
> 若联合密度 $g(u,v)=h_1(u)h_2(v)$ 在矩形（乘积型）区域上成立，则 $U,V$ 独立，且各自密度正比于 $h_1,h_2$——把每个因子各自归一化（乘常数使积分为 1）即得边缘密度，无需再积分求边缘。例 1.8、例 1.10 都用了这一招。

> [!IMPORTANT] 定理 1.2（同分布经函数映射仍同分布）
> 设 $n$ 维随机向量 $\boldsymbol{X}$ 和 $\boldsymbol{Y}$ 有相同的分布，$g:\mathbb{R}^n\to\mathbb{R}^m$ 是可测的，则 $g(\boldsymbol{X})$ 与 $g(\boldsymbol{Y})$ 有相同的分布。
> 
> **直觉**：分布只由"取值的概率规律"决定，对同分布的输入做同一个加工，输出的概率规律当然也一样。

> [!EXAMPLE]- 例题 1.9：Box–Muller 正态随机数（不要求掌握，仅用于展示定理 1.2 的功能）
> 设 $U,V$ 独立，$U,V\sim\mathcal{U}(0,1)$，定义
> 
> $$
> \begin{cases}X=\sqrt{-2\ln U}\cos(2\pi V)\\ Y=\sqrt{-2\ln U}\sin(2\pi V)\end{cases}
> $$
> 
> 则 $X,Y$ 独立，且服从 $\mathcal{N}(0,1)$。【用来产生正态随机变量】
> 
> **证明**：$R=\sqrt{-2\ln U}\sim$ Rayleigh 分布（注：补全验证——$\mathbb{P}(R\le r)=\mathbb{P}(U\ge e^{-r^2/2})=1-e^{-r^2/2}$，求导得密度 $re^{-r^2/2}$，正是 Rayleigh），$\Theta=2\pi V\sim\mathcal{U}[0,2\pi)$，且 $R$ 与 $\Theta$ 独立。由例 1.8，"Rayleigh × 独立均匀角度"经过 $(r,\theta)\mapsto(r\cos\theta,r\sin\theta)$ 映射后得到两个独立 $\mathcal{N}(0,1)$；由定理 1.2（同分布输入 → 同分布输出）易得结论成立。

> [!EXAMPLE]- 例题 1.10：$U=X/Y$ 与 $V=X^2+Y^2$ 的联合密度
> 设 $X,Y$ 独立，$X,Y\sim\mathcal{N}(0,1)$，求 $U=X/Y$ 和 $V=X^2+Y^2$ 的联合密度。
> 
> **解**（课件只给了结果，以下推导为补全）：取 $D=\{(u,v)\mid u\in\mathbb{R},v>0\}$。由 $x=uy$ 及 $x^2+y^2=v$ 得 $y^2(1+u^2)=v$，于是反解有**两个分支**（$y$ 取正负）：
> 
> $$
> \Delta_{\pm}:\quad y_{\pm}=\pm\sqrt{\frac{v}{1+u^2}},\qquad x_{\pm}=u\,y_{\pm}.
> $$
> 
> 计算分支 $\Delta_+$ 的 Jacobian（依据：对 $u,v$ 分别求偏导）：
> 
> $$
> \frac{\partial y}{\partial u}=-\frac{u\sqrt{v}}{(1+u^2)^{3/2}},\quad \frac{\partial y}{\partial v}=\frac{1}{2\sqrt{v}\sqrt{1+u^2}},\quad \frac{\partial x}{\partial u}=y+u\frac{\partial y}{\partial u},\quad \frac{\partial x}{\partial v}=u\frac{\partial y}{\partial v},
> $$
> 
> $$
> \frac{\partial(x,y)}{\partial(u,v)}=\frac{\partial x}{\partial u}\frac{\partial y}{\partial v}-\frac{\partial x}{\partial v}\frac{\partial y}{\partial u}=y\frac{\partial y}{\partial v}=\sqrt{\frac{v}{1+u^2}}\cdot\frac{1}{2\sqrt{v}\sqrt{1+u^2}}=\frac{1}{2(1+u^2)}.
> $$
> 
> 分支 $\Delta_-$ 同理，Jacobian 绝对值也是 $\frac{1}{2(1+u^2)}$。而两个分支上 $x^2+y^2=v$ 都成立，故 $f(x_{\pm},y_{\pm})=\frac{1}{2\pi}e^{-v/2}$。由定理 1.1 把两支贡献相加：
> 
> $$
> g(u,v)=2\cdot\frac{1}{2\pi}e^{-\frac{v}{2}}\cdot\frac{1}{2(1+u^2)}=\frac{1}{\pi(1+u^2)}\cdot\frac{1}{2}e^{-\frac{v}{2}},\quad v\ge 0,\ u\in\mathbb{R}.
> $$
> 
> 即 $U,V$ **独立**（密度可分离），且 $U$ 服从 **Cauchy 分布**（密度 $\frac{1}{\pi(1+u^2)}$），$V$ 服从**指数分布** $\mathcal{E}(\frac{1}{2})$（也就是 $\chi^2_2$）。
> 
> **附带收获**：两个独立标准正态之商是 Cauchy 分布——这就是"曲线救国"求出 Cauchy 密度的经典办法。

> [!NOTE] 思考题（课件小结页）
> 乘法 $Z=XY$、除法 $Z=X/Y$ 的特殊情形公式该如何做？（提示：增补变量法——补一个变量如 $W=X$ 凑成二维可逆变换，用定理 1.1 求联合密度后再积分掉 $W$；或仿照例 1.4 用 CDF+换元直接推。）

---

## 三、次序统计量

### 3.1 定义

> [!IMPORTANT] 定义 2.1（次序统计量）
> 设 $X_1,X_2,\ldots,X_n$ 是概率空间 $(\Omega,\mathcal{F},\mathbb{P})$ 上的随机变量，对 $\omega\in\Omega$，将 $X_1(\omega),X_2(\omega),\ldots,X_n(\omega)$ 从小到大排列得到
> 
> $$
> X_{(1)}(\omega)\le X_{(2)}(\omega)\le\cdots\le X_{(n)}(\omega),
> $$
> 
> 称 $X_{(1)},X_{(2)},\ldots,X_{(n)}$ 为 $X_1,X_2,\ldots,X_n$ 的**次序统计量 (order statistics)**。

**直觉**：对每个样本点 $\omega$ 都把这组数"现场排序"，$X_{(k)}$ 就是"第 $k$ 小"这个名次上的值；名次是固定的，占据名次的人随 $\omega$ 变化。特别地 $X_{(1)}=\min$，$X_{(n)}=\max$。

> [!EXAMPLE]- 例题 2.1：三位百米运动员
> 设某省有 3 位百米运动员，用 $X_i$ 表示第 $i$ 个运动员的成绩。设 $X_i$ 都是样本空间 $\Omega=\{\omega_1,\omega_2,\omega_3\}$ 上的随机变量，其中 $\omega_i=$ 第 $i$ 次训练的成绩（单位：秒）。记 $X_{(i)}$ 为第 $i$ 名次运动员的成绩。
> 
> **解**：
> 
> | 第几次训练 | $X_1$ | $X_2$ | $X_3$ | $X_{(1)}$ | $X_{(2)}$ | $X_{(3)}$ |
> | --- | --- | --- | --- | --- | --- | --- |
> | $\omega_1$ | 11.3 | 11.6 | 11.0 | 11.0 | 11.3 | 11.6 |
> | $\omega_2$ | 11.0 | 11.5 | 11.8 | 11.0 | 11.5 | 11.8 |
> | $\omega_3$ | 12.0 | 11.9 | 12.2 | 11.9 | 12.0 | 12.2 |
> 
> $X_{(1)},X_{(2)},X_{(3)}$ 即为 $X_1,X_2,X_3$ 的次序统计量。注意每行排序后"第 1 名"可能来自不同的 $X_i$。

### 3.2 次序统计量的分布密度

以下设随机变量 $X_1,X_2,\ldots,X_n$ **独立同分布**，有公共的分布函数 $F(x)$ 和密度函数 $f(x)$。性质汇总：

| 性质 | 内容 | 公式 | 标注 |
| --- | --- | --- | --- |
| 性质 2.1 | 全体次序统计量的联合密度 | $g(x_1,\ldots,x_n)=n!\prod_{i=1}^{n}f(x_i)$，$x_1<\cdots<x_n$ | 常用 |
| 性质 2.2 | 单个 $X_{(k)}$ 的密度 | $g_k(x_k)=n\binom{n-1}{k-1}[F(x_k)]^{k-1}[1-F(x_k)]^{n-k}f(x_k)$ | 常用 |
| 性质 2.3 | 有序区域积分引理 | $\int_{a<x_1<\cdots<x_k<b}f(x_1)\cdots f(x_k)dx_1\cdots dx_k=\frac{(F(b)-F(a))^k}{k!}$ | 工具 |
| 性质 2.4 | 两个次序统计量的联合密度 | 见下 | 了解即可 |
| 性质 2.5 | $(X_{(1)},\ldots,X_{(n)})$ 的联合分布函数连续 | 见附录 | 了解即可 |

> [!IMPORTANT] 性质 2.1（联合密度）
> $(X_{(1)},X_{(2)},\ldots,X_{(n)})$ 有联合密度
> 
> $$
> g(x_1,\ldots,x_n)=\begin{cases}n!\displaystyle\prod_{i=1}^{n}f(x_i), & \text{if } x_1<\cdots<x_n,\\ 0, & \text{others}.\end{cases}
> $$

**证明思路（微元法）**：对 $x_1<\cdots<x_n$，事件"诸 $X_{(i)}$ 分别落在 $x_i$ 附近的小区间"等价于"$n$ 个原始变量以**某种排列**一一落入这些小区间"。排列共 $n!$ 种且互斥，每种的概率约为 $\prod_i f(x_i)dx_i$，故密度为 $n!\prod_i f(x_i)$。这就是为何比独立情形多了因子 $n!$。

> [!IMPORTANT] 性质 2.3（有序区域积分引理）
> 对于 $-\infty\le a<x_1<x_2<\cdots<x_k<b\le\infty$，有
> 
> $$
> \int_{a<x_1<\cdots<x_k<b}f(x_1)\cdots f(x_k)\,dx_1\cdots dx_k=\frac{(F(b)-F(a))^k}{k!}.
> $$

**证明（归纳法）**：$k=1$ 时即 $\int_a^b f=F(b)-F(a)$，结论成立。假设结论对 $k-1$ 成立，对于 $k$，用 Fubini 定理先固定最外层的 $x_k$：

$$
\int_{a<x_1<\cdots<x_k<b}f(x_1)\cdots f(x_k)\,dx_1\cdots dx_k=\int_a^b\left(\int_{a<x_1<\cdots<x_{k-1}<x_k}f(x_1)\cdots f(x_{k-1})\,dx_1\cdots dx_{k-1}\right)f(x_k)\,dx_k
$$

$$
=\int_a^b\frac{(F(x_k)-F(a))^{k-1}}{(k-1)!}f(x_k)\,dx_k=\frac{(F(b)-F(a))^k}{k!}.
$$

（注：最后一步补全依据——令 $G(x)=F(x)-F(a)$，则 $G'=f$，被积函数是 $\frac{G^{k-1}G'}{(k-1)!}$，原函数为 $\frac{G^k}{k!}$。）

> [!IMPORTANT] 性质 2.2（$X_{(k)}$ 的边缘密度）
> $X_{(k)}$ 有密度
> 
> $$
> g_k(x_k)=n\binom{n-1}{k-1}[F(x_k)]^{k-1}[1-F(x_k)]^{n-k}f(x_k).
> $$

**证明（课件 Thinking 页）**：从性质 2.1 的联合密度出发，把除 $x_k$ 外的变量都积分掉。记 $c=x_k$：

$$
g_k(c)=\int_{\{x_1<\cdots<x_{k-1}<c<x_{k+1}<\cdots<x_n\}}g(x_1,\ldots,x_n)\,dx_1\ldots dx_{k-1}dx_{k+1}\ldots dx_n
$$

$$
=n!\,f(c)\left[\int_{x_1<\cdots<x_{k-1}<c}f(x_1)\cdots f(x_{k-1})\,dx_1\cdots dx_{k-1}\right]\cdot\left[\int_{c<x_{k+1}<\cdots<x_n}f(x_{k+1})\cdots f(x_n)\,dx_{k+1}\cdots dx_n\right].
$$

由性质 2.3（前一块取 $a=-\infty,b=c$，后一块取 $a=c,b=+\infty$）：

$$
g_k(c)=n!\,f(c)\cdot\frac{F(c)^{k-1}}{(k-1)!}\cdot\frac{(1-F(c))^{n-k}}{(n-k)!}=n\binom{n-1}{k-1}F(c)^{k-1}(1-F(c))^{n-k}f(c).
$$

（注：此步补全了组合数化简：$\frac{n!}{(k-1)!(n-k)!}=n\cdot\frac{(n-1)!}{(k-1)!(n-k)!}=n\binom{n-1}{k-1}$。）

**直觉记忆**：要让"第 $k$ 小"落在 $c$ 处，需要 $k-1$ 个比它小（每个概率 $F(c)$）、$n-k$ 个比它大（每个概率 $1-F(c)$）、1 个恰好在 $c$ 处（密度 $f(c)$）；再乘上"选谁当这三拨人"的多项式系数 $\frac{n!}{(k-1)!\,1!\,(n-k)!}$。

**特例（常用）**：
- 最小值 $X_{(1)}$：$g_1(x)=n[1-F(x)]^{n-1}f(x)$，等价地 $\mathbb{P}(X_{(1)}>x)=[1-F(x)]^n$；
- 最大值 $X_{(n)}$：$g_n(x)=n[F(x)]^{n-1}f(x)$，等价地 $\mathbb{P}(X_{(n)}\le x)=[F(x)]^n$。

> [!IMPORTANT] 性质 2.4（两个次序统计量的联合密度）（了解即可）
> 对 $k_1<k_2$，$(X_{(k_1)},X_{(k_2)})$ 有联合密度
> 
> $$
> \begin{align}
> g(x_{k_1},x_{k_2})&=\frac{n!}{(k_1-1)!\,(k_2-k_1-1)!\,(n-k_2)!}\\
> &\quad\times[F(x_{k_1})]^{k_1-1}\,[F(x_{k_2})-F(x_{k_1})]^{k_2-k_1-1}\\
> &\quad\times[1-F(x_{k_2})]^{n-k_2}\,f(x_{k_1})f(x_{k_2}),\qquad x_{k_1}<x_{k_2}.
> \end{align}
> $$

**证明思路**：与性质 2.2 同法——从联合密度积分掉其余变量，按"小于 $x_{k_1}$ / 介于两者之间 / 大于 $x_{k_2}$"三块分别用性质 2.3，三块人数分别为 $k_1-1$、$k_2-k_1-1$、$n-k_2$，多项式系数即前面的阶乘比。

> [!WARNING] 辨析：$X_{(k)}$ 与 $X_k$
> - $X_1,\ldots,X_n$ i.i.d.，但 $X_{(1)},\ldots,X_{(n)}$ **既不独立也不同分布**（联合密度只在 $x_1<\cdots<x_n$ 上非零，天然耦合）；
> - $X_{(k)}$ 的密度不是 $f$，而是被 $F^{k-1}(1-F)^{n-k}$ 加权扭曲后的 $f$；
> - 不要把 $\mathbb{P}(X_{(n)}\le x)=[F(x)]^n$（最大值，全部 $\le x$）与 $\mathbb{P}(X_{(1)}>x)=[1-F(x)]^n$（最小值，全部 $>x$）混淆。

> [!EXAMPLE]- 例题 2.2：教室灯泡——最小值的分布
> 某教学楼原来每个教室有 4 只灯泡用于室内照明，新装修后每个教室有 24 只灯泡用于室内照明。装修后教室管理员总认为灯泡更容易坏了，试解释其中的原因。
> 
> **解**：设所有灯泡的使用寿命相互独立，且服从 $\mathcal{E}(\lambda)$。用 $X_i$ 表示第 $i$ 只灯泡的使用寿命，则装修前等待第一只灯泡烧坏的时间长度 $X$ 为
> 
> $$
> X=\min\{X_1,X_2,X_3,X_4\},
> $$
> 
> 装修后等待第一只灯泡烧坏的时间长度 $Y$ 为
> 
> $$
> Y=\min\{X_1,X_2,\ldots,X_{24}\}.
> $$
> 
> 利用性质 2.2（取 $k=1$）的结论分别得到 $X$ 和 $Y$ 的密度函数（注：此步补全代入过程——指数分布 $F(t)=1-e^{-\lambda t}$，$f(t)=\lambda e^{-\lambda t}$，故 $g_1(t)=n[1-F(t)]^{n-1}f(t)=n\lambda e^{-n\lambda t}$）：
> 
> $$
> f_X(t)=4\lambda e^{-4\lambda t},\qquad f_Y(t)=24\lambda e^{-24\lambda t},\qquad t>0,
> $$
> 
> 即 $X\sim\mathcal{E}(4\lambda)$，$Y\sim\mathcal{E}(24\lambda)$。于是有 $\mathbb{P}(X>t)=e^{-4\lambda t}$ 和 $\mathbb{P}(Y>t)=e^{-24\lambda t}$。
> 
> 当 $\lambda=1/6000$（小时）时（比如 Philips 牌 5W LED 球泡），
> 
> $$
> \mathbb{P}(X>400)=0.7659,\quad\mathbb{P}(X>200)=0.8752;\qquad\mathbb{P}(Y>400)=0.2019,\quad\mathbb{P}(Y>200)=0.4493.
> $$
> 
> 从中可以看到 $Y$ 要比 $X$ **随机地小很多**——灯泡本身没变，只是"24 个里最早坏的那个"自然比"4 个里最早坏的那个"来得早。

> [!NOTE] 备注
> 顺带得到一个常用结论：$n$ 个独立 $\mathcal{E}(\lambda)$ 的最小值服从 $\mathcal{E}(n\lambda)$。

### 3.3 Beta 分布

> [!IMPORTANT] 定义（Beta 分布 $\text{Beta}(\alpha,\beta)$）
> 设 $\alpha,\beta$ 是正常数，如果 $X$ 的密度是
> 
> $$
> f(x)=\frac{1}{B(\alpha,\beta)}x^{\alpha-1}(1-x)^{\beta-1},\quad 0<x<1,
> $$
> 
> 其中 $B(\alpha,\beta)=\dfrac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}$，则称 $X$ 服从参数为 $(\alpha,\beta)$ 的 Beta 分布，记作 $X\sim\text{Beta}(\alpha,\beta)$。

**直觉**：Beta 分布是"取值限制在 $(0,1)$ 上的万能形状分布"，常用来描述一个**概率/比例**本身的不确定性。

密度形状（随参数变化）：
- 当 $\alpha=\beta=1$ 时，为均匀分布 $\mathcal{U}(0,1)$；
- 当 $\alpha=2$，$\beta=1$ 时，密度函数呈直线型；
- 当 $\alpha=\beta=1/2$ 时，密度函数呈上 U 型（两端高中间低）；
- 当 $\alpha=\beta=2$ 时，密度函数呈下 U 型（中间高两端低）。

> [!NOTE] 备注：Beta 分布的两个身份
> 1. **贝叶斯统计中的先验分布**：它是二项分布的**共轭分布**。若 $X\mid p\sim\text{Binomial}(n,p)$，参数 $p$ 的先验取 $\text{Beta}(\alpha,\beta)$，观测 $X$ 后得到后验 $p\mid X\sim\text{Beta}(\alpha+X,\beta+n-X)$（直观解释：$\alpha,\beta$ 像"虚拟的成功/失败次数"；学习条件分布后将可以证明）。
> 2. **均匀分布的次序统计量**：Beta 分布可看作是均匀分布 $\mathcal{U}(0,1)$ 的次序统计量。（注：此步补全对应关系——设 $U_1,\ldots,U_n$ i.i.d. $\sim\mathcal{U}(0,1)$，则 $F(x)=x$，$f(x)=1$，由性质 2.2，$U_{(k)}$ 的密度为 $n\binom{n-1}{k-1}x^{k-1}(1-x)^{n-k}$，恰为 $\text{Beta}(k,\ n-k+1)$。）

---

## 四、随机变量的 p 分位数

设 $X$ 是 $(\Omega,\mathcal{F},\mathbb{P})$ 上的 r.v.，$F(x)$ 是其分布函数。

### 4.1 定义

> [!IMPORTANT] 直观定义（随机变量的 p 分位数, p-quantile）
> 对 $p\in(0,1)$，如果
> 
> $$
> \mathbb{P}(X\le x)\ge p,\qquad\mathbb{P}(X\ge x)\ge 1-p,
> $$
> 
> 称 $x$ 为 $X$ 的 **p-分位数**。

**直觉**：$x$ 把分布"按概率 $p:(1-p)$ 切开"——左边至少占 $p$，右边至少占 $1-p$。**上述定义方式所确定的 p-分位数不一定唯一**（如 CDF 有平台段时，一整段都满足）。

> [!IMPORTANT] 正式定义（满足唯一性）
> 对 $p\in(0,1)$，定义
> 
> $$
> F^{-1}(p)=\inf\{x\mid F(x)\ge p\}.
> $$
> 
> 称 $F^{-1}(p)$ 为 $F$ 的或者 $X$ 的 p 分位数，通常用 $\xi_p$ 表示。特别地，称 $\xi_{\frac{1}{2}}$ 为 $F$ 或 $X$ 的**中位数**。

**直觉**：在所有"CDF 已经爬到 $p$ 以上"的位置里取最左边那个，强行选出唯一代表。$F^{-1}$ 称为**广义反函数/分位数函数**——即使 $F$ 不严格单调、不连续，它也总有定义。

> [!NOTE] 备注：其它等价定义
> 对 $p\in(0,1)$，
> 
> $$
> F^{-1}(p)=\sup\{x\mid F(x)<p\}.
> $$
> 
> （从右逼近平台/跳跃点，与 $\inf$ 定义给出同一个值。）

> [!EXAMPLE]- 例题：$\mathcal{N}(0,1)$ 的分位数（查表 $p\mapsto x=F^{-1}(p)$）
> **解**：标准正态 CDF 连续且严格递增，$F^{-1}$ 就是普通反函数。常用值：
> 
> | $p$（area from $-\infty$ to $x$） | $x=F^{-1}(p)$ |
> | --- | --- |
> | 0.999 | 3.090232 |
> | 0.998 | 2.878162 |
> | 0.995 | 2.575829 |
> | 0.99 | 2.326348 |
> | 0.98 | 2.053749 |
> | 0.95 | 1.644854 |
> | 0.90 | 1.281552 |
> | 0.80 | 0.841621 |
> | 0.50 | 0.000000 |

### 4.2 常见应用简介

- **统计推断**（通常不要求唯一性）。例：抛 100 次均匀的硬币，得到 100 次正面很罕见，我们就会怀疑它不均匀；但 99 次罕见么？98 次？通常，我们会基于概率定义一个范围——95% 的概率落在多少次内？（即用分位数确定取值范围）
- **统计计算**（要求唯一性）。例：Simulation（随机模拟/生成随机数），见 4.4 节。

### 4.3 p 分位数的性质

> [!IMPORTANT] p 分位数的性质（设 $F^{-1}(p)=\inf\{x\mid F(x)\ge p\}$）
> 
> | 编号 | 性质 | 标注 |
> | --- | --- | --- |
> | 1 | $F^{-1}(p)$ 单调非降 | 常用 |
> | 2 | $F^{-1}(F(x))\le x$，$\forall x\in\mathbb{R}$ | 常用 |
> | 3 | $F\big(F^{-1}(p)\big)\ge p$，$\forall p\in(0,1)$ | 常用 |
> | 4 | $F^{-1}(p)\le t\Leftrightarrow p\le F(t)$ | 常用（生成随机数的关键） |
> | 5 | $F^{-1}(p)$ 是左连续的 | 了解即可 |
> | 6 | 如果 $F$ 是连续的，则 $F\big(F^{-1}(p)\big)=p$，$\forall p\in(0,1)$ | 常用 |
> 
> 性质的证明依赖于 CDF 的性质（单调非降、右连续），详见附录（第六部分）。

> [!WARNING] 辨析：$F^{-1}$ 不是普通的反函数
> - 一般只有不等式：$F^{-1}(F(x))\le x$（$F$ 在平台段上"压缩信息"，反推回去只能到平台左端）与 $F(F^{-1}(p))\ge p$（$F$ 有跳跃时会"跳过" $p$）；
> - 仅当 $F$ 连续时才有 $F(F^{-1}(p))=p$（性质 6）；仅当 $F$ 严格递增时才有 $F^{-1}(F(x))=x$；
> - 最常用的桥梁是性质 4 的等价关系 $F^{-1}(p)\le t\Leftrightarrow p\le F(t)$，它无条件成立，很多证明（如定理 3.1）靠它"搬运"不等号。

### 4.4 随机变量的生成

> [!IMPORTANT] 定理 3.1（产生服从分布函数 $F(x)$ 的随机变量）
> 设 $X\sim\mathcal{U}(0,1)$，$F(x)$ 是连续分布函数，则 $Y=F^{-1}(X)\sim F$。

**证明**：显然（利用性质 4：$F^{-1}(X)\le y\Leftrightarrow X\le F(y)$，以及 $X\sim\mathcal{U}(0,1)$ 时 $\mathbb{P}(X\le u)=u$）

$$
F_Y(y)=\mathbb{P}(Y\le y)=\mathbb{P}\big(F^{-1}(X)\le y\big)=\mathbb{P}\big(X\le F(y)\big)=F(y),
$$

因此 $Y\sim F$。

**直觉**：均匀随机数 $U$ 落在 $[0,p]$ 的概率恰好是 $p$，把它通过 $F^{-1}$ "搬"到 $x$ 轴上，落在 $(-\infty,x]$ 的概率就恰好是 $F(x)$——这就是**逆变换采样法 (inverse transform sampling)**。

> [!EXAMPLE]- 例题：直观理解随机变量的生成——两点分布 $B(0.8)$
> **解**：目标：生成 $\mathbb{P}(X=1)=0.8$，$\mathbb{P}(X=0)=0.2$ 的随机数。流程：
> 
> $$
> B(0.8)\ \to\ F(x)\ \to\ F^{-1}(x)\ \to\ F^{-1}(U)\ \to\ F^{-1}(u_1),F^{-1}(u_2),\ldots
> $$
> 
> 这里 $F(x)$ 在 $0$ 处跳到 $0.2$、在 $1$ 处跳到 $1$，故（注：此步补全分位数函数的显式形式）
> 
> $$
> F^{-1}(u)=\begin{cases}0, & 0<u\le 0.2,\\ 1, & 0.2<u<1.\end{cases}
> $$
> 
> e.g. $F^{-1}(0.12)=0$，$F^{-1}(0.91)=1$，……多次 i.i.d. 实现后，0 与 1 的频数比例约为 $0.2:0.8$（课件直方图所示）。可见**离散分布也能用 $F^{-1}(U)$ 生成**（定理 3.1 的"连续"假设是为了证明 $Y$ 的 CDF 恰为 $F$；对离散情形按上式分段定义同样可行）。

> [!EXAMPLE]- 例题 3.1：用均匀随机数生成 $\mathcal{E}(\lambda)$、Cauchy、$\mathcal{N}(0,1)$
> 设易生成服从均匀分布的随机变量，如何生成服从下列分布函数的随机变量：(1) $\mathcal{E}(\lambda)$，(2) Cauchy 分布，(3) $\mathcal{N}(0,1)$。
> 
> **解**：设 $U,V\sim\mathcal{U}(0,1)$。
> 
> (1) $X=-\lambda^{-1}\log(1-U)$。
> 
> （注：此步补全推导——$\mathcal{E}(\lambda)$ 的 CDF 为 $F(x)=1-e^{-\lambda x}$，$x>0$。解 $F(x)=u$：$e^{-\lambda x}=1-u\Rightarrow x=-\lambda^{-1}\log(1-u)$，即 $F^{-1}(u)=-\lambda^{-1}\log(1-u)$，套用定理 3.1。课件演示了 R 代码 `u = runif(1); x = -log(1-u)/lambda` 及生成 Exp(3.5) 直方图。）
> 
> (2) $Z=X/Y$，其中 $X,Y$ 是独立的且服从 $\mathcal{N}(0,1)$。
> 
> （由例 1.10，两独立标准正态之商服从 Cauchy 分布；而 $X,Y$ 可由 (3) 生成。这是"殊途同归/曲线救国"：不用 Cauchy 的 $F^{-1}(u)=\tan(\pi(u-\frac{1}{2}))$ 也能生成。）
> 
> (3) 令 $\theta=2\pi U$，$R=\sqrt{-2\log V}$，则 $X=R\cos\theta$ 和 $Y=R\sin\theta$ 独立，都服从 $\mathcal{N}(0,1)$。
> 
> 【这里巧妙使用了坐标变换（Box–Muller，见例 1.8、例 1.9），具体推导**不要求掌握**。背景：$\mathcal{N}(0,1)$ 的 CDF 没有初等闭式反函数，直接用定理 3.1 不便，于是借助极坐标"曲线救国"。】

> [!NOTE] 总结：随机变量的 p 分位数（课件要求）
> - **掌握**定义（直观定义；满足唯一性的正式定义）。
> - **能够应用**：
>   - 统计推断——确定取值范围：给定分布和 $p$ 值下，能计算对应的 p-分位数；
>   - 统计计算——生成随机数：掌握理论，例如 $F^{-1}(U)\sim F(x)$；了解如何模拟生成随机数。
> - **建议**：连续型随机变量一定掌握（本质就是 CDF 的反函数）；例题中正态分布、Cauchy 分布的生成属于较复杂情形，不做硬性要求；离散型随机变量根据自己情况酌情掌握。

---

## 五、小结

### 5.1 小结：随机向量函数的分布

- **问题**：一般情形；特殊情形（和、差；多对多）。
- **方法**：
  - CDF 曲线法（先求分布函数再求导）；
  - PDF 直接法：微元法、增补变量法、转换成已有结果法（e.g. 减法转为加法、乘法转为除法）。
- **经典结论**：
  - 3 大统计核心分布（$\chi^2$、$t$、$F$）与正态分布的关系；
  - Cauchy 分布的密度函数求解（正态之商）；
  - 多个叠加趋近正态——直观感受（CLT 预览）。

### 5.2 小结：重点知识点与技巧

- **重点知识点**：
  - 计算随机向量函数的分布 (CDF, PDF, PMF) / 相应概率；
  - 次序统计量的定义、（连续型随机变量下）PDF/CDF 的计算；
  - 基于分布函数得到的 p-分位数。
- **技巧**：
  - 蕴含独立性的联合概率密度的快速拆解（归一化）；
  - 殊途同归的选择：同一问题的不同解法，可能曲线救国计算更简便（e.g. Cauchy 分布 PDF 的计算、Normal r.v. 的生成）；
  - 微元法求解/理解 PDF。

---

## 六、附录：次序统计量性质、p 分位数性质的证明

### 6.1 性质 2.5 及证明

> [!IMPORTANT] 性质 2.5
> $(X_{(1)},X_{(2)},\ldots,X_{(n)})$ 的联合分布 $F_n(x_1,x_2,\ldots,x_n)$ 是连续函数。

**证明**：只须证明每个 $X_{(k)}$ 的分布函数连续，即单点概率为零。利用 $\mathbb{P}(X_1=x)=0$（$X_1$ 连续型），得

$$
\begin{align}
\mathbb{P}(X_{(k)}=x)&=\mathbb{P}(\{X_j\}\text{中有}k-1\text{个}<x,\ \text{有一个}=x,\ \text{有}n-k\text{个}>x)\\
&=\frac{n!}{(k-1)!\,1!\,(n-k)!}\,[\mathbb{P}(X_1<x)]^{k-1}\,\mathbb{P}(X_1=x)\,[1-F_1(x)]^{n-k}\\
&=0.
\end{align}
$$

### 6.2 p 分位数性质 1–6 的证明

**性质 1：$F^{-1}(p)$ 单调非降。**

证明：对任意的 $p_1<p_2$：如果 $F(t)\ge p_2$，则 $F(t)\ge p_2>p_1$，所以 $\{t:F(t)\ge p_1\}\supset\{t:F(t)\ge p_2\}$，于是

$$
F^{-1}(p_1)=\inf\{t:F(t)\ge p_1\}\le\inf\{t:F(t)\ge p_2\}=F^{-1}(p_2).
$$

（集合越大，下确界越小或不变。）

**性质 2：$F^{-1}(F(x))\le x$，$\forall x\in\mathbb{R}$。**

证明：$F^{-1}(F(x))=\inf\{t:F(t)\ge F(x)\}\le x$，因为 $x\in\{t:F(t)\ge F(x)\}$（$x$ 本身就满足条件，下确界不超过它）。

**性质 3：$F(F^{-1}(p))\ge p$，$\forall p\in(0,1)$。**

证明：首先，集合 $\{t:F(t)\ge p\}$ 一定具有如下形式：

$$
\{t:F(t)\ge p\}=(a,\infty)\ \text{或}\ [a,\infty).\tag{1}
$$

（事实上一定不是 $(a,\infty)$ 这种开形式，见下。）为此，假定 $r\in\{t:F(t)\ge p\}$（蕴含了 $F(r)\ge p$），则对任意的 $r'>r$ 有 $F(r')\ge F(r)\ge p$（$F$ 单调非降），即 $r'\in\{t:F(t)\ge p\}$——所以该集合是向右无界的区间。

由 (1)，得 $F^{-1}(p)=\inf\{t:F(t)\ge p\}=a$。由于 $a+n^{-1}\in\{t:F(t)\ge p\}$，有 $F(a+n^{-1})\ge p$。令 $n\to\infty$，并利用 $F$ 的**右连续性**，得

$$
F\big(F^{-1}(p)\big)=F(a)=\lim_{n\to\infty}F(a+n^{-1})\ge p.
$$

> [!NOTE] 注
> 上述证明中，$a=F^{-1}(p)\in\{t:F(t)\ge p\}$，因此有
> 
> $$
> \{t:F(t)\ge p\}=[a,\infty)=[F^{-1}(p),\infty),
> $$
> 
> 故 $F^{-1}(p)=\inf\{t:F(t)\ge p\}=\min\{t:F(t)\ge p\}$（下确界可以取到）。

**性质 4：$F^{-1}(p)\le t\Leftrightarrow p\le F(t)$。**

证明：($\Leftarrow$) 如果 $F(t)\ge p$，则 $t\in\{t:F(t)\ge p\}$，于是 $t\ge\inf\{t:F(t)\ge p\}=F^{-1}(p)$。

($\Rightarrow$) 如果 $F^{-1}(p)\le t$，由于 $F$ 是单调非降的，利用性质 3 有 $F(t)\ge F\big(F^{-1}(p)\big)\ge p$。

**性质 5：$F^{-1}(p)$ 是左连续的。**

证明：令 $p_n\uparrow p$。

- 由性质 1，$F^{-1}(p_n)\le F^{-1}(p)$ 且单调，不妨设 $F^{-1}(p_n)\uparrow b$；
- 则 $F^{-1}(p_n)\le b\le F^{-1}(p)$，$\forall n$；由 $F^{-1}(p_n)\le b$ 与性质 4 得 $p_n\le F(b)$；
- 令 $n\to\infty$：$F(b)\ge\lim_{n\to\infty}p_n=p$；
- 于是 $b\ge F^{-1}\big(F(b)\big)\ge F^{-1}(p)$（第一个不等号利用性质 2，第二个由 $F(b)\ge p$ 与性质 1 的单调性得到）；
- 结合 $b\le F^{-1}(p)$，得 $\lim_{n\to\infty}F^{-1}(p_n)=b=F^{-1}(p)$。

**性质 6：如果 $F$ 是连续的，则 $F(F^{-1}(p))=p$，$\forall p\in(0,1)$。**

证明：由性质 3，$F(F^{-1}(p))\ge p$。现在证明等号成立。

（反证法）假设不成立，令 $a=F^{-1}(p)$，有 $F(a)>p$。利用 $F$ 的连续性和单调性，则存在 $\delta>0$ 使得 $F(a-\delta)\ge p$，因此

$$
a-\delta\ge F^{-1}\big(F(a-\delta)\big)\ge F^{-1}(p)=a
$$

（第一个不等号利用性质 2，第二个利用性质 1）。此蕴含了 $\delta\le 0$，矛盾！

---

## 本讲方法/题型清单

- **求 $g(\vec{X})$ 的分布（一般情形）** → CDF 曲线法 → 写出 $F_Z(z)=\mathbb{P}(g(\vec{X})\le z)$，化为联合密度在区域 $\{g(\vec{x})\le z\}$ 上的积分（几何面积/极坐标常帮大忙），最后对 $z$ 求导得密度（例 1.1、1.2）。
- **求和 $Z=X+Y$ 的分布** → 卷积公式 → 离散：$P_Z(z)=\sum_x P_X(x)P_Y(z-x)$；连续：$f_Z(z)=\int f_X(x)f_Y(z-x)dx$；关键步骤：定支撑集 → 解示性函数约束得积分限 → 分段讨论（例 1.3–1.6）。
- **求差 $V=X-Y$** → 套差公式 $f_V(v)=\int f_X(x)f_Y(x-v)dx$，或转化为 $X+(-Y)$ 用加法卷积（例 1.7）。
- **求多对多变换 $(U,V)=T(X,Y)$ 的联合密度** → 定理 1.1 Jacobian 法 → 关键步骤：① 确定 $D$ 使 $\mathbb{P}((U,V)\in D)=1$；② 反解出全部分支 $x_i(u,v),y_i(u,v)$；③ 算 $\left|\frac{\partial(x,y)}{\partial(u,v)}\right|$（注意是**旧变量对新变量**求导）；④ 代入 $\sum_i f(x_i,y_i)|J_i|$（例 1.8、1.10）。
- **求乘积/商的分布** → 增补变量法 → 补 $W=X$（或 $W=Y$）凑成二维可逆变换，求联合密度后积分掉辅助变量；或如例 1.1 直接 CDF 法。
- **判断变换后变量是否独立** → 看联合密度能否在乘积型区域上分离变量 → 能分离则独立，各因子归一化即边缘密度（例 1.8、1.10 的"快速拆解"）。
- **求 $X_{(k)}$（最小/最大/第 $k$ 小）的分布** → 性质 2.2 → 套 $g_k=n\binom{n-1}{k-1}F^{k-1}(1-F)^{n-k}f$；最小/最大值也可直接用 $\mathbb{P}(X_{(1)}>x)=[1-F]^n$、$\mathbb{P}(X_{(n)}\le x)=[F]^n$（例 2.2）。
- **求若干次序统计量的联合分布** → 性质 2.1（全体）或性质 2.4（两个）→ 记忆口诀：按"各段人数"写多项式系数 × 各段概率幂 × 在场点的密度。
- **遇到有序区域上的多重积分** → 性质 2.3 → $\int_{a<x_1<\cdots<x_k<b}\prod f=\frac{(F(b)-F(a))^k}{k!}$，配合 Fubini 归纳。
- **求给定分布的 p-分位数** → 正式定义 $F^{-1}(p)=\inf\{x:F(x)\ge p\}$ → 连续严格增时解方程 $F(x)=p$；有平台/跳跃时取"最左满足点"（注意不唯一性只出现在直观定义下）。
- **用均匀随机数生成指定分布** → 逆变换法（定理 3.1）→ 求 $F^{-1}$ 闭式（如 $\mathcal{E}(\lambda)$：$-\lambda^{-1}\log(1-u)$）；$F^{-1}$ 无闭式时曲线救国：Cauchy 用正态之商，正态用 Box–Muller 坐标变换（例 3.1）。
- **证明涉及 $F^{-1}$ 的命题** → 性质 4 桥梁 → 用 $F^{-1}(p)\le t\Leftrightarrow p\le F(t)$ 把分位数语句翻译成 CDF 语句（定理 3.1 的证明）。


---


> [!ABSTRACT] 补充笔记：p 分位数（p-quantile）

---

## 一、p 分位数的定义

### 1.1 直观定义（非正式）

> [!INFO] 定义（直观版）
> 
> 设 X 是概率空间 $(\Omega, \mathcal{F}, \mathbb{P})$ 上的随机变量，$F(x)$ 是其分布函数。
> 
> 对 $p \in (0, 1)$，如果实数 x 满足： $$\mathbb{P}(X \leq x) \geq p \quad \text{且} \quad \mathbb{P}(X \geq x) \geq 1-p$$ 则称 x 为 X 的 **p 分位数（p-quantile）**。

**解读这个定义**：

- 第一个条件 $\mathbb{P}(X \leq x) \geq p$：x 左边（含 x）累积了至少 p 的概率。
- 第二个条件 $\mathbb{P}(X \geq x) \geq 1-p$：x 右边（含 x）累积了至少 $1-p$ 的概率。

**为什么两个条件都要？**

如果只要第一个条件，那么比 x 大的任何值都会满足（因为 CDF 单调非降）。加上第二个条件，就是要求 x 不能太靠右——它右边也要有足够的概率。两个条件合起来，才把 x 夹在了"合理"的位置。

**⚠️ 注意：直观定义下，p 分位数不一定唯一！**

以最简单的例子说明：设 X 服从均匀分布 $\mathcal{U}(0,1)$，求 0.5 分位数（中位数）。

按直观定义，任何 $x = 0.5$ 都满足：$\mathbb{P}(X \leq 0.5) = 0.5 \geq 0.5$，$\mathbb{P}(X \geq 0.5) = 0.5 \geq 0.5$。  
事实上对连续分布，中位数是唯一的，但对**离散分布**，可能存在一个区间上的点都满足直观定义。

> **例**：抛一枚均匀硬币，$X \in {0, 1}$，$\mathbb{P}(X=0)=\mathbb{P}(X=1)=0.5$。
> 
> 寻找 0.5 分位数：
> 
> - 对 $x = 0$：$\mathbb{P}(X \leq 0) = 0.5 \geq 0.5$，$\mathbb{P}(X \geq 0) = 1 \geq 0.5$ ✓
> - 对 $x = 0.3$：$\mathbb{P}(X \leq 0.3) = 0.5 \geq 0.5$，$\mathbb{P}(X \geq 0.3) = 0.5 \geq 0.5$ ✓
> - 对 $x = 1$：$\mathbb{P}(X \leq 1) = 1 \geq 0.5$，$\mathbb{P}(X \geq 1) = 0.5 \geq 0.5$ ✓
> 
> 所以 $[0,1]$ 上的所有点都是 0.5 分位数！不唯一。

---

### 1.3 正式定义（唯一版）

由于不唯一性在某些应用场合（特别是统计计算，如模拟）很麻烦，我们需要一个能给出唯一答案的定义。

> [!INFO] 定义（正式版）
> 
> 对 $p \in (0, 1)$，定义： $$F^{-1}(p) = \inf{x \mid F(x) \geq p}$$ 称 $F^{-1}(p)$ 为 F 或 X 的 **p 分位数**，通常用 $\xi_p$ 表示。
> 
> 特别地，称 $\xi_{1/2}$（即 $p = 0.5$ 时的分位数）为 F 或 X 的**中位数（median）**。

**解读这个定义**：

$\inf$ 是"下确界"，即"最小的上界"，在实数中通常理解为：所有满足 $F(x) \geq p$ 的 x 中，**最小的那个**。

用人话说：从左往右扫描数轴，找到 **CDF 第一次不低于 p** 的那个 x 值，这就是 $F^{-1}(p)$。

**为什么这个定义是唯一的？**

因为下确界（inf）操作对一个集合总是给出唯一的值（集合的最小元素，或最大下界）。

**等价表述**（另一种写法，两者完全等价）：

$$F^{-1}(p) = \sup{x \mid F(x) < p}$$

即：所有使 CDF **严格小于** p 的 x 中，取最大的那个。（可以验证两种写法给出同一个值。）

---

### 1.4 两种定义之间的关系

- **直观定义**：不唯一，适用于统计推断（不需要精确唯一值的场合）。
- **正式定义**：唯一，适用于统计计算（需要精确唯一值，如随机数生成）。

正式定义给出的 $F^{-1}(p)$ **一定是**直观定义意义下的某个 p 分位数。（即正式定义是直观定义的一个特例。）

---

## 二、以标准正态分布为例

### 2.1 标准正态分布 $\mathcal{N}(0,1)$

标准正态分布的密度函数是那个著名的钟形曲线： $$f(x) = \frac{1}{\sqrt{2\pi}} e^{-x^2/2}$$

其 CDF 记为 $\Phi(x) = \mathbb{P}(X \leq x)$，没有解析表达式，通常查表。

**p 分位数的几何含义**：  
在钟形曲线上，从 $-\infty$ 积分到 x，得到的面积（概率）恰好等于 p。所以 $F^{-1}(p) = x$ 就是这个面积为 p 时对应的 x 值。

### 2.2 常用分位数表

|  左尾面积 p  | p 分位数 x = F⁻¹(p) |
| :------: | :--------------: |
|  0.999   |     3.090232     |
|  0.998   |     2.878162     |
|  0.995   |     2.575829     |
|   0.99   |     2.326348     |
|   0.98   |     2.053749     |
|   0.95   |     1.644854     |
|   0.90   |     1.281552     |
|   0.80   |     0.841621     |
| **0.50** |   **0.000000**   |

**解读**：

- p = 0.95 对应 x ≈ 1.645：标准正态分布中，95% 的概率落在 1.645 以下。
- p = 0.50 对应 x = 0：中位数是 0（由对称性，恰好一半落在左边，一半在右边）。
- 注意：表里只列了 p > 0.5 的情况。由对称性，若要 p = 0.05 的分位数，就是 $-1.645$（即 $\xi_{0.05} = -\xi_{0.95}$）。

---

## 三、p 分位数的常见应用

### 3.1 统计推断（不要求唯一性）

**场景**：判断一个硬币是否均匀。

抛 100 次均匀硬币，得到正面次数 X 服从 $\text{Binomial}(100, 0.5)$。

- 得到 100 次正面：几乎不可能（概率 $\approx 10^{-30}$），肯定有问题。
- 得到 99 次正面：也极罕见。
- 得到 80 次正面：还罕见吗？

我们的做法：**利用分位数定出一个合理范围**。例如，"在均匀硬币假设下，95% 的概率，正面次数会落在哪个区间？"

如果实际观测值落在这个区间之外，我们就有理由怀疑硬币不均匀。

这里用到的就是 p 分位数——取 $\xi_{0.025}$ 和 $\xi_{0.975}$，构成一个 95% 置信区间。

**注意**：这里不要求 p 分位数唯一，因为我们只需要一个合理的范围。

### 3.2 统计计算（要求唯一性）

**场景**：用计算机模拟生成服从特定分布的随机数（Simulation / 随机数生成）。

这里需要唯一的分位数，因为要对每个均匀分布的随机数 U 精确计算 $F^{-1}(U)$。

具体方法见第四节（随机变量的生成）。

---

## 四、p 分位数的性质

### 4.1 六条基本性质

设 F 是某个连续型或离散型随机变量的 CDF，$F^{-1}$ 是按正式定义给出的分位数函数。

**性质 1**：$F^{-1}(p)$ 关于 p 单调非降。

> **理解**：p 越大（要求累积更多概率），对应的分位数 x 只能更大或不变。

**性质 2**：$F^{-1}(F(x)) \leq x$，对所有 $x \in \mathbb{R}$ 成立。

> **理解**：先把 x 用 F 映射到概率空间，再用 $F^{-1}$ 映射回来，结果不超过原来的 x。
> 
> **为什么是 ≤ 而不是 =？** 对于连续分布，等号成立；但对于离散分布，CDF 是阶梯函数，从一个"台阶"上的 x 映射到概率 F(x)，再反映射回来，会回到台阶的左端点（可能比原来的 x 小）。

**性质 3**：$F(F^{-1}(p)) \geq p$，对所有 $p \in (0,1)$ 成立。

> **理解**：先用 $F^{-1}$ 把概率 p 映射到实数轴，再用 F 映射回来，结果不低于原来的 p。
> 
> **为什么是 ≥？** 因为 $F^{-1}(p)$ 被定义为"使 F(x) ≥ p 的最小 x"，所以 $F(F^{-1}(p)) \geq p$ 是定义的直接推论。

**性质 4**：$F^{-1}(p) \leq t \iff p \leq F(t)$，对所有 $t \in \mathbb{R}$，$p \in (0,1)$。

**性质 5**：$F^{-1}(p)$ 是左连续的。

> **理解**：当 p 从左边趋向某个值时，$F^{-1}$ 的极限等于该点的值。
> 
> 注意：CDF 本身是右连续的；而它的"广义逆"（分位数函数）是**左连续**的。两者的连续性方向相反，这是个重要但容易搞混的细节。

**性质 6**：如果 F 是连续的（即 X 是连续型随机变量），则 $F(F^{-1}(p)) = p$，对所有 $p \in (0,1)$ 成立。

> **理解**：性质 3 说的是 ≥，但当 F 连续时，等号成立。即先走 $F^{-1}$ 再走 F，完美"还原"了原来的 p。
> 
> 这对应着我们熟悉的"连续型随机变量的 CDF 是严格单调的，因此 $F^{-1}$ 是真正的反函数"。

### 4.2 如何记住这些性质？

| 性质                       | 记忆口诀                                 |
| ------------------------ | ------------------------------------ |
| 1. 单调非降                  | 分位数随 p 增大只增不减                        |
| 2. $F^{-1}(F(x)) \leq x$ | 反-正 组合，结果不超过原来                       |
| 3. $F(F^{-1}(p)) \geq p$ | 正-反 组合，结果不低于原来                       |
| 4. 互逆关系                  | $F^{-1}(p) \leq t$ 等价于 $p \leq F(t)$ |
| 5. 左连续                   | F 右连续，$F^{-1}$ 左连续（方向相反）             |
| 6. 连续时等号成立               | F 连续 → $F(F^{-1}(p)) = p$（真正的反函数）    |

> **证明提示**（不要求掌握细节）：所有这些性质的证明都依赖于 CDF 的基本性质，详见教材附录。

---

## 五、随机变量的生成（Simulation）

这一节解释了 p 分位数最重要的实际应用之一：**用均匀分布随机数生成任意分布的随机数**。

### 5.1 核心定理

> [!NOTE] 定理 3.1（概率积分变换的逆）
> 
> 设 $X \sim \mathcal{U}(0,1)$（X 服从 [0,1] 上的均匀分布），F(x) 是某个**连续**分布函数，则：
> 
> $$Y = F^{-1}(X) \sim F$$
> 
> 即 Y 服从分布函数为 F 的分布。

**证明**（很简洁，建议理解）：

计算 Y 的 CDF：

$$F_Y(y) = \mathbb{P}(Y \leq y) = \mathbb{P}(F^{-1}(X) \leq y)$$

利用性质 4（$F^{-1}(p) \leq t \iff p \leq F(t)$，令 $p = X$，$t = y$）：

$$= \mathbb{P}(X \leq F(y))$$

由于 $X \sim \mathcal{U}(0,1)$，$\mathbb{P}(X \leq c) = c$（对 $0 \leq c \leq 1$）：

$$= F(y)$$

所以 $Y \sim F$。证毕。✓

### 5.2 为什么这个定理很重要？

计算机只能直接生成均匀分布 $\mathcal{U}(0,1)$ 的随机数（通过伪随机数算法）。但实际应用中，我们需要指数分布、正态分布等各种分布的随机数。

这个定理告诉我们：**只需要两步**：

1. 生成 $U \sim \mathcal{U}(0,1)$（计算机容易做到）
2. 计算 $Y = F^{-1}(U)$（即求 p 分位数）

就可以得到服从分布 F 的随机数 Y。

### 5.3 直观理解：以 Bernoulli(0.8) 为例

**Bernoulli(0.8)**：X 取值 0 或 1，$\mathbb{P}(X=0) = 0.2$，$\mathbb{P}(X=1) = 0.8$。

**第一步**：写出 CDF：$$F(x) = \begin{cases} 0, & x < 0 \\ 0.2, & 0 \leq x < 1 \\ 1, & x \geq 1 \end{cases}$$

**第二步**：求 $F^{-1}$（分位数函数）：$$F^{-1}(p) = \begin{cases} 0, & 0 < p \leq 0.2 \\ 1, & 0.2 < p \leq 1 \end{cases}$$
**第三步**：生成随机数的过程：

- 计算机生成 $u_1 = 0.12$：$F^{-1}(0.12) = 0$（因为 $0.12 \leq 0.2$）→ 输出 0
- 计算机生成 $u_2 = 0.91$：$F^{-1}(0.91) = 1$（因为 $0.91 > 0.2$）→ 输出 1

**直觉验证**：均匀分布中，0.12 在 0.2 的左边，落入"输出 0"的区域（概率 20%）；0.91 在 0.2 的右边，落入"输出 1"的区域（概率 80%）。这正好对应 Bernoulli(0.8)！

多次重复这个过程，生成的 0 和 1 序列，就会以大约 20%:80% 的比例分布。

### 5.4 具体例子：如何生成常见分布的随机数

**例 3.1**：假设已经能生成 $\mathcal{U}(0,1)$ 随机数，如何生成以下分布的随机数？

---

#### 情形 (1)：指数分布 $\mathcal{E}(\lambda)$（需要掌握）

**指数分布的 CDF**： $$F(x) = 1 - e^{-\lambda x}, \quad x \geq 0$$

**求 $F^{-1}(p)$**：令 $F(x) = p$，即 $1 - e^{-\lambda x} = p$，解出 x： $$e^{-\lambda x} = 1-p \Rightarrow -\lambda x = \log(1-p) \Rightarrow x = -\frac{1}{\lambda}\log(1-p)$$

**生成方法**：设 $U \sim \mathcal{U}(0,1)$，令 $$X = -\frac{1}{\lambda}\log(1-U)$$ 则 $X \sim \mathcal{E}(\lambda)$。

**R 语言验证**（课件中给出的示例）：

```r
> u = runif(1)   # 生成一个 [0,1] 均匀随机数
> u
[1] 0.335191
> x = -log(1-u)/lambda
> x
[1] 0.1166444
```

**小技巧**：由于 $1-U$ 也服从 $\mathcal{U}(0,1)$（均匀分布关于 0.5 对称），实际中常写成： $$X = -\frac{1}{\lambda}\log U$$ （用 $U$ 代替 $1-U$，因为二者同分布，结果一样。）

---

#### 情形 (2)：Cauchy 分布（了解即可，不做硬性要求）

**生成方法**：令 X, Y 独立且都服从 $\mathcal{N}(0,1)$，则 $Z = X/Y$ 服从 Cauchy 分布。

（这里用到了两个独立正态随机变量的比值服从 Cauchy 分布的结论。）

---

#### 情形 (3)：标准正态分布 $\mathcal{N}(0,1)$（了解即可，不做硬性要求）

标准正态的 CDF $\Phi(x)$ 没有解析表达式，因此直接用 $F^{-1}(U)$ 的方法不方便（无法写出 $\Phi^{-1}$ 的解析式）。

**Box-Muller 变换**：设 $U, V \sim \mathcal{U}(0,1)$ 独立，令 $$X = \sqrt{-2\log U} \cos(2\pi V), \quad Y = \sqrt{-2\log U} \sin(2\pi V)$$ 则 X, Y 相互独立，都服从 $\mathcal{N}(0,1)$。

> 这里用了极坐标变换的技巧（详见附录），课件标注"不要求掌握"，了解结论即可。

---

### 5.5 总结：生成随机数的通用流程

```
目标分布 F
  ↓  求 CDF 的反函数（分位数函数）
F⁻¹(x)
  ↓  代入均匀随机数 U
F⁻¹(U)  ←  这就是服从分布 F 的随机数！
```

---

## 六、p 分位数的等价定义

课件最后补充了一个等价定义：

> **等价定义**： $$F^{-1}(p) = \sup{x \mid F(x) < p}$$

和正式定义 $F^{-1}(p) = \inf{x \mid F(x) \geq p}$ 是完全等价的。

**两者的区别**（集合不同，但结论相同）：

- 正式定义：在"CDF 已经≥p"的 x 中取最小值。
- 等价定义：在"CDF 还<p"的 x 中取最大值。

这两个边界从两侧夹住了同一个点，所以结果相同。

---

## 七、知识总结与考试要求

### 7.1 必须掌握的内容

|知识点|具体要求|
|---|---|
|**直观定义**|能写出 $\mathbb{P}(X \leq x) \geq p$ 且 $\mathbb{P}(X \geq x) \geq 1-p$，理解其含义|
|**正式定义（唯一性）**|能写出 $F^{-1}(p) = \inf{x \mid F(x) \geq p}$，知道为什么用 inf|
|**两者关系**|直观定义不唯一，正式定义唯一；正式定义用于统计计算|
|**性质 1-6**|理解每条性质的含义，知道连续情况下性质 6 等号成立|
|**定理 3.1**|能陈述并证明：若 $U \sim \mathcal{U}(0,1)$，F 连续，则 $F^{-1}(U) \sim F$|
|**连续分布的随机数生成**|能对给定连续分布求出 $F^{-1}$ 并写出生成公式（如指数分布）|
|**应用场景**|知道统计推断和统计计算对唯一性的不同需求|

### 7.2 了解即可（不做硬性要求）

- Cauchy 分布和正态分布的具体生成方法
- Box-Muller 变换的证明
- 极坐标变换的技术细节（附录内容）

### 7.3 离散分布的情况

课件建议"根据自己情况酌情掌握"。对于离散分布，$F$ 是阶梯函数，$F^{-1}$ 仍然是按照 $\inf{x \mid F(x) \geq p}$ 定义的，但要注意 CDF 在跳跃点的值。如本讲义 5.3 节的 Bernoulli(0.8) 例子，是离散分布生成的好示范。

---

## 八、常见疑问解答

**Q1：p 分位数中的 p 必须在 (0,1) 内吗？**

A：是的，定义要求 $p \in (0,1)$。$p=0$ 和 $p=1$ 对应 $-\infty$ 和 $+\infty$，没有实际意义。

**Q2：中位数就是均值吗？**

A：不一定！中位数是 $\xi_{1/2}$（0.5 分位数），均值是期望 $\mathbb{E}[X]$。对称分布（如正态分布）中二者相等，但偏斜分布中通常不同。

**Q3：如果 CDF 在某点跳跃，分位数怎么取？**

A：按定义，$F^{-1}(p) = \inf{x \mid F(x) \geq p}$，即找到 CDF **第一次**达到 p 的 x 值。如果 CDF 在 $x_0$ 处跳跃，从 $F(x_0^-)$ 跳到 $F(x_0)$，那么所有 $p \in (F(x_0^-), F(x_0)]$ 的分位数都是 $x_0$。

**Q4：为什么 $F^{-1}$ 是左连续而 F 是右连续？**

A：这是数学上的对偶性。CDF 的右连续性来自于概率测度的基本性质；而 $F^{-1}$ 的左连续性可以从其定义 $\inf{x \mid F(x) \geq p}$ 中通过极限论证得到（详见附录）。记住这个"方向相反"的结论即可。

**Q5：定理 3.1 要求 F 连续，如果不连续（离散分布）怎么办？**

A：对于离散分布，$F^{-1}(U)$ 仍然有意义，只是证明不能直接用性质 4（此时需要处理 CDF 的跳跃）。结论仍然成立：$F^{-1}(U) \sim F$，但证明略复杂，不做要求。
