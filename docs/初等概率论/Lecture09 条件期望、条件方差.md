---
title: "Lecture09 条件期望、条件方差"
tags:
  - 概率论
  - 后半学期
  - 条件期望
  - 条件方差
  - 全期望定理
---

# Lecture09 条件期望、条件方差

## 引言：为什么需要条件期望？

已知全体人群的平均身高是 $EX$（期望）。当已知某人足长为 25cm，或已知某人能翻墙时，我们想在**给定该信息下**重新总结身高的数字特征——这就是**条件期望**。

核心问题：**给定信息下，如何定义一个数字特征来总结一个随机变量？**

---

## 一、条件概率回顾

### 1.1 几种定义

**$P(A|B)$**（Lecture 2 已学）：$P(A|B) = \frac{P(A\cap B)}{P(B)}$

**$P(X|A)$**（Ch2.6, Ch3.5 已学）：

- 离散：$p_{X|A}(x) = P(X=x|A) = \frac{P({X=x}\cap A)}{P(A)}$
- 连续：$P(X\in B|A) = \int_B f_{X|A}(x)dx$，其中 $f_{X|A}(x)\geq 0$

**$P(X|Y)$**（Lecture 6 已学）：

- 离散：$P(X=x_i|Y=y_j) = \frac{P(X=x_i,Y=y_j)}{P(Y=y_j)} = \frac{p_{ij}}{q_j}$
- 连续：$f_{X|Y}(x|y) = \frac{f(x,y)}{f_Y(y)} = \frac{f(x,y)}{\int_{-\infty}^\infty f(x,y)dx}$，$x\in\mathbb{R}$

**$P(A|X)$**（选修，不要求了解）：令 $g(x) = P(A|X=x)$，则 $g(X)$ 是事件 $A$ 关于 $X$ 的条件概率（随机变量）。

### 1.2 乘法法则

条件概率定义的等价写法，将条件概率和联合概率相互转化：

- $P(A|B)$：$P(A\cap B) = P(B|A)P(A)$
- $P(X|A)$：
    - 离散：$P({X=x_i}\cap A) = P(X=x_i|A)\cdot P(A)$
    - 连续：$f_X(x)\cdot I_A(x) = f_{X|{X\in A}}(x)\cdot P(X\in A)$
- $P(X|Y)$：
    - 离散：$P(X=x_i, Y=y_j) = P(X=x_i|Y=y_j)\cdot P(Y=y_j)$
    - 连续：$f(x,y) = f_{X|Y}(x|y)\cdot f_Y(y)$

### 1.3 全概率公式 ⭐（本节需重点掌握）

设 $A_1,\ldots,A_n$ 构成 $\Omega$ 的一个**分割**（互不相交，并为全集）：

**$P(A|B)$** 的全概率：$P(B) = \sum_{i=1}^n P(B|A_i)P(A_i)$

**$P(X|A)$** 的全概率（将边缘分布表示为条件分布的加权平均）：

- 离散：$p_X(x) = \sum_{i=1}^n p_{X|A_i}(x)\cdot P(A_i)$
- 连续：$f_X(x) = \sum_{i=1}^n f_{X|A_i}(x)\cdot P(A_i)$

**$P(X|Y)$** 的全概率（对 $Y$ 的所有取值求和/积分还原边缘分布）：

- 离散：$p_X(x) = \sum_y p_{X|Y}(x|y)\cdot P_Y(y)$
- 连续：$f_X(x) = \int f_{X|Y}(x|y)\cdot f_Y(y)dy$

> **直觉**：把所有情形分类，各类情形下的条件分布以概率为权重加权平均，还原无条件分布。

### 1.4 贝叶斯准则

设 $A_1,\ldots,A_n$ 是 $\Omega$ 的分割，$P(B)>0$，$P(A_i)>0$：

$$P(A_i|B) = \frac{P(A_i)P(B|A_i)}{\sum_{j=1}^n P(A_j)P(B|A_j)}, \quad i=1,\ldots,n$$

对于 $P(X|Y)$ 的情形，分四种情况讨论：

**情形 1：$X, Y$ 皆离散**

$$P_{X|Y}(x|y) = \frac{P_{X,Y}(x,y)}{P_Y(y)} = \frac{P_X(x)P_{Y|X}(y|x)}{P_Y(y)}$$

其中分母 $P_Y(y) = \sum_x P_X(x)P_{Y|X}(y|x)$（全概率公式）

> 例：$X=1,0$ 表示飞机是否出现；$Y=1,0$ 表示雷达是否报警。已知雷达报警概率，反推飞机出现概率。

**情形 2：$(X,Y)$ 皆连续**

$$f_{X|Y}(x|y) = \frac{f_{X,Y}(x,y)}{f_Y(y)} = \frac{f_X(x)f_{Y|X}(y|x)}{f_Y(y)}$$

其中分母 $f_Y(y) = \int f_X(x)f_{Y|X}(y|x),dx$

> 例：$X$ 是连续信号，$Y$ 是对 $X$ 的含噪声测量，$f_{Y|X}(y|x)$ 是有噪声的连续型模型。

**情形 3：$X$ 离散，$Y$ 连续**

$$P_{X|Y}(x|y) = \frac{P_X(x)f_{Y|X}(y|x)}{f_Y(y)}$$

其中分母 $f_Y(y) = \sum_x P_X(x)f_{Y|X}(y|x)$

> 例：$X$ 是否感染某疾病（离散），$Y$ 是血液中白细胞浓度（连续），$f_{Y|X}(y|x)$ 是给定患病与否时白细胞浓度的分布模型。

**情形 4：$X$ 连续，$Y$ 离散**

$$f_{X|Y}(x|y) = \frac{f_X(x)P_{Y|X}(y|x)}{P_Y(y)}$$

其中分母 $P_Y(y) = \int f_X(x)P_{Y|X}(y|x),dx$

> 例：$X$ 是身高（连续），$Y$ 是鞋码（离散），$P_{Y|X}(y|x)$ 是用身高预测鞋码的模型。

> **记忆结构（四种情形统一规律）**：  
> 分子 = 先验（$X$ 的边缘）× 似然（$Y|X$ 的条件）  
> 分母 = 对 $X$ 求和或积分（对应离散或连续），即全概率公式

---

## 二、条件期望 $E(X|A)$ 的定义

### 2.1 定义

$E(X|A)$ 的定义完全类比普通期望的定义，只需把概率换成**条件概率**：

**普通期望 → 条件期望**（离散型）：

**存在条件：**
- 无条件：$\sum_i |x_i| P(X=x_i) < \infty$
- 条件：$\sum_i |x_i| P(X=x_i \mid A) < \infty$

**定义：**
- 无条件：$EX = \sum_i x_i P(X=x_i)$
- 条件：$E(X \mid A) = \sum_i x_i P(X=x_i \mid A)$

