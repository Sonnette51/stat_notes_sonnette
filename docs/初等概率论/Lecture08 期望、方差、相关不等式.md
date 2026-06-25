---
title: "Lecture08 期望、方差、相关不等式"
tags:
  - 概率论
  - 后半学期
  - 期望
  - 方差
  - 不等式
---

# Lecture08 期望、方差、相关不等式

## 一、期望的来源——赌金分配问题

### 1.1 引例

甲、乙二人对赌，水平相当（即每局各自赢的概率均为 $\frac{1}{2}$），先赢满 5 局者获得全部赌金 100 个金币。当甲赢了 4 局、乙赢了 3 局时，他们被迫中断赌局。**该如何分配赌金？**

会计师建议按已赢局数 4:3 的比例分配，但这公平吗？

**正确思路：** 考虑从当前局面继续玩下去的所有可能结果。

从 4:3 的局面出发，最多还需要再打 2 局：

- 若接下来甲赢（概率 $\frac{1}{2}$），变成 5:3，甲赢得全部赌金。
- 若接下来乙赢（概率 $\frac{1}{2}$），变成 4:4，再打一局：
    - 甲赢（概率 $\frac{1}{2}$），变成 5:4，甲赢。
    - 乙赢（概率 $\frac{1}{2}$），变成 4:5，乙赢。

因此：

- 甲最终获胜的概率 = $\frac{1}{2} + \frac{1}{2} \times \frac{1}{2} = \frac{3}{4}$
- 乙最终获胜的概率 = $\frac{1}{2} \times \frac{1}{2} = \frac{1}{4}$

设甲的收益 $X$：

$$X = \begin{cases} 100, & \text{概率 } \dfrac{3}{4} \ 0, & \text{概率 } \dfrac{1}{4} \end{cases}$$

甲的**预期收益**（即加权平均值）：

$$100 \times \frac{3}{4} + 0 \times \frac{1}{4} = 75$$

所以应按 **75:25 = 3:1** 的比例分配，而不是 4:3。这个"预期收益"就是**数学期望**。

---

## 二、离散型随机变量的数学期望

### 2.1 正式定义

> [!INFO] 定义 1.1（离散型随机变量的期望）
> 
> 设 $X$ 有概率分布 $\mathbb{P}(X = x_j)$，$j = 1, 2, \ldots$
> 
> 如果 $\displaystyle\sum_{j=1}^{\infty} |x_j| \mathbb{P}(X = x_j) < +\infty$，则称
> 
> $$E(X) = \sum_{j=1}^{\infty} x_j \mathbb{P}(X = x_j)$$
> 
> 为 $X$ 的**数学期望**（Mathematical Expectation）或**均值**（Mean）。

**几点说明：**

1. **存在性条件**：要求绝对值之和收敛（绝对收敛），这是为了确保无穷级数的和不依赖于求和顺序。只取有限个值的随机变量，期望一定存在。
    
2. **直观含义**：期望是 $X$ 分布的**加权平均**，权重就是各取值的概率。物理上，期望可以理解为 $X$ 的概率分布的**质心**（重心）——想象在数轴上，每个点 $x_j$ 处放一个质量为 $\mathbb{P}(X = x_j)$ 的砝码，质心所在的位置就是 $E(X)$。
    

---

## 三、常见离散分布的期望

### 3.1 两点分布 $B(1, p)$

设 $X \sim B(1, p)$，即

$$\mathbb{P}(X = 1) = p, \quad \mathbb{P}(X = 0) = 1 - p$$

则

$$E(X) = 1 \cdot p + 0 \cdot (1-p) = p$$

**直观**：抛一枚正面概率为 $p$ 的硬币，平均得到正面的次数就是 $p$。

**推论**：设 $A$ 是事件，$I_A$ 是 $A$ 的示性函数（$A$ 发生时 $I_A = 1$，否则 $I_A = 0$）。则 $I_A$ 服从两点分布，且

$$E(I_A) = \mathbb{P}(A)$$

这说明**事件概率等于其示性函数的期望**，是一个非常有用的视角。

---

### 3.2 二项分布 $B(n, p)$

设 $X \sim B(n, p)$，即

$$\mathbb{P}(X = j) = \binom{n}{j} p^j (1-p)^{n-j}, \quad 0 \leq j \leq n$$

则 $E(X) = np$。

**证明：** 按定义展开，利用组合恒等式 $j \binom{n}{j} = n \binom{n-1}{j-1}$：

$$E(X) = \sum_{j=0}^{n} j \binom{n}{j} p^j (1-p)^{n-j} = np \sum_{j=1}^{n} \binom{n-1}{j-1} p^{j-1} (1-p)^{n-j}$$

令 $k = j-1$，上式变为：

$$= np \sum_{k=0}^{n-1} \binom{n-1}{k} p^k (1-p)^{n-1-k} = np \cdot (p + (1-p))^{n-1} = np$$

**直观**：$n$ 次独立试验，每次成功概率为 $p$，平均成功次数当然是 $np$。后面学了期望的线性性质，可以用更简洁的方法推导这个结论。

---

### 3.3 Poisson 分布 $\mathcal{P}(\lambda)$

设 $X \sim \mathcal{P}(\lambda)$，即

$$\mathbb{P}(X = k) = \frac{\lambda^k}{k!} e^{-\lambda}, \quad k = 0, 1, 2, \ldots$$

则（由归一化性质）：

$$E(X) = \sum_{k=0}^{\infty} k \cdot \frac{\lambda^k}{k!} e^{-\lambda} = \lambda \sum_{k=1}^{\infty} \frac{\lambda^{k-1}}{(k-1)!} e^{-\lambda} = \lambda \cdot e^{\lambda} \cdot e^{-\lambda} = \lambda$$

**直观**：Poisson 分布的参数 $\lambda$ 本身就是平均发生次数，这也是 $\lambda$ 在实际中被称为"强度"的原因。

---

### 3.4 几何分布 $G(p)$

设 $X \sim G(p)$，即

$$\mathbb{P}(X = k) = p(1-p)^{k-1}, \quad k = 1, 2, \ldots$$

$X$ 的含义是：独立重复进行伯努利试验，直到第一次成功所需的试验次数。

$$E(X) = \sum_{k=1}^{\infty} k \cdot p(1-p)^{k-1} = \frac{1}{p}$$

