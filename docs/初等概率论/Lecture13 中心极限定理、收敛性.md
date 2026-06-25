---
title: 中心极限定理（CLT）讲义
tags:
  - 概率论
  - 后半学期
  - 中心极限定理
  - CLT
  - 收敛性
date: 2026-06-05
---

# Lecture 13：中心极限定理（CLT）

> [!INFO] 本讲概览
> 本讲基于清华大学《初等概率论》课程，对应 Bertsekas & Tsitsiklis Ch5 §5.4。
>
> **学习要求**：
> - 掌握：基本定理内容与证明、依分布收敛的定义、应用计算
> - 理解：CLT 的意义、正态分布的核心地位
> - 能从实际场景中识别并运用 CLT 解题（确定样本量、求分位点、近似概率）

---

## 一、引入：从大数定律到 CLT

### 回顾：大数定律的局限

设人群中疫苗有效比例为 $\mu$，随机抽 $n$ 个人，令

$$
X_i = \begin{cases} 1, & \text{有效} \\ 0, & \text{无效} \end{cases}, \quad M_n = \frac{X_1 + \cdots + X_n}{n}
$$

**大数定律**告诉我们：$M_n \xrightarrow{\text{a.s.}} \mu$（几乎处处收敛）。

但大数定律**只告诉我们极限在哪里，不告诉我们收敛速度有多快，也不告诉我们"偏差"的分布形态**。

### 收敛速度与什么有关？

观察发现，$n^{1/2} \cdot \dfrac{M_n - \mu}{\sqrt{\operatorname{Var}(X_1)}}$ 这个量在 $n$ 增大时趋向某个固定分布——这就是 CLT 要回答的问题。

---

## 二、预备概念：依分布收敛

> [!NOTE] 定义 1.1（依分布收敛，Convergence in Distribution）
> 设 $Y_n,\, Y$ 的分布函数分别为 $F_n(x),\, F(x)$。若在 $F(x)$ 的所有连续点 $x$ 处，均有
>
> $$\lim_{n \to \infty} F_n(x) = F(x)$$
>
> 则称 $Y_n$ **依分布收敛**到 $Y$，记作 $Y_n \xrightarrow{d} Y$；
> 也称 $F_n$ **弱收敛**到 $F$，记作 $F_n \xrightarrow{w} F$。

> [!TIP] 理解要点
> - 依分布收敛是**最弱**的收敛模式（弱于依概率收敛、几乎处处收敛）。
> - 只要求 CDF 在连续点处逐点收敛，不要求 $Y_n$ 和 $Y$ 定义在同一概率空间。
> - CLT 的结论就是"依分布收敛到标准正态"。

---

## 三、基本定理

### 3.1 Lindeberg–Lévy 中心极限定理

> [!IMPORTANT] 定理 1.1（Lindeberg–Lévy CLT）
> 设 $\{X_n\}$ 是**独立同分布（i.i.d.）**的随机变量序列，期望 $E[X_i] = \mu$，方差 $\operatorname{Var}(X_i) = \sigma^2 < \infty$。
>
> 令 $S_n = X_1 + \cdots + X_n$，则：
>
> $$\frac{S_n - E[S_n]}{\sqrt{\operatorname{Var}(S_n)}} \xrightarrow{d} \mathcal{N}(0,1)$$

### 3.2 各种等价表述

由于 $E[S_n] = n\mu$，$\operatorname{Var}(S_n) = n\sigma^2$，以及 $M_n = S_n/n$，定理有以下三种等价写法：

| 对象 | 表述 |
| :--- | :--- |
| 关于 $S_n$ | $\dfrac{S_n - n\mu}{\sigma\sqrt{n}} \xrightarrow{d} \mathcal{N}(0,1)$ |
| 关于 $M_n$ | $\dfrac{M_n - \mu}{\sigma/\sqrt{n}} \xrightarrow{d} \mathcal{N}(0,1)$ |
| 理论意义写法 | $n^{1/2}\cdot\dfrac{M_n - \mu}{\sqrt{\operatorname{Var}(X_1)}} \xrightarrow{d} \mathcal{N}(0,1)$ |

### 3.3 近似分布（实用形式）

当 $n$ 充分大时，CLT 给出以下**近似**（注意是近似，不是精确等号）：

$$
S_n \approx \mathcal{N}(n\mu,\; n\sigma^2)
$$

$$
M_n \approx \mathcal{N}\!\left(\mu,\; \frac{\sigma^2}{n}\right)
$$

> [!TIP] 直觉解读
> **大量独立同分布随机因素的叠加，近似服从正态分布。**
> 无论原始分布是什么形状（伯努利、泊松、均匀……），只要 $n$ 足够大，它们的和就"趋向正态"。

---

## 四、定理证明思路

> [!NOTE] 证明策略
> 证明分两步：
> 1. 标准化，把问题化归到均值0、方差1的情形。
> 2. 用特征函数 + 连续性定理（Continuity Theorem）完成收敛的证明。

### Step 1：标准化

令 $Y_k = \dfrac{X_k - \mu}{\sigma}$，则 $\{Y_k\}$ i.i.d.，$EY_k = 0$，$\operatorname{Var}(Y_k) = 1$。

原命题等价于证明：

$$
\frac{1}{\sqrt{n}} \sum_{k=1}^n Y_k \xrightarrow{d} \mathcal{N}(0,1)
$$

### Step 2：计算特征函数

设 $Y_1$ 的特征函数为 $\phi(t) = E e^{itY_1}$。

由特征函数的性质：

$$
\phi'(0) = iEY_1 = 0, \quad \phi''(0) = i^2 EY_1^2 = -1
$$

在 $t = 0$ 处做 Taylor 展开（注意 $t/\sqrt{n} \to 0$）：

$$
\phi(t) = \phi(0) + \phi'(0)t + \frac{1}{2}\phi''(0)t^2 + o(t^2) = 1 - \frac{t^2}{2} + o(t^2)
$$

因此，$\dfrac{1}{\sqrt{n}}\sum_{k=1}^n Y_k$ 的特征函数为：

$$
\phi_n(t) = E\exp\!\left(\frac{it(Y_1+\cdots+Y_n)}{\sqrt{n}}\right) = \left[\phi\!\left(\frac{t}{\sqrt{n}}\right)\right]^n
$$

