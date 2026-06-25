---
title: "Lecture04 常见随机变量"
tags:
  - 概率论
  - 前半学期
  - 常见分布
  - 离散分布
  - 连续分布
---

# Lecture04 常见随机变量

> [!ABSTRACT] 本讲概要
> 把握一个随机变量，最直接的方式就是写出它的分布。本讲把实际中最常见的随机变量"建档立卡"：离散型用分布列（PMF）刻画，连续型用密度函数（PDF）刻画，并通过实际情景（重复试验、等待时间、抽样检验、计数过程、测量误差）理解各分布的来源与相互关系。
>
> 参考教材：Bertsekas & Tsitsiklis Ch2 2.1–2.2, Ch3 3.1, 3.3。
>
> ---

## 一、离散型随机变量与分布列

### 1.1 离散型随机变量（定义）

如果随机变量 $X$ 只取有限个值 $x_1, \ldots, x_m$ 或者可列个值 $x_1, x_2, \ldots$，则称 $X$ 是**离散型随机变量**（discrete random variable），简称离散随机变量。

**直觉**：离散随机变量的所有可能取值能"一个一个数出来"，比如计数类的量（次数、个数、人数）。

### 1.2 概率分布与分布列（定义）

设 $X$ 为离散型随机变量，称

$$
\mathbb{P}(X = x_k) = p_k, \quad k \geq 1
$$

为 $X$ 的**概率分布**，称 $\{p_k\}$ 是**概率分布列**，简称为**分布列**（Probability mass function, PMF）。

**直觉**：分布列就是把每个可能取值"分到多少概率"逐一列出来，全部信息都在这张清单里。

当分布列 $p_k$ 的规律性不够明显时，概率分布常写成表格：

| $X$ | $x_1$ | $x_2$ | $x_3$ | $\cdots$ |
| --- | --- | --- | --- | --- |
| $\mathbb{P}$ | $p_1$ | $p_2$ | $p_3$ | $\cdots$ |

分布列 $\{p_k\}$ 满足以下性质：

| 性质 | 公式 |
| --- | --- |
| 非负性 | $p_k \geq 0$ |
| 归一性 | $\displaystyle\sum_{k=1}^{\infty} p_k = 1$ |

---

## 二、常见离散型分布

### 2.1 两点分布 $B(1,p)$（定义，常用）

任何试验，当只考虑成功（质量合格、健康状态、政治态度、电话机待机状态等）与否时，就可以用如下随机变量描述：

$$
X = \begin{cases} 1, & \text{试验成功}, \\ 0, & \text{试验不成功}. \end{cases}
$$

> [!IMPORTANT] 定义：Bernoulli 分布（两点分布）
> 如果 $X$ 只取值 $0$ 或 $1$，概率分布是 $\mathbb{P}(X=1) = p = 1 - \mathbb{P}(X=0)$，则称 $X$ 服从**两点分布（Bernoulli 分布）**，记作 $X \sim B(1,p)$ 或 $X \sim B(p)$。其分布列为：
>
> | $X$ | $0$ | $1$ |
> | --- | --- | --- |
> | $\mathbb{P}$ | $1-p$ | $p$ |

**直觉**：一次"是/否"试验的数学模型，是构造一切重复试验类分布的基本砖块。

### 2.2 二项分布 $B(n,p)$（常用）

#### 2.2.1 从 $n$ 重独立试验推导

设试验 $S$ 成功的概率为 $p$，将试验 $S$ 重复 $n$ 次，用 $X$ 表示成功的次数，求 $\mathbb{P}(X=k)$。

**解**：用 $A_j$ 表示第 $j$ 次试验成功，则 $A_1, A_2, \ldots, A_n$ 相互独立，且 $\mathbb{P}(A_j) = p$。从 $n$ 次试验中选定 $k$ 次试验的方法共有 $\binom{n}{k}$ 种。对第 $i$ 种取法，设其对应着 $j_1, j_2, \ldots, j_k$，用

$$
B_i = A_{j_1} \cap A_{j_2} \cap \cdots \cap A_{j_k} \cap A_{j_{k+1}}^c \cap \cdots \cap A_{j_n}^c
$$

表示第 $j_1, j_2, \ldots, j_k$ 次试验成功、其余不成功，则诸 $B_i$ 互不相容，并且

$$
\{X = k\} = \bigcup_{i=1}^{\binom{n}{k}} B_i, \quad \mathbb{P}(B_i) = p^k (1-p)^{n-k}.
$$

利用概率的有限可加性，可得

$$
\mathbb{P}(X = k) = \sum_{i=1}^{\binom{n}{k}} \mathbb{P}(B_i) = \binom{n}{k} p^k (1-p)^{n-k}.
$$

**发现**：$\binom{n}{k} p^k (1-p)^{n-k}$ 恰为二项展开式

$$
1 = \left(p + (1-p)\right)^n = \sum_{k=0}^{n} \binom{n}{k} p^k (1-p)^{n-k}
$$

的第 $k+1$ 项——这正是"二项分布"名字的来源，也顺带验证了归一性。

#### 2.2.2 定义与可加性

> [!IMPORTANT] 定义：Binomial 分布
> 如果随机变量 $X$ 的概率分布如下：
>
> $$
> \mathbb{P}(X = k) = \binom{n}{k} p^k (1-p)^{n-k}, \quad k = 0, 1, \ldots, n,
> $$
>
> 则称 $X$ 服从**二项分布**，其中 $p \in (0,1)$，记作 $X \sim B(n,p)$。$B$ 是 Binomial 的首字母。

**直觉**：$n$ 次独立的"是/否"试验中成功的总次数。

两条重要的可加性结论（了解推导，结论常用）：

- 如果随机变量 $X_1, \ldots, X_n$ 相互独立，都服从两点分布 $B(1,p)$，则 $S = X_1 + \cdots + X_n \sim B(n,p)$。
- 如果随机变量 $X, Y$ 相互独立，且 $X \sim B(n,p)$，$Y \sim B(m,p)$，则 $X + Y \sim B(m+n, p)$。

**证明思路**：$n$ 次试验加 $m$ 次试验，合起来就是 $n+m$ 次独立试验，成功概率不变；按情景直接理解即可（用母函数也可严格证明）。

#### 2.2.3 二项分布的单调性与中心项

课件展示了 $p = 0.5,\ 0.2,\ 0.8$ 三组二项分布折线图（$n = 3, 6, 9, 12, 15, 18/30$）：$p=0.5$ 时图形对称；$p=0.2$ 时峰偏左；$p=0.8$ 时峰偏右；随 $n$ 增大峰位置右移、图形渐趋"钟形"。

令 $b(k,n,p) = \mathbb{P}(X=k)$，则相邻两项之比为

$$
\frac{b(k,n,p)}{b(k-1,n,p)} = \frac{(n-k+1)p}{k(1-p)} = 1 + \frac{(n+1)p - k}{k(1-p)}.
$$

故：
1. 当 $k < (n+1)p$ 时，$b(k,n,p) > b(k-1,n,p)$，此时后项大于前项，$b(k,n,p)$ 随 $k$ 的增大而增大；
2. 当 $k > (n+1)p$ 时，$b(k,n,p) < b(k-1,n,p)$，此时后项小于前项，$b(k,n,p)$ 随 $k$ 的增大而减小；
3. 当 $k = (n+1)p$ 时，$b(k,n,p) = b(k-1,n,p)$，此时 $b((n+1)p, n, p)$ 与 $b((n+1)p - 1, n, p)$ 两项相等且为最大。

> [!IMPORTANT] 定理 1.1（二项分布的最大可能值）
> 二项分布的最大可能值 $k_0$ 存在，即满足
>
> $$
> b(k_0, n, p) = \max_{0 \leq k \leq n} b(k,n,p)
> $$
>
> 的整数 $k_0$ 存在，且
>
> $$
> k_0 = \begin{cases} (n+1)p \ \text{与}\ (n+1)p - 1, & \text{如果}\ (n+1)p\ \text{为整数}, \\ \lfloor (n+1)p \rfloor, & \text{如果}\ (n+1)p\ \text{不是整数}. \end{cases}
> $$
>
> 即，(a) 当 $(n+1)p$ 为整数时，$b((n+1)p, n, p)$ 与 $b((n+1)p - 1, n, p)$ 均为最大项；(b) 当 $(n+1)p$ 不为整数时，$b(\lfloor (n+1)p \rfloor, n, p)$ 为唯一的最大项。