（推导过程利用幂级数求导：$\sum_{k=1}^{\infty} k x^{k-1} = \frac{1}{(1-x)^2}$，令 $x = 1-p$ 即可。）

**直观**：每次成功概率为 $p$，平均需要 $\frac{1}{p}$ 次才能第一次成功。比如掷骰子，掷出 6 的概率为 $\frac{1}{6}$，平均需要 6 次。

---

## 四、连续型随机变量的数学期望

### 4.1 正式定义

> [!INFO] 定义 1.2（连续型随机变量的期望）
> 
> 设 $X$ 有概率密度函数 $f(x)$，如果
> 
> $$\int_{-\infty}^{\infty} |x| f(x)dx < +\infty$$
> 
> 则称
> 
> $$E(X) = \int_{-\infty}^{\infty} x f(x)dx$$
> 
> 为 $X$ 的**数学期望**或**均值**。

**与离散情况的对比：**

|      | 离散型                                           | 连续型                                             |
| ---- | --------------------------------------------- | ----------------------------------------------- |
| 期望公式 | $\displaystyle\sum_j x_j \mathbb{P}(X = x_j)$ | $\displaystyle\int_{-\infty}^{\infty} x f(x)dx$ |
| 类比关系 | 求和                                            | 积分                                              |
| 权重   | 概率 $\mathbb{P}(X = x_j)$                      | 密度 $f(x),dx$                                    |

两者的含义一致，都是**加权平均**，只是求和方式不同。

---

## 五、常见连续分布的期望

### 5.1 均匀分布 $U(a, b)$

设 $X \sim U(a, b)$，即

$$f(x) = \frac{1}{b-a} \cdot I_{(a,b)}(x)$$

则

$$E(X) = \int_a^b \frac{x}{b-a}dx = \frac{1}{b-a} \cdot \frac{b^2 - a^2}{2} = \frac{a+b}{2}$$

**直观**：均匀分布关于 $\frac{a+b}{2}$ 对称，质心当然在中点。

---

### 5.2 指数分布 $\mathcal{E}(\lambda)$

设 $X \sim \mathcal{E}(\lambda)$，即 $f(x) = \lambda e^{-\lambda x}$（$x > 0$）。

由分部积分（令 $u = x$，$dv = \lambda e^{-\lambda x}dx$）并利用归一化：

$$E(X) = \int_0^{\infty} x \lambda e^{-\lambda x}dx = \frac{1}{\lambda}$$

**直观**：$\lambda$ 是事件发生的"速率"（单位时间内平均发生次数），那么两次事件之间的平均等待时间就是 $\frac{1}{\lambda}$。

---

### 5.3 Gamma 分布 $\Gamma(\alpha, \beta)$

设 $X \sim \Gamma(\alpha, \beta)$，即

$$f(x) = \frac{\beta^{\alpha}}{\Gamma(\alpha)} x^{\alpha-1} e^{-\beta x}, \quad x > 0$$

其中 $\Gamma(\alpha) = \int_0^{\infty} t^{\alpha-1} e^{-t}dt$ 是 Gamma 函数，满足 $\Gamma(\alpha + 1) = \alpha \Gamma(\alpha)$。

利用换元 $t = \beta x$：

$$E(X) = \int_0^{\infty} \frac{\beta^{\alpha}}{\Gamma(\alpha)} x^{\alpha} e^{-\beta x}dx = \frac{1}{\beta \Gamma(\alpha)} \int_0^{\infty} t^{(\alpha+1)-1} e^{-t}dt = \frac{\Gamma(\alpha+1)}{\beta \Gamma(\alpha)} = \frac{\alpha}{\beta}$$

**特殊情况**：当 $\alpha = 1$ 时，$\Gamma(1, \beta)$ 退化为 $\mathcal{E}(\beta)$，期望为 $\frac{1}{\beta}$，与上节一致。

---

### 5.4 正态分布 $\mathcal{N}(\mu, \sigma^2)$

设 $X \sim \mathcal{N}(\mu, \sigma^2)$，即

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$

利用对称性和归一化：

$$E(X) = \int_{-\infty}^{\infty} \mu f(x),dx + \int_{-\infty}^{\infty} (x-\mu) f(x),dx = \mu + \frac{1}{\sigma\sqrt{2\pi}} \int_{-\infty}^{\infty} t \exp\left(-\frac{t^2}{2\sigma^2}\right)dt = \mu$$

最后一个积分为 0，因为被积函数 $t \exp(-t^2 / 2\sigma^2)$ 是**奇函数**，在 $(-\infty, +\infty)$ 上的积分为零。

**结论**：$\mathcal{N}(\mu, \sigma^2)$ 的期望就是参数 $\mu$，这正是 $\mu$ 被称为"均值参数"的原因。

**一般结论（例 1.10）**：设 $X$ 的期望存在，若 $X$ 的概率密度 $f(x)$ 关于 $x = \mu$ 对称（即 $f(x + \mu) = f(\mu - x)$），则 $E(X) = \mu$。这把正态分布的计算技巧一般化了——只要分布关于 $\mu$ 对称，期望就等于 $\mu$。

---

## 六、一般随机变量的期望（了解）

对于既不纯离散也不纯连续的随机变量（如例 1.11：抛硬币决定获得固定值还是连续分布随机值），期望的统一定义为：

$$E(X) = \int_{\Omega} Xd\mathbb{P} = \int_{\mathbb{R}} xdF(x)$$

其中 $F(x)$ 是 $X$ 的分布函数。如果分布函数可以分解为连续部分 $F_1$ 和离散跳跃部分 $F_2$，则：

$$E(X) = \int_{-\infty}^{\infty} x f_0(x)dx + \sum_{j=1}^{\infty} x_j \mathbb{P}(X = x_j)$$

即连续部分的积分加上离散部分的求和。

**重要结论**：同分布的随机变量有相同的期望（如果期望存在）。

> **注**：这部分内容课件标注为"不要求"，了解即可。

---

## 七、期望的性质

### 7.1 随机变量函数的期望（LOTUS 定理）

在计算 $Y = g(X)$ 的期望时，有一个非常方便的定理，让我们**不需要先求 $Y$ 的分布**。

