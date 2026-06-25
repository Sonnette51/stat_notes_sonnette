---
title: "Lecture05 概率分布函数、随机变量函数的分布、随机向量的分布(I)"
tags:
  - 概率论
  - 前半学期
  - CDF
  - 随机向量
  - 联合分布
---

# Lecture05 概率分布函数、随机变量函数的分布、随机向量的分布(I)

> [!ABSTRACT] 本讲概要
> PMF 只管离散、PDF 只管连续，而**分布函数 $F(x)=\mathbb{P}(X\le x)$ 对一切随机变量都适用**——它是刻画随机变量信息的统一工具。本讲先建立 CDF 及其与 PMF/PDF 的转换，再解决"$Y=g(X)$ 服从什么分布"，最后把单个随机变量推广为随机向量，引入联合分布、边缘分布与独立性判定。

## 一、概率分布函数（CDF）

### 1.1 分布函数的定义（定义 1.1）

> [!IMPORTANT] 定义 1.1（分布函数）
> 对随机变量 $X$，称 $x$ 的函数
>
> $$
> F(x) = \mathbb{P}(X \le x), \quad x \in \mathbb{R}
> $$
>
> 为 $X$ 的**概率分布函数**或**累积分布函数**（cumulative distribution function, CDF），简称**分布函数**。

**直觉**：$F(x)$ 回答"$X$ 落在 $x$ 左边（含 $x$）的概率有多大"，把整条概率分布的信息"累积"进一个普通的一元函数。引入它的动机：PMF 只能描述离散变量、PDF 只能描述连续变量，各有局限，而我们需要一个回应"完整刻画一个随机变量的信息"需求的万能工具。

---

### 1.2 CDF 与 PMF（离散型）

如果 $X$ 是离散型随机变量，有概率分布

$$
p_k = \mathbb{P}(X = x_k), \quad k = 1, 2, \ldots
$$

（也可写成分布列表格），则 $X$ 的分布函数为

$$
F(x) = \mathbb{P}(X \le x) = \mathbb{P}\left(\bigcup_{j: x_j \le x} \{X = x_j\}\right) = \sum_{j: x_j \le x} p_j.
$$

**直觉**：把 $x$ 左侧所有取值点的概率加起来，所以离散变量的 CDF 是一条**单调不减的阶梯函数**。

几个要点（课件配有"某些离散随机变量的 CDF"图示）：
- $F(x)$ 在每个 $x_j$ 处有**跳跃**，跳跃高度恰为 $p_j$；
- PMF 与 CDF **相互唯一决定**。例：假设 $\mathbb{P}(1)=0.2$，$\mathbb{P}(2)=0.5$，则 $F(1.5)=\mathbb{P}(X\le 1.5)=0.2$；反过来，已知 $F(x),\forall x$，由跳跃高度可读出 $\mathbb{P}(2)=F(2)-F(2^-)$；
- 若 $\{x_k\}$ 单增，则

$$
p_k = \mathbb{P}(X \le x_k) - \mathbb{P}(X \le x_{k-1}) = F(x_k) - F(x_{k-1});
$$

- 令 $H(x)$ 是 Heaviside 函数：$H(x) = I_{[0,\infty)}(x)$，则

$$
F(x) = \sum_{k=1}^{\infty} p_k H(x - x_k). \tag{1}
$$

> [!NOTE] 备注
> 如果分布函数 $F(x)$ 可以表示为 (1) 式的形式，称 $F(x)$ 是**离散的**（$F(x)$ is called *discrete*）。

---

### 1.3 CDF 与 PDF（连续型）

如果 $X$ 是连续型随机变量，有概率密度 $f(x)$，则

$$
F(x) = \mathbb{P}(X \le x) = \int_{-\infty}^{x} f(t)\,dt, \quad x \in \mathbb{R}
$$

是连续函数，并且在 $f(x)$ 的连续点上 $f(x) = F'(x)$，称 $F(x)$ 是 $f(x)$ 的**分布函数**。

**直觉**：连续情形把"求和"换成"积分"——CDF 是密度曲线下从 $-\infty$ 累积到 $x$ 的面积；反过来对 CDF 求导就还原出密度。

---

### 1.4 标准正态分布的分布函数（例 1.1）

> [!EXAMPLE]- 例题 1.1：标准正态分布的分布函数与一般正态概率的计算
> **解**
>
> 标准正态分布的分布函数记为
>
> $$
> \Phi(x) = \int_{-\infty}^{x} \varphi(t)\,dt = \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}} e^{-\frac{t^2}{2}}\,dt.
> $$
>
> **对称性**：利用 $\varphi(t)$ 是偶函数（密度关于 $0$ 对称），得
>
> $$
> \Phi(x) + \Phi(-x) = 1, \quad \text{或} \quad \Phi(-x) = 1 - \Phi(x), \quad x \in \mathbb{R}.
> $$
>
> （注：此步补全了推导——$\Phi(-x)=\int_{-\infty}^{-x}\varphi(t)dt$ 作换元 $t\mapsto -t$ 后等于 $\int_{x}^{\infty}\varphi(t)dt = 1-\Phi(x)$。）
>
> **一般正态分布**：对 $X \sim N(\mu, \sigma^2)$，有
>
> $$
> \begin{align}
> \mathbb{P}(X \le a) &= \frac{1}{\sigma\sqrt{2\pi}} \int_{-\infty}^{a} \exp\left\{-\frac{(x-\mu)^2}{2\sigma^2}\right\} dx \\
> &= \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{(a-\mu)/\sigma} e^{-y^2/2}\,dy \\
> &= \Phi\!\left(\frac{a-\mu}{\sigma}\right).
> \end{align}
> $$
>
> （注：此步补全了换元——令 $y = \dfrac{x-\mu}{\sigma}$，$dx = \sigma\,dy$，积分上限变为 $\dfrac{a-\mu}{\sigma}$。）
>
> **结论**：任何正态概率都可以**标准化**后查标准正态表求得。

> [!TIP] 方法：查标准正态表
> 表的行给出 $x$ 的整数与十分位、列给出百分位。例如查 $\Phi(0.84)$：找到行 $0.8$、列 $.04$ 的交叉处，读出 $\Phi(0.84) = 0.7995$。

---

### 1.5 $3\sigma$ 与 $6\sigma$ 原则

当 $X \sim N(\mu, \sigma^2)$ 时，利用标准化与对称性：

| 区间 | 概率 |
| --- | --- |
| $\mathbb{P}(\lvert X-\mu\rvert \le \sigma) = \Phi(1)-\Phi(-1) = 2\Phi(1)-1$ | $68.27\%$ |
| $\mathbb{P}(\lvert X-\mu\rvert \le 2\sigma) = \Phi(2)-\Phi(-2) = 2\Phi(2)-1$ | $95.45\%$ |
| $\mathbb{P}(\lvert X-\mu\rvert \le 3\sigma) = \Phi(3)-\Phi(-3) = 2\Phi(3)-1$ | $99.73\%$ |
| $\mathbb{P}(\lvert X-\mu\rvert \le 6\sigma) = 2\Phi(6)-1$ | $99.9999998\%$ |