一般称 $b(k_0, n, p)$ 为二项分布的**中心项**。

**直觉**：相邻项之比从大于 1 变到小于 1，分布列先增后减，峰就在 $(n+1)p$ 附近——最可能的成功次数约为 $np$。

> [!EXAMPLE]- 例题 1：连打 9 枪的命中问题
> 一个人向同一目标连打 9 枪，如果每次射击是相互独立的且每次射击击中的概率均为 0.3，求有两次以上击中目标的概率以及最可能击中目标的次数。
>
> **解**：设 $X$ 为击中目标的次数，则 $X \sim B(9, 0.3)$。所求概率为
>
> $$
> \begin{align}
> \mathbb{P}(X > 2) &= \sum_{k=3}^{9} \binom{9}{k} (0.3)^k (1-0.3)^{9-k} \\
> &= 1 - \sum_{k=0}^{2} \binom{9}{k} (0.3)^k (1-0.3)^{9-k}.
> \end{align}
> $$
>
> 逐项计算（注：此步补全了三项的具体数值计算）：
>
> $$
> \begin{align}
> k=0: &\quad (0.7)^9 \approx 0.0404, \\
> k=1: &\quad 9 \times 0.3 \times (0.7)^8 \approx 0.1556, \\
> k=2: &\quad 36 \times (0.3)^2 \times (0.7)^7 \approx 0.2668.
> \end{align}
> $$
>
> 三项之和约为 $0.4628$（课件取 $0.4624$，为舍入差异），于是
>
> $$
> \mathbb{P}(X > 2) = 1 - 0.4624 = 0.5376.
> $$
>
> 又因为 $(n+1)p = 10 \times 0.3 = 3$ 为整数，由定理 1.1，最可能击中目标的次数是 $3$ 或者 $2$（两者概率相等且最大）。

### 2.3 几何分布 $G(p)$（常用）

> [!EXAMPLE]- 例题 2：首次击中的射击次数（几何分布的引出）
> 甲向一个目标射击，直到击中为止。用 $X$ 表示首次击中目标时的射击次数。如果甲每次击中的概率是 $p > 0$，求 $\mathbb{P}(X = k)$。
>
> **解**：用 $A_j$ 表示甲第 $j$ 次没击中目标，由 $\{A_j\}$ 的独立性知
>
> $$
> \mathbb{P}(X = k) = \mathbb{P}(A_1 \cap \cdots \cap A_{k-1} \cap A_k^c) = (1-p)^{k-1} p, \quad k = 1, 2, \ldots
> $$
>
> 注意到
>
> $$
> \mathbb{P}(X < \infty) = \sum_{k=1}^{\infty} (1-p)^{k-1} p = p \cdot \frac{1}{1 - (1-p)} = 1
> $$
>
> （注：此步补全了等比级数求和），可知甲一直射击下去总有击中目标的时候。这相当于独立重复试验一直做下去，总有成功的时候。

> [!IMPORTANT] 定义：Geometric 分布
> 如果随机变量 $X$ 的概率分布如下：
>
> $$
> \mathbb{P}(X = k) = (1-p)^{k-1} p, \quad k = 1, 2, \ldots,
> $$
>
> 则称 $X$ 服从参数为 $p$ 的**几何分布**，记作 $X \sim G(p)$。

**直觉**：独立重复试验中"等到第一次成功"所需的总试验次数。名字来源：分布列各项构成**几何级数**（等比数列）。

#### 几何分布的无记忆性

> [!IMPORTANT] 定理 1.2（几何分布 $\Longleftrightarrow$ 无记忆性）
> 取正整数值的随机变量 $X \sim G(p)$ 的充要条件是 $X$ 有**无记忆性**，即对每个 $k \geq 1$，
>
> $$
> \mathbb{P}(X = k+1 \mid X > k) = \mathbb{P}(X = 1).
> $$

**直觉**：已经失败了 $k$ 次，"接下来一次就成功"的概率与从头开始时完全一样——过去的失败不积累任何信息。

**证明**：

($\Longrightarrow$) 由条件概率公式得

$$
\begin{align}
\mathbb{P}(X = k+1 \mid X > k) &= \frac{\mathbb{P}(X = k+1,\ X > k)}{\mathbb{P}(X > k)} = \frac{\mathbb{P}(X = k+1)}{\mathbb{P}\left(\bigcup_{j=k+1}^{\infty} \{X = j\}\right)} \\
&= \frac{(1-p)^k p}{\sum_{j=k+1}^{\infty} (1-p)^{j-1} p} = \frac{(1-p)^k p}{(1-p)^k} = p = \mathbb{P}(X = 1).
\end{align}
$$

（注：此步补全了分母的求和：$\sum_{j=k+1}^{\infty} (1-p)^{j-1} p = (1-p)^k p \cdot \frac{1}{1-(1-p)} = (1-p)^k$。）

($\Longleftarrow$) 设 $r_k = \mathbb{P}(X > k)$，利用 $\{X = k+1\} = \{X > k\} \setminus \{X > k+1\}$，得

$$
p = \mathbb{P}(X = k+1 \mid X > k) = \frac{\mathbb{P}(X > k) - \mathbb{P}(X > k+1)}{\mathbb{P}(X > k)} = 1 - \frac{r_{k+1}}{r_k}.
$$

利用 $r_0 = \mathbb{P}(X > 0) = 1$，可得

$$
r_{k+1} = (1-p) r_k = (1-p)^2 r_{k-1} = \cdots = (1-p)^{k+1} r_0 = (1-p)^{k+1}.
$$

因此

$$
\mathbb{P}(X = k) = \mathbb{P}(X > k-1) - \mathbb{P}(X > k) = r_{k-1} - r_k = (1-p)^{k-1} p. \qquad \blacksquare
$$

### 2.4 帕斯卡分布（了解即可）

> [!EXAMPLE]- 例题 3：击中 r 次为止的射击次数（Pascal 分布的引出）
> 甲向一个目标射击，直到击中 $r$ 次为止。用 $X$ 表示射击停止时的射击次数。如果甲每次击中的概率是 $p \in (0,1)$，求 $\mathbb{P}(X = k)$。
>
> **解**（注：此步补全了课件略去的推导）：事件 $\{X = k\}$ 等价于"第 $k$ 次射击击中，且前 $k-1$ 次射击中恰有 $r-1$ 次击中"。前 $k-1$ 次中选出 $r-1$ 次击中的方式有 $\binom{k-1}{r-1}$ 种，每种方式的概率为 $p^{r-1}(1-p)^{k-r}$，再乘上第 $k$ 次击中的概率 $p$，得
>
> $$
> \mathbb{P}(X = k) = \binom{k-1}{r-1} (1-p)^{k-r} p^r, \quad k = r, r+1, \ldots
> $$

> [!IMPORTANT] 定义：Pascal 分布
> 如果随机变量 $X$ 的概率分布如下：
>
> $$
> \mathbb{P}(X = k) = \binom{k-1}{r-1} (1-p)^{k-r} p^r, \quad k = r, r+1, \ldots,
> $$
>
> 则称 $X$ 服从**帕斯卡分布**。

**直觉**：等到第 $r$ 次成功为止的总试验次数。当 $r = 1$ 时，帕斯卡分布就是几何分布。

### 2.5 负二项分布 $\text{NB}(r,p)$（了解即可）

在上述例 3 中，令 $Y = X - r$，则 $Y$ 是射击停止时，射击**失败**的次数。

> [!IMPORTANT] 定义：负二项分布
> 如果随机变量 $Y$ 的概率分布如下：
>
> $$
> \mathbb{P}(Y = k) = \binom{k+r-1}{r-1} (1-p)^k p^r, \quad k = 0, 1, \ldots, \tag{1}
> $$
>
> 则称 $Y$ 服从**负二项分布**，记作 $Y \sim \text{NB}(r,p)$。