> [!NOTE] 定理 2.1（LOTUS）
> 
> 设 $\boldsymbol{X} = (X_1, \ldots, X_n)$ 是随机向量，联合分布函数为 $F(\boldsymbol{x})$，$g$ 是实值函数，且 $\int_{\mathbb{R}^n} |g(\boldsymbol{x})|,dF(\boldsymbol{x}) < \infty$，则
> 
> $$E(g(\boldsymbol{X})) = \int_{\mathbb{R}^n} g(\boldsymbol{x}),dF(\boldsymbol{x})$$

**对一元情况**，这就变成了：

- **$X$ 离散**：$E(g(X)) = \displaystyle\sum_j g(x_j) \mathbb{P}(X = x_j)$
- **$X$ 连续**：$E(g(X)) = \displaystyle\int_{-\infty}^{\infty} g(x) f(x),dx$

**为什么这个定理很重要？** 原本计算 $E(g(X))$ 需要：

1. 推导 $Y = g(X)$ 的分布
2. 用 $Y$ 的分布和期望定义计算 $E(Y)$

LOTUS 告诉我们可以跳过第一步，直接用 $X$ 的分布计算。

**例（验证 LOTUS 的直觉）**：设 $g(x) = x^2$，$X$ 取值 $-1, 1, 2$，概率分别为 $\frac{1}{8}, \frac{1}{8}, \frac{3}{4}$。

- $Y = X^2$ 取值 $1, 4$，概率分别为 $\frac{1}{8}+\frac{1}{8}=\frac{1}{4}$ 和 $\frac{3}{4}$。
- $E(Y) = 1 \cdot \frac{1}{4} + 4 \cdot \frac{3}{4} = \frac{13}{4}$。

用 LOTUS 直接算：$E(X^2) = (-1)^2 \cdot \frac{1}{8} + 1^2 \cdot \frac{1}{8} + 2^2 \cdot \frac{3}{4} = \frac{1}{8} + \frac{1}{8} + 3 = \frac{13}{4}$。结果一致，且 LOTUS 更简洁。

---

### 7.2 期望的重要性质

> [!NOTE] 定理 2.2
> 
> 设 $E|X| < +\infty$，$E|Y| < +\infty$，$a, b, C$ 均为实数，则：
> 
> 1. $E(C) = C$（常数的期望是常数本身）
> 2. $|EX| \leq E|X|$（期望的绝对值不超过绝对值的期望）
> 3. $E(aX + bY) = aEX + bEY$（**线性性**，Linearity）
> 4. 若 $X \leq Y$（几乎处处），则 $EX \leq EY$（**单调性**）
> 5. 若 $X$ 和 $Y$ **独立**，则 $E(XY) = (EX)(EY)$（独立则乘积的期望等于期望的乘积）

**性质 3（线性性）** 是最重要的，几乎用于每个期望计算。注意：这里 $X$ 和 $Y$ **不需要独立**，对任意两个期望存在的随机变量都成立。

**性质 5 的反向不成立**：$E(XY) = (EX)(EY)$ 不能推出 $X$ 和 $Y$ 独立。

**⚠️ 一般来说 $E(g(X)) \neq g(E(X))$**（除非 $g$ 是线性函数）。例如：$E(X^2) \neq (EX)^2$（这正是方差 $Var(X) = E(X^2) - (EX)^2 \geq 0$ 的由来）。

---

### 7.3 期望的优化解释

> [!NOTE] 定理 2.3
> 
> 设 $EX = \mu$，$E(X^2) < \infty$，则对所有 $c \in \mathbb{R}$，
> 
> $$E(X - \mu)^2 \leq E(X - c)^2$$

等价地（从最优化角度）：

$$E(X) = \underset{c \in \mathbb{R}}{\arg\min}; E(X - c)^2$$

**意义**：在用常数 $c$ 来预测随机变量 $X$ 时，若损失函数是均方误差 $E(X-c)^2$，那么**最优的常数预测就是期望 $E(X)$**。这也解释了为什么期望在统计学中如此核心。

**证明**（简洁）：

$$E(X-c)^2 = E((X-\mu) + (\mu - c))^2 = E(X-\mu)^2 + 2(\mu-c)E(X-\mu) + (\mu-c)^2$$

注意 $E(X-\mu) = EX - \mu = 0$，所以

$$E(X-c)^2 = E(X-\mu)^2 + (\mu-c)^2 \geq E(X-\mu)^2$$

当且仅当 $c = \mu$ 时等号成立。

---

### 7.4 中位数与期望的比较

> [!NOTE] 定理 2.4
> 
> 设 $X$ 有概率密度 $f(x)$，$m$ 是其中位数，则
> 
> $$m = \underset{c \in \mathbb{R}}{\arg\min}; E|X - c|$$

即**中位数**是在 $L^1$ 损失（绝对值损失）意义下的最优预测，而**期望**是在 $L^2$ 损失（均方损失）意义下的最优预测。

**为什么概率统计中期望比中位数更重要？**

- **期望有优良的数学性质**：尤其是线性性，使其在推导和计算中极为方便。中位数不满足线性性（$\text{median}(X+Y) \neq \text{median}(X) + \text{median}(Y)$）。
- **中位数可能不唯一**：例如，当 $F(x)$ 在某段区间上取 $\frac{1}{2}$ 时，中位数有无穷多个（如右图所示，两个分开的密度峰的情况）。

中位数的优点：不易受极端值（outlier）影响，社会经济统计中常用（如"居民中位数收入"比均值更能反映多数人的收入水平）。

---

## 八、期望性质的应用

### 8.1 利用线性性重新推导二项分布和 Gamma 分布的期望

**二项分布 $B(n,p)$**：

设 $X \sim B(n,p)$，将 $X$ 写成 $n$ 个独立两点随机变量之和：$X = X_1 + X_2 + \cdots + X_n$，其中 $X_k \sim B(1,p)$。

由线性性：

$$E(X) = E(X_1) + \cdots + E(X_n) = n \cdot p = np$$

比直接用定义计算要简洁得多！

**Gamma 分布 $\Gamma(k, \lambda)$（$k$ 为整数）**：

$\Gamma(k, \lambda)$ 可以理解为 $k$ 个独立 $\mathcal{E}(\lambda)$ 随机变量之和。由线性性：

$$E(X) = k \cdot \frac{1}{\lambda} = \frac{k}{\lambda}$$

---

### 8.2 质量抽查（例 2.4）

$N$ 件产品中有 $M$ 件正品，从中无放回取 $n$ 件，期望抽到几件正品？

设 $X$ 是抽到正品的件数，$X$ 服从超几何分布，直接用定义计算 $E(X)$ 非常复杂。

