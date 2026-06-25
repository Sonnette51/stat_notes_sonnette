---
title: "Lecture14 多元正态分布"
tags:
  - 概率论
  - 后半学期
  - 多元正态分布
  - 协方差矩阵
  - MVN
---

# Lecture14 多元正态分布

## 一、随机向量的期望与协方差矩阵

> [!NOTE] 说明
> 本节内容与 Lecture 8 期望 handout 最后部分一致，此处作为完整回顾收录。

### 1.1 随机向量的期望

设 $\mathbf{X} = (X_1, \dots, X_n)^T$ 是 $n$ 维随机向量。如果对每个 $i$，$\mu_i = EX_i$ 存在，就称 $\mathbf{X}$ 的数学期望存在，并定义

$$
\boldsymbol{\mu} := E\mathbf{X} = (EX_1, \dots, EX_n)^T = (\mu_1, \dots, \mu_n)^T
$$

即**逐分量取期望**。

类似地，对随机矩阵

$$
\mathbf{Y} = \begin{pmatrix} X_{11} & X_{12} & \cdots & X_{1n} \\ X_{21} & X_{22} & \cdots & X_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ X_{m1} & X_{m2} & \cdots & X_{mn} \end{pmatrix}
$$

其数学期望定义为逐元素取期望：

$$
E\mathbf{Y} = \begin{pmatrix} EX_{11} & EX_{12} & \cdots & EX_{1n} \\ EX_{21} & EX_{22} & \cdots & EX_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ EX_{m1} & EX_{m2} & \cdots & EX_{mn} \end{pmatrix}
$$

### 1.2 期望的矩阵运算性质

> [!IMPORTANT] 性质 2.1（期望性质）
> 设 $\mathbf{X}, \mathbf{Y}$ 如上定义，且数学期望都存在。对任何常数向量 $\mathbf{a} = (a_1, \dots, a_n)^T$，常数矩阵 $\mathbf{A}_{k \times m}$，$\mathbf{B}_{n \times j}$，有
>
> 1. $E(\mathbf{a}^T \mathbf{X}) = \mathbf{a}^T E\mathbf{X}$
> 2. $(E\mathbf{Y})^T = E(\mathbf{Y}^T)$
> 3. $E(\mathbf{A}\mathbf{Y}) = \mathbf{A} E(\mathbf{Y})$
> 4. $E(\mathbf{Y}\mathbf{B}) = E(\mathbf{Y}) \mathbf{B}$
> 5. $E(\mathbf{A}\mathbf{Y}\mathbf{B}) = \mathbf{A} E(\mathbf{Y}) \mathbf{B}$

本质上都基于**期望的线性性质**：期望可以和常数矩阵的乘法交换顺序。

> [!TIP] 约定
> 常见的写法是把向量都写成**列向量**。

### 1.3 随机向量的方差——协方差矩阵

以二维为例，设 $\vec{X} = (X_1, X_2)^T$。类比一维方差 $\operatorname{var}(X) = E[(X - \mu)^2]$，在向量情形中"平方"有两种理解：

**外积**（得到矩阵）：$(\mathbf{X} - \boldsymbol{\mu})(\mathbf{X} - \boldsymbol{\mu})^T$ 是 $n \times n$ 矩阵——这就是**协方差矩阵**。

**内积**（得到标量）：$(\mathbf{X} - \boldsymbol{\mu})^T(\mathbf{X} - \boldsymbol{\mu})$ 是 $1 \times 1$ 标量——这是 Mahalanobis 距离的平方（后面会用到）。

以 $n = 2$ 展开外积：

$$
\operatorname{var}(\vec{X}) = E\left[(\mathbf{X} - \boldsymbol{\mu})(\mathbf{X} - \boldsymbol{\mu})^T\right] = E\left[\begin{pmatrix} X_1 - \mu_1 \\ X_2 - \mu_2 \end{pmatrix} \begin{pmatrix} X_1 - \mu_1 & X_2 - \mu_2 \end{pmatrix}\right]
$$

$$
= E\begin{pmatrix} (X_1 - \mu_1)^2 & (X_1 - \mu_1)(X_2 - \mu_2) \\ (X_2 - \mu_2)(X_1 - \mu_1) & (X_2 - \mu_2)^2 \end{pmatrix} = \begin{pmatrix} \operatorname{var}(X_1) & \operatorname{cov}(X_1, X_2) \\ \operatorname{cov}(X_1, X_2) & \operatorname{var}(X_2) \end{pmatrix}
$$

> [!IMPORTANT] 定义 2.1（协方差矩阵 Covariance Matrix）
> 如果随机向量 $\mathbf{X}$ 的数学期望 $\boldsymbol{\mu} = E\mathbf{X}$ 存在，对每个分量 $X_i$ 的方差有限，则称
>
> $$\Sigma = E\left[(\mathbf{X} - \boldsymbol{\mu})(\mathbf{X} - \boldsymbol{\mu})^T\right] = (\sigma_{ij})$$
>
> 为 $\mathbf{X}$ 的**协方差矩阵**，其中 $\sigma_{ij} = \operatorname{cov}(X_i, X_j)$。

协方差矩阵 $\Sigma$ 是**对称矩阵**（因为 $\operatorname{cov}(X_i, X_j) = \operatorname{cov}(X_j, X_i)$）。如果行列式 $\det(\Sigma) = 0$，就称 $\Sigma$ 是**退化的**。

### 1.4 协方差矩阵的线性变换

> [!IMPORTANT] 常用性质
> 若 $B$ 是常数矩阵，$\vec{X}$ 有协方差矩阵 $\Sigma$，则
>
> $$\operatorname{var}(B\vec{X}) = E\left[B(\mathbf{X} - \boldsymbol{\mu})(\mathbf{X} - \boldsymbol{\mu})^T B^T\right] = B \Sigma B^T$$