**直觉**：与帕斯卡分布只差一个平移——帕斯卡数"总次数"，负二项数"失败次数"。

**名称来源 (a)：负指数二项展开式。** 由

$$
\begin{align}
(1-x)^{-r} &= \sum_{k=0}^{\infty} \frac{(-r)(-r-1)\cdots(-r-k+1)}{k!} (-x)^k \\
&= \sum_{k=0}^{\infty} \frac{(r+k-1)(r+k-2)\cdots(r+1)r}{k!} x^k \\
&= \sum_{k=0}^{\infty} \binom{k+r-1}{r-1} x^k, \quad |x| < 1.
\end{align}
$$

令 $x = 1-p$ 并两边乘以 $p^r$，得

$$
1 = p^r \left(1 - (1-p)\right)^{-r} = \sum_{k=0}^{\infty} \binom{k+r-1}{r-1} (1-p)^k p^r.
$$

这验证了 $(1)$ 确实是分布列——分布列来自"负指数"的二项展开，故名负二项分布。

**名称来源 (b)：试验方式不同。** 与二项分布是"反其道而行之"：二项分布是定下总抽样个数 $n$ 而把废品个数 $X$ 作为随机变量；负二项分布则相反，它定下废品个数 $r$ 而把总抽样次数减去 $r$ 作为随机变量。

> [!EXAMPLE]- 例题 4：检查废品率的两种试验方案
> 为了检查某厂产品的废品率 $p$ 大小，有两个试验方案可采取：
>
> **方案一**：从该厂产品中有放回地抽取若干个，检查其中的废品数 $X$，这一方案导致**二项分布**。
>
> **方案二**：先指定一个自然数 $r$，一个一个有放回地从该厂产品中抽样调查，直到发现第 $r$ 个废品为止。以 $X$ 记到当时为止已检出的**合格品**个数，则 $X \sim \text{NB}(r, p)$（注：此结论补全了——每次抽到废品的概率为 $p$，"成功"即抽到废品，合格品数就是失败次数）。
>
> 显然，若废品率 $p$ 小，则 $X$ 倾向于取较大的值；反之，则 $X$ 倾向于取小值。故 $X$ 可用于研究 $p$ 的目的。

> [!WARNING] 辨析：几何 / 帕斯卡 / 负二项
> - 几何分布 $G(p)$：等第 $1$ 次成功的**总试验次数**，取值从 $k=1$ 起。
> - 帕斯卡分布：等第 $r$ 次成功的**总试验次数**，取值从 $k=r$ 起；$r=1$ 时即几何分布。
> - 负二项分布 $\text{NB}(r,p)$：等第 $r$ 次成功过程中的**失败次数**，取值从 $k=0$ 起；与帕斯卡分布相差平移 $r$。
> - 与二项分布的本质区别：二项分布**固定试验总数** $n$、成功数随机；负二项/帕斯卡**固定成功数** $r$、试验总数随机。

### 2.6 超几何分布 $H(n,M,N)$（了解即可）

**引例**：在包含 $N$ 个元素的总体中，$M$ 个是红的，$N-M$ 个是黑的。任意选取 $n$ 个元素组成一组，试求所取出的这一组中，恰有 $k$ 个红元素的概率。

> [!IMPORTANT] 定义：超几何分布
> 如果随机变量 $X$ 的概率分布如下：
>
> $$
> \mathbb{P}(X = k) = \frac{\binom{M}{k} \binom{N-M}{n-k}}{\binom{N}{n}}, \quad k = 0, 1, \ldots, \min\{n, M\},
> $$
>
> 则称 $X$ 服从**超几何分布**（Hypergeometric distribution），记作 $X \sim H(n, M, N)$。

**直觉**：**无放回**抽样下抽中"红球"个数的分布，分子是"选 $k$ 个红、$n-k$ 个黑"的方法数，分母是总方法数——古典概型的直接产物。

**应用**：质量检测；捕获-再捕获模型；……

> [!EXAMPLE]- 例题 5：次品抽检与有放回/无放回的差异
> $N$ 件产品中恰有 $M$ 件次品，从中任取 $n$ 件，用 $X$ 表示这 $n$ 件中的次品数，则 $X$ 服从超几何分布 $H(n,M,N)$。
>
> **讨论**：如果这批产品充分多，无放回的抽取和有放回的抽取的差异？
>
> **解**：有放回抽取时，$\tilde{X} \sim B(n, p_N)$，其中 $p_N = \frac{M}{N}$ 是次品率。实际上，当 $\lim_{N \to \infty} \frac{M}{N} = p$ 时，有
>
> $$
> \begin{align}
> \mathbb{P}(X = m) &= \frac{\binom{M}{m} \binom{N-M}{n-m}}{\binom{N}{n}} = \frac{M!}{m!(M-m)!} \cdot \frac{(N-M)!}{(n-m)!(N-M-n+m)!} \cdot \frac{n!(N-n)!}{N!} \\
> &= \binom{n}{m} \cdot \frac{M(M-1)\cdots(M-m+1)}{N^m} \times \frac{(N-M)\cdots(N-M-n+m+1)}{N^{n-m}} \\
> &\quad \times \frac{N^n}{N(N-1)\cdots(N-n+1)} \\
> &\longrightarrow \binom{n}{m} p^m (1-p)^{n-m} \quad (N \to \infty).
> \end{align}
> $$
>
> （注：最后一步补全说明——第一个分式中每个因子 $\frac{M-i}{N} \to p$，第二个分式中每个因子 $\frac{N-M-j}{N} \to 1-p$，第三个分式中每个因子 $\frac{N}{N-i} \to 1$，三部分极限相乘即得。）
>
> **结论**：总体充分大时，无放回抽样与有放回抽样几乎没有差异。

即，**超几何分布可以用二项分布近似**。在实际问题中，对于较大的 $N$，计算 $\binom{N}{n}, \binom{M}{m}, \binom{N-M}{n-m}$ 要比计算 $\binom{n}{m}$ 费时多了。因为抽样的个数 $n$ 一般不会很大，所以对较大的 $N$ 和 $M$，采用近似公式

$$
\frac{\binom{M}{m} \binom{N-M}{n-m}}{\binom{N}{n}} \approx \binom{n}{m} p_N^m (1 - p_N)^{n-m}
$$

往往会更方便。

### 2.7 负超几何分布 $NH(r,M,N)$（了解即可）

**引例**：在包含 $N$ 个元素的总体中，$M$ 个是红的，$N-M$ 个是黑的。每次无放回地抽取一个元素，直到抽到 $r$ 个红元素为止，求此时共抽取了 $k$ 个黑元素的概率。

> [!IMPORTANT] 定义：负超几何分布
> 如果随机变量 $X$ 的概率分布如下：
>
> $$
> \mathbb{P}(X = k) = \frac{\binom{k+r-1}{k} \binom{N-k-r}{M-r}}{\binom{N}{M}}, \quad k = 0, 1, \ldots, N - M,
> $$
>
> 则称 $X$ 服从**负超几何分布**（Negative Hypergeometric distribution），记作 $X \sim NH(r, M, N)$。

**直觉**：负超几何分布之于超几何分布，正如负二项分布之于二项分布——把"固定抽取总数"换成"固定抽到的红球数"，且抽样是无放回的。

**应用**：质量检测；捕获-再捕获模型；……

### 2.8 Poisson 分布 $\mathcal{P}(\lambda)$（常用）

> [!IMPORTANT] 定义：Poisson 分布
> 如果随机变量 $X$ 的概率分布如下：
>
> $$
> \mathbb{P}(X = k) = \frac{\lambda^k}{k!} e^{-\lambda}, \quad k = 0, 1, 2, \ldots,
> $$
>
> 则称 $X$ 服从参数为 $\lambda$ 的 **Poisson 分布**，记作 $X \sim \mathcal{P}(\lambda)$，其中 $\lambda$ 是正常数。

