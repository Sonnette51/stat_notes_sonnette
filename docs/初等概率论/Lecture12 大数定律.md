---
title: "Lecture12 大数定律"
tags:
  - 概率论
  - 后半学期
  - 大数定律
  - WLLN
  - SLLN
  - 收敛性
---

# Lecture12 大数定律

## 写在前面：这讲在讲什么？

在之前的课里，我们学过随机变量 $X$ 的**期望** $EX$——它代表总体的"平均水平"。但 $EX$ 是一个理论上的数，在现实中我们无法直接观测到全体人群，只能随机抽一些人来测量，得到**样本均值**。

这讲的核心问题只有一个：

> **用样本均值来估计总体均值，可靠吗？**

大数定律（Law of Large Numbers，LLN）给出了肯定的回答，并精确刻画了"样本量 $n$ 越大，样本均值越接近总体均值"这一现象。

**课程地位**：大数定律是统计推断（用样本认识总体）的理论基础，也是蒙特卡洛方法、经验分布等重要工具的依据。

---

## 一、引入：疫苗有效性问题

### 1.1 现实背景

疫苗研发需要做临床试验，评估安全性和有效性。我们不可能对全体人群都接种，只能随机招募 $n$ 位受试者。问题是：

**能否通过 $n$ 位受试者（样本）来了解整个人群（总体）的有效性？**

### 1.2 概率建模

随机招入 $n$ 位受试者，定义随机变量：

$$X_i = \begin{cases} 1, & \text{疫苗对第 } i \text{ 人有效（概率为 } p \text{）} \\ 0, & \text{疫苗对第 } i \text{ 人无效（概率为 } 1-p \text{）} \end{cases}$$

由于受试者是**随机**招入的，$X_1, X_2, \ldots, X_n$ 是**独立同分布（i.i.d.）**的随机变量。

- **总体均值**（我们想知道但未知的）：$p = EX_1$
- **样本均值**（我们能计算的）：$M_n = \dfrac{1}{n}\displaystyle\sum_{i=1}^{n} X_i$

**知识点关联**：这个问题体现了概率论的核心演进路径：

$$(\Omega, \mathcal{F}, P) \longrightarrow X / \vec{X} \longrightarrow EX \longrightarrow X_n \to ?$$

从概率空间，到随机变量，到数字特征（期望），到**随机变量序列的极限**——大数定律就是研究这最后一步的。

### 1.3 模拟观察

用 $p = 0.5$ 的硬币做模拟实验，可以看到：当 $n$ 很小时，样本均值 $M_n$ 波动很大；随着 $n$ 增大，$M_n$ 越来越稳定地靠近 $0.5 = EX_1$。大数定律就是这个现象的数学化。

---

## 二、基本定理：弱大数定律（WLLN）

### 2.1 定理内容

> [!NOTE] 定理 1.1（弱大数定律，Weak Law of Large Numbers，WLLN）
> 
> 设 ${X_n}$ 是**独立同分布**的随机变量序列，且 $\mathrm{Var}(X_1) < \infty$（方差有限），则对任意给定的 $\varepsilon > 0$，
> 
> $$\lim_{n \to \infty} \mathbb{P}\left(\left|\frac{1}{n}\sum_{i=1}^{n} X_i - EX_1\right| \geq \varepsilon\right) = 0$$
> 
> 也称 $\dfrac{1}{n}\displaystyle\sum_{k=1}^{n} X_k$ **依概率收敛**到 $EX_1$，记作
> 
> $$\frac{1}{n}\sum_{k=1}^{n} X_k \xrightarrow{p} EX_1$$

**白话解读**：当 $n$ 很大时，我们有很大的把握（但非 100%）断言样本均值 $\dfrac{1}{n}\sum X_i$ 与总体均值 $EX_1$ 之差的绝对值小于任意小的 $\varepsilon$。换言之，样本均值偏离总体均值很多的概率趋于零。

**大数定律的哲学意义**：它是"连接偶然性与必然性的桥梁"——单次实验结果（$X_i$）是偶然的，但大量重复之后，平均结果（$M_n$）趋向必然（$EX_1$）。