这个公式在后面 MVN 的线性组合、条件分布等多处都会反复使用。推导只需把常数矩阵 $B$ 提到期望外面。

### 1.5 协方差矩阵的基本定理

> [!IMPORTANT] 定理 2.1
> 设 $\Sigma$ 是 $\mathbf{X} = (X_1, \dots, X_n)$ 的协方差矩阵，则
>
> 1. $\Sigma$ 是**非负定矩阵**；
> 2. $\Sigma$ 退化的充要条件是存在不全为零的常数 $a_1, \dots, a_n$ 使得
>
> $$\sum_{i=1}^{n} a_i(X_i - EX_i) = 0 \quad a.s.$$

**证明.**

任取一个 $n$ 维实向量 $\mathbf{a} = (a_1, \dots, a_n)^T$，有

$$
\mathbf{a}^T \Sigma \mathbf{a} = \sum_{i=1}^{n}\sum_{j=1}^{n} a_i a_j \sigma_{ij} = \sum_{i=1}^{n}\sum_{j=1}^{n} a_i a_j E\left[(X_i - EX_i)(X_j - EX_j)\right]
$$

利用期望的线性性，将 $\sum\sum$ 合并到期望内部：

$$
= E\left[\left(\sum_{i=1}^{n} a_i(X_i - EX_i)\right)^2\right] = \operatorname{var}\left[\sum_{i=1}^{n} a_i(X_i - EX_i)\right] \geq 0
$$

所以 $\Sigma$ 非负定。

$\Sigma$ 退化（即存在非零 $\mathbf{a}$ 使得 $\mathbf{a}^T \Sigma \mathbf{a} = 0$）等价于

$$
\operatorname{var}\left[\sum_{i=1}^{n} a_i(X_i - EX_i)\right] = 0 \quad \Longleftrightarrow \quad \sum_{i=1}^{n} a_i(X_i - EX_i) = 0 \quad a.s. \quad \blacksquare
$$

---

## 二、多元正态分布（MVN）

> [!NOTE] 考核说明
> 本节内容中，**二元正态分布在考核范围内**。目标：**掌握结论**，**了解证明**（证明过程主要基于特征函数和矩阵运算）。

### 2.1 MVN 的两种等价定义

#### 定义方式一：联合密度函数（$\Sigma$ 正定时）

> [!IMPORTANT] MVN 定义（密度函数形式）
> 当 $\Sigma$ 正定时，$\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$ 有联合密度函数
>
> $$f(\vec{x}) = \frac{1}{(\sqrt{2\pi})^n \sqrt{\det(\Sigma)}} \exp\left[-\frac{1}{2}(\vec{x} - \vec{\mu})^T \Sigma^{-1}(\vec{x} - \vec{\mu})\right]$$

其中 $\vec{\mu} \in \mathbb{R}^n$ 是均值向量，$\Sigma$ 是 $n \times n$ 正定协方差矩阵。

#### 定义方式二：线性变换（等价定义）

> [!IMPORTANT] 定义 1.1（multivariate normal distribution, MVN）
> 设 $\vec{\mu} = (\mu_1, \mu_2, \dots, \mu_n)^T$ 是 $n$ 维常数列向量，$\mathbf{B}$ 是 $n \times m$ 常数矩阵，$\varepsilon_1, \varepsilon_2, \dots, \varepsilon_m$ 是相互独立且服从标准正态分布的随机变量。如果
>
> $$\vec{X} = \vec{\mu} + \mathbf{B}\vec{\varepsilon}$$
>
> 其中 $\vec{\varepsilon} = (\varepsilon_1, \varepsilon_2, \dots, \varepsilon_m)^T$，且矩阵 $\mathbf{B}\mathbf{B}^T$ 满秩，就称 $\vec{X} = (X_1, X_2, \dots, X_n)^T$ 服从 $n$ 维正态分布，记作 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \mathbf{B}\mathbf{B}^T)$。

**核心思想：** 多元正态 = 均值平移 + 线性变换作用于独立标准正态。

**验证均值和协方差：** 因为 $\operatorname{cov}(\vec{\varepsilon}, \vec{\varepsilon}) = E(\vec{\varepsilon}\vec{\varepsilon}^T) = \mathbf{I}$（独立标准正态），所以

$$
E(\vec{X}) = \vec{\mu} + \mathbf{B} E(\vec{\varepsilon}) = \vec{\mu}
$$

$$
\Sigma := E\left[(\vec{X} - \vec{\mu})(\vec{X} - \vec{\mu})^T\right] = E\left[(\mathbf{B}\vec{\varepsilon})(\mathbf{B}\vec{\varepsilon})^T\right] = \mathbf{B} E(\vec{\varepsilon}\vec{\varepsilon}^T) \mathbf{B}^T = \mathbf{B}\mathbf{I}\mathbf{B}^T = \mathbf{B}\mathbf{B}^T
$$

> [!EXAMPLE] 例子
> 设 $\varepsilon_1 \sim \mathcal{N}(0,1)$，$\varepsilon_2 \sim \mathcal{N}(0,1)$，二者独立。令
>
> $$\begin{pmatrix} X_1 \\ X_2 \end{pmatrix} = \begin{pmatrix} \mu_1 \\ \mu_2 \end{pmatrix} + \begin{pmatrix} 1 & 1 \\ 1 & -1 \end{pmatrix}\begin{pmatrix} \varepsilon_1 \\ \varepsilon_2 \end{pmatrix}$$
>
> 则 $\vec{X} \sim \mathcal{N}\left(\begin{pmatrix}\mu_1\\\mu_2\end{pmatrix},\ \begin{pmatrix}1&1\\1&-1\end{pmatrix}\begin{pmatrix}1&1\\1&-1\end{pmatrix}^T\right) = \mathcal{N}\left(\begin{pmatrix}\mu_1\\\mu_2\end{pmatrix},\ \begin{pmatrix}2&0\\0&2\end{pmatrix}\right)$。