**普通期望 → 条件期望**（连续型）：

**存在条件：**
- 无条件：$\int_{-\infty}^\infty |x| f_X(x)dx < \infty$
- 条件：$\int_{-\infty}^\infty |x| f_{X\mid A}(x)dx < \infty$

**定义：**
- 无条件：$EX = \int_{-\infty}^\infty xf_X(x)dx$
- 条件：$E(X\mid A) = \int_{-\infty}^\infty xf_{X\mid A}(x)dx$

> **本质**：把条件分布当作普通分布，然后用完全相同的方式求期望。$E(X|A)$ 是一个**数**（常数）。

### 2.2 期望的等价计算公式（Aside，选做内容）

$$\mathbf{E}X = \sum_{k=0}^{\infty} k \cdot P(X=k) = \sum_{k=1}^{\infty} P(X \geq k)$$


把期望想象成一块面积（横轴为 $X$ 的取值，纵轴为概率），有两种切法：

| |竖切（按定义）|横切（尾概率求和）|
|---|---|---|
|**切法**|按 $X$ 的取值分列|按概率大小分层|
|**每块面积**|$P(X=k) \times k$|$1 \times P(X \geq k)$|
|**求和**|$\sum_k k\cdot P(X=k)$|$\sum_{k=1}^\infty P(X\geq k)$|

两种切法面积相同，故结果相等。

**连续型的对应结论**

$$\mathbf{E}X = \int_0^{+\infty} P(X > t), dt$$

原理相同：将面积横切为无穷多薄层，每层宽度为 $P(X>t),dt$。

- **同分布**（不需要独立）就可以直接推出期望相等
---

## 三、由无条件期望获得 $E(X|A)$

### 3.1 核心公式

**定理 2.1**：设 $P(A)>0$，$X$ 是非负随机变量，则

$$\boxed{E(X|A) = \frac{E(XI_A)}{P(A)}}$$

其中 $I_A = \mathbf{1}_A$ 是事件 $A$ 的示性函数（$A$ 发生时为 1，否则为 0）。

**推论 2.1**：设 $P(A)>0$，$E(X|A)$ 存在，则同样有

$$E(X|A) = \frac{E(XI_A)}{P(A)}$$

推论将定理推广到一般（可正可负）的随机变量。推导方法：令 $X^+ = XI_{{X\geq 0}}$（正部），$X^- = -XI_{{X<0}}$（负部），则 $X = X^+ - X^-$，对正负部分别应用定理 2.1，利用线性性合并即可。

> **两个公式的证明本身不要求掌握**，但**公式本身和使用方法**要掌握。

**证明思路理解**（定理 2.1，帮助理解为何成立）：

由于 $E(X|A)$ 是在条件概率 $P_A(\cdot)=P(\cdot|A)$ 下对 $X$ 求期望，利用非负随机变量期望公式 $EX=\int_0^\infty P(X>x)dx$，可得：

$$E(X|A) = \int_0^\infty P(X>x|A)dx = \frac{1}{P(A)}\int_0^\infty P({X>x}\cap A)dx$$

注意 ${X>x}\cap A = {XI_A > x}$（因为 $XI_A > x > 0$ 当且仅当 $X>x$ 且 $A$ 发生），故

$$= \frac{1}{P(A)}\int_0^\infty P(XI_A > x)dx = \frac{E(XI_A)}{P(A)}$$

### 3.2 使用场合

当条件事件 $A$ 是 ${X>a}$、${X<Y}$ 等由不等式定义的集合时，直接写条件密度往往繁琐。此时用定理 2.1 / 推论 2.1，将条件期望转化为无条件期望的积分（分子）除以概率（分母），通常更便捷。

### 3.3 例 2.1：指数分布的截断期望

**题目**：设 $X\sim\varepsilon(\lambda)$，对 $a>0$，证明 $E(X|X>a) = a+\frac{1}{\lambda}$。

**证明（方法一：定理 2.1）**：

$X$ 有密度函数 $f(x)=\lambda e^{-\lambda x}$，$x>0$。$P(X>a) = e^{-\lambda a}$。

$$E(X|X>a) = \frac{E(XI_{{X>a}})}{P(X>a)} = \frac{1}{e^{-\lambda a}}\int_a^\infty x\lambda e^{-\lambda x}dx$$

计算分子（分部积分 $\int_a^\infty x\lambda e^{-\lambda x}dx$，令 $u=x$，$dv=\lambda e^{-\lambda x}dx$）：

$$\int_a^\infty x\lambda e^{-\lambda x}dx = \left[-xe^{-\lambda x}\right]_a^\infty + \int_a^\infty e^{-\lambda x}dx = ae^{-\lambda a} + \frac{1}{\lambda}e^{-\lambda a} = \left(a+\frac{1}{\lambda}\right)e^{-\lambda a}$$

故 $E(X|X>a) = \frac{(a+1/\lambda)e^{-\lambda a}}{e^{-\lambda a}} = a+\frac{1}{\lambda}$。

**证明（方法二：指数分布的无记忆性，更快捷）**：

$$E(X|X>a) = a + E(X-a|X-a>0) = a + EX = a + \frac{1}{\lambda}$$

关键步骤说明：指数分布具有**无记忆性**，在条件 $X>a$ 下，$X-a$ 依然服从 $\varepsilon(\lambda)$，所以 $E(X-a|X>a) = EX = 1/\lambda$。

### 3.4 例 2.2：两个指数分布的截断期望

**题目**：设 $X, Y$ 独立，$X\sim\varepsilon(\lambda)$，$Y\sim\varepsilon(\mu)$，计算 $E(X|X<Y)$。

**解（利用定理 2.1 转化为二重积分）**：

由推论 2.1：

$$E(X|X<Y) = \frac{E(XI_{{X<Y}})}{P(X<Y)}$$

**计算分子**：由于 $X,Y$ 独立，联合密度为 $f(x,y)=\lambda e^{-\lambda x}\cdot\mu e^{-\mu y}$。

$$E(XI_{{X<Y}}) = \int_0^\infty\int_0^\infty xI_{{x<y}}\lambda e^{-\lambda x}\mu e^{-\mu y}dy,dx$$

对内层积分先对 $y$ 从 $x$ 到 $\infty$ 积分（$I_{{x<y}}$ 要求 $y>x$）：

$$= \int_0^\infty x\lambda e^{-\lambda x}\left(\int_x^\infty\mu e^{-\mu y}dy\right)dx = \int_0^\infty x\lambda e^{-\lambda x}\cdot e^{-\mu x}dx = \int_0^\infty x\lambda e^{-(\lambda+\mu)x}dx$$

利用 $\int_0^\infty x e^{-(\lambda+\mu)x}dx = \frac{1}{(\lambda+\mu)^2}$（这是 $\Gamma$ 积分，$\int_0^\infty x^{n-1}e^{-sx}dx = \frac{(n-1)!}{s^n}$，此处 $n=2$），得：