> [!NOTE] 备注
> 在产品质量或服务质量管理中，所谓的 $3\sigma$ 或 $6\sigma$ **管理原则**就是要求产品质量的合格率、产品性能的可靠性或服务系统的满意度等达到 $\mathbb{P}(|X-\mu| \le 3\sigma)$ 或 $\mathbb{P}(|X-\mu| \le 6\sigma)$ 的水平。

---

### 1.6 分布函数的功能 1：统一框架下比较不同类型的随机变量

分布函数对一切随机变量都适用，可以用来探讨**离散和连续随机变量之间的关系**。例如，考虑几何随机变量与指数随机变量间的关系。

$X_1 \sim G(p)$，即 $\mathbb{P}(X_1 = k) = p(1-p)^{k-1}$。记 $n = [x]$（取整），则 $X_1$ 的 CDF 为

$$
F_1(x) = F_1(n) = \mathbb{P}(X_1 \le n) = \sum_{k=1}^{n} p(1-p)^{k-1} = p\,\frac{1-(1-p)^n}{1-(1-p)} = 1-(1-p)^n, \quad n = 1, 2, \ldots
$$

$X_2 \sim \mathcal{E}(\lambda)$，则 $X_2$ 的 CDF 为

$$
F_2(x) = \mathbb{P}(X_2 \le x) = \int_{-\infty}^{x} \lambda e^{-\lambda t}\,dt = -e^{-\lambda t}\Big|_0^x = 1 - e^{-\lambda x}, \quad x > 0.
$$

**比较两分布函数**：令 $\delta = -\dfrac{\ln(1-p)}{\lambda}$，即 $e^{-\lambda\delta} = 1-p$。则对于 $n = 1, 2, \ldots$，有

$$
F_1(n) = 1-(1-p)^n = 1 - e^{-\lambda n\delta} = F_2(n\delta).
$$

（注：此步补全了中间等式——$(1-p)^n = (e^{-\lambda\delta})^n = e^{-\lambda n\delta}$。）

**直觉解释**：快速抛掷硬币，每 $\delta$ 秒抛一次，每次正面的概率为 $p$。则 $X_1$ 表示第一次出正面时的抛掷次数，$X_1\delta$ 表示这一时刻。从分布函数图像（几何 CDF 阶梯 $1-(1-p)^n$ 紧贴指数 CDF 曲线 $1-e^{-\lambda x}$）可以看到 $X_1\delta \approx X_2$——**几何分布是指数分布的离散化**。

---

### 1.7 分布函数的功能 2：研究混合型随机变量

分布函数对于一切随机变量都适用，也可以用来研究**其他类型**（既非纯离散又非纯连续）的随机变量。

> [!EXAMPLE]- 例题：抛硬币 + 幸运转盘（混合型随机变量）
> 抛匀质硬币：正面直接得钱 $0.5$ 元；反面转一个幸运转盘，可得钱为 $0$ 到 $1$（元）的均匀分布。求所得钱数 $X$ 的分布函数。
>
> **解**
>
> $X$ 的结构：以概率 $\dfrac{1}{2}$ 取定值 $0.5$（离散成分）；以概率 $\dfrac{1}{2}$ 服从 $\mathcal{U}(0,1)$（连续成分）。由全概率公式，对任意 $x$：
>
> $$
> F(x) = \frac{1}{2}\,I_{[0.5,\infty)}(x) + \frac{1}{2}\,\mathbb{P}(U \le x), \quad U \sim \mathcal{U}(0,1).
> $$
>
> 逐段写出（注：此步补全了课件图 (2) 对应的解析表达式）：
>
> $$
> F(x) =
> \begin{cases}
> 0, & x < 0, \\
> \dfrac{x}{2}, & 0 \le x < \dfrac{1}{2}, \\
> \dfrac{x}{2} + \dfrac{1}{2}, & \dfrac{1}{2} \le x < 1, \\
> 1, & x \ge 1.
> \end{cases}
> $$
>
> 图像：CDF 先以斜率 $\dfrac{1}{2}$ 上升到 $F\left(\dfrac{1}{2}^-\right) = \dfrac{1}{4}$，在 $x = \dfrac{1}{2}$ 处**跳跃** $\dfrac{1}{2}$ 到 $\dfrac{3}{4}$，再以斜率 $\dfrac{1}{2}$ 升到 $1$。它既不是阶梯函数，也不是连续函数——这正是混合型随机变量的 CDF。

---

### 1.8 概率分布函数的性质（定理 1.1）

> [!IMPORTANT] 定理 1.1（分布函数 $F(x)$ 的性质）
> 1. $F(x)$ 单调非降；
> 2. $F(-\infty) = \lim\limits_{x \to -\infty} F(x) = 0$，$F(\infty) = \lim\limits_{x \to \infty} F(x) = 1$；
> 3. $F(x)$ 是**右连续**的。

**证明**：

(1) 对任意的 $x < y$，有

$$
F(y) - F(x) = \mathbb{P}(x < X \le y) \ge 0,
$$

即 $F(x) \le F(y)$，故结论 (1) 成立。

(2) 由概率的连续性，可得

$$
F(\infty) = \lim_{n \to \infty} F(n) = \lim_{n \to \infty} \mathbb{P}(X \le n) = \mathbb{P}\left(\bigcup_{n=1}^{\infty} \{X \le n\}\right) = \mathbb{P}(X < \infty) = 1.
$$

同理可证 $F(-\infty) = 0$。

(3) 由 $F(x)$ 的单调性和概率的连续性，可得

$$
\begin{align}
\lim_{n \to \infty} F(x + n^{-1}) &= \lim_{n \to \infty} \mathbb{P}(X \le x + n^{-1}) \\
&= \mathbb{P}\left(\bigcap_{n=1}^{\infty} \{X \le x + n^{-1}\}\right) \\
&= \mathbb{P}(X \le x) = F(x).
\end{align}
$$

（注：此步补全了说明——由于 $F$ 单调，右极限存在，故只需沿一列 $x + n^{-1} \downarrow x$ 验证即可得 $F(x^+)=F(x)$。）

> [!WARNING] 易错
> 分布函数是**右连续**而非左连续的：$F(x^+) = F(x)$ 恒成立，但 $F(x^-) = F(x) - \mathbb{P}(X = x)$ 可以有跳跃。这来源于定义中用的是 $\le$（事件 $\{X \le x\}$ 包含端点）。因此 $\mathbb{P}(X = x) = F(x) - F(x^-)$，且 $\mathbb{P}(a < X \le b) = F(b) - F(a)$ 中区间是**左开右闭**的。