### 2.2 由等价定义得到联合密度

> [!IMPORTANT] 定理 1.1（密度函数）
> 当 $\Sigma$ 正定时，$\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$ 有联合密度函数
>
> $$f(\vec{x}) = \frac{1}{(\sqrt{2\pi})^n \sqrt{\det(\Sigma)}} \exp\left[-\frac{1}{2}(\vec{x} - \vec{\mu})^T \Sigma^{-1}(\vec{x} - \vec{\mu})\right]$$

**证明思路：**

因为 $\Sigma$ 正定，存在可逆方阵 $B$ 使得 $\Sigma = BB^T$，且 $\vec{X} = \vec{\mu} + B\vec{\varepsilon}$，其中 $\vec{\varepsilon} \sim \mathcal{N}(\vec{0}, \mathbf{I})$。

$\vec{\varepsilon}$ 的密度函数为 $f_{\vec{\varepsilon}}(\vec{y}) = \frac{1}{(\sqrt{2\pi})^n} \exp\left(-\frac{1}{2}\vec{y}^T\vec{y}\right)$。

做变量替换 $\vec{y} = B^{-1}(\vec{x} - \vec{\mu})$，这是一个可逆映射，雅克比行列式为

$$
\left|\frac{\partial \vec{y}}{\partial \vec{x}}\right| = |B^{-1}| = \frac{1}{\sqrt{\det(\Sigma)}}
$$

其中最后一步用到 $\det(\Sigma) = \det(BB^T) = (\det B)^2$，所以 $|B^{-1}| = 1/|\det B| = 1/\sqrt{\det(\Sigma)}$。

将 $\vec{y} = B^{-1}(\vec{x} - \vec{\mu})$ 代入 $\vec{y}^T \vec{y}$：

$$
\vec{y}^T \vec{y} = [B^{-1}(\vec{x}-\vec{\mu})]^T [B^{-1}(\vec{x}-\vec{\mu})] = (\vec{x}-\vec{\mu})^T (B^{-1})^T B^{-1} (\vec{x}-\vec{\mu}) = (\vec{x}-\vec{\mu})^T \Sigma^{-1} (\vec{x}-\vec{\mu})
$$

其中 $(B^{-1})^T B^{-1} = (BB^T)^{-1} = \Sigma^{-1}$。

综合得到 $f(\vec{x}) = f_{\vec{\varepsilon}}(\vec{y}) \cdot \left|\frac{\partial \vec{y}}{\partial \vec{x}}\right|$，即定理中的密度公式。$\blacksquare$

### 2.3 MVN 的特征函数

> [!IMPORTANT] 特征函数
> 若 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$，则 $\vec{X}$ 的特征函数为
>
> $$\phi_{\vec{X}}(\vec{t}) = E\exp(i\vec{t}^T\vec{X}) = \exp\left[i\vec{t}^T\vec{\mu} - \frac{1}{2}\vec{t}^T\Sigma\vec{t}\right]$$

**推导：**

先求 $\vec{\varepsilon} \sim \mathcal{N}(\vec{0}, \mathbf{I})$ 的特征函数。由独立性：

$$
\phi_{\vec{\varepsilon}}(\vec{t}) = E\left[\exp(i\vec{t}^T\vec{\varepsilon})\right] = E\left[\prod_{i=1}^{n}\exp(it_i\varepsilon_i)\right] = \prod_{i=1}^{n}E[\exp(it_i\varepsilon_i)] = \prod_{j=1}^{n}\exp\left(\frac{-t_j^2}{2}\right) = \exp\left(-\frac{\vec{t}^T\vec{t}}{2}\right)
$$

然后对 $\vec{X} = \vec{\mu} + \mathbf{B}\vec{\varepsilon}$：

$$
\phi_{\vec{X}}(\vec{t}) = E\exp(i\vec{t}^T\vec{X}) = E\exp\left[i(\vec{t}^T\vec{\mu} + \vec{t}^T\mathbf{B}\vec{\varepsilon})\right] = \exp(i\vec{t}^T\vec{\mu}) \cdot E\exp\left[i(\vec{t}^T\mathbf{B})\vec{\varepsilon}\right]
$$

注意 $\vec{t}^T\mathbf{B}$ 是一个 $1 \times m$ 行向量，将其视作新的参数向量代入 $\phi_{\vec{\varepsilon}}$：

$$
= \exp(i\vec{t}^T\vec{\mu}) \cdot \exp\left[-\frac{1}{2}(\vec{t}^T\mathbf{B})(\vec{t}^T\mathbf{B})^T\right] = \exp\left[i\vec{t}^T\vec{\mu} - \frac{1}{2}\vec{t}^T\mathbf{B}\mathbf{B}^T\vec{t}\right]
$$

因为 $\mathbf{B}\mathbf{B}^T = \Sigma$，得到最终结果。

> [!TIP] 重要推论
> 从特征函数可以看出，$\vec{X}$ 的**期望和协方差矩阵唯一决定了特征函数**。由于随机向量的特征函数与分布函数相互唯一决定，所以 $\vec{X}$ 的分布由 $\vec{\mu}$ 和 $\Sigma$ **唯一决定**。

### 2.4 边缘分布

> [!IMPORTANT] 边缘分布性质
> 如果 $\vec{X}$ 服从多元正态分布，则 $\vec{X}$ 的**任何分量子向量** $(X_{j_1}, \dots, X_{j_k})^T$ 也服从（多元）正态分布。