$$E(XI_{{X<Y}}) = \frac{\lambda}{(\lambda+\mu)^2}$$

**计算分母**（标准结论，两独立指数分布中 $X$ 较小的概率）：

$$P(X<Y) = \int_0^\infty\lambda e^{-\lambda x}\left(\int_x^\infty\mu e^{-\mu y}dy\right)dx = \int_0^\infty\lambda e^{-\lambda x}e^{-\mu x}dx = \frac{\lambda}{\lambda+\mu}$$

**最终结果**：

$$E(X|X<Y) = \frac{\lambda/(\lambda+\mu)^2}{\lambda/(\lambda+\mu)} = \frac{1}{\lambda+\mu}$$

---

## 四、全期望定理（定理 2.2）⭐

### 4.1 定理内容

**定理 2.2（全期望定理）**：设 $A_1,\ldots,A_n$ 构成 $\Omega$ 的一个分割，则

$$\boxed{E(X) = \sum_{i=1}^n P(A_i)E(X|A_i)}$$

> **直觉**：将整体期望按情形分类，各类的条件期望以概率为权重加权平均，得回总体期望。是全概率公式对期望的类比。

### 4.2 证明

**离散情形**（利用全概率公式对分布求期望）：

由全概率公式，$p_X(x) = \sum_{i=1}^n p_{X|A_i}(x)P(A_i)$，故

$$EX = \sum_x x,p_X(x) = \sum_x x\sum_{i=1}^n p_{X|A_i}(x)P(A_i) = \sum_{i=1}^n\underbrace{\left(\sum_x x,p_{X|A_i}(x)\right)}_{=E(X|A_i)}P(A_i)$$

交换求和顺序（括号内恰好是条件期望定义），即得 $EX = \sum_{i=1}^n E(X|A_i)P(A_i)$。

**连续情形**（类似，利用全概率公式 $f_X(x) = \sum_i f_{X|A_i}(x)P(A_i)$ 求积分）。

### 4.3 应用例：用全期望定理推导几何分布的期望

**题目**：$X\sim G(p)$，用全期望定理推导 $EX$。

**解**：取分割 $A_1={X=1}$，$A_2={X>1}$，则 $P(A_1)=p$，$P(A_2)=1-p$。

$$EX = E(X|A_1)P(A_1) + E(X|A_2)P(A_2) = 1\times p + E(X|X>1)\times(1-p)$$

利用几何分布的**无记忆性**：在 $X>1$ 的条件下，$X-1$ 仍服从 $G(p)$，故

$$E(X|X>1) = E(X-1|X-1>0) + 1 = EX + 1$$

（第一步把 $X$ 拆成 $(X-1)+1$；第二步用无记忆性 $E(X-1|X>1) = EX$。）

代入方程：

$$EX = p + (EX+1)(1-p) = p + EX(1-p) + (1-p)$$

$$EX - EX(1-p) = 1 \implies EX\cdot p = 1 \implies EX = \frac{1}{p}$$

---

## 五、解题策略总结

### 5.1 贝叶斯公式四情形速查

**$X$ 离散，$Y$ 离散：**

- 公式：$P_{X\mid Y}(x\mid y) = \dfrac{P(X=x, Y=y)}{P(Y=y)}$
- 分母：$P(Y=y) = \sum_x P(X=x, Y=y)$

**$X$ 连续，$Y$ 连续：**

- 公式：$f_{X\mid Y}(x\mid y) = \dfrac{f_{X,Y}(x,y)}{f_Y(y)}$
- 分母：$f_Y(y) = \int_{-\infty}^\infty f_{X,Y}(x,y)dx$

**$X$ 离散，$Y$ 连续：**

- 公式：$P_{X\mid Y}(x\mid y) = \dfrac{f_{Y\mid X}(y\mid x)P(X=x)}{f_Y(y)}$
- 分母：$f_Y(y) = \sum_x f_{Y\mid X}(y\mid x)P(X=x)$

**$X$ 连续，$Y$ 离散：**

- 公式：$f_{X\mid Y}(x\mid y) = \dfrac{P(Y=y\mid X=x)f_X(x)}{P(Y=y)}$
- 分母：$P(Y=y) = \int_{-\infty}^\infty P(Y=y\mid X=x)f_X(x)dx$

### 5.2 计算 $E(X|A)$ 的两条路

**路线一（条件分布定义法）**：适合条件事件结构简单的情形。

1. 写出条件分布 $f_{X|A}$ 或 $p_{X|A}$
2. 按定义直接积分/求和

**路线二（定理 2.1 / 推论 2.1）**：适合条件事件为不等式形式（${X>a}$、${X<Y}$ 等）的情形。

1. 计算分子 $E(XI_A)$（无条件期望，写成积分/求和）
2. 计算分母 $P(A)$
3. 相除得 $E(X|A)$

**何时用无记忆性**：$X$ 是指数分布 $\varepsilon(\lambda)$ 或几何分布 $G(p)$，条件是 ${X>a}$ 或 ${X>k}$：

- 指数：$E(X|X>a) = a + EX = a + \frac{1}{\lambda}$
- 几何：$E(X|X>k) = k + EX = k + \frac{1}{p}$

### 5.3 用全期望定理求 $EX$

适用于能自然分割成若干情形的问题：

1. 找合适分割 $A_1,\ldots,A_n$（常见：按"第一步结果"分割，如 ${X=1}$ vs ${X>1}$）
2. 对每个 $A_i$ 计算 $E(X|A_i)$（常借助无记忆性或对称性）
3. 套公式 $EX = \sum_i P(A_i)E(X|A_i)$
4. 若结果含 $EX$ 本身，则列方程解之

---


> [!ABSTRACT] 条件在随机变量上的条件期望与条件方差

---

## 一、$E(X \mid Y=y)$ 的定义

### 1.1 从普通期望到条件期望

条件期望的定义与普通期望完全类比，只需将所有概率/密度替换为条件概率/条件密度。

|类型|普通期望 $E(X)$|条件期望 $E(X \mid Y=y)$|
|---|---|---|
|**离散型**（定义 2.2）|若 $\sum_i \|x_i\| \mathbb{P}(X=x_i) < \infty$，则 $E(X)=\sum_i x_i \mathbb{P}(X=x_i)$|若 $\sum_i \|x_i\| \mathbb{P}(X=x_i \mid Y=y) < \infty$，则 $E(X \mid Y=y)=\sum_i x_i \mathbb{P}(X=x_i \mid Y=y)$|
|**连续型**（定义 2.2'）|若 $\int_{-\infty}^{\infty} \|x\| f_X(x),dx < \infty$，则 $E(X)=\int_{-\infty}^{\infty} x f_X(x),dx$|若 $\int_{-\infty}^{\infty} \|x\| f_{X\mid Y}(x\mid y),dx < \infty$，则 $E(X \mid Y=y)=\int_{-\infty}^{\infty} x f_{X\mid Y}(x\mid y),dx$|