**直觉**：单位时间（或单位区域）内"稀有事件"发生总次数的分布，$\lambda$ 是平均发生次数（强度）。

**实际应用**：
1. 某段高速公路上一年内的交通事故数；
2. 某市场一天中到达的顾客次数；
3. 某办公室一天中收到的电话数；
4. 某大学一天中上课迟到的总人数；
5. ……

课件展示了 $\lambda = 1, \ldots, 6$ 的 Poisson 分布折线图：$\lambda$ 越大，峰越靠右、越平缓；$\lambda$ 较小时分布集中在 0 附近。课件提问：$\lambda$ 什么含义？为什么有这样的规律？——$\lambda$ 是平均发生次数，下面的例题与推导回答了这个问题。

> [!EXAMPLE]- 例题 6：Rutherford–Geiger 的 α 粒子观测（Poisson 分布的来源）
> 1910 年，著名科学家 Rutherford 和 Geiger 观察了放射性物质钋（Polonium）放射 $\alpha$ 粒子的情况。他们进行了 $N = 2608$ 次观测，每次观测 7.5 秒，一共观察到 10094 个 $\alpha$ 粒子放出。下表是观测记录，最后一列中的随机变量 $Y \sim \mathcal{P}(3.87)$，其中 $3.87 = 10094/2608$ 是 7.5 秒中放射出 $\alpha$ 粒子的**平均数**。用 $X$ 表示这块放射性钋在 7.5 秒放射出的 $\alpha$ 粒子数，下表的最后两列表明事件 $\{X = k\}$ 在 $N = 2608$ 次重复观测中发生的频率和 $\mathbb{P}(Y = k)$ 基本相同。
>
> | 观察到的 $\alpha$ 粒子数 $k$ | 观察到 $k$ 个粒子的次数 $m_k$ | 发生的频率 $m_k/N$ | $\mathbb{P}(Y=k)$ |
> | --- | --- | --- | --- |
> | 0 | 57 | 0.022 | 0.021 |
> | 1 | 203 | 0.078 | 0.081 |
> | 2 | 383 | 0.147 | 0.156 |
> | 3 | 525 | 0.201 | 0.201 |
> | 4 | 532 | 0.204 | 0.195 |
> | 5 | 408 | 0.156 | 0.151 |
> | 6 | 273 | 0.105 | 0.097 |
> | 7 | 139 | 0.053 | 0.054 |
> | 8 | 45 | 0.017 | 0.026 |
> | 9 | 27 | 0.010 | 0.011 |
> | 10+ | 16 | 0.006 | 0.007 |
> | 总计 | 2608 | 0.999 | 1.00 |
>
> **下面证明 $X \sim \mathcal{P}(\lambda)$。** 设想将 $t = 7.5$ 秒等分成 $n$ 段，每段是 $\delta_n = t/n$ 秒。对充分大的 $n$，假定：
> 1. 在 $\delta_n$ 内最多只有一个 $\alpha$ 粒子放出，并且放出一个粒子的概率是 $p_n = \mu \delta_n = \frac{\mu t}{n}$，这里 $\mu$ 是正常数；
> 2. 各个小时间段内是否放射出 $\alpha$ 粒子相互独立。
>
> 在上述假定下，这块放射性物质放射出的粒子数 $X \sim B(n, p_n)$。于是
>
> $$
> \begin{align}
> \mathbb{P}(X = k) &= \lim_{n \to \infty} \binom{n}{k} p_n^k (1 - p_n)^{n-k} \\
> &= \lim_{n \to \infty} \frac{(\mu t)^k}{k!} \cdot \frac{n(n-1)\cdots(n-k+1)}{n^k} \left(1 - \frac{\mu t}{n}\right)^{n-k} \\
> &= \frac{(\mu t)^k}{k!} e^{-\mu t}.
> \end{align}
> $$
>
> （注：最后一步补全说明——$\frac{n(n-1)\cdots(n-k+1)}{n^k} \to 1$；$\left(1 - \frac{\mu t}{n}\right)^{n} \to e^{-\mu t}$，用到 $\lim_{x \to 0}(1+x)^{1/x} = e$；而 $\left(1 - \frac{\mu t}{n}\right)^{-k} \to 1$。）
>
> 取 $\lambda = \mu t$，得 $X \sim \mathcal{P}(\lambda)$。课件还给出了频率 $m_k/N$ 与概率 $\mathbb{P}(Y=k)$ 的对比图，两条折线几乎重合。

> [!NOTE] 备注：二项分布的 Poisson 近似
> 上述例子中，我们验证了二项分布可以用 Poisson 分布近似的事实：如果 $n$ 很大，$p$ 很小，且 $np \approx \lambda$，其中 $\lambda$ 是大小适当的固定常数，则可用 $\mathcal{P}(\lambda)$ 近似二项分布 $B(n,p)$；特别是当 $n$ 无法确定时，就应该使用 Poisson 分布了。
>
> 教材第二章习题 2.2 可体会此用途、精确与近似的差异（非作业）。
>
> **思考**：一张纸上的雨点个数可看作服从何分布？——纸面分成大量小格，每格被雨点打中概率很小且近似独立，总雨点数近似服从 Poisson 分布。

---

## 三、连续型随机变量与密度函数

### 3.1 连续型随机变量、概率密度（定义）

设随机变量 $X$，如果存在非负函数 $f(x)$ 使得对任意的 $a < b$，

$$
\mathbb{P}(a < X \leq b) = \int_a^b f(x)dx,
$$

则称 $X$ 是**连续型随机变量**（continuous r.v.），称 $f(x)$ 是 $X$ 的**概率密度函数**，简称概率密度或者密度（probability density function, PDF）。

**直觉**：概率不再"堆"在一个个点上，而是像质量一样"抹"在数轴上，$f(x)$ 就是概率的"线密度"，区间上的概率 = 密度曲线下的面积。

### 3.2 密度函数的性质

设 $f(x)$ 是 $X$ 的概率密度，则：

| 性质 | 公式 |
| --- | --- |
| 归一性 | $\displaystyle\int_{-\infty}^{\infty} f(x)dx = 1$ |
| Borel 集上的概率 | 对任意的 Borel 集 $A$，$\mathbb{P}(X \in A) = \displaystyle\int_A f(x)dx$ |
| 单点概率为零 | $\mathbb{P}(X = a) = 0$（推论：$\mathbb{P}(a < X \leq b) = \mathbb{P}(a \leq X \leq b)$） |

**性质 1 的证明**：事件 $A_n = \{X \in (-n, n]\}$ 单调增，利用概率的连续性得

$$
\int_{-\infty}^{\infty} f(x)dx = \lim_{n \to \infty} \int_{-n}^{n} f(x)dx = \lim_{n \to \infty} \mathbb{P}(A_n) = \mathbb{P}\left(\bigcup_{n=1}^{\infty} A_n\right) = \mathbb{P}(X \in (-\infty, \infty)) = 1.
$$

**性质 3 的证明**：利用概率的性质得

$$
\mathbb{P}(X = a) \leq \mathbb{P}(X \in (a - \varepsilon, a]) = \int_{a-\varepsilon}^{a} f(x)dx \to 0, \quad \text{as } \varepsilon \downarrow 0.
$$

> [!WARNING] 辨析：单点概率为零 ≠ 不可能
> 连续型随机变量取任何一个固定值的概率都是 $0$，但这不代表"$X = a$"是不可能事件——$X$ 总会取到某个值。概率为零的事件未必是空事件。也因此，对连续型随机变量，区间端点取不取到不影响概率。

### 3.3 密度函数未必有界

**是否需要约束 $f(x)$ 有界么？** 答案是否定的：密度函数（PDF）在其定义域内未必有界。

> [!EXAMPLE]- 例题 7（课件连续部分例 1）：无界的密度函数
> 考虑函数
>
> $$
> f(x) = \frac{1}{2\sqrt{x}}, \quad x \in (0, 1).
> $$
>
> **解**（注：此步补全了验证过程）：显然 $f(x) \geq 0$，且
>
> $$
> \int_0^1 \frac{1}{2\sqrt{x}}dx = \left.\sqrt{x}\right|_0^1 = 1,
> $$
>
> 故 $f(x)$ 是密度函数。但 $f(x)$ 在 $(0,1)$ 上无界，因为 $\lim_{x \downarrow 0} f(x) = +\infty$。