> [!TIP] 为什么可以这样分解？
> 由于 $Y_1,\ldots,Y_n$ 独立，它们之和的特征函数等于各自特征函数的乘积，即 $E e^{it(Y_1+\cdots+Y_n)} = \prod_{k=1}^n E e^{itY_k} = [\phi(t)]^n$。把 $t$ 替换为 $t/\sqrt{n}$ 即得上式。

将 Taylor 展开代入：

$$
\phi_n(t) = \left[1 - \frac{t^2}{2n} + o\!\left(\frac{t^2}{n}\right)\right]^n \xrightarrow{n\to\infty} e^{-t^2/2}
$$

> [!TIP] 为什么极限是 $e^{-t^2/2}$？
> 这是 $1^\infty$ 型极限的标准结果：$\lim_{n\to\infty}\left(1 - \frac{a}{n}\right)^n = e^{-a}$，这里 $a = t^2/2$（高阶项 $o(t^2/n)$ 乘以 $n$ 趋于0，不影响极限）。

而 $e^{-t^2/2}$ 正是标准正态 $\mathcal{N}(0,1)$ 的特征函数。

### Step 3：用连续性定理收尾

> [!NOTE] 定理 1.2（连续性定理，Continuity Theorem）
> 设 $X_n$ 的特征函数为 $\phi_n(t)$，$X$ 的特征函数为 $\phi(t)$。则：
>
> $$X_n \xrightarrow{d} X \iff \lim_{n\to\infty} \phi_n(t) = \phi(t), \quad \forall t \in \mathbb{R}$$

由 $\phi_n(t) \to e^{-t^2/2}$（$\mathcal{N}(0,1)$ 的特征函数），由连续性定理得 $\dfrac{1}{\sqrt{n}}\sum Y_k \xrightarrow{d} \mathcal{N}(0,1)$，证毕。

> [!WARNING] 一个常见误区
> 依分布收敛关注的是**分布函数的逐点极限**，而**不是**：
> $$\mathbb{P}\!\left(\frac{1}{\sqrt{n}}\sum Y_i \le x\right) \;\text{v.s.}\; \mathbb{P}(Y_i \le x)$$
> 后者毫无意义——两者的维度和结构完全不同，不能直接比较。

---

## 五、应用举例

CLT 的核心应用场景可以归结为一个基本关系式：

$$
P\!\left(c_1 \le \frac{\sqrt{n}}{\sigma}\left(\frac{S_n}{n} - \mu\right) \le c_2\right) \approx \Phi(c_2) - \Phi(c_1) = \alpha
$$

其中 $\Phi$ 是标准正态 CDF。根据已知量的不同，分三类题型：

| 题型 | 已知 | 求 | 代表例题 |
| :---: | :---: | :---: | :---: |
| 求样本量 | $c$（误差限），$\alpha$（置信度） | $n$ | 疫苗例 |
| 求分位点/座位数 | $n$，$\alpha$ | $c$ | 电影院例 |
| 求概率 | $n$，$c$ | $\alpha$ | 面包例 |

### 5.1 例 2.1：求样本量（疫苗问题）

**问题**：设疫苗有效比例为 $\mu$，抽 $n$ 人，需多少样本量能以 **95% 概率**保证 $|M_n - \mu| < 0.03$？

**解题步骤**：

$$
\mathbb{P}(|M_n - \mu| < 0.03) \ge 0.95
$$

**Step 1**：标准化。令 $\sigma = \sqrt{\operatorname{Var}(X_1)}$，

$$
= \mathbb{P}\!\left(\left|\frac{M_n - \mu}{\sigma/\sqrt{n}}\right| < \frac{0.03}{\sigma/\sqrt{n}}\right) \approx \mathbb{P}\!\left(|Z| < \frac{0.03\sqrt{n}}{\sigma}\right)
$$

**Step 2**：利用上界。$X_i \in \{0,1\}$ 时，$\sigma \le \dfrac{1}{2}$，因此：

$$
\mathbb{P}\!\left(|Z| < \frac{0.03\sqrt{n}}{\sigma}\right) \ge \mathbb{P}(|Z| < 0.06\sqrt{n})
$$

**Step 3**：令 $\mathbb{P}(|Z| < 0.06\sqrt{n}) = 0.95$，即 $\Phi(0.06\sqrt{n}) - \Phi(-0.06\sqrt{n}) = 0.95$。

由正态分布对称性，$\Phi(0.06\sqrt{n}) = 0.975$，查表得 $0.06\sqrt{n} = 1.96$。

**Step 4**：解出 $n$：

$$
n = \left(\frac{1.96}{0.06}\right)^2 \approx 1068
$$

> [!TIP] 关键技巧：利用方差上界
> 对 $X_i \sim B(1,p)$，$\sigma^2 = p(1-p) \le \frac{1}{4}$，即 $\sigma \le \frac{1}{2}$。
> 利用此上界，可以在不知道 $p$ 的情况下给出保守的样本量估计（最坏情形）。

### 5.2 例 2.2：理论近似（均匀分布）

**问题**：$\{X_n\}$ i.i.d. $\sim \mathcal{U}(-1,1)$，$S_n$ 的精确密度公式极其复杂。

CLT 给出简洁近似：

$$
S_n \approx \mathcal{N}\!\left(0,\;\frac{n}{3}\right)
$$

> [!TIP] 推导
> $E[X_i] = 0$，$\operatorname{Var}(X_i) = \dfrac{(1-(-1))^2}{12} = \dfrac{1}{3}$，故 $S_n \approx \mathcal{N}(0, n \cdot \frac{1}{3})$。

图形验证：$n=2$ 时近似较粗糙，$n=10$ 时正态曲线与精确密度已高度吻合。这体现了**近似可大大简化计算**的价值。

### 5.3 生活中的应用：庞加莱买面包

**背景**：面包店声称每块面包平均重 1000 克，标准差 50 克，即 $\mu=1000$，$\sigma=50$。

庞加莱买了 $n=30$ 次面包，发现平均值总在 940–960 克之间。这件事的概率有多小？