**要点：** $E(\cdot \mid Y=y)$ 与 $E(\cdot)$ 有完全相同的性质，因为它本质上也是在某个（条件）概率空间下求期望。

---

### 1.2 $E(X \mid Y)$ 的定义（定义 2.3）

**从函数到随机变量的升级：**

- $E(X \mid Y=y)$ 是关于 $y$ 的函数，记为 $m(y)$。
- 将 $y$ 替换为随机变量 $Y$，得到**随机变量** $m(Y)$，称其为**给定 $Y$ 时 $X$ 的条件期望**，记作 $E(X \mid Y)$。

$$\boxed{E(X \mid Y) := m(Y), \quad \text{其中 } m(y) = E(X \mid Y=y)}$$

**关键理解：**

- $E(X \mid Y=y)$ 是一个**数**（给定 $Y=y$ 后的条件均值）。
- $E(X \mid Y)$ 是一个**随机变量**（$Y$ 的函数），其取值随 $Y$ 的取值而变化。

> **计算口诀：** 要计算 $E(X \mid Y)$，先把 $Y$ 当作固定值 $y$，计算 $m(y)=E(X\mid Y=y)$，再将 $y$ 换回 $Y$ 即得 $E(X\mid Y)=m(Y)$。

**注意：** $X, Y$ 不需要同为离散或连续型，只要条件期望有合理定义即可。

---

## 二、$E(X \mid Y)$ 的计算（例题分析）

### 2.1 离散情形

**例 2.3（泊松分布）：** 设 $X, Y$ 独立同分布，且 $X \sim P(\lambda)$，求 $E(X+Y \mid X=x)$。

**解题思路：** 利用线性性和独立性。

$$E(X+Y \mid X=x) = E(X \mid X=x) + E(Y \mid X=x)$$

- $E(X \mid X=x) = x$（$X$ 已知为 $x$，期望就是 $x$）
- $E(Y \mid X=x) = E(Y) = \lambda$（$X, Y$ 独立，所以 $Y$ 的条件期望等于无条件期望）

$$\therefore E(X+Y \mid X=x) = x + \lambda$$

---

**例 2.3 进阶：** 求 $E(X+Y \mid X)$ 和 $E(X \mid X+Y)$。

**（1）求 $E(X+Y \mid X)$：**

由上可知 $m(x)=E(X+Y \mid X=x)=x+\lambda$，将 $x$ 换回 $X$：

$$E(X+Y \mid X) = X + \lambda$$

**（2）求 $E(X \mid X+Y)$：** 设 $Z = X+Y$，需要求 $E(X \mid Z=n)$。

**关键事实：** 由于 $X \sim P(\lambda)$，$Y \sim P(\lambda)$ 且独立，故 $Z = X+Y \sim P(2\lambda)$。

再由 Poisson 分布的拆分性质，$X \mid Z=n \sim B\left(n, \frac{1}{2}\right)$（二项分布，成功概率 $1/2$）。

因此： $$E(X \mid Z=n) = \frac{n}{2}$$

将 $n$ 换回 $Z = X+Y$：

$$E(X \mid X+Y) = \frac{X+Y}{2}$$

> **思考（课件中的疑问"?"）：** 能否用对称性直接得到？由对称性 $E(X \mid X+Y) = E(Y \mid X+Y)$，而 $E(X \mid X+Y) + E(Y \mid X+Y) = E(X+Y \mid X+Y) = X+Y$，故两者各为 $\frac{X+Y}{2}$，与直接计算一致。

---

### 2.2 连续情形（二元正态分布）

**例 2.4（身高与足长）：** 设 $(X, Y) \sim \mathcal{N}(\mu_1, \mu_2, \sigma_1^2, \sigma_2^2, \rho)$，求 $E(X \mid Y)$。

**解题思路：** 利用二元正态分布的条件分布结论。

已知：给定 $Y=y$ 时，$X \mid Y=y$ 仍为正态分布：

$$X \mid Y=y \sim \mathcal{N}\left(\mu_1 + \rho\frac{\sigma_1}{\sigma_2}(y-\mu_2), (1-\rho^2)\sigma_1^2\right)$$

因此（正态分布的期望即均值参数）：

$$E(X \mid Y=y) = \mu_1 + \rho\frac{\sigma_1}{\sigma_2}(y-\mu_2)$$

将 $y$ 换回 $Y$：

$$\boxed{E(X \mid Y) = \mu_1 + \rho\frac{\sigma_1}{\sigma_2}(Y-\mu_2)}$$

**实际应用：** 测得案犯足长 $y=26\text{cm}$，代入即可估计身高约 $E(X \mid Y=y)=180\text{cm}$。这正是统计学中**线性回归模型**的思想基础。

---

### 2.3 综合计算（例 2.6：混合型）

**题目：** $Y \sim \Gamma(\alpha, \beta)$，给定 $Y=y$ 时 $X \sim \mathcal{E}(y)$（指数分布，参数为 $y$）。求 $E(X\mid Y)$、$E(Y\mid X)$、$E(X)$。

**第一步：求 $E(X \mid Y)$**

条件密度 $f_{X\mid Y}(x\mid y) = ye^{-xy}$（$x>0$），因此：

$$E(X \mid Y=y) = \int_0^\infty x \cdot ye^{-xy}dx = \frac{1}{y}$$

（指数分布 $\mathcal{E}(y)$ 的均值为 $1/y$）

$$\therefore\quad E(X \mid Y) = \frac{1}{Y}$$

**第二步：求联合密度和 $E(Y \mid X)$**

联合密度： $$f(x,y) = f_{X\mid Y}(x\mid y) \cdot f_Y(y) = ye^{-xy} \cdot \frac{\beta^\alpha}{\Gamma(\alpha)} y^{\alpha-1} e^{-\beta y}, \quad x,y>0$$

$X$ 的边缘密度（对 $y$ 积分）： $$f_X(x) = \int_0^\infty f(x,y)dy = \frac{\alpha\beta^\alpha}{(x+\beta)^{\alpha+1}}, \quad x>0$$

> **为什么这样积分？** 将 $f(x,y)$ 中关于 $y$ 的部分整理为 $y^\alpha e^{-(x+\beta)y}$，利用 $\Gamma$ 函数公式 $\int_0^\infty y^\alpha e^{-(x+\beta)y} dy = \frac{\Gamma(\alpha+1)}{(x+\beta)^{\alpha+1}}$ 即得。

条件密度： $$f_{Y\mid X}(y\mid x) = \frac{f(x,y)}{f_X(x)} = \frac{(x+\beta)^{\alpha+1}}{\Gamma(\alpha+1)} y^\alpha e^{-(x+\beta)y}$$