**用线性性的技巧**：记 $X_k$ 为"第 $k$ 次抽到的是否为正品"（$k = 1, \ldots, n$），则 $X = X_1 + \cdots + X_n$。

由对称性（无放回抽取时每件产品被抽到的概率相同），

$$E(X_k) = \mathbb{P}(\text{第 } k \text{ 次抽到正品}) = \frac{M}{N}$$

由线性性：

$$E(X) = \sum_{k=1}^{n} E(X_k) = n \cdot \frac{M}{N}$$

**结论**：从 $N$ 件产品中无放回取 $n$ 件，期望抽到正品 $\frac{nM}{N}$ 件，这与按比例缩放的直觉完全一致。

---

### 8.3 机器人打字问题（例 2.5）

一个机器人在只有 26 个小写字母的键盘上打字，每次独立等可能地选择一个字母。要打出 $k$ 个不同的字母，期望打字多少次？

**思路**：设 $S_k$ 为打出第 $k$ 个新字母时的总打字次数（$S_0 = 0$）。令 $X_k = S_k - S_{k-1}$ 为等待第 $k$ 个新字母的次数。

在已出现 $k-1$ 个不同字母后，还有 $N - (k-1) = N - k + 1$ 个新字母（$N = 26$），所以下一次打字打到新字母的概率为 $p_k = \frac{N - k + 1}{N}$。

$X_k$ 服从几何分布 $G(p_k)$，期望为 $E(X_k) = \frac{1}{p_k} = \frac{N}{N-k+1}$。

由线性性：

$$E(S_k) = \sum_{j=1}^{k} E(X_j) = \sum_{j=1}^{k} \frac{N}{N-j+1} = N\sum_{j=N-k+1}^{N} \frac{1}{j} \approx N \ln\frac{N+1}{N-k+1}$$

**特殊情况**：

- 打出全部 $N = 26$ 个字母：$E(S_N) \approx N \ln(N+1) \approx 26 \times 3.26 \approx 84.8$ 次。
- 打出前一半（13 个不同字母）：$E(S_{N/2}) \approx N \ln 2 \approx 26 \times 0.693 \approx 18$ 次。

**结论**：打出前一半字母相对容易，而要凑齐全部字母则需要多得多的次数（因为越到后面，每次碰巧打出新字母的概率越小）。

---

### 8.4 金融投资例

某公司可选择 A、B 两家银行的三款投资产品（对应各自独立的项目）：

|      | 产品一(获利/概率)  | 产品二(获利/概率)  | 产品三(获利/概率)  |
| ---- | ----------- | ----------- | ----------- |
| A 银行 | 281 万 / 67% | 236 万 / 10% | 259 万 / 23% |
| B 银行 | 283 万 / 66% | 242 万 / 15% | 260 万 / 19% |

（各产品只有获利或零两种结果）

**A 银行总获利** $X = X_1 + X_2 + X_3$：

$$EX = 281 \times 0.67 + 236 \times 0.10 + 259 \times 0.23 = 271.44 \text{ 万元}$$

**B 银行总获利** $Y = Y_1 + Y_2 + Y_3$：

$$EY = 283 \times 0.66 + 242 \times 0.15 + 260 \times 0.19 = 271 \text{ 万元}$$

**结论**：A 银行期望获利略高，应选择 A 银行。

---

## 九、高阶矩

### 9.1 定义

> [!INFO] 定义 2.1（矩，Moment）
> 
> 设 $X$ 是随机变量，$m$ 是正整数。若 $E(|X|^m) < \infty$，则：
> 
> - 称 $E(X^m)$ 为 $X$ 的 **$m$ 阶原点矩**
> - 称 $E(X - EX)^m$ 为 $X$ 的 **$m$ 阶中心矩**
> 
> 当 $m > 2$ 时，统称为**高阶矩**。

**各阶矩的含义：**

- **$m = 1$ 阶原点矩**：$E(X)$，即均值/期望。
- **$m = 2$ 阶中心矩**：$E(X - EX)^2 = Var(X)$，即**方差**（衡量随机变量的离散程度）。
- **$m = 3$ 阶中心矩（标准化后）**——**偏度（Skewness）**：

$$\text{Skewness} = \frac{E(X - EX)^3}{[E(X-EX)^2]^{3/2}}$$

偏度衡量分布的**不对称程度**。偏度为负（左偏）、零（对称）、正（右偏）分别对应分布左侧尾巴长、两侧对称、右侧尾巴长的情形。

- **$m = 4$ 阶中心矩（标准化后）**——**峰度（Kurtosis）**：

$$\text{Kurtosis} = \frac{E(X - EX)^4}{[E(X-EX)^2]^2} - 3$$

峰度衡量分布**尾部的厚重程度**，减 3 是为了让正态分布的峰度为 0（作为基准）。峰度大于 0（尖峰厚尾）、等于 0（正态）、小于 0（平峰薄尾）。

---

## 十、期望的补充性质

### 10.1 例 2.7：$E|X| = 0$ 则 $X = 0$（几乎处处）

这说明：如果一个非负随机变量的期望为 0，则它几乎处处等于 0。

**证明**：对任意正整数 $n$，

$$\mathbb{P}\left(|X| > \frac{1}{n}\right) = \mathbb{P}(n|X| > 1) = E\left[I_{{n|X|>1}}\right] \leq E\left[n|X| \cdot I_{{n|X|>1}}\right] \leq n E|X| = 0$$

由概率的连续性，

$$\mathbb{P}(|X| > 0) = \mathbb{P}\lbrace(\bigcup_{n=1}^{\infty}\lbrace{|X| > \frac{1}{n}\rbrace}\rbrace) = \lim_{n\to\infty} \mathbb{P}\lbrace(|X| > \frac{1}{n}\rbrace) = 0$$

因此 $\mathbb{P}(X = 0) = 1 - \mathbb{P}(|X| > 0) = 1$。

### 10.2 例 2.6：Cauchy 分布的期望不存在

设 $X, Y \sim \mathcal{N}(0,1)$ 且相互独立，则 $T = X/Y$ 服从 $t_1$（即 Cauchy）分布。

注意：**不能**因为 $EX = EY = 0$ 就认为 $E(X/Y) = 0/0$ 不存在！

期望的性质 $E(XY) = (EX)(EY)$（独立时）要求 $X, Y$ 独立，但 $\frac{X}{Y}$ 是 $X, Y$ 的函数，不能套用。