这可以直接从定义 1.1 看出：选取 $\vec{X}$ 的若干分量，相当于用一个选取矩阵左乘 $\vec{X}$，结果仍然是正态向量加上常数的形式。

> [!EXAMPLE] 例子
> 接上面的例子，$\vec{X} = \vec{\mu} + \mathbf{B}\vec{\varepsilon}$，其中 $X_1 = \mu_1 + \varepsilon_1 + \varepsilon_2$。由于 $\varepsilon_1 + \varepsilon_2$ 是独立标准正态的线性组合，$X_1$ 自然服从一元正态分布 $\mathcal{N}(\mu_1, 2)$。

### 2.5 线性组合

> [!IMPORTANT] 定理 1.2（线性组合）
> 如果 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$，则对任意常数矩阵 $\mathbf{A}$ 和常数向量 $\vec{b}$，只要 $\vec{b} + \mathbf{A}\vec{X}$ 有意义且 $\mathbf{A}\Sigma\mathbf{A}^T$ 满秩，则
>
> $$\vec{Y} = \vec{b} + \mathbf{A}\vec{X} \sim \mathcal{N}\left(\vec{b} + \mathbf{A}\vec{\mu},\ \mathbf{A}\Sigma\mathbf{A}^T\right)$$

**证明：**

$\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$ 意味着存在 $\mathbf{B}$ 和独立标准正态 $\vec{\varepsilon}$ 使得 $\vec{X} = \vec{\mu} + \mathbf{B}\vec{\varepsilon}$。

$$
\vec{Y} = \vec{b} + \mathbf{A}\vec{X} = (\vec{b} + \mathbf{A}\vec{\mu}) + (\mathbf{A}\mathbf{B})\vec{\varepsilon}
$$

这恰好是定义 1.1 的形式（新均值 $= \vec{b} + \mathbf{A}\vec{\mu}$，新矩阵 $= \mathbf{A}\mathbf{B}$），所以 $\vec{Y}$ 服从多元正态分布。其协方差矩阵为 $(\mathbf{A}\mathbf{B})(\mathbf{A}\mathbf{B})^T = \mathbf{A}\mathbf{B}\mathbf{B}^T\mathbf{A}^T = \mathbf{A}\Sigma\mathbf{A}^T$。$\blacksquare$

> [!EXAMPLE] 例：线性变换计算
> 设 $\begin{pmatrix}X_1\\X_2\end{pmatrix} \sim \mathcal{N}\left(\begin{pmatrix}1\\-5\end{pmatrix}, \begin{pmatrix}4&-2\\-2&9\end{pmatrix}\right)$，令
>
> $$\begin{pmatrix}Y_1\\Y_2\end{pmatrix} = \begin{pmatrix}1\\0\end{pmatrix} + \begin{pmatrix}1&0\\1&1\end{pmatrix}\begin{pmatrix}X_1\\X_2\end{pmatrix}$$
>
> 则 $\vec{Y} \sim \mathcal{N}\left(\begin{pmatrix}1\\0\end{pmatrix} + \begin{pmatrix}1&0\\1&1\end{pmatrix}\begin{pmatrix}1\\-5\end{pmatrix},\ \begin{pmatrix}1&0\\1&1\end{pmatrix}\begin{pmatrix}4&-2\\-2&9\end{pmatrix}\begin{pmatrix}1&1\\0&1\end{pmatrix}\right)$
>
> 均值为 $\begin{pmatrix}2\\-4\end{pmatrix}$，协方差矩阵需要具体计算矩阵乘法。

### 2.6 判定法则（实用工具）

> [!IMPORTANT] 定理 1.3（重要判定法则）
> $\vec{X} = (X_1, X_2, \dots, X_n)^T \sim \mathcal{N}(\vec{\mu}, \Sigma)$ 的**充要条件**是：对任何 $\vec{a} = (a_1, a_2, \dots, a_n)^T \in \mathbb{R}^n$，
>
> $$Y := \vec{a}^T\vec{X} \sim \mathcal{N}(\vec{a}^T\vec{\mu},\ \vec{a}^T\Sigma\vec{a})$$

**翻译成人话：** 一个随机向量是多元正态的，当且仅当它的**所有一维线性组合**都是一元正态的。

**证明：**

**（$\Rightarrow$）** 若 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$，$Y = \vec{a}^T\vec{X}$ 的特征函数：

$$
\phi_Y(t) = E\exp(itY) = E\exp\left[i(t\vec{a}^T)\vec{X}\right] = \exp\left[it(\vec{a}^T\vec{\mu}) - \frac{1}{2}t^2 \vec{a}^T\Sigma\vec{a}\right] \tag{1}
$$

这正是 $\mathcal{N}(\vec{a}^T\vec{\mu}, \vec{a}^T\Sigma\vec{a})$ 的特征函数，所以 $Y \sim \mathcal{N}(\vec{a}^T\vec{\mu}, \vec{a}^T\Sigma\vec{a})$。

**（$\Leftarrow$）** 在 (1) 中取 $t = 1$，得

$$
E\exp(i\vec{a}^T\vec{X}) = \phi_Y(1) = \exp\left[i\vec{a}^T\vec{\mu} - \frac{1}{2}\vec{a}^T\Sigma\vec{a}\right]
$$

由于这对**所有** $\vec{a}$ 成立，而右端恰好是 $\mathcal{N}(\vec{\mu}, \Sigma)$ 的特征函数在 $\vec{t} = \vec{a}$ 处的值，由特征函数唯一确定分布，故 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$。$\blacksquare$