### 2.2 定理证明

**前提条件**：${X_n}$ 独立同分布，$\mathrm{Var}(X_1) < \infty$。

**目标**：证明对 $\forall \varepsilon > 0$，$\lim_{n\to\infty} \mathbb{P}\left(\left|\frac{1}{n}\sum_{i=1}^n X_i - EX_1\right| \geq \varepsilon\right) = 0$。

**关键工具——切比雪夫不等式**（复习）：

> 对随机变量 $X$ 和 $\varepsilon > 0$： $$\mathbb{P}(|X - EX| \geq \varepsilon) \leq \frac{\mathrm{Var}(X)}{\varepsilon^2}$$

**证明步骤**：

**第一步**：注意到（因为 ${X_n}$ 同分布，各 $X_i$ 期望相同均为 $EX_1$）： $$E\left(\frac{1}{n}\sum_{i=1}^n X_i\right) = \frac{1}{n} \cdot n \cdot EX_1 = EX_1$$

所以： $$\mathbb{P}\left(\left|\frac{1}{n}\sum_{i=1}^n X_i - EX_1\right| \geq \varepsilon\right) = \mathbb{P}\left(\left|\frac{1}{n}\sum_{i=1}^n X_i - E\left(\frac{1}{n}\sum_{i=1}^n X_i\right)\right| \geq \varepsilon\right)$$

**第二步**：对随机变量 $\dfrac{1}{n}\sum_{i=1}^n X_i$ 应用切比雪夫不等式： $$\leq \frac{\mathrm{Var}\left(\frac{1}{n}\sum_{i=1}^n X_i\right)}{\varepsilon^2}$$

**第三步**：计算方差。由于 ${X_n}$ **独立同分布**： $$\mathrm{Var}\left(\frac{1}{n}\sum_{i=1}^n X_i\right) = \frac{1}{n^2}\sum_{i=1}^n \mathrm{Var}(X_i) = \frac{1}{n^2} \cdot n \cdot \mathrm{Var}(X_1) = \frac{\mathrm{Var}(X_1)}{n}$$

（这里用到了独立变量方差可加，以及同分布方差相同。）

**第四步**：合并，得到： $$\mathbb{P}\left(\left|\frac{1}{n}\sum_{i=1}^n X_i - EX_1\right| \geq \varepsilon\right) \leq \frac{\mathrm{Var}(X_1)}{n\varepsilon^2} \xrightarrow{n \to +\infty} 0$$

因为 $\mathrm{Var}(X_1) < \infty$，分母趋于无穷，故极限为 0。证毕。✓

**常见疑问**：为什么第一步要把 $EX_1$ 换成 $E\left(\frac{1}{n}\sum X_i\right)$？因为切比雪夫不等式的形式是 $\mathbb{P}(|X - EX| \geq \varepsilon)$，要让等式左边的形式凑成这个样子，就需要将 $EX_1$ 换写成样本均值自身的期望。由同分布条件二者相等，故这步替换是合法的。

### 2.3 结合切比雪夫不等式：样本量计算

**例 1.1（接上述疫苗问题）**

需要多少样本量，才能保证"误差大于 3% 的概率不超过 5%"？

**目标**：$\mathbb{P}(|M_n - p| \geq 0.03) \leq 0.05$。

由证明过程知： $$\mathbb{P}(|M_n - p| \geq 0.03) \leq \frac{\mathrm{Var}(X_1)}{n \cdot (0.03)^2}$$

对 $X_i \sim B(1, p)$，有 $\mathrm{Var}(X_1) = p(1-p)$。

利用 $p(1-p) \leq \dfrac{1}{4}$（对任意 $p \in [0,1]$ 成立，在 $p=0.5$ 时取等），可以在不知道 $p$ 真实值的情况下给出保守上界：

$$\frac{\mathrm{Var}(X_1)}{n \cdot (0.03)^2} \leq \frac{1}{4n(0.03)^2} \leq 0.05$$

解不等式： $$n \geq \frac{1}{4 \times (0.03)^2 \times 0.05} = \frac{1}{0.00018} \approx 5556$$

**结论**：取 $n = 5556$ 人即可保证目标成立。