实际上直接计算：

$$E|T| = \int_{-\infty}^{\infty} |t| \cdot \frac{1}{\pi(1+t^2)},dt = \frac{2}{\pi} \int_0^{\infty} \frac{t}{1+t^2},dt = \frac{1}{\pi} \left[\ln(1+t^2)\right]_0^{\infty} = +\infty$$

所以 Cauchy 分布的期望**不存在**（积分发散）。这是一个反直觉的例子：分布关于 0 对称，直觉上"均值应该是 0"，但期望在数学意义上不存在。

---

## 十一、几个重要例题

### 例 2.2：$X \sim \mathcal{N}(0,1)$，计算 $E(|X|^{\alpha})$

$X$ 的密度为 $\varphi(x) = \frac{1}{\sqrt{2\pi}} e^{-x^2/2}$。对 $\alpha > -1$：

$$E(|X|^{\alpha}) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{\infty} |x|^{\alpha} e^{-x^2/2},dx = \sqrt{\frac{2^{\alpha}}{\pi}} \cdot \Gamma!\left(\frac{\alpha+1}{2}\right)$$

（利用换元 $x = \sqrt{2t}$，然后利用 Gamma 函数的定义化简。）

**特别地**：

- $\alpha = 2$：$E(X^2) = 1$（标准正态的二阶矩为 1）
- $\alpha = 1$：$E|X| = \sqrt{2/\pi}$
- $\alpha \leq -1$：$E(|X|^{\alpha}) = +\infty$（期望不存在）

注意：$\Gamma(1/2) = \sqrt{\pi}$ 是一个常用结论。

### 例 2.3：$(X,Y)$ 在单位圆内均匀分布，求 $E(X)$，$E(Y)$

$(X,Y)$ 的联合密度为 $f(x,y) = \frac{1}{\pi} I_D$，其中 $D = {(x,y) : x^2 + y^2 \leq 1}$。

$$E(X) = \frac{1}{\pi} \int_{-1}^{1} \left(\int_{-\sqrt{1-y^2}}^{\sqrt{1-y^2}} x,dx\right) dy = \frac{1}{\pi} \int_{-1}^{1} 0,dy = 0$$

**直观**：单位圆关于 $y$ 轴对称，$x$ 的"质心"当然在 0；同理 $E(Y) = 0$。

---

## 十二、本讲知识框架总结

**一、期望的定义**

- 离散：$E(X) = \sum_j x_j \mathbb{P}(X = x_j)$（需绝对收敛）
- 连续：$E(X) = \int_{-\infty}^{\infty} x f(x),dx$（需绝对可积）
- 一般：$E(X) = \int_{\mathbb{R}} x,dF(x)$（了解）

**二、直观含义**：加权平均值 = 分布的质心

**三、常见分布的期望**

| 分布                             | 参数             | 期望             |
| ------------------------------ | -------------- | -------------- |
| 两点分布 $B(1,p)$                  | $p$            | $p$            |
| 二项分布 $B(n,p)$                  | $n,p$          | $np$           |
| Poisson $\mathcal{P}(\lambda)$ | $\lambda$      | $\lambda$      |
| 几何分布 $G(p)$                    | $p$            | $1/p$          |
| 均匀分布 $U(a,b)$                  | $a,b$          | $(a+b)/2$      |
| 指数分布 $\mathcal{E}(\lambda)$    | $\lambda$      | $1/\lambda$    |
| Gamma $\Gamma(\alpha,\beta)$   | $\alpha,\beta$ | $\alpha/\beta$ |
| 正态 $\mathcal{N}(\mu,\sigma^2)$ | $\mu,\sigma^2$ | $\mu$          |

**四、LOTUS 定理**：$E(g(X)) = \int g(x) f(x),dx$，无需先求 $g(X)$ 的分布。

**五、重要性质**：线性性（最常用）、单调性、独立则乘积拆分。

**六、优化解释**：$E(X)$ 是 $L^2$ 损失下最优预测；中位数是 $L^1$ 损失下最优预测。

**七、高阶矩**：方差（2 阶）、偏度（3 阶标准化）、峰度（4 阶标准化）。




---


> [!ABSTRACT] 方差、标准化与不等式

---

## 一、方差（Variance）

### 1.1 定义

**定义 3.1**：若随机变量 $X$ 的期望 $\mu = EX$ 有限，则定义 $X$ 的**方差**为：

$$\text{var}(X) = E(X - \mu)^2$$

记作 $\text{var}(X)$ 或 $\sigma_X^2$。当 $\text{var}(X) < \infty$ 时，称 $X$ 的方差有限。

> **直观理解**：方差衡量随机变量 $X$ 在其期望附近的"分散程度"。方差越小，$X$ 的取值越集中在均值附近；方差越大，取值越分散。

### 1.2 计算公式（两种等价形式）

|形式|公式|适用场景|
|---|---|---|
|定义式|$\text{var}(X) = E(X - EX)^2$|理论推导、证明|
|**展开式**（常用）|$\text{var}(X) = E(X^2) - (EX)^2$|**实际计算首选**|

**展开式推导**（补充课件未注明的步骤）：

$$\text{var}(X) = E(X-\mu)^2 = E(X^2 - 2\mu X + \mu^2) = EX^2 - 2\mu \cdot EX + \mu^2 = EX^2 - \mu^2$$

即 $\text{var}(X) = E(X^2) - (EX)^2$。

> **解题策略**：计算方差时，先分别算 $E(X^2)$ 和 $(EX)^2$，再相减。

---

## 二、常见分布的方差（重点记忆）

### 2.1 两点分布 $B(1, p)$

$X \sim B(1,p)$，即 $P(X=1)=p,\ P(X=0)=q=1-p$。

**关键观察**：$X$ 只取 0 和 1，故 $X^2 = X$，因此 $E(X^2) = EX = p$。

$$\text{var}(X) = E(X^2) - (EX)^2 = p - p^2 = p(1-p) = pq$$

### 2.2 二项分布 $B(n, p)$

$X \sim B(n,p)$。将 $X = X_1 + X_2 + \cdots + X_n$（$n$ 个独立两点分布之和），利用方差的可加性（见定理 3.1 性质 4）：

$$\text{var}(X) = n \cdot \text{var}(X_i) = npq$$

### 2.3 Poisson 分布 $\mathcal{P}(\lambda)$