$$
M_n \approx \mathcal{N}(1000, 50^2/30)
$$

$$
\mathbb{P}(940 \le M_{30} \le 960) \approx \mathbb{P}\!\left(\frac{940-1000}{50/\sqrt{30}} \le Z \le \frac{960-1000}{50/\sqrt{30}}\right) \approx 6 \times 10^{-6}
$$

> [!TIP] 为什么这一结果说明店家欺诈？
> 概率只有六百万分之一，正常情况下几乎不可能发生。庞加莱由此断定：面包重量分布的均值远低于 1000 克（约在 950 克左右），面包店偷工减料。面包质量是面粉量、水量、酵母、温度等多个微小因素叠加，按 CLT 应服从正态分布，而实际分布是右偏的（从柱状图可见），说明店家刻意把重一点的面包卖给庞加莱，却依然欺骗其他顾客。

---

## 六、理论拓展（了解）

### 6.1 Lindeberg–Feller 定理（独立不同分布的 CLT）

> [!NOTE] 定理 3.1（Lindeberg–Feller CLT）——选修
> 设 $\{X_n\}$ **独立**（不要求同分布），令 $\sigma_k^2 = \operatorname{Var}(X_k)$，$B_n^2 = \sum_{k=1}^n \sigma_k^2$。
>
> 在 $B_n^2 \to \infty$ 且 $\sigma_n^2/B_n^2 \to 0$ 的条件下，
>
> $$\frac{1}{B_n}\sum_{k=1}^n (X_k - EX_k) \xrightarrow{d} \mathcal{N}(0,1)$$
>
> 成立的**充要条件**是 **Lindeberg 条件**：对任意 $\varepsilon > 0$，
>
> $$\lim_{n\to\infty} \frac{1}{B_n^2}\sum_{k=1}^n E\!\left\{(X_k-EX_k)^2 \mathbf{1}_{\{|X_k - EX_k| > \varepsilon B_n\}}\right\} = 0$$

> [!TIP] Lindeberg 条件的直觉
> 这个条件等价于：每一个 $X_k$ 对总方差的贡献比例趋于零，即**没有占主导地位的随机变量**。也就是说，正态分布出现的条件是"大量微小独立随机因素的叠加"，而不允许某个因素一家独大。
>
> 这一条件等价于 **Feller 条件**：$\lim_{n\to\infty} \max_{1\le k\le n} \dfrac{\sigma_k^2}{B_n^2} = 0$。

### 6.2 正态分布的自然法则地位

这解释了为什么现实中正态分布如此普遍：
- **测量误差**：由大量微小、独立的误差来源叠加而成（Gauss 最初引入正态分布的动机）。
- **工程噪声**：高斯白噪声假设的理论依据。
- **产品重量**：同型号同批次产品，受众多微小工艺因素影响，重量近似正态。

---

## 七、细致讨论

### 7.1 离散化修正（Continuity Correction）

#### 为什么需要修正？

当用**连续**的正态分布近似**离散**随机变量时，会出现两个问题：
1. **区间端点的歧义**：$\mathbb{P}(S_n \le 21) = \mathbb{P}(S_n < 22)$，用哪个端点做近似？
2. **单点概率为零**：连续分布的单点概率为0，但离散情形 $\mathbb{P}(S_n = k) \ne 0$。

#### 修正方法的几何直觉

将整数 $k$ 处的概率质量，近似为连续分布在区间 $[k-0.5, k+0.5]$ 上的面积。这样，离散分布的矩形柱与正态曲线下面积的匹配更加准确。

> [!IMPORTANT] 定理 4.1（de Moivre–Laplace 修正定理）
> 设 $S_n \sim B(n, p)$，$n$ 充分大，$k, m$ 为非负整数，则：
>
> **未修正版**（近似较粗糙）：
>
> $$\mathbb{P}(k \le S_n \le m) \approx \Phi\!\left(\frac{m - np}{\sqrt{np(1-p)}}\right) - \Phi\!\left(\frac{k - np}{\sqrt{np(1-p)}}\right)$$
>
> **修正版**（近似更精确）：
>
> $$\mathbb{P}(k \le S_n \le m) \approx \Phi\!\left(\frac{m + 0.5 - np}{\sqrt{np(1-p)}}\right) - \Phi\!\left(\frac{k - 0.5 - np}{\sqrt{np(1-p)}}\right)$$
>
> **单点概率**（修正版特有优势）：
>
> $$\mathbb{P}(S_n = k) \approx \Phi\!\left(\frac{k + 0.5 - np}{\sqrt{np(1-p)}}\right) - \Phi\!\left(\frac{k - 0.5 - np}{\sqrt{np(1-p)}}\right)$$

> [!WARNING] 修正规则总结
> - 计算 $\mathbb{P}(S_n \le m)$：上限 $m$ 换成 $m + 0.5$
> - 计算 $\mathbb{P}(S_n \ge k)$：下限 $k$ 换成 $k - 0.5$
> - 计算 $\mathbb{P}(S_n = k)$：用区间 $[k-0.5,\; k+0.5]$
> - **该修正方法对其他离散型随机变量（如泊松分布）同样适用。**

#### 数值对比示例（例 4.1）

设 $S_n \sim B(36, 0.5)$，$np = 18$，$\sqrt{np(1-p)} = 3$，求 $\mathbb{P}(S_n \le 21)$。

| 方法 | 结果 |
| :--- | :---: |
| 精确值（二项分布求和） | $0.8785$ |
| CLT 近似（未修正） | $\Phi\!\left(\frac{21-18}{3}\right) = \Phi(1) = 0.8413$ |
| CLT 近似（修正后） | $\Phi\!\left(\frac{21.5-18}{3}\right) = \Phi(1.17) = 0.8790$ |

修正后误差从 $0.037$ 降至 $0.0005$，精度大幅提升。

另：$\mathbb{P}(S_n = 19) = 0.1251$，正态近似修正后 $\approx 0.124$，效果良好。

### 7.2 综合应用：计算区间边界 + 离散修正（例 4.2，电影院问题）

**问题**：某地区每日看电影者约 $n = 1600$ 人，其中 $3/4$ 去新电影院。要求"空座达 200 或更多"的概率不超过 10%，问应设多少座位？