---

### 1.9 如何通过分布函数判断随机变量的类型（定理 1.2）

> [!IMPORTANT] 定理 1.2
> 如果对 $\forall x \in \mathbb{R}$ 都有 $\mathbb{P}(X = x) = 0$，则 $F(x) = \mathbb{P}(X \le x)$ 是连续的。

**证明**：由分布函数的右连续性，

$$
\begin{align}
0 = \mathbb{P}(X = x) &= \mathbb{P}\left(\bigcap_{m=1}^{\infty} \left\{x - \frac{1}{m} < X \le x\right\}\right) \\
&= \lim_{m \to \infty} \left[F(x) - F(x - m^{-1})\right] \\
&= F(x) - F(x^-),
\end{align}
$$

即 $F(x)$ 是左连续的；又因为 $F(x)$ 是右连续的，因此 $F$ 是连续的。$\square$

> [!NOTE] 备注
> **说明**：若 $F$ 不连续，则 $X$ 必非连续型随机变量（跳跃点处 $\mathbb{P}(X=x)>0$，是"原子"）。

---

### 1.10 概率分布函数的补充性质（定理 1.3）：由 $F$ 求密度

> [!IMPORTANT] 定理 1.3
> 设 $X$ 的分布函数 $F(x)$ **连续**，数集 $A$ 中任何两点之间的距离大于某个正数 $\delta$。如果在 $A^c$ 上导数 $F'(x)$ 存在且连续，则
>
> $$
> f(x) =
> \begin{cases}
> F'(x), & \text{当 } x \notin A, \\
> 0, & \text{当 } x \in A
> \end{cases}
> $$
>
> 是 $X$ 的密度函数。

**证明思路**：对任何的 $a < b$，不妨设 $(a,b)$ 中只有集合 $A$ 中的 $a_1, a_2, \ldots, a_k$，并且记 $a_0 = a < a_1 < a_2 < \cdots < a_k < b = a_{k+1}$。此时利用 $F$ 的连续性逐段累加：

$$
\mathbb{P}(a < X \le b) = \sum_{j=0}^{k} \mathbb{P}(a_j < X \le a_{j+1}) = \sum_{j=0}^{k} \left[F(a_{j+1}) - F(a_j)\right] = \sum_{j=0}^{k} \int_{a_j}^{a_{j+1}} f(t)\,dt = \int_a^b f(t)\,dt.
$$

故 $f(x)$ 是 $X$ 的概率密度。$\square$

> [!NOTE] 备注
> 在该定理中，$F$ **连续**的条件是至关重要的。尽管 $F$ 连续不能保证 $X$ 是连续型随机变量，但是 $F$ 不连续能保证 $X$ **不是**连续型随机变量。当 $F$ 是不连续的随机变量的分布函数时，除去有限（跳跃）点外 $F'(x) = 0$，所以 $X$ 的密度不存在。定理中关于数集 $A$ 的限制条件是有必要的（详见附录）。

> [!WARNING] 辨析
> "$F$ 连续" $\ne$ "$X$ 是连续型随机变量"！连续型要求 $F$ 能写成密度的积分（绝对连续）。存在 $F$ 处处连续、却**没有密度**的反例——附录中的 Cantor 分布（奇异分布）：$F$ 连续单调上升，但除一个零测集外 $F'(x) = 0$，$\int F' = 0 \ne 1$。正确的逻辑链是：$F$ 有跳跃 $\Rightarrow$ 必非连续型；$F$ 连续且满足定理 1.3 条件 $\Rightarrow$ 连续型，密度取 $F'$。

---

## 二、随机变量函数的分布

为什么需要这一板块：实际中常对 $X$ 做变换（平方、标准化、取余弦……），需要求 $Y = g(X)$ 的分布。

### 2.1 离散型随机变量的函数

**方法**：对 $Y = g(X)$ 的每一个可能值，计算分布（$Y$ 也是离散的，故需算其分布列）——把映到同一个 $y$ 值的那些 $x$ 的概率**合并相加**（课件配有 $x$ 轴经 $g(x)$ 多对一映到 $y$ 轴的示意图）。

> [!EXAMPLE]- 例题 2.1：求 $Y = X^2$ 的分布
> 设 $X$ 有如下的概率分布：
>
> | $X$ | $-2$ | $-1$ | $0$ | $1$ | $3$ |
> | --- | --- | --- | --- | --- | --- |
> | $\mathbb{P}$ | $0.1$ | $0.2$ | $0.3$ | $0.2$ | $0.2$ |
>
> 求 $Y = X^2$ 的分布。
>
> **解**
>
> $Y$ 可能的取值为 $0, 1, 4, 9$，而且
>
> $$
> \mathbb{P}(Y = 0) = \mathbb{P}(X = 0) = 0.3
> $$
>
> $$
> \mathbb{P}(Y = 1) = \mathbb{P}(|X| = 1) = \mathbb{P}(X = -1) + \mathbb{P}(X = 1) = 0.2 + 0.2 = 0.4
> $$
>
> $$
> \mathbb{P}(Y = 4) = \mathbb{P}(X = -2) = 0.1
> $$
>
> $$
> \mathbb{P}(Y = 9) = \mathbb{P}(X = 3) = 0.2
> $$
>
> （注：此步补全了 $\mathbb{P}(Y=1)$ 的展开加法。）于是 $Y$ 的分布列为：
>
> | $Y$ | $0$ | $1$ | $4$ | $9$ |
> | --- | --- | --- | --- | --- |
> | $\mathbb{P}$ | $0.3$ | $0.4$ | $0.1$ | $0.2$ |

---

### 2.2 连续型随机变量的函数：CDF 两步法（常用）

考察 $Y = g(X)$ 的分布。若 $g(x)$ 是连续函数，则可通过下面两步实现：

> [!TIP] 方法：CDF 两步法
> 1. 得到 $Y$ 的 CDF：$F_Y(y) = \mathbb{P}(Y \le y) = \mathbb{P}(g(X) \le y)$（化为关于 $X$ 的事件，用 $X$ 的分布算）；
> 2. 求导得到：$f_Y(y) = \dfrac{dF_Y(y)}{dy}$。

> [!EXAMPLE]- 例题 2.2：正态标准化
> 设 $X \sim N(\mu, \sigma^2)$，则 $Y = (X - \mu)/\sigma \sim N(0, 1)$。
>
> **解**
>
> 显然
>
> $$
> \begin{align}
> \mathbb{P}(Y \le y) &= \mathbb{P}(X \le \mu + \sigma y) \\
> &= \int_{-\infty}^{\mu + \sigma y} \frac{1}{\sigma\sqrt{2\pi}} \exp\left\{-\frac{(x-\mu)^2}{2\sigma^2}\right\} dx \\
> &= \int_{-\infty}^{y} \frac{1}{\sqrt{2\pi}} \exp\left\{-\frac{t^2}{2}\right\} dt \\
> &= \int_{-\infty}^{y} \varphi(t)\,dt
> \end{align}
> $$
>
> （注：此步补全了换元——第三个等号令 $t = \dfrac{x-\mu}{\sigma}$，$dx = \sigma\,dt$。）
>
> 因此 $Y \sim N(0,1)$。