$X \sim \mathcal{P}(\lambda)$，即 $P(X=k) = \frac{\lambda^k}{k!}e^{-\lambda}$，$k=0,1,\ldots$

**计算技巧**：利用分解 $X^2 = X(X-1) + X$，可以把二阶矩转化为"阶乘矩"：

$$E(X^2) = E[X(X-1)] + EX$$

计算 $E[X(X-1)]$：

$$E[X(X-1)] = \sum_{k=0}^{\infty} k(k-1) \frac{\lambda^k}{k!}e^{-\lambda} = \lambda^2 \sum_{k=2}^{\infty} \frac{\lambda^{k-2}}{(k-2)!}e^{-\lambda} = \lambda^2$$

（最后一步利用 Poisson 分布的归一性：$\sum_{j=0}^{\infty}\frac{\lambda^j}{j!}e^{-\lambda}=1$）

故 $E(X^2) = \lambda^2 + \lambda$，因此：

$$\text{var}(X) = \lambda^2 + \lambda - \lambda^2 = \lambda$$

> **Poisson 分布的特点**：均值 = 方差 = $\lambda$。

### 2.4 几何分布 $G(p)$

$X \sim G(p)$，即 $P(X=k) = p(1-p)^{k-1}$，$k=1,2,\ldots$，其中 $q=1-p$。

已知 $EX = \frac{1}{p}$。同样利用 $E(X^2) = E[X(X-1)] + EX$：

$$E[X(X-1)] = \sum_{j=1}^{\infty} j(j-1)pq^{j-1} = pq \cdot \left(\sum_{j=0}^{\infty} q^j\right)''$$

对等比级数 $\frac{1}{1-q}$ 求两次导数（关于 $q$），得 $\left(\frac{1}{1-q}\right)'' = \frac{2}{(1-q)^3} = \frac{2}{p^3}$。

故 $E[X(X-1)] = pq \cdot \frac{2}{p^3} = \frac{2q}{p^2}$，从而 $E(X^2) = \frac{2q}{p^2} + \frac{1}{p}$。

$$\text{var}(X) = \frac{2q}{p^2} + \frac{1}{p} - \frac{1}{p^2} = \frac{2q - 1}{p^2} + \frac{1}{p} = \frac{q}{p^2}$$

### 2.5 均匀分布 $U(a, b)$

$X \sim U(a,b)$，密度 $f(x) = \frac{1}{b-a} \mathbf{1}_{(a,b)}(x)$。已知 $EX = \frac{a+b}{2}$。

$$E(X^2) = \int_a^b \frac{x^2}{b-a}dx = \frac{b^3-a^3}{3(b-a)} = \frac{a^2+ab+b^2}{3}$$

（利用因式分解 $b^3-a^3=(b-a)(b^2+ab+a^2)$）

$$\text{var}(X) = \frac{a^2+ab+b^2}{3} - \left(\frac{a+b}{2}\right)^2 = \frac{(b-a)^2}{12}$$

### 2.6 指数分布 $\varepsilon(\lambda)$

$X \sim \varepsilon(\lambda)$，密度 $f(x) = \lambda e^{-\lambda x}$，$x>0$。已知 $EX = \frac{1}{\lambda}$。

$$E(X^2) = \int_0^\infty x^2 \lambda e^{-\lambda x}dx = \frac{1}{\lambda^2}\Gamma(3) = \frac{2}{\lambda^2}$$

（利用 Gamma 函数：$\int_0^\infty t^{n-1}e^{-t}dt = \Gamma(n)$；令 $t=\lambda x$，$\Gamma(3)=2!=2$）

$$\text{var}(X) = \frac{2}{\lambda^2} - \frac{1}{\lambda^2} = \frac{1}{\lambda^2}$$

### 2.7 正态分布 $\mathcal{N}(\mu, \sigma^2)$

$X \sim \mathcal{N}(\mu,\sigma^2)$，密度 $f(x) = \frac{1}{\sigma\sqrt{2\pi}}\exp!\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$。

$$\text{var}(X) = \int_{-\infty}^\infty (x-\mu)^2 f(x)dx$$

令 $t = \frac{x-\mu}{\sigma}$（换元），得：

$$\text{var}(X) = \frac{\sigma^2}{\sqrt{2\pi}}\int_{-\infty}^\infty t^2 e^{-t^2/2}dt = \sigma^2$$

（最后一步利用标准正态的归一化性质：$\frac{1}{\sqrt{2\pi}}\int t^2 e^{-t^2/2}dt = 1$，可由分部积分或 Gamma 函数验证）

### 2.8 Gamma 分布 $\Gamma(\alpha, \beta)$

$X \sim \Gamma(\alpha,\beta)$，密度 $f(x) = \frac{\beta^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\beta x}$，$x>0$。已知 $EX = \frac{\alpha}{\beta}$。

令 $t=\beta x$ 换元，利用 $\Gamma$ 函数的递推关系 $\Gamma(\alpha+1)=\alpha\Gamma(\alpha)$：

$$E(X^2) = \frac{\Gamma(\alpha+2)}{\beta^2\Gamma(\alpha)} = \frac{(\alpha+1)\alpha}{\beta^2}$$

$$\text{var}(X) = \frac{\alpha(\alpha+1)}{\beta^2} - \left(\frac{\alpha}{\beta}\right)^2 = \frac{\alpha}{\beta^2}$$

### 常见分布方差汇总表

|分布|参数|期望|方差|
|---|---|---|---|
|$B(1,p)$|$p$|$p$|$pq$|
|$B(n,p)$|$n,p$|$np$|$npq$|
|$\mathcal{P}(\lambda)$|$\lambda$|$\lambda$|$\lambda$|
|$G(p)$|$p$|$1/p$|$q/p^2$|
|$U(a,b)$|$a,b$|$(a+b)/2$|$(b-a)^2/12$|
|$\varepsilon(\lambda)$|$\lambda$|$1/\lambda$|$1/\lambda^2$|
|$\mathcal{N}(\mu,\sigma^2)$|$\mu,\sigma^2$|$\mu$|$\sigma^2$|
|$\Gamma(\alpha,\beta)$|$\alpha,\beta$|$\alpha/\beta$|$\alpha/\beta^2$|

---

## 三、方差的性质（定理 3.1）⭐ 要求掌握证明

设 $EX = \mu$，$\text{var}(X) < \infty$，则：