这是 $\Gamma(\alpha+1, x+\beta)$ 分布的密度，期望为 $\frac{\alpha+1}{x+\beta}$，故：

$$E(Y \mid X) = \frac{\alpha+1}{X+\beta}$$

**第三步：用重期望法则求 $E(X)$**

$$E(X) = E[E(X\mid Y)] = E\left(\frac{1}{Y}\right) = \int_0^\infty y^{-1} \cdot \frac{\beta^\alpha}{\Gamma(\alpha)} y^{\alpha-1} e^{-\beta y}dy = \frac{\beta^\alpha}{\Gamma(\alpha)} \int_0^\infty y^{\alpha-2} e^{-\beta y}dy$$

利用 $\int_0^\infty y^{\alpha-2} e^{-\beta y} dy = \frac{\Gamma(\alpha-1)}{\beta^{\alpha-1}}$（需 $\alpha>1$）：

$$\boxed{E(X) = \begin{cases} \dfrac{\beta}{\alpha-1}, & \alpha > 1 \\ +\infty, & \alpha \in (0,1] \end{cases}}$$

---

## 三、重期望法则（Law of Total Expectation）

### 3.1 定理陈述与直观

**定理 2.3（重期望法则）：** $$\boxed{E[E(X \mid Y)] = E(X)}$$

**直观理解：** 以身高-足长例子为例——先按足长分组，计算每组的平均身高（条件期望 $E(X\mid Y)$），再对所有组的平均身高按各组比例加权平均，就得到总体平均身高（$EX$）。

**证明思路（离散情形）：**

$$E[E(X\mid Y)] = \sum_y E(X\mid Y=y) P_Y(y) = \sum_y \left(\sum_x x P_{X\mid Y}(x\mid y)\right) P_Y(y)$$

交换求和顺序：

$$= \sum_x x \underbrace{\sum_y P_{X\mid Y}(x\mid y) P_Y(y)}_{=P_X(x)} = \sum_x x P_X(x) = E(X)$$

> **关键步骤说明：** 最后一行用了全概率公式 $P_X(x) = \sum_y P_{X\mid Y}(x\mid y) P_Y(y)$。

---

### 3.2 重期望法则的应用方法

**适用场景：** 直接求 $E(X)$ 困难，但引入辅助随机变量 $Y$ 后，$E(X \mid Y=y)$ 容易计算。

**通用步骤：**

1. 引入辅助变量 $Y$（通常是某个"阶段"或"条件"）
2. 对每个 $Y=y$，计算条件期望 $E(X \mid Y=y)$
3. 应用 $E(X) = E[E(X\mid Y)] = \sum_y E(X\mid Y=y) \cdot P(Y=y)$

---

### 3.3 例题：密室逃脱（例 2.5）

**题目：** 三个门，门1走3小时出口，门2走5小时回原地，门3走7小时回原地，每次均匀随机选门，求平均逃脱时间 $E(X)$。

**解：** 令 $Y$ 为首次选择的门编号，$P(Y=i)=1/3$（$i=1,2,3$）。

关键——条件期望的建立：

- $E(X \mid Y=1) = 3$（直接到达出口）
- $E(X \mid Y=2) = 5 + E(X)$（走5小时回到原点，相当于重新开始）
- $E(X \mid Y=3) = 7 + E(X)$（走7小时回到原点，相当于重新开始）

> **步骤说明：** 走错门回到原地后，问题完全重置，因此剩余期望时间仍为 $E(X)$，故条件期望含 $E(X)$。

由全期望公式： $$E(X) = \frac{3 + (5+E(X)) + (7+E(X))}{3} = \frac{15 + 2E(X)}{3}$$

解方程：$3E(X) = 15 + 2E(X)$，故 $\mathbf{E(X) = 15}$。

---

### 3.4 例题：折断木棍（课件手写例题）

**题目：** 一根长度为1的木棍，连续随机折断2次，第一次得长度 $X$（均匀分布于 $[0,1]$），再对 $X$ 随机折断一次得长度 $Y$（均匀分布于 $[0,X]$），求 $EY$。

**解：** $$EY = E[E(Y \mid X)]$$

给定 $X=x$，$Y \sim U[0,x]$，故 $E(Y \mid X=x) = \frac{x}{2}$，即 $E(Y\mid X) = \frac{X}{2}$。

$$EY = E\left(\frac{X}{2}\right) = \frac{1}{2} EX = \frac{1}{2} \cdot \frac{1}{2} = \frac{1}{4}$$

---

## 四、$E(X \mid Y)$ 的性质

**定理 2.4（条件期望的性质）：** 设期望均有限，则：

|编号|性质|说明|
|---|---|---|
|1|$\|E(X\mid Y)\| \le E(\|X\|\mid Y)$|绝对值不等式（Jensen不等式特例）|
|2|$[E(X\mid Y)]^2 \le E(X^2\mid Y)$|Cauchy-Schwarz特例|
|3|$E[h(Y)g(X)\mid Y] = h(Y) \cdot E[g(X)\mid Y]$|**提出已知量**：$h(Y)$ 在给定 $Y$ 时是常数，可提到期望外|
|4|$E[E(g(X)\mid Y)] = Eg(X)$|重期望法则|
|5|$X, Y$ 独立 $\Rightarrow$ $E[g(X)\mid Y] = Eg(X)$|独立则条件无影响|
|6|$E!\left(c + \sum_i c_i X_i \mid Y\right) = c + \sum_i c_i E(X_i \mid Y)$|**线性性**（最常用）|
|7|$X_1 \le X_2 \Rightarrow E(X_1\mid Y) \le E(X_2\mid Y)$|单调性|

> **性质3的使用场景：** 凡是含有 $Y$ 的函数（如 $h(Y)$）乘以某个关于 $X$ 的量，在以 $Y$ 为条件时，$h(Y)$ 视为常数可提出。

---

### 4.1 重要例题：正交性（例 2.7）

**命题：** 若 $E(X^2)<\infty$，$E[h^2(Y)]<\infty$，则

$$E\big[(X - E(X\mid Y)) \cdot h(Y)\big] = 0$$

**含义：** 预测误差 $X - E(X\mid Y)$ 与 $Y$ 的任意函数 $h(Y)$ 正交（内积为零）。

**证明：** $$E\big[(X - E(X\mid Y))h(Y)\big] = E[Xh(Y)] - E[E(X\mid Y)h(Y)]$$

对第二项，由性质3：$E(X\mid Y)h(Y) = E(Xh(Y)\mid Y)$（因为 $h(Y)$ 在给定 $Y$ 时可提出）

> **步骤说明：** $E[E(X\mid Y) \cdot h(Y)] = E[E(X\cdot h(Y) \mid Y)]$。这一步用了性质3：在给定 $Y$ 下，$h(Y)$ 是已知量，故 $E(X\mid Y)\cdot h(Y) = E(X \cdot h(Y)\mid Y)$。