> [!EXAMPLE] 例
> $\begin{pmatrix}X_1\\X_2\end{pmatrix} \sim \mathcal{N}\left(\begin{pmatrix}1\\-5\end{pmatrix}, \begin{pmatrix}4&-2\\-2&9\end{pmatrix}\right)$ 等价于：对所有 $\vec{a} = \begin{pmatrix}a_1\\a_2\end{pmatrix}$，
>
> $$a_1 X_1 + a_2 X_2 \sim \mathcal{N}\left((a_1\ a_2)\begin{pmatrix}1\\-5\end{pmatrix},\ (a_1\ a_2)\begin{pmatrix}4&-2\\-2&9\end{pmatrix}\begin{pmatrix}a_1\\a_2\end{pmatrix}\right)$$

### 2.7 独立性判定

#### 子向量间的独立性

> [!IMPORTANT] 定理 1.4（独立性判定——子向量）
> 设 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$，如果将 $\vec{X}$、$\vec{\mu}$、$\Sigma$ 分块为
>
> $$\vec{X} = \begin{pmatrix}\vec{X}_1\\\vec{X}_2\end{pmatrix},\quad \vec{\mu} = \begin{pmatrix}\vec{\mu}_1\\\vec{\mu}_2\end{pmatrix},\quad \Sigma = \begin{pmatrix}\Sigma_{11}&0\\0&\Sigma_{22}\end{pmatrix}$$
>
> 其中 $\vec{X}_1$、$\vec{\mu}_1$ 和方阵 $\Sigma_{11}$ 的行数相同，则 $\vec{X}_1$ 和 $\vec{X}_2$ **独立**，而且
>
> $$\vec{X}_1 \sim \mathcal{N}(\vec{\mu}_1, \Sigma_{11}), \quad \vec{X}_2 \sim \mathcal{N}(\vec{\mu}_2, \Sigma_{22})$$

**证明：** 将 $\vec{X}$ 的特征函数按分块展开：

$$
\phi(\vec{t}) = \phi(\vec{t}_1, \vec{t}_2) = \exp\left[i\vec{t}^T\vec{\mu} - \frac{1}{2}\vec{t}^T\Sigma\vec{t}\right]
$$

由于 $\Sigma$ 的非对角块为零，二次型分解为

$$
\vec{t}^T\Sigma\vec{t} = \vec{t}_1^T\Sigma_{11}\vec{t}_1 + \vec{t}_2^T\Sigma_{22}\vec{t}_2
$$

线性项也可分离：$\vec{t}^T\vec{\mu} = \vec{t}_1^T\vec{\mu}_1 + \vec{t}_2^T\vec{\mu}_2$。于是

$$
\phi(\vec{t}_1, \vec{t}_2) = \underbrace{\exp\left[i\vec{t}_1^T\vec{\mu}_1 - \frac{1}{2}\vec{t}_1^T\Sigma_{11}\vec{t}_1\right]}_{\phi_1(\vec{t}_1)} \times \underbrace{\exp\left[i\vec{t}_2^T\vec{\mu}_2 - \frac{1}{2}\vec{t}_2^T\Sigma_{22}\vec{t}_2\right]}_{\phi_2(\vec{t}_2)}
$$

联合特征函数 = 边缘特征函数之积，故 $\vec{X}_1$ 和 $\vec{X}_2$ 独立。$\blacksquare$

> [!EXAMPLE] 例
> $$\begin{pmatrix}X_1\\X_2\\X_3\end{pmatrix} \sim \mathcal{N}\left(\begin{pmatrix}2\\7\\3\end{pmatrix}, \begin{pmatrix}4&0&0\\0&9&-3\\0&-3&8\end{pmatrix}\right)$$
>
> 由于 $X_1$ 与 $(X_2, X_3)$ 之间的协方差块为零，所以 $X_1 \perp (X_2, X_3)$，且 $X_1 \sim \mathcal{N}(2, 4)$，$\begin{pmatrix}X_2\\X_3\end{pmatrix} \sim \mathcal{N}\left(\begin{pmatrix}7\\3\end{pmatrix}, \begin{pmatrix}9&-3\\-3&8\end{pmatrix}\right)$。
>
> 注意 $X_2$ 和 $X_3$ 之间协方差为 $-3 \neq 0$，所以 $X_2$ 和 $X_3$ 并**不**独立。

#### 各分量的相互独立性

> [!IMPORTANT] 定理 1.5（独立性判定——各分量）
> 如果 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$，则 $(X_1, X_2, \dots, X_n)$ 相互独立的**充要条件**是
>
> $$\Sigma = \operatorname{diag}(\sigma_1^2, \sigma_2^2, \dots, \sigma_n^2)$$

即协方差矩阵是**对角矩阵**。

> [!WARNING] 注意
> 对于一般的随机变量，不相关（$\operatorname{cov} = 0$）**不等价于**独立。但在**联合正态**的前提下，不相关 $\Leftrightarrow$ 独立。这是多元正态分布的一个非常特殊且实用的性质。

### 2.8 常用应用（1）：判定线性组合的独立性

> [!EXAMPLE] 例：$X+Y$ 与 $X-Y$ 何时独立？
> 设 $\begin{pmatrix}X\\Y\end{pmatrix} \sim \mathcal{N}\left(\begin{pmatrix}\mu_1\\\mu_2\end{pmatrix}, \Sigma\right)$，其中 $\Sigma = \begin{pmatrix}\sigma_{11}&\sigma_{12}\\\sigma_{21}&\sigma_{22}\end{pmatrix}$ 正定。求 $X+Y$ 与 $X-Y$ 独立的充分必要条件。

**解题步骤：**

**第一步**：构造线性变换。令

$$
\begin{pmatrix}Z_1\\Z_2\end{pmatrix} = \begin{pmatrix}1&1\\1&-1\end{pmatrix}\begin{pmatrix}X\\Y\end{pmatrix}
$$

**第二步**：由定理 1.2，$\vec{Z}$ 仍服从多元正态分布，其协方差矩阵为