---

## 三、理论深化

### 3.1 条件"独立同分布"可放宽

定理 1.1 要求 ${X_n}$ 独立同分布，这个条件可以放宽。从最一般到最严格，条件的层次如下：

| 条件层次                                                                    | 对应结论                                       |
| ----------------------------------------------------------------------- | ------------------------------------------ |
| 无任何约束                                                                   | 大数定律不一定成立                                  |
| **马尔可夫条件**：$\mathrm{Var}\left(\frac{1}{n}\sum_{k=1}^n X_k\right) \to 0$ | $\Rightarrow$ 大数定律（**马尔可夫大数定律**）           |
| ${X_n}$ 独立同分布（i.i.d.）（定理 1.1 的条件）                                       | $\Rightarrow$ 上面的马尔可夫条件 $\Rightarrow$ 大数定律 |

**关键点**：我们证明 WLLN 的核心一步就是：$\mathrm{Var}\left(\frac{1}{n}\sum X_k\right) = \frac{\mathrm{Var}(X_1)}{n} \to 0$。独立同分布是一个**充分条件**，但不是必要条件；只要方差之和被 $n$ 压制（即马尔可夫条件），大数定律就成立。

### 3.2 条件"方差有限"可放宽

定理 1.1 还要求 $\mathrm{Var}(X_1) < \infty$，这个条件也可以放宽：

$$\mathrm{Var}(X_1) < \infty \implies E|X_1| < \infty \implies n\mathbb{P}(|X_1| \geq n) \to 0$$

（注意这是**蕴含**关系，箭头方向是从强到弱。）

因此，在 i.i.d. 条件下：

> [!NOTE] 定理 1.1 扩展版 a（辛钦大数定律，Khinchin LLN）
> 
> 设 ${X_n}$ 是 i.i.d.，且 $E|X_1| < \infty$（期望存在有限），则 $$\frac{1}{n}\sum_{k=1}^n X_k \xrightarrow{p} EX_1$$

辛钦（Khinchin，1894–1959，苏联数学家）将条件从"方差有限"减弱到"期望有限"。

> [!NOTE] 定理 1.1 扩展版 b（最一般的 WLLN）　（不要求掌握）
> 
> 设 ${X_n}$ 是 i.i.d.，则存在实数列 ${a_n}$ 使得 $\dfrac{1}{n}\sum X_k - a_n \xrightarrow{p} 0$ 的**充要条件**是 $n\mathbb{P}(|X_1| \geq n) \to 0$。此时可取 $a_n = E(X_1 I_{{|X_1| < n}})$。

---

## 四、强大数定律（SLLN）

### 4.1 "依概率收敛"是什么意思？

在讨论强弱大数定律的区别之前，先理解两种收敛模式。

**定义 1.1（依概率收敛）**：如果对 $\forall \varepsilon > 0$，有 $$\lim_{n\to\infty} \mathbb{P}(|Y_n - Y| \geq \varepsilon) = 0$$ 则称 $Y_n$ **依概率收敛**到 $Y$，记作 $Y_n \xrightarrow{p} Y$。

等价条件：令 $A_n = {|Y_n - Y| < \varepsilon}$，则依概率收敛 $\Leftrightarrow$ $\lim_{n\to\infty} \mathbb{P}(A_n) = 1$。

**直觉**：固定任意误差范围 $\varepsilon$，当 $n$ 足够大时，$Y_n$ 落在 $Y$ 的 $\varepsilon$ 邻域内的概率接近 1。但注意，这是对**每个固定的 $n$** 而言的概率，不同的 $n$ 对应不同的概率值。

### 4.2 "几乎处处收敛"是什么意思？

**定义 1.2（几乎处处收敛 / 以概率 1 收敛）**：如果 $$\mathbb{P}\left(\lim_{n\to\infty} Y_n = Y\right) = 1$$ 则称 $Y_n$ **几乎处处收敛**到 $Y$，记作 $Y_n \xrightarrow{a.s.} Y$，或 $Y_n \to Y$ a.s.（almost surely）。