再由性质4（重期望）：$E[E(Xh(Y)\mid Y)] = E[Xh(Y)]$。

故整个表达式 $= E[Xh(Y)] - E[Xh(Y)] = 0$。

---

### 4.2 几何直观

条件期望有优美的几何解释：将随机变量视为内积空间中的向量（内积定义为 $\langle X, Y\rangle = E(XY)$），则 $E(X\mid Y) = m(Y)$ 是 $X$ 在"由 $Y$ 的所有函数张成的子空间" $\sigma(Y) = {g(Y): \forall\text{ 实函数 }g}$ 上的**正交投影**。

误差 $Z = X - m(Y)$ 垂直于该子空间（即与所有 $h(Y)$ 正交），这正是上述正交性定理的几何意义。

---

## 五、$E(X \mid Y)$ 的统计意义：最佳预测

### 5.1 最佳预测定理（例 2.8）

**定理：** 设 $E(X^2)<\infty$，$m(Y)=E(X\mid Y)$，则对任意实函数 $g(y)$，有

$$\boxed{E[X-m(Y)]^2 \le E[X-g(Y)]^2}$$

等号成立当且仅当 $g(Y) = m(Y)$ a.s.

**含义：** 在所有用 $Y$ 预测 $X$ 的方案中，$E(X\mid Y)$ 使均方误差最小，故称为 $X$ 的**最佳预测**（optimal forecast）。

**证明要点：** 将 $X - g(Y)$ 拆分为 $[X - m(Y)] + [m(Y) - g(Y)]$，展开平方：

$$E[X-g(Y)]^2 = E[X-m(Y)]^2 + E[m(Y)-g(Y)]^2 + 2E{[X-m(Y)][m(Y)-g(Y)]}$$

交叉项 $= 0$（由正交性，因 $m(Y)-g(Y)$ 是 $Y$ 的函数）。

故 $E[X-g(Y)]^2 = E[X-m(Y)]^2 + \underbrace{E[m(Y)-g(Y)]^2}_{\ge 0} \ge E[X-m(Y)]^2$。

---

### 5.2 正态分布下最佳预测 = 最佳线性预测（例 2.9）

对二元正态 $(X,Y)$：

$$E(X\mid Y) = \mu_1 + \rho\frac{\sigma_1}{\sigma_2}(Y-\mu_2)$$

这是 $Y$ 的**线性函数**，因此对正态分布，最佳预测恰好等于最佳线性预测。

> **直观推论：** 若 $(X,Y)$ 服从二元正态且 $E(X\mid Y) = \mu$（常数），则 $\rho \frac{\sigma_1}{\sigma_2}(Y-\mu_2) = 0$，由于 $\sigma_1, \sigma_2 > 0$，故 $\rho = 0$，即 $X, Y$ 不相关，在正态分布下等价于独立。

---

### 5.3 实际应用：EM 算法

条件期望在机器学习中的核心应用——**EM算法（Expectation-Maximization）**：

- **核心思想：** 引入隐变量（latent variable）处理不完全数据问题
- **E步（期望步）：** 计算"完全数据的对数似然函数"关于隐变量的条件期望，本质即为 $E(X\mid Y)$
- **M步（最大化步）：** 最大化该期望
- **应用举例：** 对古代中文文本（如《红楼梦》）进行无监督语义分析
    - **观测数据 Y**：每篇文章里出现的词
	- **隐变量 X**：每篇文章的主题分布（不知道）
	- **目标**：找到最能解释这些词的主题结构
	**E步**：在当前参数下，估计每篇文章"属于各主题的概率"，即算
	**M步**：根据这个估计，反过来更新"每个主题长什么样"（哪些词高频）
---

## 六、条件方差

### 6.1 定义（定义 3.1）

$$\boxed{\text{var}(X\mid Y) := E\big[(X - E(X\mid Y))^2 \mid Y\big]}$$

即在给定 $Y$ 的条件下，$X$ 偏离其条件均值的均方。类比普通方差，只是将期望换为条件期望。

逐步理解：

- 先固定 $Y=y$，得 $\text{var}(X\mid Y=y) = E{[X - E(X\mid Y=y)]^2 \mid Y=y}$（这是一个数）
- 将 $y$ 换为 $Y$，得 $\text{var}(X\mid Y)$（这是一个随机变量）

**计算公式：** 与普通方差类似， $$\text{var}(X\mid Y) = E(X^2\mid Y) - [E(X\mid Y)]^2$$

---

### 6.2 全方差法则（定理 3.1）

$$\boxed{\text{var}(X) = E[\text{var}(X\mid Y)] + \text{var}[E(X\mid Y)]}$$

**记忆口诀：** "方差 = 组内方差的均值 + 组间方差"（类比方差分析 ANOVA 的分解）。

**两项的含义：**

- $E[\text{var}(X\mid Y)]$：在各个 $Y$ 值下，$X$ 在组内的平均波动（**组内变异**）
- $\text{var}[E(X\mid Y)]$：各组条件均值自身的波动（**组间变异**）

**应用场景：** 方差分析（ANOVA）、线性回归、因果推断。

**证明思路：**

$$\text{var}(X) = E(X-EX)^2 = E{[X-E(X\mid Y)] + [E(X\mid Y) - EX]}^2$$

展开并利用：

1. 交叉项 $= 0$（正交性，$E(X\mid Y)-EX$ 是 $Y$ 的函数，与 $X-E(X\mid Y)$ 正交）
2. $E[X-E(X\mid Y)]^2 = E{E[X-E(X\mid Y)]^2\mid Y} = E[\text{var}(X\mid Y)]$
3. $E[E(X\mid Y)-EX]^2 = \text{var}[E(X\mid Y)]$（$EX = E[E(X\mid Y)]$ 由重期望法则）

---

### 6.3 应用例题：论文数问题（例 3.1）

**题目：** $Y$ = 选课人数，$X_i$ = 第 $i$ 位同学5年内论文数（i.i.d.，且与 $Y$ 独立），$X = \sum_{i=1}^Y X_i$，已知 $E(X_1), E(Y), \text{var}(X_1), \text{var}(Y)$，求 $E(X)$ 和 $\text{var}(X)$。

**解题步骤：**

**第一步：建立条件期望和条件方差**

给定 $Y=n$，$X = X_1 + \cdots + X_n$ 为 $n$ 个独立同分布随机变量之和：

$$E(X \mid Y=n) = nE(X_1) \quad \Rightarrow \quad E(X\mid Y) = Y \cdot E(X_1)$$

$$\text{var}(X \mid Y=n) = n\text{var}(X_1) \quad \Rightarrow \quad \text{var}(X\mid Y) = Y\cdot\text{var}(X_1)$$