**性质 1（线性变换）**：$\text{var}(aX+b) = a^2\text{var}(X)$，$\forall a,b \in \mathbb{R}$

> **证明**：$\text{var}(aX+b) = E[(aX+b - E(aX+b))^2] = E[(aX+b-a\mu-b)^2] = a^2E[(X-\mu)^2] = a^2\text{var}(X)$。注意常数 $b$ 对方差无影响，只有系数 $a$ 影响方差（且取平方）。

**性质 2（最小性）**：$\text{var}(X) = E(X-\mu)^2 \leq E(X-c)^2$，$\forall c \in \mathbb{R}$

> **理解**：期望是使均方误差最小的预测值。即在所有常数中，用均值 $\mu$ 来"预测" $X$ 的均方误差最小。

**性质 3（零方差的含义）**：$\text{var}(X) = 0 \iff X = \mu \text{ a.s.}$

> **理解**：方差为零意味着 $X$ 几乎处处等于常数（其期望），即 $X$ 是退化的随机变量。

**性质 4（独立变量之和）**：若 $X_1, \ldots, X_n$ 相互独立，则

$$\text{var}!\left(\sum_{k=1}^n X_k\right) = \sum_{k=1}^n \text{var}(X_k)$$

> **注意**：此性质**要求独立**！不独立时需要引入协方差修正项（后续课程内容）。

> **性质 4 证明思路**：利用独立性 $\Rightarrow$ $E(X_iX_j) = EX_i \cdot EX_j$（$i\neq j$），展开 $\text{var}(\sum X_k)$ 后交叉项全消。

---

## 四、应用例：配对问题（示范指示函数法）

**题目**：某人写了 $n$ 封信，随机装入 $n$ 个信封（随机排列），记 $X$ 为正确匹配的封数。求 $EX$ 和 $\text{var}(X)$。

**方法：指示函数分解**（标准做法）

令 $X_i = \mathbf{1}_{{\text{第}i\text{封信正确匹配}}}$，则 $X = \sum_{i=1}^n X_i$。

**求 $EX$**：$P(X_i = 1) = \frac{1}{n}$，故 $EX_i = \frac{1}{n}$，由线性性 $EX = n \cdot \frac{1}{n} = 1$。

**求 $\text{var}(X)$**：注意 $X_i$ 不独立，需用展开式：

$$\text{var}(X) = E(X^2) - (EX)^2$$

先求 $E(X^2) = E!\left(\sum_i X_i\right)^2 = \sum_i E(X_i^2) + \sum_{i\neq j} E(X_iX_j)$。

- $E(X_i^2) = E(X_i) = \frac{1}{n}$（因为 $X_i^2 = X_i$ 是指示变量）
- $E(X_iX_j) = P(X_i=1, X_j=1) = P(\text{第}i\text{和}j\text{均正确}) = \frac{1}{n} \cdot \frac{1}{n-1} = \frac{1}{n(n-1)}$

$$E(X^2) = n \cdot \frac{1}{n} + n(n-1) \cdot \frac{1}{n(n-1)} = 1 + 1 = 2$$

$$\text{var}(X) = 2 - 1^2 = 1$$

> **结论**：无论 $n$ 多大，正确匹配数的均值恒为 1，方差也恒为 1。

---

## 五、标准差与标准化

### 5.1 标准差（定义 3.2）

$$\sigma_X = \sqrt{\text{var}(X)}$$

称为 $X$ 的**标准差**（Standard deviation）。标准差与 $X$ 量纲相同，比方差更直观。

例：若 $X \sim \mathcal{N}(\mu, \sigma^2)$，则标准差恰为参数 $\sigma$。

### 5.2 标准化（定义 3.3）

设 $\text{var}(X) < \infty$，令：

$$Y = \frac{X - EX}{\sqrt{\text{var}(X)}}$$

则 $EY = 0$，$\text{var}(Y) = 1$。称 $Y$ 为 $X$ 的**标准化**（Standardization）。

**验证**（课件未列出的步骤）：

- $EY = \frac{EX - EX}{\sqrt{\text{var}(X)}} = 0$（用期望线性性）
- $\text{var}(Y) = \text{var}!\left(\frac{X}{\sqrt{\text{var}(X)}}\right) = \frac{1}{\text{var}(X)}\text{var}(X) = 1$（用方差性质 1）

**特例**：$X \sim \mathcal{N}(\mu, \sigma^2)$ 时，$Y = \frac{X-\mu}{\sigma} \sim \mathcal{N}(0,1)$（标准正态）。

### 5.3 标准化的意义：提供可比性

不同量纲、不同尺度的随机变量，经标准化后均转化为均值 0、方差 1 的变量，从而可以在同一尺度下比较其相对位置。

> **例**：两个班级考试，甲班均值 50 分，乙班均值 65 分。某学生在甲班考了 65 分，另一学生在乙班考了 70 分，直接比分数不合理；标准化后才能客观比较各自在班级中的相对水平。

---

## 六、高阶矩：偏度与峰度（了解）

方差是二阶中心矩，更高阶矩刻画分布形状的更精细特征：

**偏度（Skewness，$m=3$）**：

$$\text{Skewness} = \frac{E(X-EX)^3}{[E(X-EX)^2]^{3/2}} = E\left[\left(\frac{X-\mu}{\sigma}\right)^3\right]$$

- 偏度 $> 0$：右偏（右尾长）
- 偏度 $= 0$：对称
- 偏度 $< 0$：左偏（左尾长）

**峰度（Kurtosis，$m=4$）**：

$$\text{Kurtosis} = \frac{E(X-EX)^4}{[E(X-EX)^2]^2} - 3 = E\left[\left(\frac{X-\mu}{\sigma}\right)^4\right] - 3$$

- 减 3 是为了使正态分布峰度为 0（以正态为基准）
- 峰度 $> 0$：比正态更"尖峰厚尾"
- 峰度 $< 0$：比正态更"平坦"

---

## 七、不等式

### 7.1 Markov 不等式（定理 4.1）

**结论**：对随机变量 $X$ 和 $\varepsilon > 0$，有

$$P(|X| \geq \varepsilon) \leq \frac{E|X|^\alpha}{\varepsilon^\alpha}, \quad \alpha > 0$$

**证明**（理解思路）：