$$
\operatorname{var}(\vec{Z}) = \begin{pmatrix}1&1\\1&-1\end{pmatrix}\Sigma\begin{pmatrix}1&1\\1&-1\end{pmatrix}^T
$$

**第三步**：计算该矩阵。经过矩阵乘法，非对角元素为 $\sigma_{11} - \sigma_{22}$。

**第四步**：由定理 1.4，$Z_1 \perp Z_2$ 当且仅当非对角元为零，即

$$
\boxed{\sigma_{11} - \sigma_{22} = 0 \quad \Longleftrightarrow \quad \operatorname{var}(X) = \operatorname{var}(Y)}$$

> [!TIP] 解题模式
> 遇到"判定某些线性组合独立"的题目，统一模式为：
> 1. 把线性组合写成 $\mathbf{A}\vec{X}$ 的形式；
> 2. 由定理 1.2 得到新向量的多元正态分布及其协方差 $\mathbf{A}\Sigma\mathbf{A}^T$；
> 3. 检查对应的协方差块是否为零。

### 2.9 条件分布

> [!IMPORTANT] 定理 1.6（条件分布）
> 设 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$，$\det(\Sigma) > 0$，分块为
>
> $$\vec{X} = \begin{pmatrix}\vec{X}_1\\\vec{X}_2\end{pmatrix},\quad \vec{\mu} = \begin{pmatrix}\vec{\mu}_1\\\vec{\mu}_2\end{pmatrix},\quad \Sigma = \begin{pmatrix}\Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{pmatrix}$$
>
> 其中 $\vec{X}_1$、$\vec{\mu}_1$ 和方阵 $\Sigma_{11}$ 的行数相同。则在条件 $\vec{X}_1 = \vec{x}_1$ 下，$\vec{X}_2$ 服从多元正态分布：
>
> $$\vec{X}_2 \mid \vec{X}_1 = \vec{x}_1 \sim \mathcal{N}\left(\vec{\mu}_2 + \Sigma_{21}\Sigma_{11}^{-1}(\vec{x}_1 - \vec{\mu}_1),\quad \Sigma_{22} - \Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}\right)$$

条件分布的两个关键特征：

- **条件均值**是 $\vec{x}_1$ 的**线性函数**：$\vec{\mu}_2 + \Sigma_{21}\Sigma_{11}^{-1}(\vec{x}_1 - \vec{\mu}_1)$
- **条件协方差** $\Sigma_{22} - \Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}$ **不依赖于** $\vec{x}_1$ 的取值

**证明思路：**

构造变换

$$
\begin{pmatrix}\vec{Y}_1\\\vec{Y}_2\end{pmatrix} = \begin{pmatrix}I_{11}&0\\-\Sigma_{21}\Sigma_{11}^{-1}&I_{22}\end{pmatrix}\begin{pmatrix}\vec{X}_1 - \vec{\mu}_1\\\vec{X}_2 - \vec{\mu}_2\end{pmatrix}
$$

可以验证 $\vec{Y}_1 = \vec{X}_1 - \vec{\mu}_1$，$\vec{Y}_2 = (\vec{X}_2 - \vec{\mu}_2) - \Sigma_{21}\Sigma_{11}^{-1}(\vec{X}_1 - \vec{\mu}_1)$。

由定理 1.2，$(\vec{Y}_1, \vec{Y}_2)^T$ 服从多元正态分布。经过矩阵计算，其协方差矩阵为

$$
\begin{pmatrix}\Sigma_{11}&0\\0&\Sigma_{22} - \Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}\end{pmatrix}
$$

非对角块为零，所以由定理 1.4，$\vec{Y}_1$ 与 $\vec{Y}_2$ **独立**。

由 $\vec{X}_2 = \vec{Y}_2 + \vec{\mu}_2 + \Sigma_{21}\Sigma_{11}^{-1}(\vec{X}_1 - \vec{\mu}_1)$，以及 $\vec{Y}_1$ 与 $\vec{Y}_2$ 独立，得

$$
P(\vec{X}_2 \leq \vec{x}_2 \mid \vec{X}_1 = \vec{x}_1) = P(\vec{Y}_2 + \vec{\mu}_2 + \Sigma_{21}\Sigma_{11}^{-1}(\vec{x}_1 - \vec{\mu}_1) \leq \vec{x}_2 \mid \vec{Y}_1 = \vec{x}_1 - \vec{\mu}_1)
$$

由独立性，条件可以去掉：$= P(\vec{Y}_2 + \vec{\mu}_2 + \Sigma_{21}\Sigma_{11}^{-1}(\vec{x}_1 - \vec{\mu}_1) \leq \vec{x}_2)$。

又 $\vec{Y}_2 \sim \mathcal{N}(\vec{0}, \Sigma_{22} - \Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12})$，故条件分布为定理所述。$\blacksquare$

#### 二元正态的条件分布（特化）

> [!EXAMPLE] 例 2.2（二元正态的条件密度）
> 设 $(X, Y) \sim \mathcal{N}(\mu_1, \mu_2, \sigma_1^2, \sigma_2^2, \rho)$，已知 $X = x$ 时，$Y$ 的条件分布为
>
> $$Y \mid X = x \sim \mathcal{N}\left(\mu_2 + \rho\frac{\sigma_2}{\sigma_1}(x - \mu_1),\quad (1 - \rho^2)\sigma_2^2\right)$$
>
> 同理，$X \mid Y = y \sim \mathcal{N}\left(\mu_1 + \rho\frac{\sigma_1}{\sigma_2}(y - \mu_2),\quad (1 - \rho^2)\sigma_1^2\right)$。
>
> 当 $X$ 和 $Y$ 独立时，$\rho = 0$，于是 $f_{Y|X}(y|x) = f_Y(y)$，即条件分布退化为边缘分布。