> **步骤说明：** 给定 $Y=n$，$X_i$ 与 $Y$ 独立，条件期望等于无条件期望，$X_i$ 之间仍独立，方差可加。

**第二步：求 $E(X)$（用重期望法则）**

$$E(X) = E[E(X\mid Y)] = E[Y \cdot E(X_1)] = E(Y) \cdot E(X_1)$$

**第三步：求 $\text{var}(X)$（用全方差法则）**

$$\text{var}(X) = E[\text{var}(X\mid Y)] + \text{var}[E(X\mid Y)]$$

$$= E[Y \cdot \text{var}(X_1)] + \text{var}[Y \cdot E(X_1)]$$

$$= E(Y)\text{var}(X_1) + [E(X_1)]^2\text{var}(Y)$$

> **步骤说明：** 第二项 $\text{var}[Y \cdot E(X_1)] = [E(X_1)]^2 \text{var}(Y)$，因为 $E(X_1)$ 是常数，常数平方提出方差。

---


> [!ABSTRACT] 综合例题与方法

---

## 七、题型总结与应对策略

### 题型一：直接计算条件期望 $E(X\mid Y=y)$

**应对方法：**

1. 写出条件分布（离散：条件概率；连续：条件密度 $f_{X\mid Y}(x\mid y)$）
2. 按定义计算期望（求和或积分）
3. 若已知条件分布属于某已知分布族，直接使用其期望公式

**常用条件分布记忆：**

- 二元正态：$X\mid Y=y \sim \mathcal{N}\left(\mu_1+\rho\frac{\sigma_1}{\sigma_2}(y-\mu_2),,(1-\rho^2)\sigma_1^2\right)$
- Poisson 分裂：$X \mid X+Y=n \sim B(n, 1/2)$（$X, Y$ 独立同 Poisson）

---

### 题型二：计算 $E(X\mid Y)$（随机变量形式）

**应对方法：**

1. 先算 $m(y) = E(X\mid Y=y)$（参考题型一）
2. 将结果中的 $y$ 替换为 $Y$

---

### 题型三：利用重期望法则求 $E(X)$

**适用信号：** 直接求 $E(X)$ 困难；问题有层次结构（如随机个数的随机变量之和）；问题有"回到原点"的递归结构。

**应对方法：**

1. 找辅助变量 $Y$
2. 计算各条件下的 $E(X\mid Y=y)$（注意递归情形：$E(X\mid Y=y)$ 可能含 $E(X)$ 本身）
3. 用 $E(X) = \sum_y E(X\mid Y=y) P(Y=y)$（或积分形式）建立方程
4. 解出 $E(X)$

---

### 题型四：利用全方差法则求 $\text{var}(X)$

**应对方法：**

1. 找辅助变量 $Y$
2. 分别计算 $E[\text{var}(X\mid Y)]$ 和 $\text{var}[E(X\mid Y)]$
3. 相加得 $\text{var}(X)$

**特别注意：**

- $E[\text{var}(X\mid Y)]$：先求 $\text{var}(X\mid Y)$（随机变量），再对其取期望
- $\text{var}[E(X\mid Y)]$：先求 $E(X\mid Y)$（随机变量），再对其求方差

---

### 题型五：综合型（同时求 $E(X\mid Y)$、$E(Y\mid X)$、$E(X)$）

**应对方法（标准流程）：**

1. 用条件密度求 $E(X\mid Y)$
2. 写出联合密度：$f(x,y) = f_{X\mid Y}(x\mid y) \cdot f_Y(y)$
3. 对 $y$ 积分得 $f_X(x)$（边缘密度）
4. 用 $f_{Y\mid X}(y\mid x) = f(x,y)/f_X(x)$ 求条件密度
5. 识别分布族，直接读出期望，得 $E(Y\mid X)$
6. 用重期望法则：$E(X) = E[E(X\mid Y)]$

---

### 题型六：验证正交性或最佳预测性质

**应对方法：**

- 利用性质3（提出 $Y$ 的函数）和重期望法则（性质4）进行代数推导

---

## 八、核心公式汇总

|公式|名称|
|---|---|
|$E(X\mid Y) = m(Y)$，$m(y) = E(X\mid Y=y)$|条件期望定义|
|$E[E(X\mid Y)] = E(X)$|**重期望法则**|
|$E[h(Y)g(X)\mid Y] = h(Y)E[g(X)\mid Y]$|提出已知量|
|$X \perp Y \Rightarrow E(g(X)\mid Y) = Eg(X)$|独立性|
|$E[X-m(Y)]^2 \le E[X-g(Y)]^2$|最佳预测|
|$\text{var}(X\mid Y) = E(X^2\mid Y) - [E(X\mid Y)]^2$|条件方差计算公式|
|$\text{var}(X) = E[\text{var}(X\mid Y)] + \text{var}[E(X\mid Y)]$|**全方差法则**|

---

### 2.3 综合计算（例 2.6：混合型）

**题目：** $Y \sim \Gamma(\alpha, \beta)$，给定 $Y=y$ 时 $X \sim \mathcal{E}(y)$（指数分布，参数为 $y$）。求 $E(X\mid Y)$、$E(Y\mid X)$、$E(X)$。

**第一步：求 $E(X \mid Y)$**

条件密度 $f_{X\mid Y}(x\mid y) = ye^{-xy}$（$x>0$），因此：

$$E(X \mid Y=y) = \int_0^\infty x \cdot ye^{-xy}dx = \frac{1}{y}$$

（指数分布 $\mathcal{E}(y)$ 的均值为 $1/y$）

$$\therefore\quad E(X \mid Y) = \frac{1}{Y}$$

**第二步：求联合密度和 $E(Y \mid X)$**

联合密度： $$f(x,y) = f_{X\mid Y}(x\mid y) \cdot f_Y(y) = ye^{-xy} \cdot \frac{\beta^\alpha}{\Gamma(\alpha)} y^{\alpha-1} e^{-\beta y}, \quad x,y>0$$

$X$ 的边缘密度（对 $y$ 积分）： $$f_X(x) = \int_0^\infty f(x,y)dy = \frac{\alpha\beta^\alpha}{(x+\beta)^{\alpha+1}}, \quad x>0$$

> **为什么这样积分？** 将 $f(x,y)$ 中关于 $y$ 的部分整理为 $y^\alpha e^{-(x+\beta)y}$，利用 $\Gamma$ 函数公式 $\int_0^\infty y^\alpha e^{-(x+\beta)y} dy = \frac{\Gamma(\alpha+1)}{(x+\beta)^{\alpha+1}}$ 即得。

条件密度： $$f_{Y\mid X}(y\mid x) = \frac{f(x,y)}{f_X(x)} = \frac{(x+\beta)^{\alpha+1}}{\Gamma(\alpha+1)} y^\alpha e^{-(x+\beta)y}$$