等价条件：$\mathbb{P}(\liminf_{n\to\infty} A_n) = 1$，其中 $A_n = {|Y_n - Y| < \varepsilon}$，即

$$\mathbb{P}\left(\bigcup_{n=1}^{\infty}\bigcap_{k=n}^{\infty}{|Y_k - Y| < \varepsilon}\right) = 1$$

**直觉**："几乎处处"意味着对**几乎所有**样本路径 $\omega$（即除了一个概率为 0 的例外集合外），序列 $Y_n(\omega)$ 都收敛到 $Y(\omega)$。这是针对**整条轨迹**的要求，比依概率收敛更强。

### 4.3 两种收敛的关系

$$Y_n \xrightarrow{a.s.} Y \implies Y_n \xrightarrow{p} Y$$

即**几乎处处收敛蕴含依概率收敛**，反之不成立（见后面的理论例）。

**证明**（即证明$\mathbb{P}(\liminf A_n) = 1$ 能推出 $\lim \mathbb{P}(A_n) = 1$）：

$$\mathbb{P}(\liminf_{n\to\infty} A_n) = \mathbb{P}\left(\lim_{n\to\infty}\bigcap_{k=n}^{\infty} A_k\right) = \lim_{n\to\infty}\mathbb{P}\left(\bigcap_{k=n}^{\infty} A_k\right) \leq \lim_{n\to\infty} \mathbb{P}(A_n)$$

若左边等于 1，则 $\lim_{n\to\infty} \mathbb{P}(A_n) \geq 1$，从而 $\lim_{n\to\infty} \mathbb{P}(A_n) = 1$，即依概率收敛成立。

### 4.4 强大数定律的内容

> [!NOTE] 定理 1.2（强大数定律，Strong Law of Large Numbers，SLLN）
> 
> 设 ${X_n}$ 是**独立同分布**的随机变量序列：
> 
> **(1)** 若 $E|X_1| < \infty$，则 $$\frac{1}{n}\sum_{k=1}^n X_k \xrightarrow{a.s.} EX_1 \quad \text{（几乎处处收敛）}$$
> 
> **(2)** 反之，若 $\dfrac{1}{n}\sum_{k=1}^n X_k \xrightarrow{a.s.} C$ 几乎处处收敛，则 $E|X_1| < \infty$ 且 $C = EX_1$。
> 
> 即：**$E|X_1| < \infty$ 是 ${X_n}$ i.i.d. 下大数定律（a.s. 收敛）成立的充要条件。**

几乎处处收敛的直观含义： $$\mathbb{P}\left(\lim_{n\to\infty} \frac{1}{n}\sum_{k=1}^n X_k = EX_1\right) = 1$$

即样本均值序列（作为一条轨迹）以概率 1 收敛到总体均值。

### 4.5 强弱大数定律的直观区别
|                     | 弱大数定律（WLLN）                   | 强大数定律（SLLN）                 |
| ------------------- | ----------------------------- | --------------------------- |
| **收敛方式**            | 依概率收敛                         | 几乎处处收敛                      |
| **条件（i.i.d. 下，充要）** | 见下方①，比②更弱                     | 见下方②                        |
| **直觉**              | 采样次数越多，样本均值**接近总体均值的可能性越来越大** | 采样次数越多，样本均值**几乎一定渐近接近总体均值** |
| **强弱关系**            | 弱（SLLN 推出 WLLN，反之不然）          | 强                           |
① WLLN 充要条件：$n\mathbb{P}(|X_1|\geq n) \to 0$
② SLLN 充要条件：$E|X_1| < \infty$

三个条件的蕴含链：$\mathrm{Var}(X_1)<\infty \Rightarrow E|X_1|<\infty \Rightarrow n\mathbb{P}(|X_1|\geq n)\to 0$，越往右越弱。4.6 节的理论例正是满足①但不满足②的情形，即 WLLN 成立、SLLN 不成立。

### 4.6 理论例：体现强弱大数定律的区别

**例 1.1**：设 ${X_n}$ i.i.d.，共同分布为：

$$\mathbb{P}(X = m) = \mathbb{P}(X = -m) = \frac{C}{2m^2 \ln m}, \quad m \geq 3$$