> [!NOTE] 备注：连续型随机变量 ≠ 连续函数
> 虽然 $X$ 是连续型随机变量，但是并不意味着 $X = X(\omega)$ 是连续函数，因为 $X$ 的定义域——样本空间 $\Omega$ 没有任何的拓扑结构，根本谈不上任何连续性。连续型随机变量的意思是它的**分布函数绝对连续**。

---

## 四、常见连续型分布（本节要求掌握的前 3 个）

### 4.1 均匀分布 $\mathcal{U}(a,b)$（常用）

> [!IMPORTANT] 定义：均匀分布
> 对 $a < b$，如果 $X$ 的概率密度是
>
> $$
> f(x) = \begin{cases} \dfrac{1}{b-a}, & x \in (a, b), \\ 0, & x \notin (a, b), \end{cases}
> $$
>
> 称 $X$ 服从区间 $(a,b)$ 上的**均匀分布**，记作 $X \sim \mathcal{U}(a,b)$。$\mathcal{U}$ 是 Uniform 的首字母。

**直觉**：概率在区间上"摊得绝对平"，落在子区间的概率只与子区间长度成正比，与位置无关。

显然区间 $(a,b)$ 也可以写成 $[a,b]$、$[a,b)$ 或 $(a,b]$（单点概率为零，端点无所谓）。密度函数 $f(x)$ 还可以写成示性函数的形式

$$
f(x) = \frac{1}{b-a} I_{(a,b)}(x) \quad \text{或} \quad f(x) = \frac{1}{b-a} I_{x \in (a,b)}.
$$

**推广到 Borel 集**：对任意的 Borel 集 $A$，如果 $A$ 的测度 $m(A) = \int_A 1dx < \infty$，可以类似地定义 $A$ 上的均匀分布：如果 $X$ 的密度是

$$
f(x) = \begin{cases} \dfrac{1}{m(A)}, & x \in A, \\ 0, & x \notin A, \end{cases}
$$

称 $X$ 服从 Borel 集 $A$ 上的均匀分布，记作 $X \sim \mathcal{U}(A)$。对任意的 Borel 集 $B$，

$$
\mathbb{P}(B) = \frac{m(A \cap B)}{m(A)}.
$$

### 4.2 指数分布 $\mathcal{E}(\lambda)$（常用）

> [!IMPORTANT] 定义：指数分布
> 对正常数 $\lambda$，如果 $X$ 的概率密度是
>
> $$
> f(x) = \begin{cases} \lambda e^{-\lambda x}, & x \geq 0, \\ 0, & x < 0, \end{cases}
> $$
>
> 称 $X$ 服从参数 $\lambda$ 的**指数分布**，记作 $X \sim \mathcal{E}(\lambda)$。$\mathcal{E}$ 是 Exponential 的首字母。

**直觉**：等待"下一次事件发生"所需时间的分布——几何分布的连续版本。

密度函数还可以写成示性函数的形式：$f(x) = \lambda e^{-\lambda x} I_{(0,\infty)}$ 或 $f(x) = \lambda e^{-\lambda x},\ x \geq 0$。

**应用**：到发生某个事件为止所用的时间；一台仪器的使用寿命；……

> [!NOTE] 备注：另一种参数化方式
> $f(x) = \dfrac{1}{\theta} e^{-x/\theta} I_{(0,\infty)}$，即取 $\theta = 1/\lambda$（以均值为参数）。读教材或文献时要先确认用的是哪种参数化。

**尾概率**：$X$ 超过某个值的概率，随着这个值的增加而按指数递减，即

$$
\mathbb{P}(X \geq a) = e^{-\lambda a}, \quad \forall a \geq 0.
$$

课件给出了 $\lambda = 1/2, 1, 2$ 等不同参数下的指数密度图：$\lambda$ 越大，密度在 0 附近越高、衰减越快。

当随机变量 $X$ 使得 $\mathbb{P}(X < 0) = 0$，称 $X$ 是**非负随机变量**。指数分布与几何分布十分相似，后面会看到两者的比较。

#### 指数分布的无记忆性

> [!IMPORTANT] 定理 2.1（指数分布 $\Longleftrightarrow$ 无记忆性）
> 设 $X$ 是连续型非负随机变量，则 $X$ 服从指数分布的充要条件是 $X$ 有**无记忆性**，即对任意的 $s, t \geq 0$，有
>
> $$
> \mathbb{P}(X > s + t \mid X > s) = \mathbb{P}(X > t). \tag{2}
> $$

**直觉**：已经等了 $s$ 还没等到，再等 $t$ 以上的概率与从头开始等完全一样——元件"不老化"。

**证明**：

($\Longrightarrow$) 设 $X \sim \mathcal{E}(\lambda)$，则

$$
\mathbb{P}(X > x) = \int_x^{\infty} \lambda e^{-\lambda y}dy = e^{-\lambda x},
$$

由条件概率公式得

$$
\mathbb{P}(X > s + t \mid X > s) = \frac{\mathbb{P}(X > s + t,\ X > s)}{\mathbb{P}(X > s)} = \frac{\mathbb{P}(X > s + t)}{\mathbb{P}(X > s)} = \frac{e^{-\lambda(s+t)}}{e^{-\lambda s}} = e^{-\lambda t} = \mathbb{P}(X > t).
$$

($\Longleftarrow$) 设 $X$ 具有性质 $(2)$，令 $G(x) = \mathbb{P}(X > x)$。由

$$
\mathbb{P}(X > s + t \mid X > s) = \frac{\mathbb{P}(X > s + t,\ X > s)}{\mathbb{P}(X > s)} = \mathbb{P}(X > t)
$$

得 $G(s+t) = G(s)G(t)$，即 $\log G(s+t) = \log G(s) + \log G(t)$。由于 $G(x)$ 是单调非增函数，所以是可测的。由高等数学的知识知该 Cauchy 函数方程的单调解必为线性：

$$
\log G(x) = \left(\log G(1)\right) x, \quad \text{i.e.,} \quad G(x) = e^{-\lambda x},
$$

其中 $\lambda = -\log \mathbb{P}(X > 1) > 0$。最后，对任意的 $0 \leq a < b$，

$$
\mathbb{P}(a < X \leq b) = \mathbb{P}(X \leq b) - \mathbb{P}(X \leq a) = e^{-\lambda a} - e^{-\lambda b} = \int_a^b \lambda e^{-\lambda y}dy,
$$

知 $X \sim \mathcal{E}(\lambda)$。$\blacksquare$

#### 失效率与尺度参数

**失效率**就是单位长度时间内失效的概率。当 $X \sim \mathcal{E}(\lambda)$ 时，失效率

$$
\lim_{\Delta t \to 0} \frac{\mathbb{P}(t < X \leq t + \Delta t \mid X > t)}{\Delta t} = \lim_{\Delta t \to 0} \frac{1 - e^{-\lambda \Delta t}}{\Delta t} = \lambda.
$$

（注：此步补全了课件留作思考的计算——由无记忆性，$\mathbb{P}(t < X \leq t+\Delta t \mid X > t) = \mathbb{P}(X \leq \Delta t) = 1 - e^{-\lambda \Delta t}$，再用 $1 - e^{-x} \sim x$。）

**思考**：$X \sim \mathcal{E}(\lambda)$，$Y = \lambda X$，那么 $Y \sim ?$

（注：此步补全了课件留作思考的解答）对 $y \geq 0$，$\mathbb{P}(Y > y) = \mathbb{P}(X > y/\lambda) = e^{-y}$，故 $Y \sim \mathcal{E}(1)$。所以改变 $\lambda$ 只是对 $X$ 做尺度伸缩，我们称 $\lambda$ 是**尺度参数**（rate parameter）。