> [!EXAMPLE]- 例题 2.3：标准正态的平方
> 设 $X \sim N(0,1)$，求 $Y = X^2$ 的概率密度。
>
> **解**
>
> 由于 $Y \ge 0$，对于 $y > 0$，分布函数
>
> $$
> F_Y(y) = \mathbb{P}(Y \le y) = \mathbb{P}(-\sqrt{y} \le X \le \sqrt{y}) = \Phi(\sqrt{y}) - \Phi(-\sqrt{y}) = 2\Phi(\sqrt{y}) - 1
> $$
>
> （最后一步用了对称性 $\Phi(-x) = 1 - \Phi(x)$）。$F_Y$ 是连续函数，所以求导得 $Y$ 的密度为
>
> $$
> f_Y(y) = F_Y'(y) = 2\varphi(\sqrt{y}) \cdot \frac{1}{2\sqrt{y}} = \frac{1}{\sqrt{2\pi y}}\, e^{-y/2}, \quad y > 0.
> $$
>
> （注：此步补全了链式法则——$\dfrac{d}{dy}\sqrt{y} = \dfrac{1}{2\sqrt{y}}$，$\varphi(\sqrt{y}) = \dfrac{1}{\sqrt{2\pi}}e^{-y/2}$。）
>
> 即 $Y \sim \Gamma(1/2,\ 1/2) = \chi_1^2$。

---

### 2.3 插页：Gamma 分布

> [!IMPORTANT] 定义（Gamma 分布 $\Gamma(\alpha,\lambda)$）
> 设 $\alpha, \lambda$ 是正常数，如果 $X$ 的密度是
>
> $$
> f(x) = \frac{\lambda^{\alpha}}{\Gamma(\alpha)}\, x^{\alpha-1} e^{-\lambda x}, \quad x \ge 0,
> $$
>
> 称 $X$ 服从参数为 $(\alpha, \lambda)$ 的 **Gamma 分布**，记作 $X \sim \Gamma(\alpha, \lambda)$，其中
>
> $$
> \Gamma(\alpha) = \int_0^{\infty} x^{\alpha-1} e^{-x}\,dx
> $$
>
> 称为 Gamma 函数。

**直觉**：Gamma 分布是"等待第 $\alpha$ 个事件发生的时间"的连续推广，$\alpha$ 控制形状、$\lambda$ 控制时间尺度。

**Gamma 函数的性质**（常用）：
- (a) $\Gamma(n) = (n-1)!$；
- (b) $\Gamma(\alpha + 1) = \alpha\,\Gamma(\alpha)$；
- (c) $\Gamma\!\left(\dfrac{1}{2}\right) = \sqrt{\pi}$。

> [!NOTE] 备注
> - $\alpha$ 被称为形状参数（shape parameter）；$\lambda$ 被称为尺度参数（rate parameter）。
> - 当 $\alpha = 1$ 时，为指数分布 $\mathcal{E}(\lambda)$。
> - 当 $\alpha$ 为正整数时，称为 **Erlang 分布**（用在"排队论"中）。
> - 在气象学中，干旱地区的年、季或月降水量被认为服从 $\Gamma$ 分布。
> - 英国著名统计学家 Karl Pearson 在研究物理、生物及经济中的随机变量时，发现很多连续型随机变量的分布不是正态分布，这些随机变量的特点是只取非负值，于是他致力于这类随机变量的研究，参阅 Wikipedia 上的 "Pearson distribution"。

---

### 2.4 常见分布关系图（课件手绘页）

课件第 30 页手绘了常见分布之间的关系网，归纳如下：

| 关系                                                                        | 内容                                                                      |
| ------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| $B(p) \xrightarrow{\text{iid 求和}} B(n,p)$                                 | $n$ 个独立两点变量之和是二项                                                        |
| $B(n,p) \xleftarrow[N \to +\infty]{\;M/N \to p\;} HG(n,M,N)$              | 超几何（无放回）在总体无穷大时趋于二项（有放回）；二项是"固定试验次数数成功数"（# successes in fixed # trials） |
| $NB(r,p) \xleftarrow[N \to \infty]{} NHG(r,M,N)$                          | 负超几何趋于负二项；负二项是"固定成功数数试验次数"（# trials for fixed # successes）              |
| $B(n,p) \xrightarrow[n \to +\infty]{np \to \lambda} \mathcal{P}(\lambda)$ | Poisson 逼近                                                              |
| $\mathcal{E}(\lambda) \xrightarrow{\text{iid 求和}} \Gamma(n,\lambda)$      | $n$ 个独立指数之和是 Erlang/Gamma                                               |
| $G(p) \xrightarrow{\text{iid 求和}} NB(r,p)$                                | $r$ 个独立几何之和是负二项（Pascal）                                                 |
| $\mathcal{E}(\lambda) \longleftrightarrow G(p)$                           | 二者都**无记忆**（memoryless），几何是指数的离散化（见 1.6 节）                               |
| $\mathcal{U}(a,b)$、$N(\mu,\sigma^2)$                                      | 单列于图左侧的两个基本连续分布                                                         |

---

### 2.5 特殊情形：线性变换 $Y = aX + b$（常用）

一些特殊情形可以从 $f_X(x)$ **直接得到** $f_Y(y)$，无需再计算 CDF。

形如 $Y = aX + b$（例：$Y = 2X + 5$，课件给出密度曲线被平移、拉伸的图示——$f_X \to f_{2X} \to f_{2X+5}$，先把横轴拉伸 $2$ 倍、纵轴压低一半，再右移 $5$）：

$$
f_Y(y) = \frac{1}{|a|}\, f_X\!\left(\frac{y - b}{a}\right).
$$

**直觉**：$X$ 落在小区间的概率 = $Y$ 落在被放大 $|a|$ 倍的对应小区间的概率，密度因此被压缩 $|a|$ 倍。

> [!NOTE] 备注
> 可以利用该结论验证：若 $X$ 是服从正态分布的随机变量，则 $Y = aX + b$ 也是正态的（重温例 2.2 的标准化即其特例）。

---

### 2.6 严格单调函数的情形

**扩展**：$Y = g(X)$，$g(x)$ 是严格单调（增）函数。考虑小区间事件（课件配 $g$ 的切线斜率示意图）：

$$
\{x < X \le x + \delta\} = \{g(x) < Y \le g(x + \delta)\} \approx \left\{g(x) < Y \le g(x) + \delta \cdot \frac{dg}{dx}(x)\right\}.
$$