这是定理 1.6 在二维情形的直接应用。此时 $\Sigma_{11} = \sigma_1^2$，$\Sigma_{12} = \Sigma_{21} = \rho\sigma_1\sigma_2$，$\Sigma_{22} = \sigma_2^2$，代入即可得到上面的结果。

### 2.10 常用应用（2）：Mahalanobis 距离与 $\chi^2$ 分布

> [!IMPORTANT] 马氏距离的卡方性质
> 设 $\vec{X} = (X_1, X_2, \dots, X_n)^T \sim \mathcal{N}(\vec{\mu}, \Sigma)$，且 $\Sigma$ 正定，则
>
> $$(\vec{X} - \vec{\mu})^T \Sigma^{-1}(\vec{X} - \vec{\mu}) \sim \chi^2(n)$$

**证明：**

由于 $\Sigma$ 正定，对其做谱分解 $\Sigma^{-1} = P\Lambda P^T$（$P$ 正交，$\Lambda$ 对角且元素为正），定义 $\Sigma^{-1/2} = P\Lambda^{1/2}P^T$。

令 $\vec{Y} = \Sigma^{-1/2}(\vec{X} - \vec{\mu})$。由定理 1.2：

$$
\vec{Y} \sim \mathcal{N}\left(\vec{0},\ \Sigma^{-1/2}\Sigma(\Sigma^{-1/2})^T\right) = \mathcal{N}(\vec{0}, \mathbf{I}_{n \times n})
$$

所以 $Y_1, \dots, Y_n$ 是 i.i.d. $\mathcal{N}(0,1)$。

$$
(\vec{X} - \vec{\mu})^T\Sigma^{-1}(\vec{X} - \vec{\mu}) = \vec{Y}^T\vec{Y} = Y_1^2 + \dots + Y_n^2 \sim \chi^2(n) \quad \blacksquare
$$

### 2.11 常用应用（3）：样本均值与样本方差

> [!NOTE] 统计推断中的重要结论
> 设 $X_1, \dots, X_n$ 相互独立，同服从 $N(\mu, \sigma^2)$ 分布。记样本均值 $\bar{X} = \frac{1}{n}\sum_{i=1}^{n}X_i$，样本方差 $S_n^2 = \frac{1}{n-1}\sum_{i=1}^{n}(X_i - \bar{X})^2$，则有：
>
> **(a)** $\bar{X}$ 与 $S_n^2$ **独立**；
>
> **(b)** $\bar{X} \sim N\left(\mu, \frac{\sigma^2}{n}\right)$；
>
> **(c)** $\frac{(n-1)S_n^2}{\sigma^2} \sim \chi^2_{n-1}$。

高维情形同理。证明详见习题课（两种方法：母函数方法；MVN 性质方法）。

---

## 三、随机向量的 LLN 和 CLT

### 3.1 随机向量的大数定律

设 $\vec{X}_1, \vec{X}_2, \dots$ 是 i.i.d. 的 $k$ 维随机向量，$E\vec{X}_1$ 存在。大数定律在向量情形中的表述很简单：**对每个分量分别应用标量 LLN**。

以 $k = 2$ 为例，设 $\vec{X}_i = \begin{pmatrix}X_{i1}\\X_{i2}\end{pmatrix}$，则

$$
\frac{\vec{X}_1 + \dots + \vec{X}_n}{n} = \begin{pmatrix}\frac{X_{11} + \dots + X_{n1}}{n} \\ \frac{X_{12} + \dots + X_{n2}}{n}\end{pmatrix} \xrightarrow{a.s./p} \begin{pmatrix}EX_{11}\\EX_{12}\end{pmatrix} = E\vec{X}_1
$$

每个分量的收敛由标量 LLN 保证。

### 3.2 向量收敛与一维化

> [!IMPORTANT] 定理 2.8（向量依分布收敛的等价刻画）
> 设随机向量序列 $\{\mathbf{X}_n\}$ 和随机向量 $\mathbf{X}$ 的维度一致，则 $\mathbf{X}_n \xrightarrow{d} \mathbf{X}$ 的**充分必要条件**是：对任何常数向量 $\mathbf{a}$，有
>
> $$\mathbf{a}^T\mathbf{X}_n \xrightarrow{d} \mathbf{a}^T\mathbf{X}$$

> [!IMPORTANT] 引理 2.1（Cramér–Wold 定理）
> 设 $\mathbf{X}$、$\mathbf{Y}$ 都是 $p$ 维随机向量。则 $\mathbf{X}$、$\mathbf{Y}$ **同分布**的充分必要条件是：对任何常数向量 $\mathbf{a} \in \mathbb{R}^p$，$\mathbf{a}^T\mathbf{X}$ 与 $\mathbf{a}^T\mathbf{Y}$ 同分布。
>
> 证明用特征函数即得。

> [!TIP] 核心思想
> **向量问题都可转化为一维！** 想证明向量收敛，只需对所有方向 $\mathbf{a}$ 证明一维投影的收敛。

### 3.3 随机向量的中心极限定理

设 $\vec{X}_1, \vec{X}_2, \dots$ 是 i.i.d. 的 $k$ 维随机向量，$E\vec{X}_1 = \vec{\mu}$，$\operatorname{var}(\vec{X}_1) = \Sigma$（正定），$\vec{S}_n = \vec{X}_1 + \dots + \vec{X}_n$。

**推导思路（以 $k = 2$ 为例）：**

对任意 $\mathbf{a} = \begin{pmatrix}a_1\\a_2\end{pmatrix}$，考虑一维投影 $\mathbf{a}^T\vec{S}_n = \mathbf{a}^T\vec{X}_1 + \dots + \mathbf{a}^T\vec{X}_n$。