> [!NOTE] 备注：无记忆性的工程含义
> 从技术上说，"无记忆性"就是说：元件在时刻 $s$ 尚能正常工作的条件下，其失效率总保持为某一个常数 $\lambda > 0$，与 $s$ 无关。指数分布描述了元件**无老化**时的寿命分布，但"无老化"是不可能的，因而只是一种近似。对一些寿命长的元件，在初期阶段老化现象很小，在这一阶段，指数分布比较确切地描述了其寿命分布情况。

> [!WARNING] 辨析：几何分布与指数分布
> 两者是"无记忆性"在离散与连续两个世界的对应物：几何分布是**唯一**无记忆的取正整数值分布（定理 1.2），指数分布是**唯一**无记忆的连续型非负分布（定理 2.1）。几何分布数"第几次成功"，指数分布量"等多久发生"。

### 4.3 正态分布 $N(\mu, \sigma^2)$（常用）

#### 背景与应用 1：De Moivre–Laplace 中心极限定理

De Moivre (1733) 与 Laplace (1812)（均为法国数学家）证明了 De Moivre–Laplace Central Limit Theorem：

$$
\text{若 } X_n \sim B(n,p), \text{ 则 } \lim_{n \to \infty} \mathbb{P}\left(\frac{X_n - np}{\sqrt{np(1-p)}} \leq x\right) = \int_{-\infty}^{x} \frac{1}{\sqrt{2\pi}} e^{-t^2/2}dt.
$$

**直觉**：二项分布标准化后趋于一个钟形曲线——正态分布最早就是作为二项分布的极限出现的。

#### 背景与应用 2：天文学中的测量误差问题

- 初尝试：Thomas Simpson (1710–1761) 用三角形分布，Laplace (1774) 用双指数密度 $f(x \mid \theta) = \frac{\theta}{2} e^{-\theta |x|}$ 描述误差。
- Gauss 在研究测量误差时得到正态分布 (1809)。假设存在一个真实的误差分布（观测值 $X = \theta + \epsilon$，$\theta$ 为某未知固定真值，$\epsilon$ 为具有随机性的误差），他猜测 $\theta$ 的最大似然估计（Maximum likelihood estimator）就应该是观测值的平均 $\bar{X}$，由此反推出误差的密度必为正态。
- Gauss 的影响力很大，所以正态分布又称为 **Gauss 分布**。

> [!NOTE] 备注：延伸阅读
> 《数理统计学简史》、《正态分布的前世今生》。

#### 定义与基本性质

> [!IMPORTANT] 定义：正态分布
> 如果 $X$ 的密度是
>
> $$
> f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right), \quad x \in \mathbb{R},
> $$
>
> 称 $X$ 服从参数 $(\mu, \sigma^2)$ 的**正态分布**（Normal distribution），记作 $X \sim N(\mu, \sigma^2)$。$N$ 是 Normal 的首字母。
>
> 特别地，当 $X \sim N(0,1)$ 时，称 $X$ 服从**标准正态分布**，其密度函数为
>
> $$
> \varphi(x) = \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{x^2}{2}\right), \quad x \in \mathbb{R}.
> $$

**直觉**：大量独立微小因素叠加的结果就长这样；$\mu$ 定位置（峰在哪），$\sigma$ 定胖瘦（散布多大）。

正态分布的密度函数呈钟型，又称为**钟型分布**，具有以下性质：

| 性质 | 内容 |
| --- | --- |
| 对称性 | $f(x)$ 关于 $x = \mu$ 对称 |
| 最大值 | $f(\mu) = \left(\sigma\sqrt{2\pi}\right)^{-1}$ 是最大值 |
| 拐点 | $f(x)$ 在 $x = \mu \pm \sigma$ 处有拐点 |

课件密度图显示：$\sigma$ 越小曲线越高瘦，$\sigma$ 越大越矮胖，位置由 $\mu$ 平移。

#### 验证 $\varphi(x)$ 确实是密度函数

利用极坐标变换计算归一化积分的平方：

$$
\begin{align}
\left(\frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} e^{-\frac{x^2}{2}}dx\right) & \left(\frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} e^{-\frac{y^2}{2}}dy\right) \\
&= \frac{1}{2\pi} \int_{-\infty}^{\infty} \int_{-\infty}^{\infty} e^{-(x^2+y^2)/2}dxdy \\
&= \frac{1}{2\pi} \int_0^{2\pi} d\theta \int_0^{\infty} r e^{-\frac{r^2}{2}}dr \\
&= \frac{1}{2} \int_0^{\infty} e^{-\frac{r^2}{2}}d(r^2) = 1.
\end{align}
$$

（注：此步补全说明——令 $x = r\cos\theta$，$y = r\sin\theta$，Jacobi 行列式为 $r$；最后一个积分 $\int_0^\infty e^{-u/2} \frac{du}{2} = 1$。又因积分值非负，开方得积分为 1。）

一般的 $f(x)$ 也是密度函数：作换元 $t = \frac{x - \mu}{\sigma}$，

$$
\int_{-\infty}^{\infty} \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)dx = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} e^{-\frac{t^2}{2}}dt = 1.
$$

#### 背景与应用 3

- 在 Brown motion（布朗运动）的研究中，人们也得到了正态分布。
- 事实表明，产品的许多质量指标，生物和动物的许多生理指标等都服从或近似服从正态分布。
- 大量相互独立且具有相同分布的随机变量（Independent and identically distributed random variables, i.i.d.）的累积也近似服从正态分布。
- 理论上，正态分布有许多优良的性质，例如稳定性、最大熵的性质等。
- 正态分布在概率论和统计中有着特殊的地位。

---

## 五、其他连续型随机变量（拓展）

> [!NOTE] 备注
> 课件说明：后续是拓展的其他变量，会在接下来几讲陆续介绍，置于此仅为便利同学们复习整理。本节只要求掌握前 3 个（均匀、指数、正态），以下各分布了解即可。

### 5.1 Beta 分布 $\text{Beta}(\alpha, \beta)$（了解即可）

> [!IMPORTANT] 定义：Beta 分布
> 设 $\alpha, \beta$ 是正常数，如果 $X$ 的密度是
>
> $$
> f(x) = \frac{1}{B(\alpha, \beta)} x^{\alpha - 1} (1-x)^{\beta - 1}, \quad 0 < x < 1,
> $$
>
> 其中 $B(\alpha, \beta) = \dfrac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha + \beta)}$，则称 $X$ 服从参数为 $(\alpha, \beta)$ 的 **Beta 分布**，记作 $X \sim \text{Beta}(\alpha, \beta)$。

**直觉**：取值在 $(0,1)$ 上的"概率的分布"，两个参数分别控制密度在 0 端和 1 端的形状。

> [!NOTE] 备注：贝叶斯统计中的共轭先验
> Beta 分布常在贝叶斯统计方法中作为参数的先验分布。特别地，它是二项分布的**共轭分布**：$X \mid p \sim B(n, p)$，参数 $p$ 的先验取 $\text{Beta}(\alpha, \beta)$，观测 $X$ 后得到后验 $\text{Beta}(\alpha + X,\ \beta + n - X)$。直观解释：$\alpha, \beta$ 可看作"先验的成功、失败次数"，观测后直接累加（学习条件分布后将可以证明）。

由密度函数图形（课件展示了多组参数的曲线）：
- 当 $\alpha = \beta = 1$ 时，为均匀分布 $\mathcal{U}(0,1)$；
- 当 $\alpha = 2, \beta = 1$ 时，密度函数呈直线型；
- 当 $\alpha = \beta = 1/2$ 时，密度函数呈上 U 型；
- 当 $\alpha = \beta = 2$ 时，密度函数呈下 U 型（钟形）。

### 5.2 Gamma 分布 $\Gamma(\alpha, \lambda)$（了解即可）

> [!IMPORTANT] 定义：Gamma 分布
> 设 $\alpha, \lambda$ 是正常数，如果 $X$ 的密度是
>
> $$
> f(x) = \frac{\lambda^{\alpha}}{\Gamma(\alpha)} x^{\alpha - 1} e^{-\lambda x}, \quad x \geq 0,
> $$
>
> 称 $X$ 服从参数 $(\alpha, \lambda)$ 的 **Gamma 分布**，记作 $X \sim \Gamma(\alpha, \lambda)$，其中
>
> $$
> \Gamma(\alpha) = \int_0^{\infty} x^{\alpha - 1} e^{-x}dx
> $$
>
> 称为 **Gamma 函数**。