因此

$$
\delta \cdot f_X(x) \approx \delta \cdot f_Y(g(x)) \cdot |g'(x)|,
$$

即

$$
f_Y(y) = f_X(h(y))\,|h'(y)|,
$$

其中 $h(y)$ 是 $g(x)$ 的逆映射。

**直觉**：概率质量守恒——$X$ 处一小段的概率搬到 $Y$ 轴后总量不变，密度按局部伸缩率 $|h'(y)|$ 调整。

---

### 2.7 非单调函数：一般定理（定理 2.1）

仍考虑 $Y = g(X)$，如果 $g(\cdot)$ 非单调函数（如 $y = r\cos x$ 在 $(0, 2\pi)$ 上对每个 $y$ 有两个原像），怎么办？

> [!IMPORTANT] 定理 2.1
> 设 $X$ 的概率密度 $f(x)$，$D \subset \mathbb{R}$，$Y = g(X)$，$\mathbb{P}(Y \in D) = 1$。如果
> 1. 对 $y \in D$，$\{Y = y\} = \bigcup_{i=1}^{n} \{X = h_i(y)\}$；
> 2. 每个 $h_i(y)$ 是 $D$ 到其值域 $D_i$ 的可逆映射，在 $D$ 内有连续的导数；
> 3. $D_1, D_2, \ldots, D_n$ 互不相交，
>
> 则 $Y$ 的密度函数为
>
> $$
> f_Y(y) =
> \begin{cases}
> \displaystyle\sum_{i=1}^{n} f\big(h_i(y)\big)\,|h_i'(y)|, & y \in D, \\
> 0, & y \in D^c.
> \end{cases}
> $$

**直觉**：每个单调分支各自贡献一份 $f(h_i(y))|h_i'(y)|$，把各分支的贡献**加起来**就是 $Y$ 的密度。

> [!EXAMPLE]- 例题 2.4：$Y = r\cos X$ 的概率密度
> 设 $r$ 是正常数，$X \sim \mathcal{U}(0, 2\pi)$，求 $Y = r\cos X$ 的概率密度。
>
> **解（方法一：用定理 2.1）**
>
> 设 $D = (-r, r)$，则 $\mathbb{P}(Y \in D) = 1$。对于 $y \in D$，有
>
> $$
> \begin{align}
> \{Y = y\} &= \{\cos X = y/r\} \\
> &= \{\cos X = y/r,\ X \in (0,\pi)\} \cup \{\cos X = y/r,\ X \in (\pi, 2\pi)\} \\
> &= \{\cos X = y/r,\ X \in (0,\pi)\} \cup \{\cos(2\pi - X) = y/r,\ X \in (\pi, 2\pi)\} \\
> &= \{X = \arccos(y/r)\} \cup \{X = 2\pi - \arccos(y/r)\}.
> \end{align}
> $$
>
> $h_1(y) = \arccos(y/r): D \to (0, \pi)$，$h_2(y) = 2\pi - \arccos(y/r): D \to (\pi, 2\pi)$ 都是可逆的、连续可微的函数，且值域不相交。利用 $f_X(x) = \dfrac{1}{2\pi}$，$x \in (0, 2\pi)$，可得 $Y$ 的密度函数
>
> $$
> \begin{align}
> f_Y(y) &= \frac{1}{2\pi}\left|\frac{d}{dy}\arccos\left(\frac{y}{r}\right)\right| + \frac{1}{2\pi}\left|\frac{d}{dy}\left[2\pi - \arccos\left(\frac{y}{r}\right)\right]\right| \\
> &= 2 \cdot \frac{1}{2\pi} \cdot \frac{1}{r\sqrt{1 - y^2/r^2}} \\
> &= \frac{1}{\pi\sqrt{r^2 - y^2}}, \quad y \in (-r, r).
> \end{align}
> $$
>
> （注：此步补全了求导——$[\arccos(u)]' = -\dfrac{1}{\sqrt{1-u^2}}$，再乘内导数 $\dfrac{1}{r}$，取绝对值后两支贡献相同。）
>
> **解（方法二：CDF 两步法）**
>
> 对 $y \in (-r, r)$，
>
> $$
> \begin{align}
> \mathbb{P}(Y \le y) &= \mathbb{P}(\cos X \le y/r) \\
> &= \int_{\{x:\, \cos x \le y/r\}} \frac{1}{2\pi}\,dx \\
> &= \frac{1}{2\pi}\left\{2\pi - 2\arccos(y/r)\right\}
> \end{align}
> $$
>
> （注：此步补全了几何解释——在 $(0,2\pi)$ 内 $\cos x \le y/r$ 的解集是区间 $(\arccos(y/r),\ 2\pi - \arccos(y/r))$，长度为 $2\pi - 2\arccos(y/r)$。）
>
> 根据
>
> $$
> [\arccos(x)]' = -\frac{1}{\sqrt{1 - x^2}}
> $$
>
> 可得
>
> $$
> f_Y(y) = \frac{d}{dy}\left[1 - \frac{\arccos(y/r)}{\pi}\right] = \frac{1}{\pi\sqrt{r^2 - y^2}}, \quad y \in (-r, r).
> $$
>
> 两种方法结果一致。

---

## 三、随机向量及其分布（I）

内容提要：定义（针对一般的随机向量 general r.v.）、离散型随机向量（连续型随机向量下一讲介绍）。重点关注：**全面 vs 片面**（联合 vs 边缘）、**CDF vs PMF/PDF**、**独立性的判定法则**。

### 3.1 随机向量与联合分布函数（定义 3.1、3.2）

> [!IMPORTANT] 定义 3.1（n 维随机向量）
> 如果 $X_1, \ldots, X_n$ 都是概率空间 $(\Omega, \mathcal{F}, \mathbb{P})$ 上的随机变量，称 $\mathbf{X} = (X_1, \ldots, X_n)$ 是概率空间 $(\Omega, \mathcal{F}, \mathbb{P})$ 上的 **n 维随机向量**，简称**随机向量**。

**直觉**：同一个样本空间上的 $n$ 个随机变量"捆"在一起看——同一次随机试验同时产生 $n$ 个数。

> [!IMPORTANT] 定义 3.2（联合概率分布函数）
> 设 $\mathbf{X} = (X_1, \ldots, X_n)$ 是随机向量，称 $\mathbb{R}^n$ 上的 $n$ 元函数
>
> $$
> F(x_1, x_2, \ldots, x_n) = \mathbb{P}(X_1 \le x_1,\ X_2 \le x_2,\ \ldots,\ X_n \le x_n)
> $$
>
> 为 $\mathbf{X} = (X_1, \ldots, X_n)$ 的**联合概率分布函数**，简称为**分布函数**或者**联合分布**。

**直觉**：联合 CDF 度量"所有分量同时落在各自左半轴"的概率，即点 $\mathbf{x}$ 左下方无穷矩形区域的概率。