这是 i.i.d. 一维随机变量之和。由一维 CLT：

$$
\frac{\mathbf{a}^T\vec{S}_n - E(\mathbf{a}^T\vec{S}_n)}{\sqrt{\operatorname{var}(\mathbf{a}^T\vec{S}_n)}} = \frac{\mathbf{a}^T\left\{\frac{\vec{S}_n - nE\vec{X}_1}{\sqrt{n}}\right\}}{\sqrt{\mathbf{a}^T\operatorname{var}(\vec{X}_1)\mathbf{a}}} \xrightarrow{d} \mathcal{N}(0,1)
$$

这意味着

$$
\mathbf{a}^T\left\{\frac{\vec{S}_n - nE\vec{X}_1}{\sqrt{n}}\right\} \xrightarrow{d} \mathcal{N}(0,\ \mathbf{a}^T\operatorname{var}(\vec{X}_1)\mathbf{a}) = \mathbf{a}^T Z, \quad Z \sim \mathcal{N}(\vec{0}, \operatorname{var}(\vec{X}_1))
$$

由 Cramér–Wold 定理（定理 2.8），得到

> [!IMPORTANT] 向量版 CLT
> $$\frac{\vec{S}_n - nE\vec{X}_1}{\sqrt{n}} \xrightarrow{d} \mathcal{N}(\vec{0},\ \operatorname{var}(\vec{X}_1))$$
>
> 或等价地，标准化后
>
> $$\operatorname{var}(\vec{X}_1)^{-1/2} \cdot \frac{\vec{S}_n - nE\vec{X}_1}{\sqrt{n}} \xrightarrow{d} \mathcal{N}(\vec{0},\ \mathbf{I}_{k \times k})$$

### 3.4 统计推断中的重要应用

#### 一维情形

结合 MVN 性质和 CLT，若 $X \sim \mathcal{N}(\mu, \sigma^2)$，则 $\frac{(X-\mu)^2}{\sigma^2} = (X-\mu)^T(\sigma^2)^{-1}(X-\mu) \sim \chi^2(1)$。

由 CLT + Continuous Mapping Theorem：

$$
\operatorname{var}(\tilde{X}_1)^{-1/2} \cdot \frac{S_n - nE\tilde{X}_1}{\sqrt{n}} = \frac{S_n - ES_n}{\sqrt{\operatorname{var}(S_n)}} \xrightarrow{d} \mathcal{N}(0,1)
$$

平方后：$\left(\frac{S_n - ES_n}{\sqrt{\operatorname{var}(S_n)}}\right)^2 \xrightarrow{d} \chi^2(1)$。

#### 多元情形（卡方检验）

> [!IMPORTANT] 卡方检验的向量推广
> 记 $\vec{M}_n = \frac{1}{n}\vec{S}_n = \frac{1}{n}\sum_{i=1}^{n}\vec{X}_i$ 为样本均值向量。由向量 CLT 和 Continuous Mapping Theorem：
>
> $$n(\vec{M}_n - E\vec{X}_1)^T \left[\operatorname{var}(\vec{X}_1)\right]^{-1}(\vec{M}_n - E\vec{X}_1) \xrightarrow{d} \chi^2(k)$$
>
> 其中 $k$ 是随机向量的维度。

这就是多元统计中**卡方检验**的理论基础：当样本量 $n$ 足够大时，样本均值向量与总体均值之间的 Mahalanobis 距离的 $n$ 倍近似服从 $\chi^2(k)$ 分布。

---

## 四、小结与题型策略

### 知识点层次

| 层次 | 内容 |
| :---: | --- |
| 掌握 | 协方差矩阵的定义与非负定性质；MVN 定义（两种）；线性组合定理；判定法则；独立性判定；条件分布公式；$(\vec{X}-\vec{\mu})^T\Sigma^{-1}(\vec{X}-\vec{\mu}) \sim \chi^2(n)$；向量 LLN/CLT 结论 |
| 理解 | 证明过程（基于特征函数和矩阵运算）；向量收敛一维化思想；Cramér–Wold 定理 |
| 了解 | 样本均值与样本方差独立（证明见习题课） |

### 题型策略

**题型 1：求多元正态的线性组合分布**

策略：直接套定理 1.2，$\vec{Y} = \vec{b} + \mathbf{A}\vec{X} \sim \mathcal{N}(\vec{b} + \mathbf{A}\vec{\mu}, \mathbf{A}\Sigma\mathbf{A}^T)$。计算矩阵乘法即可。

**题型 2：判定线性组合是否独立**

策略：(1) 把线性组合写成 $\mathbf{A}\vec{X}$；(2) 计算 $\mathbf{A}\Sigma\mathbf{A}^T$；(3) 检查对应子块是否为零。零则独立。

**题型 3：求条件分布**

策略：直接套定理 1.6 的公式。条件均值 = $\vec{\mu}_2 + \Sigma_{21}\Sigma_{11}^{-1}(\vec{x}_1 - \vec{\mu}_1)$，条件协方差 = $\Sigma_{22} - \Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}$。

**题型 4：证明某二次型服从 $\chi^2$ 分布**

策略：构造 $\vec{Y} = \Sigma^{-1/2}(\vec{X} - \vec{\mu}) \sim \mathcal{N}(\vec{0}, \mathbf{I})$，则 $\vec{Y}^T\vec{Y} = \sum Y_i^2 \sim \chi^2(n)$。

**题型 5：利用向量 CLT 做近似**

策略：先写出 $\frac{\vec{S}_n - nE\vec{X}_1}{\sqrt{n}} \xrightarrow{d} \mathcal{N}(\vec{0}, \Sigma)$，再用 CMT 将二次型映射为 $\chi^2(k)$。