（其中 $C$ 为某归一化常数。）则 $\bar{X}_n = \frac{1}{n}\sum_{k=1}^n X_k$ **服从弱大数定律，但不服从强大数定律**。

**解**：

**(1) 验证满足弱大数定律**：弱大数定律的充要条件为 $\lim_{n\to\infty} n\mathbb{P}(|X| \geq n) = 0$。

$$n\mathbb{P}(|X| \geq n) = n\sum_{m=n}^{\infty} \mathbb{P}(|X| = m) = C \cdot n\sum_{m=n}^{\infty} \frac{1}{m^2\ln m}$$

用放缩估计（利用 $m \ln m \geq \ln n$ 以及对 $1/[m(m-1)]$ 的裂项）：

$$C \cdot n\sum_{m=n}^{\infty} \frac{1}{m^2\ln m} \leq \frac{C}{\ln n} \cdot n\sum_{m=n}^{\infty}\frac{1}{m^2} \leq \frac{C}{\ln n} \cdot n \cdot \frac{1}{n-1} \to 0$$

故 $\bar{X}_n$ 满足弱大数定律。✓

**(2) 验证不满足强大数定律**：强大数定律的充要条件为 $E|X| < \infty$。但：

$$E|X|^+ = E|X|^- = C\sum_{m=3}^{\infty} m \cdot \frac{1}{m^2\ln m} = C\sum_{m=3}^{\infty} \frac{1}{m\ln m} = \infty$$

（因为 $\sum \frac{1}{m\ln m}$ 是发散的调和级数变体。）故 $EX$ 不存在，$\bar{X}_n$ 不满足强大数定律。✓

**这个例子的意义**：强弱大数定律确实是两个不同的事，存在只满足弱不满足强的情形。

---

## 五、收敛模式补充（Aside，针对一般随机变量序列）

（这部分是对依概率收敛和几乎处处收敛的更系统论述，不局限于大数定律的情形。）

### 5.1 两种收敛的等价刻画

令 $A_n = {|Y_n - Y| < \varepsilon}$，则：

$$Y_n \xrightarrow{p} Y \iff \lim_{n\to\infty} \mathbb{P}(A_n) = 1$$

$$Y_n \xrightarrow{a.s.} Y \iff \mathbb{P}(\liminf_{n\to\infty} A_n) = 1$$

其中 $\liminf_{n\to\infty} A_n = \bigcup_{n=1}^{\infty}\bigcap_{k=n}^{\infty} A_k$ 的含义是"从某个 $n$ 开始，之后所有的 $A_k$ 都发生"。

**关键区别**：

- 依概率收敛：$\lim_{n\to\infty} \mathbb{P}(A_n) = 1$，是对**每个单独的 $n$** 要求概率趋于 1。
- 几乎处处收敛：$\mathbb{P}(\liminf A_n) = 1$，是对**整条轨迹**要求以概率 1 最终始终在 $\varepsilon$-邻域内。

### 5.2 蕴含关系

$$Y_n \xrightarrow{a.s.} Y \implies Y_n \xrightarrow{p} Y$$

反之不成立，存在依概率收敛但不几乎处处收敛的例子。（课件提示"反例"存在，未展开。）

### 5.3 经典习题：收敛的运算封闭性

**Problem 5.6（依概率收敛的运算性质）**

设 $X_n \xrightarrow{p} x$，$Y_n \xrightarrow{p} y$，$c$ 为常数，则以下序列均依概率收敛到对应的极限：

| 序列                  | 极限                |
| ------------------- | ----------------- |
| $cX_n$              | $cx$              |
| $X_n + Y_n$         | $x + y$           |
| $\max\{0,\, X_n\}$  | $\max\{0,\, x\}$  |
| $\lvert X_n \rvert$ | $\lvert x \rvert$ |
| $X_n Y_n$           | $xy$              |

**结论**：依概率收敛对加法、数乘、乘法及连续函数运算封闭；连续映射保持依概率收敛。

---

**Problem 5.13（几乎处处收敛的运算性质）**