**直觉**：当 $\alpha$ 为正整数 $k$ 时，可理解为"等到第 $k$ 个事件发生"的总时间——指数分布的"帕斯卡化"。

**Gamma 函数的性质**：

| 性质 | 公式 |
| --- | --- |
| 整数值 | $\Gamma(n) = (n-1)!$ |
| 递推 | $\Gamma(\alpha + 1) = \alpha \Gamma(\alpha)$ |
| 半整数 | $\Gamma\left(\frac{1}{2}\right) = \sqrt{\pi}$ |

$\alpha$ 被称为**形状参数**（shape parameter）；$\lambda$ 被称为**尺度参数**（rate parameter）。

- 当 $\alpha = 1$ 时，为指数分布。
- 当 $\alpha$ 为正整数时，称为 **Erlang 分布**（用在"排队论"中）。

> [!NOTE] 备注：Pearson 分布族与气象应用
> 英国著名统计学家 Karl Pearson 在研究物理、生物及经济中的随机变量时，发现很多连续型随机变量的分布不是正态分布。这些随机变量的特点是只取非负值，于是他致力于这类随机变量的研究，参阅 Wikipedia 上的 "Pearson distribution"。在气象学中，干旱地区的年、季或月降水量被认为服从 $\Gamma$ 分布。

### 5.3 Weibull 分布（了解即可）

> [!IMPORTANT] 定义：Weibull 分布
> 如果 $X$ 的密度是
>
> $$
> f(x) = \lambda \alpha x^{\alpha - 1} \exp(-\lambda x^{\alpha}), \quad x \geq 0,
> $$
>
> 称 $X$ 服从参数 $(\alpha, \lambda)$ 的 **Weibull 分布**。

**直觉**：给指数分布的"时间"加上一个幂次变形，使失效率可以随时间上升或下降，从而能描述会老化（或磨合）的寿命。

- (a) 当 $\alpha = 1$ 时，Weibull 分布为指数分布；
- (b) 当 $\alpha = 2$ 时，Weibull 分布为 **Rayleigh 分布**，其密度为

$$
f(x; \sigma) = \frac{x}{\sigma^2} \exp\left(-\frac{x^2}{2\sigma^2}\right), \quad x \geq 0.
$$

指数分布和 Weibull 分布在**可靠性分析**中占重要地位。

### 5.4 卡方分布 $\chi^2_v$（了解即可）

> [!IMPORTANT] 定义：卡方分布（Chi-squared distribution）
> 设 $v > 0$，如果 $X$ 的密度是
>
> $$
> f(x) = \frac{1}{2^{v/2} \Gamma(v/2)} x^{\frac{v}{2} - 1} e^{-\frac{x}{2}}, \quad x \geq 0,
> $$
>
> 称 $X$ 服从参数为 $v$ 的 $\chi^2_v$ 分布，记作 $X \sim \chi^2_v$。

**直觉**：$n$ 个独立标准正态的平方和，统计推断中"误差平方和"的分布原型。

- 设有独立同分布（i.i.d.）的变量 $Z_j \sim N(0,1)$，$j = 1, \ldots, n$。令 $X = Z_1^2 + \cdots + Z_n^2$，则 $X \sim \chi^2_n$。
- 可以验证 $\chi^2_1 = \Gamma\left(\frac{1}{2}, \frac{1}{2}\right)$。于是由 Gamma 分布的性质（以后会证明），有 $\chi^2_n = \Gamma\left(\frac{n}{2}, \frac{1}{2}\right)$。

### 5.5 Student's t 分布 $t_v$（了解即可）

> [!IMPORTANT] 定义：Student's t 分布
> 设 $v > 0$，如果 $X$ 的密度是
>
> $$
> f(x) = \frac{\Gamma\left(\frac{v+1}{2}\right)}{\sqrt{v\pi}\ \Gamma\left(\frac{v}{2}\right)} \left(1 + \frac{x^2}{v}\right)^{-\frac{v+1}{2}}, \quad x \in \mathbb{R},
> $$
>
> 称 $X$ 服从参数为 $v$ 的 **Student's t 分布**，简称 t 分布，记作 $X \sim t_v$。

**直觉**：长得像标准正态但尾巴更厚——小样本下用样本标准差代替真实标准差所付出的"代价"。

- 设有 $Z \sim N(0,1)$，$X \sim \chi^2_n$，且 $X$ 与 $Z$ 独立。令 $T = \dfrac{Z}{\sqrt{X/n}}$，则有 $T \sim t_n$。
- **对称性**：若 $T \sim t_v$，则 $-T \sim t_v$。
- 比正态分布**重尾**。
- 当 $v$ 很大时，$t_v$ 分布看起来和标准正态分布很像（以后将用大数定律证明）。
- 特例：当 $v = 1$ 时，性质特殊，亦称为 **Cauchy 分布**。

### 5.6 Cauchy 分布（了解即可）

> [!IMPORTANT] 定义：Cauchy 分布
> 如果 $X$ 的密度是
>
> $$
> f(x) = \frac{1}{\pi(1 + x^2)}, \quad x \in \mathbb{R},
> $$
>
> 称 $X$ 服从 **Cauchy 分布**，亦可记作 $X \sim t_1$。

**直觉**：尾巴极厚的"病态"代表——厚到连期望都不存在，是检验一切"想当然"结论的反例库。

- 设有独立同分布（i.i.d.）的变量 $Z_j \sim t_1$，$j = 1, \ldots, n$。令 $X = \dfrac{Z_1 + \cdots + Z_n}{n}$，则依然有 $X \sim t_1$——样本均值完全不"集中"，平均不能稀释 Cauchy 的随机性。
- 几何来源：当 $K$ 从 $-\infty$ 变到 $\infty$ 时，点 $C$ 的轨迹描绘出了 Maria Gaetana Agnesi（1718.5.16–1799.1.9，意大利女数学家兼哲学家）的**箕舌线**——Cauchy 密度曲线正是箕舌线（课件配图）。

### 5.7 F 分布 $F(m,n)$（了解即可）

> [!IMPORTANT] 定义：F 分布（Fisher–Snedecor distribution）
> 设 $m, n$ 是正整数，如果 $X$ 的密度是
>
> $$
> f(x) = \frac{\Gamma\left(\frac{m+n}{2}\right)}{\Gamma\left(\frac{m}{2}\right)\Gamma\left(\frac{n}{2}\right)} \cdot \frac{m^{m/2}\, n^{n/2}\, x^{\frac{m}{2}-1}}{(mx + n)^{\frac{m+n}{2}}}, \quad x \geq 0,
> $$
>
> 称 $X$ 服从参数为 $(m,n)$ 的 **F 分布**，记作 $X \sim F(m,n)$。

**直觉**：两组独立的"平均平方误差"之比的分布，用来比较两个方差谁大。

设有独立同分布（i.i.d.）的变量 $X_j \sim N(0,1)$，$j = 1, \ldots, m$ 和 $Y_j \sim N(0,1)$，$j = 1, \ldots, n$（全体相互独立）。令

$$
F = \frac{\frac{1}{m}\sum_{i=1}^{m} X_i^2}{\frac{1}{n}\sum_{i=1}^{n} Y_i^2},
$$

则 $F \sim F(m,n)$。

1924 年，英国统计学家 Fisher 提出，因此命名 F 分布。在方差分析、线性回归中有重要应用。

---

## 六、小结

**知识点**：
- 离散随机变量、分布列（PMF）
    - 重点：两点分布、二项分布、几何分布、泊松分布
- 连续型随机变量、密度函数（PDF）
    - 重点：均匀分布、指数分布、正态分布
- 分布间的关系

**技巧**：
- 利用实际情景建立不同分布之间的关系；
- 利用分布间的关系理解分布的含义。

**离散型分布汇总**：