**建模**：令 $X_i = 1$（第 $i$ 人去新院）或 $0$，$\mathbb{P}(X_i = 1) = 3/4$。设座位数为 $m$，条件为：

$$
\mathbb{P}(X_1 + \cdots + X_{1600} \le m - 200) \le 0.1
$$

取等号时 $m$ 最大。

**参数**：$np = 1600 \times \frac{3}{4} = 1200$，$\sqrt{np(1-p)} = \sqrt{1600 \times \frac{3}{4} \times \frac{1}{4}} = 10\sqrt{3}$。

**按修正公式**（$m-200$ 为离散上限，加 $0.5$）：

$$
\Phi\!\left(\frac{(m-200) + 0.5 - 1200}{10\sqrt{3}}\right) = 0.1
$$

查标准正态表：$\Phi^{-1}(0.1) = -1.2816$，故：

$$
\frac{m - 199.5 - 1200}{10\sqrt{3}} = -1.2816 \implies m = 1200 + 199.5 - 1.2816 \times 10\sqrt{3} \approx 1377
$$

**答**：应设 **1377 个座位**。

### 7.3 适用条件

> [!WARNING] 使用 CLT 的前提条件
> 1. $\{X_n\}$ **独立**（或满足 Lindeberg 条件）。
> 2. $EX_i = \mu$ **存在有限**，$\operatorname{Var}(X_i) = \sigma^2 < \infty$。
>
> 缺少任一条件，CLT 可能失效。

#### 反例：柯西分布（例 4.3）

若 $X_1, X_2, \ldots$ i.i.d. 服从柯西分布，则期望不存在（积分不收敛）。此时 $M_n = \frac{1}{n}\sum X_i$ **仍然服从柯西分布**（由特征函数可证），不收敛到正态分布。

#### n 多大才够？

没有简单普遍的准则。关键影响因素：
- **原始分布的对称性**：越接近正态（越对称），$n$ 越小即可。
  - $X_i \sim \mathcal{U}(-1,1)$（对称）：$n = 10$ 已经很好。
  - $X_i \sim \mathcal{E}(\lambda)$（右偏）：需要更大的 $n$。
- **近似点距均值的远近**：在均值附近的近似精度更高，尾部精度较低。

#### 泊松估计 vs 正态估计

对二项分布 $B(\tilde{n}, \tilde{p})$，选哪种近似取决于参数：

| 条件 | 推荐近似 |
| :--- | :--- |
| $\tilde{p}$ 很小，$\tilde{n}\tilde{p}$ 固定（小概率事件） | 泊松近似 $\mathcal{P}(\tilde{n}\tilde{p})$ |
| $\tilde{n}$ 很大，$\tilde{n}\tilde{p}(1-\tilde{p})$ 较大 | 正态近似 $\mathcal{N}(n\tilde{p},\,n\tilde{p}(1-\tilde{p}))$ |
| $\tilde{n}\tilde{p}$ 固定且很大 | 两者均可（泊松可进一步用正态近似） |

---

## 八、题型解题模板

### 前置：建模三行法

> [!TIP] 为什么读懂讲义还是不会做题？
> 讲义展示的是**已建好模之后**的推导，而做题最难的部分恰恰是建模本身。套公式之前，先把下面三行写清楚：
>
> $$X = \underline{\quad},\quad X \sim \text{Bin}(n = \underline{\quad},\; p = \underline{\quad})$$
>
> $$\text{我要求：} P(\underline{\qquad\qquad})$$
>
> $$\text{等价于：} P(\underline{\qquad\qquad}) \quad \longleftarrow \text{翻译成数学语言，这步最关键}$$
>
> 第三行写出来之后，查下方速查表套公式即可。

**示例（题 9）**：每天崩溃概率 5%，50 天内至少 45 天无崩溃的概率。

$$X = \text{崩溃天数},\quad X \sim \text{Bin}(50,\; 0.05)$$

$$\text{我要求：} P(\text{至少 45 天无崩溃})$$

$$\text{等价于：} P(X \le 5) \quad \longleftarrow \text{"至少 45 天无崩溃"= "至多 5 天崩溃"}$$

> [!WARNING] 建模时的三个常见陷阱
> 1. **$p$ 的方向**：$p$ 定义为崩溃（0.05）还是不崩溃（0.95）？选定后全程统一。
> 2. **不等号方向**："至少 45 天无崩溃" $\Rightarrow$ 崩溃天数"至多 5 天" $\Rightarrow$ $X \le 5$，方向易错。
> 3. **近似方法的选择**：$p$ 小时优先泊松近似；$np(1-p)$ 大时用正态近似（见 §7.3 对比表）。

---

### 类型一：求样本量 $n$

**已知**：误差限 $\varepsilon$（即要求 $|M_n - \mu| < \varepsilon$），置信概率 $1 - \alpha$。

**步骤**：
1. 写出 $\mathbb{P}(|M_n - \mu| < \varepsilon) \ge 1 - \alpha$。
2. 标准化为 $\mathbb{P}\!\left(|Z| < \dfrac{\varepsilon\sqrt{n}}{\sigma}\right) \ge 1 - \alpha$。
3. 若 $\sigma$ 未知，用分布性质给出上界（如 $\sigma \le 1/2$）。
4. 令 $\Phi\!\left(\dfrac{\varepsilon\sqrt{n}}{\sigma}\right) = 1 - \alpha/2$，查表得 $z_{\alpha/2}$，解出 $n = \left(\dfrac{z_{\alpha/2} \cdot \sigma}{\varepsilon}\right)^2$。

### 类型二：求分位点/边界 $c$

**已知**：$n$，置信概率。

**步骤**：
1. 标准化，令 $\Phi\!\left(\dfrac{c - np}{\sqrt{np(1-p)}}\right) = \alpha$（注意离散情形加 0.5 修正）。
2. 查表得 $z$ 值，反解 $c$。

### 类型三：求概率

**已知**：$n$，边界 $c$。

**步骤**：
1. 标准化：$\mathbb{P}(S_n \le c) \approx \Phi\!\left(\dfrac{c \pm 0.5 - np}{\sqrt{np(1-p)}}\right)$（离散加修正）。
2. 查标准正态表。