> [!NOTE] 备注
> 联合分布函数 $F(x_1, x_2, \ldots, x_n)$ 是 $\mathbb{R}^n$ 上的右连续函数，关于每个自变元 $x_j$ 单调非降。记号约定：
>
> $$
> F(\mathbf{x}) = \mathbb{P}(\mathbf{X} \le \mathbf{x}),\quad \text{其中 } \mathbf{X} \le \mathbf{x} \Leftrightarrow X_j \le x_j,\ j = 1, \ldots, n.
> $$

---

### 3.2 离散型随机向量

#### A. 联合分布列：引例

考虑同时抛掷两个 4 面的骰子（一红一黑），记 $X$、$Y$ 分别为红、黑骰子的点数。联合分布列用表格给出（$x$ 横轴、$y$ 纵轴，空格为 $0$）：

| $y \backslash x$ | $1$ | $2$ | $3$ | $4$ |
| --- | --- | --- | --- | --- |
| $4$ | $1/20$ | $2/20$ | $2/20$ | $0$ |
| $3$ | $2/20$ | $4/20$ | $1/20$ | $2/20$ |
| $2$ | $0$ | $1/20$ | $3/20$ | $1/20$ |
| $1$ | $0$ | $1/20$ | $0$ | $0$ |

#### B. 联合分布列的定义（定义 3.3）

> [!IMPORTANT] 定义 3.3（离散型随机向量）
> 如果 $X_1, X_2, \ldots, X_n$ 都是离散型随机变量，则称 $\mathbf{X} = (X_1, X_2, \ldots, X_n)$ 为**离散型随机向量**。如果 $\mathbf{X}$ 所有的不同取值是
>
> $$
> \mathbf{x}(j_1, j_2, \ldots, j_n) = \big(x_1(j_1), x_2(j_2), \ldots, x_n(j_n)\big), \quad j_1, j_2, \ldots, j_n \ge 1,
> $$
>
> 则称
>
> $$
> p_{j_1, j_2, \ldots, j_n} = \mathbb{P}\big(\mathbf{X} = \mathbf{x}(j_1, j_2, \ldots, j_n)\big), \quad j_1, j_2, \ldots, j_n \ge 1
> $$
>
> 是 $\mathbf{X}$ 的**联合分布列**。

**直觉**：把一维分布列的"取值 $\to$ 概率"对应表升维：每个**取值组合**对应一个概率。

**概率分布的性质**：
1. $p_{j_1, j_2, \ldots, j_n} \ge 0$；
2. $\displaystyle\sum_{j_1, j_2, \ldots, j_n} p_{j_1, j_2, \ldots, j_n} = 1$。

#### 表格表达

如前面例子所示，当 $(X, Y)$ 的联合分布列的规律性不强时，还可以用表格的形式表达：行标 $x_1, x_2, \ldots$、列标 $y_1, y_2, \ldots, y_n$，表内填 $p_{ij}$；其中 $p_i$ 是其所在**行**中 $p_{ij}$ 的和，$q_j$ 是其所在**列**的和，总和 $\Sigma = 1$。则易见 $\{p_i\}, \{q_j\}$ 分别为 $X, Y$ 的概率分布列（PMF）。

#### C. 边缘分布列（定义 3.4）

> [!IMPORTANT] 定义 3.4（边缘分布列）
> 设离散型随机向量 $\mathbf{X}$ 的联合分布列为 $p_{j_1, j_2, \ldots, j_n}$，则称（对其余坐标求和）
>
> $$
> \mathbb{P}\big(X_1 = x_1(j_1), X_2 = x_2(j_2), \ldots, X_k = x_k(j_k)\big) = \sum_{j_{k+1}, j_{k+2}, \ldots, j_n} p_{j_1, j_2, \ldots, j_n}, \quad j_1, j_2, \ldots, j_k \ge 1
> $$
>
> 为 $\mathbf{X}$ 的**边缘分布列**。

**直觉**：只关心前 $k$ 个分量时，把不关心的分量的所有可能"求和消掉"（marginalize out）——表格中即"行加"或"列加"。

**例（续骰子例）**：联合（边缘）分布列与联合（边缘）分布函数都可以由表格经**简单加减运算**得到。行、列求和得边缘分布列（注：此步补全了课件图中的求和结果）：

| $x$ | $1$ | $2$ | $3$ | $4$ |
| --- | --- | --- | --- | --- |
| $\mathbb{P}(X = x)$ | $3/20$ | $8/20$ | $6/20$ | $3/20$ |

| $y$ | $1$ | $2$ | $3$ | $4$ |
| --- | --- | --- | --- | --- |
| $\mathbb{P}(Y = y)$ | $1/20$ | $5/20$ | $9/20$ | $5/20$ |

---

### 3.3 随机向量 CDF 的功能（例 3.1）

> [!EXAMPLE]- 例题 3.1：矩形区域的概率与边缘分布函数
> 设 $F(x, y)$ 是 $(X, Y)$ 的联合分布，则对矩形 $D = \{a < x \le b,\ c < y \le d\}$，求 $\mathbb{P}((X,Y) \in D)$。
>
> **解**
>
> 用容斥（差分）思想：从左下方大矩形 $F(b,d)$ 中去掉左侧条带与下侧条带，下侧与左侧的公共部分被减了两次需要补回一次（课件第 49 页用骰子表格上色块直观演示了该"简单加减运算"）：
>
> $$
> \mathbb{P}\big((X,Y) \in D\big) = \mathbb{P}(a < X \le b,\ c < Y \le d) = F(b,d) - F(b,c) - F(a,d) + F(a,c).
> $$
>
> 因此联合分布函数必须满足
>
> $$
> F(b,d) - F(b,c) - F(a,d) + F(a,c) \ge 0, \quad \forall\, a < b,\ c < d.
> $$
>
> 进一步，令另一个变元趋于 $\infty$，$X$、$Y$ 各自有概率分布函数（边缘分布函数）：
>
> $$
> F_X(x) = \mathbb{P}(X \le x,\ Y \le \infty) = F(x, \infty), \quad F_Y(y) = \mathbb{P}(X \le \infty,\ Y \le y) = F(\infty, y).
> $$

> [!WARNING] 易错
> 二维情形下"$F$ 单调非降 + 右连续 + 规范性"还**不够**刻画联合分布函数，必须再加上上面的矩形不等式 $F(b,d) - F(b,c) - F(a,d) + F(a,c) \ge 0$；一维的 $\mathbb{P}(a < X \le b) = F(b) - F(a)$ 在二维变成了四项交错加减。

---

### 3.4 随机向量的边缘分布（定义 3.5）

更一般地，我们定义：