设 $X_n \xrightarrow{a.s.} a$，$Y_n \xrightarrow{a.s.} b$，则：
- $X_n + Y_n \xrightarrow{a.s.} a + b$
- 若 $Y_n$ 不能等于零，则 $X_n / Y_n \xrightarrow{a.s.} a/b$

**结论**：几乎处处收敛同样对加法和除法运算封闭（分母非零时），连续映射也保持几乎处处收敛。

---

**Problem 5.14（比值序列的几乎处处收敛）**

设 $X_1, X_2, \ldots$ 与 $Y_1, Y_2, \ldots$ 均为独立同分布随机变量序列，各自有有限期望，且 $Y_1 + \cdots + Y_n \neq 0$。令

$$Z_n = \frac{X_1 + \cdots + X_n}{Y_1 + \cdots + Y_n}$$

**结论**：$Z_n$ 以概率 1 收敛，极限为 $\dfrac{EX_1}{EY_1}$。

**原理**：由强大数定律，分子 $\frac{1}{n}\sum X_i \xrightarrow{a.s.} EX_1$，分母 $\frac{1}{n}\sum Y_i \xrightarrow{a.s.} EY_1 \neq 0$，再由 Problem 5.13 的除法性质即得。这是强大数定律与连续映射定理的典型联合应用。

---

## 六、经典应用

### 6.1 频率与概率

**伯努利大数定律**是大数定律的特例：当 $X_n \sim B(1, p)$ 时，

$$\frac{1}{n}\sum_{k=1}^n X_k \xrightarrow{p} p$$

这表明：**频率（样本均值）稳定于概率（总体均值）！**

这是用频率来确定概率的理论依据，是统计中"**频率学派**"的哲学基础。

**思考（课件提出，本课程不展开）**：所有的概率都可用频率解释吗？

### 6.2 经验分布

**例 1.3**：设 ${X_j}$ i.i.d.，$x_j = X_j(\omega)$ 是观测值。则以概率 1，观测数列 ${x_j}$ 可以决定 $X_j$ 的分布函数 $F(x)$。

**证明**：对任意固定的 $x \in \mathbb{R}$，定义示性函数：

$$g(X_j) = \begin{cases} 1, & X_j \leq x \\ 0, & X_j > x \end{cases}$$

则 ${g(X_j)}$ i.i.d.，且 $Eg(X_1) = \mathbb{P}(X_1 \leq x) = F(x)$。

由 SLLN：$\dfrac{1}{n}\displaystyle\sum_{j=1}^n g(X_j) \xrightarrow{a.s.} F(x)$，即以概率 1， $$\lim_{n\to\infty} \frac{1}{n}\sum_{j=1}^n g(x_j) = F(x)$$

这就是**经验分布函数**：

$$G_n(x) = \frac{1}{n}\sum_{i=1}^n I(x_i \leq x)$$

它以概率 1 收敛到真实的分布函数 $F(x)$，是统计推断中用数据估计总体分布的理论依据。

### 6.3 蒙特卡洛方法

**蒙特卡洛方法**由美国数学家冯·诺伊曼在 20 世纪 40 年代为研制核武器提出，是《统计计算》的核心基础，特别适用于解析法难以甚至不能求解的问题。

**例：用蒙特卡洛计算 $\pi$**

在单位正方形 $[-1,1]^2$ 中均匀撒点，令 $I_j = 1$ 表示第 $j$ 个点落在单位圆内，则

$$EI_j = \mathbb{P}(I_j = 1) = \frac{\text{单位圆面积}}{\text{正方形面积}} = \frac{\pi}{4}$$

由大数定律：$\dfrac{1}{n}\displaystyle\sum_{j=1}^n I_j \xrightarrow{a.s.} \dfrac{\pi}{4}$，故 $\hat{\pi} = 4\bar{I}$。

**例 1.4（一般情形）**：估计复杂函数 $f(x)$ 在 $[a,b]$ 上的积分 $\int_a^b f(x)dx$。

取矩形区域 $A = [a,b] \times [0,c]$，子区域 $B = {(x,y): 0 \leq y \leq f(x)}$。从 $A$ 均匀撒 $n$ 个点，用 $I_j$ 表示第 $j$ 个点落在 $B$ 中，则：