### 离散化修正速查

| 目标概率 | 修正写法 |
| :--- | :--- |
| $\mathbb{P}(S_n \le m)$ | $\Phi\!\left(\dfrac{m+0.5-np}{\sqrt{np(1-p)}}\right)$ |
| $\mathbb{P}(S_n < m)$ | $\Phi\!\left(\dfrac{m-0.5-np}{\sqrt{np(1-p)}}\right)$ |
| $\mathbb{P}(S_n \ge k)$ | $1 - \Phi\!\left(\dfrac{k-0.5-np}{\sqrt{np(1-p)}}\right)$ |
| $\mathbb{P}(k \le S_n \le m)$ | $\Phi\!\left(\dfrac{m+0.5-np}{\sqrt{np(1-p)}}\right) - \Phi\!\left(\dfrac{k-0.5-np}{\sqrt{np(1-p)}}\right)$ |
| $\mathbb{P}(S_n = k)$ | $\Phi\!\left(\dfrac{k+0.5-np}{\sqrt{np(1-p)}}\right) - \Phi\!\left(\dfrac{k-0.5-np}{\sqrt{np(1-p)}}\right)$ |

---

## 九、课堂小结

> [!IMPORTANT] 核心知识点
> - **CLT 的本质**：i.i.d. 序列（有有限方差）的标准化和依分布收敛到 $\mathcal{N}(0,1)$。
> - **应用**：$n$ 充分大时，$S_n \approx \mathcal{N}(n\mu, n\sigma^2)$，$M_n \approx \mathcal{N}(\mu, \sigma^2/n)$。
> - **证明工具**：特征函数 + Taylor 展开 + 连续性定理。
> - **离散修正**：端点 $\pm 0.5$，可计算单点概率。
> - **适用条件**：i.i.d.，有限均值和方差；柯西分布等无有限均值的分布不适用。

> [!NOTE] 课程启示
> - **抓住主要矛盾**：忽略具体分布的细节，抓住均值和方差这两个最关键的参数，即可刻画大量叠加的行为。
> - **偶然性与必然性的辩证统一**：每个 $X_i$ 的取值是偶然的，但它们的和在适当标准化后必然趋向正态分布——这是概率论中最深刻的规律之一。


---

---
title: 收敛性讲义（随机变量序列的极限）
tags:
  - 概率论
  - 收敛性
  - 初等概率论
date: 2026-06-05
---

# Lecture 13b：收敛性

> [!INFO] 本讲概览
> 对应 Bertsekas & Tsitsiklis Ch5 §5.3，何书元 Ch5 §5.6。
>
> **学习要求**：
> - 掌握：依分布收敛、依概率收敛、几乎处处收敛的定义；各收敛性之间的关系
> - 了解：$L_p$ 收敛的定义；反例（不要求掌握涉及 $L_p$ 的反例）；收敛性关系的证明（了解即可）
> - 掌握应用：会使用连续映射定理、Slutsky 定理、Delta 方法等工具

---


> [!ABSTRACT] 收敛性（Convergence）

---

## 一、为什么需要"收敛性"？

在概率论的知识体系中，收敛性是研究**随机变量序列 $X_n$ 极限行为**的核心工具，是大数定律和中心极限定理的理论基础。

从数列的收敛出发类比：数列 $\{a_n\}$ 收敛到 $a$，意味着 $|a_n - a| \to 0$。但随机变量是函数，而非数字，收敛的含义需要区分**收敛的对象**（CDF？概率？样本路径？期望？）从而形成不同的收敛模式。

---

## 二、四种收敛模式的定义

设 $(\Omega, \mathcal{F}, \mathbb{P})$ 是概率空间，$X_n$ 和 $X$ 是定义在其上的随机变量，分布函数分别为 $F_n(x)$ 和 $F(x)$。

### 2.1 依分布收敛（Convergence in Distribution）

> [!NOTE] 定义 2.2（依分布收敛）
> 若在 $F(x)$ 的所有连续点 $x$ 处，有
>
> $$\lim_{n \to \infty} F_n(x) = F(x)$$
>
> 则称 $X_n$ **依分布收敛**到 $X$，记作 $X_n \xrightarrow{d} X$；
> 也称 $F_n$ **弱收敛**到 $F$，记作 $F_n \xrightarrow{w} F$。

**如何验证**：
1. 固定一个 $x$（$F(x)$ 的连续点），得到数列 $F_n(x) = \mathbb{P}(X_n \le x)$，判断它是否收敛到 $F(x)$。
2. 对所有连续点 $x$ 都成立，才称依分布收敛。

> [!TIP] 为什么只要求在连续点处收敛？
> CDF 本身是右连续的，在间断点处 $F(x^-)$ 和 $F(x)$ 不相等，要求所有点处收敛会过于严格，且在实际应用中没有必要。只需在连续点处逐点收敛即可刻画分布的"形状"趋向。

### 2.2 几乎处处收敛（Almost Sure Convergence）

> [!NOTE] 定义 2.3（几乎处处收敛）
> 若
>
> $$\mathbb{P}\!\left(\lim_{n \to \infty} X_n = X\right) = 1$$
>
> 则称 $X_n$ **几乎处处收敛**到 $X$，记作 $X_n \xrightarrow{a.s.} X$ 或 $X_n \to X$ a.s.。

**如何验证**：
1. 固定一个样本点 $\omega \in \Omega$，得到数列 $X_n(\omega),\, X(\omega)$，判断该数列是否收敛。
2. 收集所有满足 $\lim_{n\to\infty} X_n(\omega) = X(\omega)$ 的 $\omega$，构成集合 $A \subseteq \Omega$，计算 $\mathbb{P}(A) = 1$？

**集合语言表达**：利用数列收敛的 $\varepsilon$-$N$ 定义，可以将"$\lim X_n = X$"这一事件写成：

$$\left\{\lim_{n\to\infty} X_n = X\right\} = \bigcup_{n=1}^\infty \bigcap_{k=n}^\infty \{|X_k - X| < \varepsilon\} = \liminf_{n\to\infty} A_n$$