> [!IMPORTANT] 定义 3.5（边缘分布、边际分布 marginal distribution）
> 对 $1 \le k < n$，$S_k = \{i_1, i_2, \ldots, i_k\}$ 为指标集，称 $\mathbf{X}_{S_k} = (X_{i_1}, X_{i_2}, \ldots, X_{i_k})$ 的联合分布
>
> $$
> \begin{align}
> F_k(x_{i_1}, x_{i_2}, \ldots, x_{i_k}) &= \mathbb{P}\big(X_{i_1} \le x_{i_1},\ X_{i_2} \le x_{i_2},\ \ldots,\ X_{i_k} \le x_{i_k}\big) \\
> &= \mathbb{P}\big(X_j \le x_j,\ j \in S_k;\ X_t \le \infty,\ t \in S_k^c\big)
> \end{align}
> $$
>
> 为 $F(x_1, x_2, \ldots, x_n)$ 的 **$k$-维边缘分布**。

**直觉**：把不关心的那些坐标的上限放到 $+\infty$（即"不设限制"），剩下的就是子向量自己的分布。

> [!NOTE] 备注
> - $F(x_1, x_2, \ldots, x_n)$ 一共有 $(2^n - 2)$ 个边缘分布（非空真子集的个数）。
> - 边缘分布可以由联合分布**唯一决定**；反之**不行**：已知边缘 $F_X(x)$ 和 $F_Y(y)$，可以得到联合分布 $F_{X,Y}(x,y)$ 吗？——**不可以**。

> [!WARNING] 辨析
> **联合 $\Rightarrow$ 边缘，但边缘 $\nRightarrow$ 联合**。联合分布是"全面"信息，边缘分布是"片面"信息：不同的联合分布可以有完全相同的边缘分布（差别在于分量间的相依结构）。只有在**独立**这一额外假设下，边缘才能拼出联合（$F = \prod F_i$）。

---

### 3.5 随机向量的独立性

**独立性定义回顾**：

> [!IMPORTANT] 定义（随机变量的相互独立性）
> 设 $X_1, \ldots, X_n$ 是 $(\Omega, \mathcal{F})$ 上的随机变量，如果对任意的实数 $x_1, \ldots, x_n$ 都有
>
> $$
> \mathbb{P}(X_1 \le x_1, \ldots, X_n \le x_n) = \mathbb{P}(X_1 \le x_1) \cdots \mathbb{P}(X_n \le x_n),
> $$
>
> 称随机变量 $X_1, \ldots, X_n$ 相互独立。

**等价表达**：设 $X_1, \ldots, X_n$ 有联合分布 $F(x_1, x_2, \ldots, x_n)$，$X_i$ 有边缘分布 $F_i(x_i)$。则 $X_1, \ldots, X_n$ 相互独立**当且仅当**

$$
F(x_1, x_2, \ldots, x_n) = F_1(x_1) F_2(x_2) \cdots F_n(x_n).
$$

**直觉**：独立 = 联合分布函数处处可以拆成边缘的乘积，分量之间互不传递信息。

#### D. 离散型随机向量的独立性（定理 3.1）

> [!IMPORTANT] 定理 3.1
> 设离散型随机向量 $\mathbf{X} = (X_1, X_2, \ldots, X_n)$ 有概率分布
>
> $$
> p_{j_1, j_2, \ldots, j_n} = \mathbb{P}\big(\mathbf{X} = \mathbf{x}(j_1, j_2, \ldots, j_n)\big), \quad j_1, j_2, \ldots, j_n \ge 1.
> $$
>
> 则 $X_1, \ldots, X_n$ 相互独立的充分必要条件是：对任意的 $\big(x_1(j_1), x_2(j_2), \ldots, x_n(j_n)\big)$，有
>
> $$
> \mathbb{P}\big(X_1 = x_1(j_1), \ldots, X_n = x_n(j_n)\big) = \prod_{i=1}^{n} \mathbb{P}\big(X_i = x_i(j_i)\big).
> $$

**直觉**：离散场合判独立不用碰 CDF，直接逐格检查"联合分布列 = 边缘分布列的乘积"即可——表格里每个格子都等于所在行和乘列和。

> [!IMPORTANT] 推论 3.1（二维情形）
> 设离散型随机向量 $(X, Y)$ 的所有不同取值是 $(x_i, y_j),\ i, j \ge 1$。则 $X, Y$ 相互独立的充分必要条件是：对任意的 $(x_i, y_j)$，有
>
> $$
> \mathbb{P}(X = x_i,\ Y = y_j) = \mathbb{P}(X = x_i)\,\mathbb{P}(Y = y_j).
> $$

**证明**：

($\Leftarrow$) 对任意的 $x, y \in \mathbb{R}$，利用概率的可列可加性得

$$
\begin{align}
\mathbb{P}(X \le x,\ Y \le y) &= \mathbb{P}\left(\bigcup_{i:\, x_i \le x} \{X = x_i\},\ \bigcup_{j:\, y_j \le y} \{Y = y_j\}\right) \\
&= \sum_{i:\, x_i \le x} \sum_{j:\, y_j \le y} \mathbb{P}(X = x_i,\ Y = y_j) \\
&= \sum_{i:\, x_i \le x} \sum_{j:\, y_j \le y} \mathbb{P}(X = x_i)\,\mathbb{P}(Y = y_j) \\
&= \sum_{i:\, x_i \le x} \mathbb{P}(X = x_i) \sum_{j:\, y_j \le y} \mathbb{P}(Y = y_j) \\
&= \mathbb{P}(X \le x)\,\mathbb{P}(Y \le y),
\end{align}
$$

即按定义 $X$ 与 $Y$ 独立。

($\Rightarrow$) 由于 $A = \{x_i\}$ 和 $B = \{y_j\}$ 都是 Borel 集，故 $\{X = x_i\} = \{X \in A\}$ 与 $\{Y = y_j\} = \{Y \in B\}$ 独立（利用了 Lecture3 handout p37 定理 2.1 的结论：由 CDF 意义下的独立可推出对一切 Borel 集 $A, B$，事件 $\{X \in A\}$ 与 $\{Y \in B\}$ 独立），因此

$$
\mathbb{P}(X = x_i,\ Y = y_j) = \mathbb{P}(X = x_i)\,\mathbb{P}(Y = y_j). \qquad \square
$$

> [!NOTE] 备注
> **思考题**：如果不利用 Lecture3 定理 2.1，可以如何证明（$\Rightarrow$）方向？

#### E. 经典离散型随机向量例：多项分布（例 3.2）