$$P(|X| \geq \varepsilon) = E\mathbf{1}_{{|X|\geq\varepsilon}} = E\mathbf{1}_{{|X|^\alpha \geq \varepsilon^\alpha}} \leq E\left[\frac{|X|^\alpha}{\varepsilon^\alpha}\mathbf{1}_{{|X|^\alpha \geq \varepsilon^\alpha}}\right] \leq E\frac{|X|^\alpha}{\varepsilon^\alpha} = \frac{E|X|^\alpha}{\varepsilon^\alpha}$$

关键步骤：在集合 ${|X|^\alpha \geq \varepsilon^\alpha}$ 上，有 $1 \leq \frac{|X|^\alpha}{\varepsilon^\alpha}$，故第一个不等号成立；去掉指示函数只会变大，故第二个不等号成立。

> **直觉**：知道均值有限，就能控制大偏差的概率。

### 7.2 Chebyshev 不等式（推论 4.1）

Markov 不等式取 $\alpha=2$，令 $X \leftarrow X - EX$：

$$P(|X - EX| \geq \varepsilon) \leq \frac{\text{var}(X)}{\varepsilon^2}$$

> **意义**：**定量刻画 $X$ 在均值附近的集中程度**。方差越小，$X$ 偏离均值超过 $\varepsilon$ 的概率越小。

**应用场景**：

- 在不知道分布的具体形式时，只需知道均值和方差，就可以估计尾概率
- 是大数定律的证明工具

**解题模板**：已知 $EX$ 和 $\text{var}(X)$，求 $P(|X - EX| \geq \varepsilon)$ 的上界，直接套 Chebyshev 不等式。

### 7.3 内积不等式（Cauchy-Schwarz 不等式，定理 4.2）

**结论**：若 $EX^2 < \infty$ 且 $EY^2 < \infty$，则

$$|E(XY)| \leq \sqrt{EX^2 \cdot EY^2}$$

等号成立 $\iff$ 存在不全为零的常数 $a,b$ 使得 $aX + bY = 0$ a.s.（即 $X$ 与 $Y$ 成比例）。

**证明思路**：构造关于实参数 $(a,b)$ 的二次型：

$$E(aX+bY)^2 = a^2EX^2 + 2abE(XY) + b^2EY^2 = (a,b)\Sigma(a,b)^T \geq 0$$

其中 $\Sigma = \begin{pmatrix}EX^2 & E(XY)\ E(XY) & EY^2\end{pmatrix}$。$\Sigma$ 非负定 $\Rightarrow$ $\det(\Sigma) \geq 0$ $\Rightarrow$ $EX^2 \cdot EY^2 - [E(XY)]^2 \geq 0$，即得结论。

等号成立时 $\det(\Sigma)=0$，意味着 $E(aX+bY)^2=0$，即 $aX+bY=0$ a.s.。

### 7.4 Jensen 不等式（定理 4.3）

**结论**：设 $\psi$ 是 $\mathbb{R}$ 上的**凸函数**，且 $X$ 和 $\psi(X)$ 都有有限期望，则

$$\psi(EX) \leq E[\psi(X)]$$

对于严格凸的 $\psi$，等号成立当且仅当 $X = EX$ a.s.。

**证明思路**：凸函数有性质：对任意点 $a$，存在切线斜率 $c = \psi'_r(a)$（右导数），使得

$$\psi(b) - \psi(a) \geq c(b-a), \quad \forall b$$

令 $a = EX$，$b = X$（$b$ 是随机变量）：

$$\psi(X) - \psi(EX) \geq c(X - EX)$$

两边取期望：$E[\psi(X)] - \psi(EX) \geq cE(X-EX) = 0$，得证。

**常见应用**：

|凸函数 $\psi$|Jensen 不等式的含义|
|---|---|
|$\psi(x) = x^2$|$(EX)^2 \leq EX^2$，即 $\text{var}(X) \geq 0$|
|$\psi(x) = e^x$|$e^{EX} \leq Ee^X$|
|$\psi(x) = -\ln x$|$-\ln(EX) \leq E(-\ln X)$，即 $\ln(EX) \geq E\ln X$|
|$\psi(x) =|x|

**重要应用**：EM 算法（其中利用 $\ln$ 的凹性）；证明最大似然估计（MLE）的一致性。

---

## 八、本讲小结与解题策略

### 8.1 期望小结（课件 P58 重点）

|知识点|内容|
|---|---|
|定义|离散：$\sum x_i p_i$；连续：$\int x f(x)dx$|
|线性性|$E(c+aX+bY) = c + aEX + bEY$|
|乘法性|$X,Y$ 独立 $\Rightarrow$ $E(XY) = EXEY$|
|解读|代数平均 / 物理质心 / 最优预测|
|计算技巧|归一性（分布归一）、对称性（关于均值对称时高次奇数阶矩为零）|

### 8.2 方差计算策略

遇到"求 $\text{var}(X)$"类题目，按以下步骤：

1. **展开式优先**：计算 $E(X^2)$ 和 $(EX)^2$，作差
2. **计算 $E(X^2)$ 的技巧**：
    - 离散型：直接求和 $\sum x_i^2 p_i$
    - 连续型：直接积分 $\int x^2 f(x)dx$
    - 若 $X$ 只取 0/1（指示变量），利用 $X^2=X$
    - 若分布复杂，用 $E[X(X-1)] + EX$ 分解
3. **独立变量之和**：各方差相加（前提：独立！）
4. **不独立时**（如配对问题）：用指示变量分解，展开 $E(X^2)$

### 8.3 不等式应用策略

|题型|使用不等式|
|---|---|
|已知期望，求尾概率上界 $P(X \geq a)$|Markov 不等式|
|已知均值和方差，求 $P(\|X-\mu\| \geq \varepsilon)$ 上界|Chebyshev 不等式|
|证明 $\|E(XY)\| \leq \sqrt{EX^2 \cdot EY^2}$|Cauchy-Schwarz（内积不等式）|
|凸函数与期望的大小关系|Jensen 不等式|
|证明 $\text{var}(X) \geq 0$|Jensen（$\psi=x^2$ 是凸函数）|

### 8.4 标准化的用途

- **统一尺度**：不同分布的随机变量标准化后均为均值 0、方差 1，可直接比较
- **正态分布查表**：$X \sim \mathcal{N}(\mu,\sigma^2)$ 的概率计算，先标准化为 $\mathcal{N}(0,1)$ 再查表
- **理论基础**：中心极限定理的表述需要用到标准化