其中 $A_n = \{|X_n - X| < \varepsilon\}$。因此 a.s. 收敛等价于对所有 $\varepsilon > 0$，上述 $\liminf$ 事件的概率为1。

> [!TIP] 与数列收敛的类比
> 数列 $a_n \to a$ $\iff$ $\forall \varepsilon > 0, \exists N, \forall k \ge N: |a_k - a| \le \varepsilon$。
> a.s. 收敛就是说：**以概率1**，存在这样的 $N$（$N$ 可能依赖于 $\omega$）。

### 2.3 依概率收敛（Convergence in Probability）

> [!NOTE] 定义 2.4（依概率收敛）
> 若对 $\forall \varepsilon > 0$，有
>
> $$\lim_{n \to \infty} \mathbb{P}(|X_n - X| \ge \varepsilon) = 0$$
>
> 则称 $X_n$ **依概率收敛**到 $X$，记作 $X_n \xrightarrow{p} X$ 或 $X_n \to X$ in prob.。

**如何验证**：
1. 固定 $n$，得到 $\Omega$ 上的集合 $A_n^c = \{\omega: |X_n(\omega) - X(\omega)| \ge \varepsilon\}$，计算 $\mathbb{P}(A_n^c)$。
2. 考察数列 $\mathbb{P}(A_n^c),\, n=1,2,\ldots$ 是否趋向 $0$。

等价表述：$\lim_{n\to\infty} \mathbb{P}(|X_n - X| \ge \varepsilon) = 0 \iff \lim_{n\to\infty} \mathbb{P}(|X_n - X| < \varepsilon) = 1$。

> [!TIP] a.s. 收敛 vs. 依概率收敛的直觉区别
> - **a.s. 收敛**：对几乎每条样本路径 $\omega$，从某个时刻 $N(\omega)$ 起，$X_n(\omega)$ 一直靠近 $X(\omega)$（"永久近"）。
> - **依概率收敛**：对任意固定的大 $n$，$X_n$ 和 $X$ 相差超过 $\varepsilon$ 的概率很小——但不同的 $n$ 可能是不同的 $\omega$ 在出问题（"当下近"，但可能反复横跳）。

### 2.4 $L_p$ 收敛（了解）

> [!NOTE] 定义 2.5（$L_p$ 收敛）——不要求掌握
> 对 $p > 0$，若
>
> $$\lim_{n \to \infty} E(|X_n - X|^p) = 0$$
>
> 则称 $X_n$ 在 $L_p$ 下收敛到 $X$，记作 $X_n \xrightarrow{L_p} X$。
>
> 特别地：$X_n \xrightarrow{L_1} X \iff \lim_{n\to\infty} E(|X_n - X|) = 0$。

### 2.5 四种定义对比总结

| | 依分布收敛 $\xrightarrow{d}$ | 依概率收敛 $\xrightarrow{p}$ | a.s. 收敛 $\xrightarrow{a.s.}$ | $L_p$ 收敛 $\xrightarrow{L_p}$ |
| :---: | :--- | :--- | :--- | :--- |
| **基于** | CDF | $\mathbb{P}(\cdot)$ | 样本路径 $X(\omega)$ | 期望 $E(\cdot)$ |
| **定义** | $\lim F_n(x)=F(x)$ 在连续点 | $\lim \mathbb{P}(\lvert X_n-X\rvert\ge\varepsilon)=0$ | $\mathbb{P}(\lim X_n = X)=1$ | $\lim E(\lvert X_n-X\rvert^p)=0$ |
| **操作** | 固定 $x$，看 CDF 数列 | 固定 $n$，看概率数列 | 固定 $\omega$，看轨迹数列 | 固定 $p$，看矩数列 |

---

## 三、收敛性之间的关系

### 3.1 关系图

$$
X_n \xrightarrow{a.s.} X \quad \searrow
$$

$$
\quad\quad\quad\quad\quad\quad\quad\quad\quad X_n \xrightarrow{p} X \;\longrightarrow\; X_n \xrightarrow{d} X
$$

$$
X_n \xrightarrow{L_p} X \quad \nearrow
$$

用一句话总结：**a.s. 收敛和 $L_p$ 收敛都蕴含依概率收敛，依概率收敛蕴含依分布收敛，反之均不成立（见反例）。** 这就是为什么依分布收敛被称为"弱收敛"——它是最弱的收敛模式。

### 3.2 定理证明（了解即可）

> [!NOTE] 定理 2.1（a.s. 蕴含依概率）
> 若 $X_n \xrightarrow{a.s.} X$，则 $X_n \xrightarrow{p} X$。

**证明思路**：由 a.s. 收敛的集合表述，$\{\lim X_n = X\} \subseteq \bigcup_{n=1}^\infty \bigcap_{k=n}^\infty \{|X_k - X| < \varepsilon\}$，因此：

$$
\lim_{n\to\infty} \mathbb{P}(|X_n - X| \ge \varepsilon) \le \lim_{n\to\infty} \mathbb{P}\!\left(\bigcup_{k=n}^\infty |X_k - X| \ge \varepsilon\right)
$$

$$
= \mathbb{P}\!\left(\bigcap_{n=1}^\infty \bigcup_{k=n}^\infty |X_k - X| \ge \varepsilon\right) = 1 - \mathbb{P}\!\left(\bigcup_{n=1}^\infty \bigcap_{k=n}^\infty |X_k - X| < \varepsilon\right) = 1 - 1 = 0
$$

> [!NOTE] 定理 2.2（$L_p$ 蕴含依概率）
> 若 $X_n \xrightarrow{L_p} X$，则 $X_n \xrightarrow{p} X$。

**证明思路**：直接用 **Markov 不等式** $\mathbb{P}(|Y| \ge a) \le E|Y|^p / a^p$：

$$
\lim_{n\to\infty} \mathbb{P}(|X_n - X| \ge \varepsilon) \le \lim_{n\to\infty} \frac{1}{\varepsilon^p} E(|X_n - X|^p) = 0
$$

> [!NOTE] 定理 2.3（依概率蕴含依分布）
> 若 $X_n \xrightarrow{p} X$，则 $X_n \xrightarrow{d} X$。

**证明思路**：将 $F_n(x)$ 用 $|X_n - X| \le \varepsilon$ 和 $|X_n - X| > \varepsilon$ 分类，利用依概率收敛，对 $F_n(x)$ 建立夹逼：