> [!EXAMPLE]- 例题 3.2：多项分布及其边缘分布
> 设 $A_1, A_2, \ldots, A_r$ 是试验 $S$ 的完备事件组。对试验 $S$ 进行 $n$ 次独立重复试验时，用 $X_i$ 表示 $A_i$ 发生的次数。求 $(X_1, \ldots, X_r)$ 的概率分布及边缘分布。
>
> **解**
>
> 记 $p_i = \mathbb{P}(A_i)$。（用归纳法可得）$(X_1, \ldots, X_r)$ 的概率分布是
>
> $$
> \mathbb{P}(X_1 = k_1, \ldots, X_r = k_r) = \frac{n!}{k_1! \cdots k_r!}\, p_1^{k_1} \cdots p_r^{k_r},
> $$
>
> 其中 $k_i \ge 0$，$\sum_{i=1}^{r} k_i = n$（完备事件组保证每次试验恰有一个 $A_i$ 发生，$n$ 次结果按类别计数；系数是多项式系数，即把 $n$ 次试验分组到 $r$ 个类别的方式数）。这就是**多项分布**。
>
> **边缘分布**：对 $1 \le m < r$，$(X_{j_1}, X_{j_2}, \ldots, X_{j_m})$ 的边缘分布为
>
> $$
> \mathbb{P}(X_{j_1} = k_1, \ldots, X_{j_m} = k_m) = \frac{n!}{k_1! \cdots k_m!\, k!}\, p_{j_1}^{k_1} \cdots p_{j_m}^{k_m}\, q^{k},
> $$
>
> 其中 $0 \le k_i \le n$，$k = n - \sum_{i=1}^{m} k_i \ge 0$，$q = 1 - \sum_{i=1}^{m} p_{j_i}$。
>
> （注：此步补全了直觉——把不关心的 $r - m$ 个类别**合并**成一个"其他"类别，它发生的概率是 $q$、次数是 $k$，于是 $m+1$ 个类别仍构成多项分布。）
>
> **特别地**（$m = 1$），单个分量服从二项分布：
>
> $$
> \mathbb{P}(X_j = k) = \binom{n}{k} p_j^{k} (1 - p_j)^{n-k}, \quad k \ge 0,
> $$
>
> 即 $X_j \sim B(n, p_j)$——只区分"$A_j$ 发生 / 不发生"，自然是二项。

---

## 四、小结（课件知识结构）

**知识点**
- 分布函数（CDF，统一性）、分布函数与 PMF/PDF 的关系；
- 随机变量函数的分布：
	- 曲线救国法：由 CDF 得 PMF/PDF；
	- 直接求解法：由 PDF 和 $g(X)$ 直接得 PMF/PDF（线性变换、单调、多支公式）；
- 随机向量：
	- 核心知识：联合分布、边缘分布、独立性的判定；
	- 经典例：离散型——多项分布（连续型的多元正态分布下一讲）。

**技巧**
- 利用变量间的关系，便捷求解随机变量函数的分布，例如求导法；
- 识别分布（PMF/PDF）的核心部分，根据归一化原则确认 PMF/PDF 的完整表达式。

---

## 五、附录（选修内容）

### 5.1 定理 1.3 中数集 $A$ 限制条件的必要性（不要求，略）

举例说明定理 1.3 中关于数集 $A$ 的限制条件（任两点距离大于正数 $\delta$）是有必要的。（不要求，略）

### 5.2 奇异分布函数（singular function）（不要求，略）

A function $F$ is called **singular** if and only if it is continuous, not identically zero, $F'$ exists almost everywhere (a.e.), and $F'(t) = 0$ a.e.（不要求，略）

### 5.3 Cantor 集上的均匀分布（不要求，略）

在 Cantor 集（从 $[0,1]$ 反复挖去每段中间 $1/3$ 所得）上定义的分布函数：$F$ 在每个被挖去的区间上取常数（$\frac{1}{2}, \frac{1}{4}, \frac{3}{4}, \ldots$），可证 $F$ 单调不减、**连续**、$F(-\infty)=0$、$F(\infty)=1$，是一个 CDF；但除 Cantor 集（零测集）外 $F'(x) = 0$，故它没有密度，是 Lebesgue 奇异函数（"Lebesgue's singular function"）——这正是"$F$ 连续 $\ne$ 连续型随机变量"的标准反例。（不要求，略）

---

## 本讲方法/题型清单

- 已知 PMF 求 CDF → 累加 → $F(x) = \sum_{j: x_j \le x} p_j$，画成右连续阶梯函数；反向由 CDF 读 PMF → 取跳跃高度 $p = F(x) - F(x^-)$。
- 求一般正态概率 $\mathbb{P}(X \le a)$ → 标准化 + 查表 → 写成 $\Phi\big(\frac{a-\mu}{\sigma}\big)$，对称区间用 $2\Phi(\cdot) - 1$（$3\sigma$/$6\sigma$ 数值要记：$68.27\%$、$95.45\%$、$99.73\%$）。
- 判断随机变量类型 → 看 CDF 形态 → 阶梯（可写成 $\sum p_k H(x - x_k)$）为离散；有跳跃必非连续型；连续且分段可导用定理 1.3 取 $f = F'$ 得密度（个别点补 $0$ 不影响）。
- 由分段可导的连续 $F$ 求密度 → 定理 1.3 → 在不可导点集 $A$ 外取 $F'$，$A$ 上取 $0$，再验证 $\int f = 1$。
- 求离散型 $Y = g(X)$ 的分布 → 枚举合并 → 列出 $Y$ 的所有取值，把映到同一 $y$ 的 $x$ 概率相加。
- 求连续型 $Y = g(X)$ 的分布（一般法）→ CDF 两步法 → 先 $F_Y(y) = \mathbb{P}(g(X) \le y)$ 化为 $X$ 的区域概率，再求导得 $f_Y$。
- $Y = aX + b$ 线性变换 → 直接公式 → $f_Y(y) = \frac{1}{|a|} f_X\big(\frac{y-b}{a}\big)$；正态的线性变换仍正态。
- $g$ 严格单调 → 反函数公式 → $f_Y(y) = f_X(h(y))\,|h'(y)|$，$h = g^{-1}$。
- $g$ 非单调（如 $r\cos x$、$x^2$）→ 定理 2.1 多支求和 → 找出全部反函数支 $h_i$，$f_Y(y) = \sum_i f(h_i(y))|h_i'(y)|$；或退回 CDF 两步法。
- 给联合分布列表格求边缘 → 行/列求和 → 行和是 $X$ 的 PMF，列和是 $Y$ 的 PMF。
- 求 $(X,Y)$ 落入矩形的概率 → 联合 CDF 容斥 → $F(b,d) - F(b,c) - F(a,d) + F(a,c)$。
- 由联合 CDF 求边缘 CDF → 放掉一个变元 → $F_X(x) = F(x, \infty)$。
- 判定离散随机变量独立 → 定理 3.1/推论 3.1 → 逐格检查 $p_{ij} = p_i \cdot q_j$（每格 = 行和 × 列和），有一格不等即不独立。
- 完备事件组 $n$ 次独立重复计数 → 多项分布 → 联合 PMF 用多项系数；求边缘把其余类别合并为"其他"，单分量是 $B(n, p_j)$。