$$EI_j = \mathbb{P}(I_j = 1) = \frac{\int_a^b f(x)dx}{c(b-a)}$$

由大数定律，以概率 1：

$$\int_a^b f(x)dx \approx c(b-a) \cdot \frac{1}{n}\sum_{j=1}^n I_j$$

### 6.4 理论拓展与前沿应用

**机器学习中的随机森林**：大数定律保证了泛化误差会收敛到一个常数，而非无限制地大。因此，不会因为树的增加而产生过拟合。

**随机过程**：概率的研究对象从古典概型 $\to$ 二项分布 $\to$ 独立同分布 $\to$ **随机过程**。随机过程中有**遍历定理**，其本质是"时间平均 = 空间平均/相平均"，这正是大数定律在随机过程中的推广。

---

## 七、课堂小结

### 7.1 课程重点

大数定律的核心公式：

$$\frac{1}{n}\sum_{k=1}^n X_k \xrightarrow{P \text{ 或 } a.s.} EX_1$$

统计（从已知到未知）：样本均值 $\xrightarrow{\text{认识}}$ 总体均值

概率（现象与规律）：偶然现象 $\xleftarrow{\text{主导}}$ 必然规律

### 7.2 课程启示

大数定律体现了**偶然性与必然性的辩证统一**：每次实验的结果（$X_i$）是偶然的，但大量重复中的规律（$EX_1$）是必然的。

### 7.3 考纲要求（掌握）

- **基本概念和区别**：
    - 样本均值 vs 总体均值
    - 依概率收敛（$\xrightarrow{p}$）vs 几乎处处收敛（$\xrightarrow{a.s.}$）的定义与关系
- **经典大数定律内容**（定理 1.1, 1.2；条件、结论），理解两定理差异
- **最简单版 WLLN 的证明**（定理 1.1，利用切比雪夫不等式）
- **理解**：LLN 的意义；对比强弱 LLN，其中强弱的含义
- **应用**：
    - LLN — 样本均值帮助认识总体均值（经验分布、随机模拟）
    - 样本量的计算：LLN + Chebyshev 不等式

### 7.4 常见疑问

**Q：弱大数定律说的是概率趋于 0，那意味着"以概率 1 成立"吗？**

A：不是。弱大数定律只说当 $n \to \infty$ 时，$\mathbb{P}(|M_n - p| \geq \varepsilon) \to 0$，即对任意固定 $\varepsilon$，误差大的概率越来越小趋于 0，但永远不等于 0。不能理解为"保证收敛"。这正是"弱"的含义——它不能保证每条样本路径都收敛。

**Q：强大数定律和弱大数定律的条件一样吗？**

A：在 i.i.d. 条件下，强大数定律要求 $E|X_1| < \infty$，弱大数定律（辛钦版本）也要求 $E|X_1| < \infty$，条件相同但结论更强（几乎处处收敛比依概率收敛强）。最一般的弱大数定律只需 $n\mathbb{P}(|X_1|\geq n) \to 0$，是比 $E|X_1| < \infty$ 更弱的条件。

**Q：切比雪夫不等式给出的是上界，为什么能精确描述极限？**

A：大数定律的结论是"极限为 0"，切比雪夫不等式给出 $\leq \dfrac{\mathrm{Var}(X_1)}{n\varepsilon^2}$，右边当 $n\to\infty$ 时趋于 0。再加上概率非负（下界为 0），由夹逼定理，极限正好等于 0。

**Q：方差有限 ($\mathrm{Var}(X_1) < \infty$) 和期望有限 ($E|X_1| < \infty$) 有什么关系？**

A：方差有限 $\Rightarrow$ 期望有限（因为 $\mathrm{Var}(X) = E(X-EX)^2 < \infty$ 意味着 $E|X|^2 < \infty$，而由 Cauchy-Schwarz 不等式 $E|X| \leq \sqrt{E|X|^2} < \infty$），反之不成立。所以辛钦大数定律的条件（$E|X_1| < \infty$）比定理 1.1 的条件（$\mathrm{Var}(X_1) < \infty$）更弱，适用范围更广。