$$
F(x-\varepsilon) - \mathbb{P}(|X_n-X|>\varepsilon) \le F_n(x) \le F(x+\varepsilon) + \mathbb{P}(|X_n-X|>\varepsilon)
$$

令 $n\to\infty$，$\mathbb{P}(|X_n-X|>\varepsilon)\to 0$；再令 $\varepsilon\downarrow 0$，在 $F(x)$ 的连续点处 $F(x\pm\varepsilon)\to F(x)$，从而 $F_n(x)\to F(x)$。

> [!TIP] 证明中关键步骤的解释
> 上界推导：$\mathbb{P}(X_n \le x,\, |X_n-X|\le\varepsilon) \le \mathbb{P}(X \le x+\varepsilon)$，因为若 $X_n \le x$ 且 $|X_n-X|\le\varepsilon$，则 $X \le X_n + \varepsilon \le x + \varepsilon$。
>
> 下界推导：$F_n(x) = 1 - \mathbb{P}(X_n > x) \ge 1 - \mathbb{P}(X > x-\varepsilon) - \mathbb{P}(|X_n-X|>\varepsilon) = F(x-\varepsilon) - \mathbb{P}(|X_n-X|>\varepsilon)$，因为 $X_n > x$ 且 $|X_n-X|\le\varepsilon$ 蕴含 $X > x - \varepsilon$。

---

## 四、反例（了解，不要求掌握涉及 $L_p$ 的部分）

反例帮助我们理解各收敛模式之间**不能反推**的方向。

### 4.1 依分布收敛 $\not\Rightarrow$ 依概率收敛

> [!EXAMPLE] 例 2.1
> 设 $\{X_n\}$ i.i.d. $\sim \mathcal{N}(0,1)$，则 $X_n \xrightarrow{d} X_1$（因为它们同分布，CDF 完全相同）。
>
> 但对 $n \ne 1$，$X_n - X_1 \sim \mathcal{N}(0,2)$，即 $\dfrac{X_n - X_1}{\sqrt{2}} \sim \mathcal{N}(0,1)$，因此：
>
> $$\mathbb{P}(|X_n - X_1| > 1) = \mathbb{P}\!\left(\left|\frac{X_n-X_1}{\sqrt{2}}\right| > \frac{1}{\sqrt{2}}\right) = \mathbb{P}\!\left(|X_1| > \frac{1}{\sqrt{2}}\right) > 0$$
>
> 该概率不趋于0，故 $X_n \not\xrightarrow{p} X_1$。

> [!TIP] 直觉解释
> 依分布收敛只要求"**分布的形状**相同"，不要求 $X_n$ 和 $X$ 在同一概率空间上彼此靠近。$X_n$ 和 $X_1$ 虽然都是标准正态，但作为随机变量它们是独立的，相差可以很大。

### 4.2 特殊情形：极限为常数时等价

> [!IMPORTANT] 例 2.2（关键结论，需掌握）
> 若 $C$ 是常数，则：
>
> $$X_n \xrightarrow{d} C \iff X_n \xrightarrow{p} C$$

**直觉**：极限是常数时，$F(x)$ 在 $x = C$ 处有间断点，在其他所有点连续。依分布收敛要求 $F_n(x) \to \mathbf{1}_{x \ge C}$，这实际上就等价于 $X_n$ 集中在 $C$ 附近，即依概率收敛。

**这一结论在大数定律中直接使用**：$M_n \xrightarrow{p} \mu \iff M_n \xrightarrow{d} \mu$。

### 4.3 依概率收敛 $\not\Rightarrow$ a.s. 收敛（了解）

> [!EXAMPLE] 例 2.6（直觉最重要）
> 设 $\{X_n\}$ 独立，$\mathbb{P}(X_n = 1) = 1/n$，$\mathbb{P}(X_n = 0) = 1 - 1/n$。
>
> 则 $X_n \xrightarrow{p} 0$（因为 $\mathbb{P}(|X_n| \ge \varepsilon) = 1/n \to 0$）。
>
> 但 $X_n \not\xrightarrow{a.s.} 0$：令 $A_n = \{X_n = 1\}$，$\sum \mathbb{P}(A_n) = \sum 1/n = \infty$，由 Borel-Cantelli 引理，$\{A_n\}$ 有无穷多个发生的概率为1，即 $X_n = 1$ 无穷多次，不可能 a.s. 收敛到0。

> [!TIP] "打地鼠"直觉
> 每一时刻 $n$，只有 $1/n$ 的概率出问题，所以单次出问题的概率趋零（依概率收敛）。但因为有无穷多次"机会"，总概率 $\sum 1/n = \infty$，出问题的次数仍是无穷多（不是 a.s. 收敛）。如果改成 $\mathbb{P}(X_n = 1) = 1/n^2$，则 $\sum 1/n^2 < \infty$，Borel-Cantelli 引理保证最终只有有限次出问题，此时就能 a.s. 收敛。

---

## 五、常用定理（会用结论即可）

### 5.1 连续映射定理（Continuous Mapping Theorem）

> [!IMPORTANT] 定理 2.4（连续映射定理）
> 设 $g$ 连续，则：
> 1. $X_n \xrightarrow{a.s.} X \implies g(X_n) \xrightarrow{a.s.} g(X)$
> 2. $X_n \xrightarrow{p} X \implies g(X_n) \xrightarrow{p} g(X)$
> 3. $X_n \xrightarrow{d} X \implies g(X_n) \xrightarrow{d} g(X)$
>
> 注意：$X_n \xrightarrow{L_p} X \not\Rightarrow g(X_n) \xrightarrow{L_p} g(X)$。

**用途**：若已知 $X_n$ 的收敛性，可以直接得到 $X_n^2$、$e^{X_n}$、$|X_n|$ 等的收敛性。

### 5.2 Slutsky 定理

> [!IMPORTANT] 定理 2.5（Slutsky's Theorem）
> 假设 $X_n \xrightarrow{d} X$，$Y_n \xrightarrow{d} c$（$c$ 为常数），则：
> 1. $X_n + Y_n \xrightarrow{d} X + c$
> 2. $X_n Y_n \xrightarrow{d} cX$
> 3. $X_n / Y_n \xrightarrow{d} X/c$（$c \ne 0$）