| 分布 | 记号 | 分布列 $\mathbb{P}(X=k)$ | 取值范围 | 典型情景 |
| --- | --- | --- | --- | --- |
| 两点分布 | $B(1,p)$ | $p^k(1-p)^{1-k}$ | $k = 0, 1$ | 单次"是/否"试验 |
| 二项分布 | $B(n,p)$ | $\binom{n}{k} p^k (1-p)^{n-k}$ | $0 \leq k \leq n$ | $n$ 次试验的成功数 |
| 几何分布 | $G(p)$ | $(1-p)^{k-1} p$ | $k \geq 1$ | 首次成功的试验次数 |
| 帕斯卡分布 | — | $\binom{k-1}{r-1}(1-p)^{k-r} p^r$ | $k \geq r$ | 第 $r$ 次成功的试验次数 |
| 负二项分布 | $\text{NB}(r,p)$ | $\binom{k+r-1}{r-1}(1-p)^k p^r$ | $k \geq 0$ | 第 $r$ 次成功前的失败数 |
| 超几何分布 | $H(n,M,N)$ | $\binom{M}{k}\binom{N-M}{n-k} \big/ \binom{N}{n}$ | $0 \leq k \leq \min\{n,M\}$ | 无放回抽样的红球数 |
| 负超几何分布 | $NH(r,M,N)$ | $\binom{k+r-1}{k}\binom{N-k-r}{M-r} \big/ \binom{N}{M}$ | $0 \leq k \leq N-M$ | 无放回抽到第 $r$ 个红球前的黑球数 |
| Poisson 分布 | $\mathcal{P}(\lambda)$ | $\dfrac{\lambda^k}{k!} e^{-\lambda}$ | $k \geq 0$ | 稀有事件的计数 |

**连续型分布汇总**：

| 分布 | 记号 | 密度 $f(x)$ | 支撑 | 备注 |
| --- | --- | --- | --- | --- |
| 均匀分布 | $\mathcal{U}(a,b)$ | $\frac{1}{b-a}$ | $(a,b)$ | 要求掌握 |
| 指数分布 | $\mathcal{E}(\lambda)$ | $\lambda e^{-\lambda x}$ | $x \geq 0$ | 要求掌握；无记忆 |
| 正态分布 | $N(\mu,\sigma^2)$ | $\frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$ | $\mathbb{R}$ | 要求掌握；钟形 |
| Beta 分布 | $\text{Beta}(\alpha,\beta)$ | $\frac{x^{\alpha-1}(1-x)^{\beta-1}}{B(\alpha,\beta)}$ | $(0,1)$ | 拓展；共轭先验 |
| Gamma 分布 | $\Gamma(\alpha,\lambda)$ | $\frac{\lambda^{\alpha}}{\Gamma(\alpha)} x^{\alpha-1} e^{-\lambda x}$ | $x \geq 0$ | 拓展；$\alpha=1$ 即指数 |
| Weibull 分布 | — | $\lambda\alpha x^{\alpha-1} e^{-\lambda x^{\alpha}}$ | $x \geq 0$ | 拓展；可靠性 |
| 卡方分布 | $\chi^2_v$ | $\frac{x^{v/2-1} e^{-x/2}}{2^{v/2}\Gamma(v/2)}$ | $x \geq 0$ | 拓展；$= \Gamma(\frac{v}{2},\frac{1}{2})$ |
| t 分布 | $t_v$ | $\frac{\Gamma(\frac{v+1}{2})}{\sqrt{v\pi}\Gamma(\frac{v}{2})}(1+\frac{x^2}{v})^{-\frac{v+1}{2}}$ | $\mathbb{R}$ | 拓展；重尾 |
| Cauchy 分布 | $t_1$ | $\frac{1}{\pi(1+x^2)}$ | $\mathbb{R}$ | 拓展；期望不存在 |
| F 分布 | $F(m,n)$ | 见 5.7 | $x \geq 0$ | 拓展；方差比 |

**分布间关系一览**：
- $n$ 个独立 $B(1,p)$ 之和 $\sim B(n,p)$；独立 $B(n,p) + B(m,p) \sim B(m+n,p)$。
- 帕斯卡分布 $\xrightarrow{r=1}$ 几何分布；负二项 = 帕斯卡平移 $r$。
- 超几何 $\xrightarrow{N \to \infty,\ M/N \to p}$ 二项；二项 $\xrightarrow{n \to \infty,\ np \to \lambda}$ Poisson。
- 几何（离散无记忆）$\leftrightarrow$ 指数（连续无记忆）。
- $\text{Beta}(1,1) = \mathcal{U}(0,1)$；$\Gamma(1,\lambda) = \mathcal{E}(\lambda)$；Weibull$(\alpha=1)$ = 指数，Weibull$(\alpha=2)$ = Rayleigh。
- $\chi^2_n = \Gamma(\frac{n}{2}, \frac{1}{2}) = \sum_{j=1}^n Z_j^2$；$t_n = Z \big/ \sqrt{\chi^2_n / n}$；$t_1$ = Cauchy；$F(m,n) = \frac{\chi^2_m/m}{\chi^2_n/n}$。
- 二项 $\xrightarrow{\text{标准化}, n \to \infty}$ 正态（De Moivre–Laplace）。

---

## 本讲方法/题型清单

- 求"$n$ 次独立试验恰好/至少成功 $k$ 次"的概率 → 二项分布 $B(n,p)$ → 识别 $n, p$，写 $\binom{n}{k}p^k(1-p)^{n-k}$；"至少"型用对立事件 $1 - \sum_{k \leq k_0}$ 减少计算量。
- 求二项分布的最可能值 → 定理 1.1（中心项）→ 算 $(n+1)p$：为整数则 $(n+1)p$ 与 $(n+1)p-1$ 并列最大，否则取 $\lfloor (n+1)p \rfloor$。
- "试验直到首次成功"类问题 → 几何分布 $G(p)$ → 概率 $(1-p)^{k-1}p$；涉及"已经失败若干次"的条件概率直接用无记忆性。
- "试验直到第 $r$ 次成功"类问题 → 帕斯卡分布（数总次数）或负二项分布（数失败次数）→ 最后一次必为成功，前面用组合数安排其余成功位置。
- 验证某数列是分布列 → 检查非负 + 求和为 1 → 常用工具：二项展开式、几何级数、负指数二项展开式、$e^{\lambda}$ 的 Taylor 展开。
- 无放回抽样"恰好抽到 $k$ 个某类"→ 超几何分布 → 分子分母组合数；$N$ 很大时用二项近似 $p_N = M/N$。
- 稀有事件计数（$n$ 大 $p$ 小或 $n$ 未知）→ Poisson 近似/Poisson 分布 → 取 $\lambda = np$（或平均发生数），用 $\frac{\lambda^k}{k!}e^{-\lambda}$。
- 证明/使用离散无记忆性 → 定理 1.2 → 正向用条件概率公式直接算；反向设 $r_k = \mathbb{P}(X>k)$ 建立递推 $r_{k+1} = (1-p)r_k$。
- 验证某函数是密度 → 检查非负 + $\int_{-\infty}^{\infty} f = 1$ → 正态用极坐标技巧，Gamma 类用 $\Gamma$ 函数定义换元。
- 求连续型变量落在区间/Borel 集的概率 → $\mathbb{P}(X \in A) = \int_A f(x)dx$ → 注意单点概率为 0，端点开闭不影响结果。
- "寿命/等待时间在已存活 $s$ 后再超过 $t$"的条件概率 → 指数分布无记忆性（定理 2.1）→ 直接等于 $\mathbb{P}(X > t) = e^{-\lambda t}$，无需重新积分。
- 证明连续无记忆性刻画指数分布 → 设 $G(x) = \mathbb{P}(X>x)$ → 导出函数方程 $G(s+t) = G(s)G(t)$，取对数得线性，$\lambda = -\log G(1)$。
- 识别"由情景建立分布"类问题 → 先问四件事：试验独立吗？有放回吗？固定的是试验数还是成功数？数的是次数、失败数还是时间？→ 对号入座选分布。