这是 $\Gamma(\alpha+1, x+\beta)$ 分布的密度，期望为 $\frac{\alpha+1}{x+\beta}$，故：

$$E(Y \mid X) = \frac{\alpha+1}{X+\beta}$$

**第三步：用重期望法则求 $E(X)$**

$$E(X) = E[E(X\mid Y)] = E\left(\frac{1}{Y}\right) = \int_0^\infty y^{-1} \cdot \frac{\beta^\alpha}{\Gamma(\alpha)} y^{\alpha-1} e^{-\beta y}dy = \frac{\beta^\alpha}{\Gamma(\alpha)} \int_0^\infty y^{\alpha-2} e^{-\beta y}dy$$

利用 $\int_0^\infty y^{\alpha-2} e^{-\beta y} dy = \frac{\Gamma(\alpha-1)}{\beta^{\alpha-1}}$（需 $\alpha>1$）：

$$\boxed{E(X) = \begin{cases} \dfrac{\beta}{\alpha-1}, & \alpha > 1 \\ +\infty, & \alpha \in (0,1] \end{cases}}$$

### 6.3 应用例题：论文数问题（例 3.1）

**题目：** $Y$ = 选课人数，$X_i$ = 第 $i$ 位同学5年内论文数（i.i.d.，且与 $Y$ 独立），$X = \sum_{i=1}^Y X_i$，已知 $E(X_1), E(Y), \text{var}(X_1), \text{var}(Y)$，求 $E(X)$ 和 $\text{var}(X)$。

**解题步骤：**

**第一步：建立条件期望和条件方差**

给定 $Y=n$，$X = X_1 + \cdots + X_n$ 为 $n$ 个独立同分布随机变量之和：

$$E(X \mid Y=n) = nE(X_1) \quad \Rightarrow \quad E(X\mid Y) = Y \cdot E(X_1)$$

$$\text{var}(X \mid Y=n) = n\text{var}(X_1) \quad \Rightarrow \quad \text{var}(X\mid Y) = Y\cdot\text{var}(X_1)$$

> **步骤说明：** 给定 $Y=n$，$X_i$ 与 $Y$ 独立，条件期望等于无条件期望，$X_i$ 之间仍独立，方差可加。

**第二步：求 $E(X)$（用重期望法则）**

$$E(X) = E[E(X\mid Y)] = E[Y \cdot E(X_1)] = E(Y) \cdot E(X_1)$$

**第三步：求 $\text{var}(X)$（用全方差法则）**

$$\text{var}(X) = E[\text{var}(X\mid Y)] + \text{var}[E(X\mid Y)]$$

$$= E[Y \cdot \text{var}(X_1)] + \text{var}[Y \cdot E(X_1)]$$

$$= E(Y)\text{var}(X_1) + [E(X_1)]^2\text{var}(Y)$$

> **步骤说明：** 第二项 $\text{var}[Y \cdot E(X_1)] = [E(X_1)]^2 \text{var}(Y)$，因为 $E(X_1)$ 是常数，常数平方提出方差。

---

## 七、题型总结与应对策略

### 题型一：直接计算条件期望 $E(X\mid Y=y)$

**应对方法：**

1. 写出条件分布（离散：条件概率；连续：条件密度 $f_{X\mid Y}(x\mid y)$）
2. 按定义计算期望（求和或积分）
3. 若已知条件分布属于某已知分布族，直接使用其期望公式

**常用条件分布记忆：**

- 二元正态：$X\mid Y=y \sim \mathcal{N}\left(\mu_1+\rho\frac{\sigma_1}{\sigma_2}(y-\mu_2),,(1-\rho^2)\sigma_1^2\right)$
- Poisson 分裂：$X \mid X+Y=n \sim B(n, 1/2)$（$X, Y$ 独立同 Poisson）

---

### 题型二：计算 $E(X\mid Y)$（随机变量形式）

**应对方法：**

1. 先算 $m(y) = E(X\mid Y=y)$（参考题型一）
2. 将结果中的 $y$ 替换为 $Y$

---

### 题型三：利用重期望法则求 $E(X)$

**适用信号：** 直接求 $E(X)$ 困难；问题有层次结构（如随机个数的随机变量之和）；问题有"回到原点"的递归结构。

**应对方法：**

1. 找辅助变量 $Y$
2. 计算各条件下的 $E(X\mid Y=y)$（注意递归情形：$E(X\mid Y=y)$ 可能含 $E(X)$ 本身）
3. 用 $E(X) = \sum_y E(X\mid Y=y) P(Y=y)$（或积分形式）建立方程
4. 解出 $E(X)$

---

### 题型四：利用全方差法则求 $\text{var}(X)$

**应对方法：**

1. 找辅助变量 $Y$
2. 分别计算 $E[\text{var}(X\mid Y)]$ 和 $\text{var}[E(X\mid Y)]$
3. 相加得 $\text{var}(X)$

**特别注意：**

- $E[\text{var}(X\mid Y)]$：先求 $\text{var}(X\mid Y)$（随机变量），再对其取期望
- $\text{var}[E(X\mid Y)]$：先求 $E(X\mid Y)$（随机变量），再对其求方差

---

### 题型五：综合型（同时求 $E(X\mid Y)$、$E(Y\mid X)$、$E(X)$）

**应对方法（标准流程）：**

1. 用条件密度求 $E(X\mid Y)$
2. 写出联合密度：$f(x,y) = f_{X\mid Y}(x\mid y) \cdot f_Y(y)$
3. 对 $y$ 积分得 $f_X(x)$（边缘密度）
4. 用 $f_{Y\mid X}(y\mid x) = f(x,y)/f_X(x)$ 求条件密度
5. 识别分布族，直接读出期望，得 $E(Y\mid X)$
6. 用重期望法则：$E(X) = E[E(X\mid Y)]$

---

### 题型六：验证正交性或最佳预测性质

**应对方法：**

- 利用性质3（提出 $Y$ 的函数）和重期望法则（性质4）进行代数推导

---

## 八、核心公式汇总

|公式|名称|
|---|---|
|$E(X\mid Y) = m(Y)$，$m(y) = E(X\mid Y=y)$|条件期望定义|
|$E[E(X\mid Y)] = E(X)$|**重期望法则**|
|$E[h(Y)g(X)\mid Y] = h(Y)E[g(X)\mid Y]$|提出已知量|
|$X \perp Y \Rightarrow E(g(X)\mid Y) = Eg(X)$|独立性|
|$E[X-m(Y)]^2 \le E[X-g(Y)]^2$|最佳预测|
|$\text{var}(X\mid Y) = E(X^2\mid Y) - [E(X\mid Y)]^2$|条件方差计算公式|
|$\text{var}(X) = E[\text{var}(X\mid Y)] + \text{var}[E(X\mid Y)]$|**全方差法则**|