> [!TIP] 证明思路（Coupling）
> 因为 $Y_n \xrightarrow{d} c$，由例2.2知 $Y_n \xrightarrow{p} c$。先证 $(X_n, Y_n) \xrightarrow{d} (X, c)$（联合收敛），再对连续函数 $g(x,y) = x+y$（或 $xy$，$x/y$）应用连续映射定理，即得。

**典型应用**：$t_n$ 分布收敛到正态分布。设 $Z \sim \mathcal{N}(0,1)$，$V_n \sim \chi^2(n)$，则：

$$t_n = \frac{Z}{\sqrt{V_n/n}} \xrightarrow{d} \mathcal{N}(0,1), \quad n \to \infty$$

这是因为 $\sqrt{V_n/n} \xrightarrow{p} 1$（大数定律），由 Slutsky 定理即得。

### 5.3 Delta 方法

> [!IMPORTANT] 定理（Delta Method）——统计推断常用
> 假设 $\sqrt{n}(X_n - a) \xrightarrow{d} \mathcal{N}(0, V)$，$g: \mathbb{R} \to \mathbb{R}$ 连续可导，则：
>
> $$\sqrt{n}\bigl(g(X_n) - g(a)\bigr) \xrightarrow{d} \mathcal{N}\!\bigl(0,\; [g'(a)]^2 \cdot V\bigr)$$

> [!TIP] 理解与推导
> 本质是 Taylor 展开 + Slutsky 定理：
>
> $$g(X_n) - g(a) \approx g'(a)(X_n - a)$$
>
> 因此 $\sqrt{n}(g(X_n)-g(a)) \approx g'(a) \cdot \sqrt{n}(X_n - a)$，由已知条件和连续映射定理即得。
>
> **应用场景**：已知样本均值的渐近正态性，推导样本方差、样本比例的对数、样本相关系数等的渐近分布。

### 5.4 连续性定理（Continuity Theorem）

> [!IMPORTANT] 定理 2.6（连续性定理）
> 设 $X_n$ 的特征函数为 $\phi_n(t)$，$X$ 的特征函数为 $\phi(t)$，则：
>
> $$X_n \xrightarrow{d} X \iff \lim_{n\to\infty} \phi_n(t) = \phi(t), \quad \forall t \in \mathbb{R}$$
>
> PGF、MGF 在满足可逆性的情况下，同样可以替换此处的特征函数。

**应用举例**：二项分布收敛到泊松分布。设 $B(n, p_n)$ 中 $np_n = \lambda$ 固定，当 $n \to \infty$，可以验证其 MGF 收敛到泊松分布的 MGF，从而 $B(n, p_n) \xrightarrow{d} \mathcal{P}(\lambda)$。

**CLT 的证明**正是通过特征函数 + 连续性定理完成的（见 Lecture 13a）。

### 5.5 多维情形：Cramér–Wold 定理

> [!NOTE] 定理 2.8 及引理 2.1（Cramér–Wold）
> 设 $\boldsymbol{X}_n, \boldsymbol{X}$ 是同维度的随机向量，则：
>
> $$\boldsymbol{X}_n \xrightarrow{d} \boldsymbol{X} \iff \boldsymbol{a}^T \boldsymbol{X}_n \xrightarrow{d} \boldsymbol{a}^T \boldsymbol{X}, \quad \forall \text{ 常数向量 } \boldsymbol{a}$$
>
> 即：**向量的依分布收敛问题，可以转化为所有一维线性投影的收敛问题。**

---

## 六、收敛关系速查表

### 6.1 成立的蕴含关系

| 已知 | 结论 | 定理 |
| :--- | :--- | :--- |
| $X_n \xrightarrow{a.s.} X$ | $X_n \xrightarrow{p} X$ | 定理 2.1 |
| $X_n \xrightarrow{L_p} X$ | $X_n \xrightarrow{p} X$ | 定理 2.2（用 Markov） |
| $X_n \xrightarrow{p} X$ | $X_n \xrightarrow{d} X$ | 定理 2.3 |
| $X_n \xrightarrow{d} C$（常数）| $X_n \xrightarrow{p} C$ | 例 2.2 |

### 6.2 不成立的方向（反例汇总）

| 命题 | 结论 | 反例类型 |
| :--- | :---: | :--- |
| $X_n \xrightarrow{d} X \Rightarrow X_n \xrightarrow{p} X$ | ✗ | i.i.d. 正态序列（例2.1）|
| $X_n \xrightarrow{p} X \Rightarrow X_n \xrightarrow{a.s.} X$ | ✗ | 打地鼠反例（例2.6）|
| $X_n \xrightarrow{a.s.} X \Rightarrow X_n \xrightarrow{L_p} X$ | ✗ | 高峰函数（例2.5）|
| $X_n \xrightarrow{p} X \Rightarrow X_n \xrightarrow{L_p} X$ | ✗ | 同上（例2.3）|
| $X_n \xrightarrow{L_p} X \Rightarrow X_n \xrightarrow{L_q} X$（$p < q$）| ✗ | 例 2.4 |

---

## 七、课堂小结

> [!IMPORTANT] 核心知识点
> - **四种收敛**：依分布（最弱）← 依概率 ← a.s. / $L_p$（最强）
> - **唯一等价**：极限为常数时，依分布 $\iff$ 依概率
> - **核心工具**：连续映射定理、Slutsky 定理、Delta 方法、连续性定理
> - **向量化**：Cramér–Wold 定理把向量问题化为一维

> [!TIP] 学习技巧
> - **用反例理解差异**：各收敛性的"不可逆"方向最容易混淆，每个反例都指向一个本质区别。
> - **从数列类比**：把随机变量理解为以 $\omega$ 为下标的函数，a.s. 收敛就是"几乎所有 $\omega$ 对应的数列都收敛"，依概率收敛是"越来越集中"，依分布收敛是"形状越来越像"。
> - **熟记 Markov 不等式**：它是从 $L_p$ 收敛推出依概率收敛的核心引擎，也是很多证明的起点。
