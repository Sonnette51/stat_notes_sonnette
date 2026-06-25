---
title: "Lecture02 概率空间、条件概率"
tags:
  - 概率论
  - 前半学期
  - 概率空间
  - 条件概率
  - 贝叶斯
---

# Lecture02 概率空间、条件概率

> [!ABSTRACT] 本讲概要
> 上一讲我们把概率理解为"事件的非负数值"，但一个自然的问题随之而来：**样本空间的任意子集都能分配概率吗？** 本讲先用"事件域 + 概率测度"搭出概率论的公理化地基（概率空间），再讨论概率作为测度的连续性，最后引入条件概率，并发展出它的三大法则：乘法公式、全概率公式与 Bayes 准则——这是"获得新信息后如何更新认知"的数学语言。

## 一、复习（Review）

### 1.1 概率模型的基本构成

- **样本空间** $\Omega$：一个试验的所有可能结果的集合；
- **概率**：就是为试验结果的集合（称之为事件）确定一个非负数 $\mathbb{P}(A)$（称为事件 $A$ 的概率），刻画对事件 $A$ 的认识或所产生的信息度量。

**概率公理**：
1. （非负性）对一切事件 $A$，满足 $\mathbb{P}(A)\geq 0$；
2. （归一化）$\mathbb{P}(\Omega)=1$；
3. （可列可加性）若 $A_1,A_2,\ldots$ 是互不相容的事件序列，则

$$
\mathbb{P}\left(\bigcup_{n=1}^{\infty}A_n\right)=\sum_{n=1}^{\infty}\mathbb{P}(A_n)
$$

### 1.2 一个"矛盾"：能给所有子集分配概率吗？

考察概率模型 $\Omega=\{(x,y)\mid 0\leq x,y\leq 1\}=\bigcup_{x,y}\{(x,y)\}$，$\mathbb{P}(A)=\text{area}(A)$（面积）。于是

$$
1=\mathbb{P}(\Omega)=\mathbb{P}\left(\bigcup_{x,y}\{(x,y)\}\right)=\sum_{x,y}\mathbb{P}(\{(x,y)\})=\sum_{x,y}0=0
$$

矛盾？！

> [!NOTE] 备注
> 问题出在"可列可加性"只对**可列**个事件成立，而 $\Omega$ 中的点有不可列多个，不能套用公理 3，所以上式第二个等号根本不成立。另外，$\mathbb{P}(A)=1$ 时我们称 $A$ **几乎必然**（a.s. almost surely）发生，例如 $\mathbb{P}((x,y)\neq(0,0))=1$。
> 
> 这个例子引出本讲的核心问题（课件红字强调）：**任意样本空间的子集都可以分配概率么？** 答案是否定的（见附录不可测集），所以必须先圈定"哪些子集算事件"——这就是事件域。

---

## 二、概率空间

### 2.1 事件域（σ-域 / σ-代数）

> [!IMPORTANT] 定义（事件域 / σ-域 / σ-代数，σ-field 或 σ-algebra）【常用】
> 设 $\Omega$ 是样本空间，$\mathcal{F}$ 是 $\Omega$ 的某些子集构成的集合。如果 $\mathcal{F}$ 满足以下三个条件：
> 1. $\Omega\in\mathcal{F}$；
> 2. 如果 $A\in\mathcal{F}$，则 $A^c\in\mathcal{F}$；
> 3. 如果 $A_n\in\mathcal{F}$，$n=1,2,\ldots$，则 $\bigcup_{n=1}^{\infty}A_n\in\mathcal{F}$；
> 
> 则称 $\mathcal{F}$ 为 $\Omega$ 上的**事件域**、**σ-域**或 **σ-代数**，称 $\mathcal{F}$ 中的元素为**事件**，称 $(\Omega,\mathcal{F})$ 是**可测空间**（measurable space）。

**直觉**：事件域就是"允许谈论概率的事件清单"——对取补、可列并（从而也对可列交）封闭，保证我们做集合运算时不会跑出清单之外。

> [!NOTE] 备注（课件"注"逐条）
> 1. $\mathcal{F}$ 中每一个事件都是**可以分配**概率的；它圈定了全部我们关心的事件的范围；
> 2. $\Omega$ 的任意子集**未必**是事件，只有 $\mathcal{F}$ 中的元素才能称之为事件；
> 3. $\mathcal{F}$ 对集合的各类可列交、并、补运算都是封闭的，包括事件列的极限运算；
> 4. $\mathcal{F}$ 中任选一个事件，其概率**是否可计算**，取决于已知条件。

### 2.2 事件域的构造

对于固定的 $\Omega$，可以构造出多个**不同**的 $\Omega$ 上的事件域。

σ-代数的例子：

| 例子 | 说明 |
| --- | --- |
| $\mathcal{F}=\{\Omega,\emptyset\}$ | 平凡的（最小的）σ-代数 |
| $\mathcal{F}=\{\Omega\text{ 的所有子集}\}$ | 最大的 σ-代数（幂集 $2^{\Omega}$） |
| $\mathcal{F}=\{\Omega,\emptyset,A,A^c\}$ | 包含 $A$ 的最小 σ-代数，记作 $\mathcal{F}=\sigma(\{A\})$ |

**$\mathcal{F}$ 的构造：一个简单的例子**

如果 $A,B$ 是 $\Omega$ 的两个子集，且 $B\neq A^c$，那么由 $\mathcal{A}=\{A,B\}$ 所生成的 σ-域 $\mathcal{F}$ 是（共 16 个元素）：

$$
\mathcal{F}=\sigma(\mathcal{A})=\{\Omega,\emptyset,A,A^c,B,B^c,AB,AB^c,A^cB,A^cB^c,A\cup B,A\cup B^c,A^c\cup B,A^c\cup B^c,AB\cup A^cB^c,AB^c\cup A^cB\}
$$

（注：此处补全了构造逻辑——先取 $A,B$ 的四个"原子" $AB,AB^c,A^cB,A^cB^c$，它们构成 $\Omega$ 的分割，σ-域的元素就是这些原子的所有并，共 $2^4=16$ 个。）

### 2.3 事件域的验证：利用封闭性或定义

关于封闭性的举例说明：$\mathcal{F}$ 和 $\mathcal{G}$ 是两个 σ-域，但 $\mathcal{F}\cup\mathcal{G}$ 并**不一定**是 σ-域。

取 $\Omega=\{a,b,c\}$，$\mathcal{F}=\{\Omega,\emptyset,\{a\},\{b,c\}\}$，$\mathcal{G}=\{\Omega,\emptyset,\{c\},\{a,b\}\}$。于是

$$
\mathcal{F}\cup\mathcal{G}=\{\Omega,\emptyset,\{a\},\{c\},\{a,b\},\{b,c\}\}
$$

但是 $\{a\}\cup\{c\}=\{a,c\}\notin\mathcal{F}\cup\mathcal{G}$，对并运算不封闭，故不是 σ-域。

而如果 $\mathcal{F}$ 和 $\mathcal{G}$ 是两个 σ-域，且 $\mathcal{F}\subset\mathcal{G}$，则 $\mathcal{F}\cup\mathcal{G}=\mathcal{G}$ 是 σ-域。

> [!TIP] 方法
> **证伪常用封闭性**（找一个反例破坏封闭性），**证实常用定义**（逐条验证定义的三个条件）。

### 2.4 概率测度与概率空间

> [!IMPORTANT] 定义（概率 / 概率测度，probability measure）【常用】
> 设 $(\Omega,\mathcal{F})$ 是可测空间，$\mathbb{P}$ 是定义在 $\mathcal{F}$ 上的函数。如果 $\mathbb{P}$ 满足下面三个条件：
> 1. （非负性）对任意的 $A\in\mathcal{F}$，$\mathbb{P}(A)\geq 0$；
> 2. （完全性）$\mathbb{P}(\Omega)=1$；
> 3. （可列可加性，σ-additivity）对于 $\mathcal{F}$ 中互不相交（disjoint，或互不相容）的事件 $A_1,A_2,\ldots$，有
> 
> $$
> \mathbb{P}\left(\bigcup_{n=1}^{\infty}A_n\right)=\sum_{n=1}^{\infty}\mathbb{P}(A_n)
> $$
> 
> 则称 $\mathbb{P}$ 为 $\mathcal{F}$ 上的**概率测度**（probability measure），简称**概率**（probability），称 $(\Omega,\mathcal{F},\mathbb{P})$ 为**概率空间**（probability space）。

**直觉**：概率就是定义在事件清单 $\mathcal{F}$ 上的一种"归一化的测度"——像长度、面积一样可加，但总量恰为 1。

### 2.5 概率空间 $(\Omega,\mathcal{F},\mathbb{P})$ 的构造：简单例子

1. **掷一枚硬币**：$\Omega=\{H,T\}$，$\mathcal{F}=\{\Omega,\emptyset,\{H\},\{T\}\}$，$\mathbb{P}(\{H\})=0.6$，$\mathbb{P}(\{T\})=0.4$。
2. **掷一枚骰子**：$\Omega=\{1,2,\ldots,6\}$，$\mathcal{F}=2^{\Omega}$（$\Omega$ 的所有子集构成的集合，称为**幂集** power set），$\mathbb{P}(\{i\})=1/6$，$i=1,\ldots,6$；对任意的 $A\in\mathcal{F}$，$\mathbb{P}(A)=\#(A)/6$。
3. **反复掷一枚硬币**（每次正面朝上的概率为 $p$），直到正面向上：

$$
\Omega=\{T^nH:n\geq 0\}\cup\{T^{\infty}\}
$$

$$
\mathbb{P}(T^nH)=(1-p)^np,\quad \mathbb{P}(T^{\infty})=\lim_{n\to\infty}(1-p)^n=0
$$

> [!NOTE] 备注
> 1. 如果 $\Omega$ 是**可列**的，则存在概率分配使得 $\Omega$ 的任一子集都可测，当然此时 $\mathcal{F}$ 可以包含 $\Omega$ 的所有子集；
> 2. 如果 $\Omega$ 是**不可列**的，则存在 $\Omega$ 的不可测子集，此时这些不可测子集就不能把它们当成事件了，因为我们无法确定其概率（见附录）。

### 2.6 概率的规范表述

- 对于 $A\in\mathcal{F}$，如果 $\mathbb{P}(A)=1$，称 $A$ **以概率 1 发生**或**几乎处处**发生。这里的几乎处处是指对几乎每个 $\omega\in\Omega$。几乎处处有时又称为**几乎必然**，记作 a.s.（almost surely）。
- 概率性质的规范表述：例如上一讲介绍的"性质 3：如果有事件 $A$，则 $\mathbb{P}(A^c)=1-\mathbb{P}(A)$"，规范写法应为：**如果 $A\in\mathcal{F}$，则 $\mathbb{P}(A^c)=1-\mathbb{P}(A)$**（强调 $A$ 必须属于事件域）。

### 2.7 概率空间小结

> [!WARNING] 辨析
> 请注意区分**事件域 $\mathcal{F}$**、**可测空间 $(\Omega,\mathcal{F})$** 与**测度空间（概率空间）$(\Omega,\mathcal{F},\mathbb{P})$**：
> 1. 事件域 $\mathcal{F}$ 包含全部我们关心的事件；其中每一个事件都是**可以分配**概率的；
> 2. 对于固定的 $\Omega$，可以构造出多个**不同**的 $\Omega$ 上的事件域；
> 3. 对同一个可测空间 $(\Omega,\mathcal{F})$，可构造**不同**的概率空间 $(\Omega,\mathcal{F},\mathbb{P})$；
> 4. $\mathcal{F}$ 中任选一个事件，其概率**是否可计算**，取决于已知条件。有时其中可能包含某事件 $A$，很复杂，导致 $\mathbb{P}(A)$ 很难计算，那么经常用容易计算的其他事件 $B_i$ 的概率 $\mathbb{P}(B_i)$ 去逼近，或通过不等式得到其上下界（精确 vs 近似、成本高 vs 成本低的 trade-off）。

---

## 三、概率的连续性

### 3.1 单调事件列及其极限

对给定的事件列 $\{A_i,i=1,2,\ldots\}$：
1. 如果 $A_1\subset A_2\subset\cdots$，称事件列 $\{A_i\}$ 是**单调递增**的；
2. 如果 $A_1\supset A_2\supset\cdots$，称事件列 $\{A_i\}$ 是**单调递减**的。

单调增序列和单调减序列统称为**单调序列**。

- 对于单调增序列 $\{A_i\}$，定义 $\displaystyle\lim_{n\to\infty}A_n=\bigcup_{i=1}^{\infty}A_i$；
- 对于单调减序列 $\{B_i\}$，定义 $\displaystyle\lim_{n\to\infty}B_n=\bigcap_{i=1}^{\infty}B_i$。

**直觉**：单调增事件列像不断扩张的水池，极限就是最终淹没的全部范围；单调减则是不断收缩，极限是始终保留的公共部分——完全类比单调数列的极限。

### 3.2 概率的连续性定理

> [!IMPORTANT] 定理（概率的连续性）【常用】
> 设 $\{A_i\}$ 和 $\{B_i\}$ 是事件列。
> 1. 如果 $\{A_i\}$ 是单调增序列，则 $\mathbb{P}(\lim_{n\to\infty}A_n)=\lim_{n\to\infty}\mathbb{P}(A_n)$；
> 2. 如果 $\{B_i\}$ 是单调减序列，则 $\mathbb{P}(\lim_{n\to\infty}B_n)=\lim_{n\to\infty}\mathbb{P}(B_n)$。

**直觉**：对单调事件列，"先取极限再求概率"等于"先求概率再取极限"——概率作为集合的函数是"连续"的。

**证明**：
（1）因为 $\{A_i\}$ 是单调增的，所以可以把并集拆成互不相交的"环带"：

$$
\bigcup_{i=1}^{\infty}A_i=A_1\cup\bigcup_{i=2}^{\infty}(A_i-A_{i-1})
$$

由概率公理（3）得

$$
\begin{align}
\mathbb{P}\left(\lim_{n\to\infty}A_n\right)&=\mathbb{P}(A_1)+\sum_{i=2}^{\infty}\left[\mathbb{P}(A_i)-\mathbb{P}(A_{i-1})\right]\\
&=\mathbb{P}(A_1)+\lim_{n\to\infty}\sum_{i=2}^{n}\left[\mathbb{P}(A_i)-\mathbb{P}(A_{i-1})\right]\\
&=\lim_{n\to\infty}\mathbb{P}(A_n)
\end{align}
$$

（注：此步补全了说明——因 $A_{i-1}\subset A_i$，有 $\mathbb{P}(A_i-A_{i-1})=\mathbb{P}(A_i)-\mathbb{P}(A_{i-1})$；末行是裂项相消。）

（2）因为 $\{B_j\}$ 是单调减序列，所以 $\{\Omega-B_j\}$ 是单调增序列，因此

$$
1-\mathbb{P}\left(\lim_{n\to\infty}B_n\right)=\mathbb{P}\left(\lim_{n\to\infty}(\Omega-B_n)\right)=\lim_{n\to\infty}\mathbb{P}(\Omega-B_n)=1-\lim_{n\to\infty}\mathbb{P}(B_n)
$$

即 $\mathbb{P}(\lim_{n\to\infty}B_n)=\lim_{n\to\infty}\mathbb{P}(B_n)$。$\blacksquare$

### 3.3 事件列的上极限与下极限【了解即可】

> [!IMPORTANT] 定义（事件列的上极限与下极限）
> 设 $\{A_i,i=1,2,\ldots\}$ 是 $\Omega$ 中的事件列，定义：
> 1. $\{A_i\}$ 的**上极限**，记作 $\limsup_{n\to\infty}A_n$，定义为
> 
> $$
> \limsup_{n\to\infty}A_n=\bigcap_{n=1}^{\infty}\bigcup_{k=n}^{\infty}A_k=\{\omega\in\Omega:\omega\text{ 属于无穷多个 }A_i\}
> $$
> 
> 2. $\{A_i\}$ 的**下极限**，记作 $\liminf_{n\to\infty}A_n$，定义为
> 
> $$
> \liminf_{n\to\infty}A_n=\bigcup_{n=1}^{\infty}\bigcap_{k=n}^{\infty}A_k=\{\omega\in\Omega:\omega\text{ 属于除了有限个之外的所有 }A_i\}
> $$
> 
> 3. 如果 $\liminf_{n\to\infty}A_n=\limsup_{n\to\infty}A_n$，则称事件列 $\{A_i\}$ 的**极限存在**，记作 $\lim_{n\to\infty}A_n$。

> [!WARNING] 辨析
> - 上极限 = "$A_n$ **无穷多次**发生"（infinitely often）：无论从第几项往后看，总还能碰到某个 $A_k$ 发生；
> - 下极限 = "$A_n$ **从某项起一直**发生"（除有限个外全部发生），这是比上极限**强**的条件，故 $\liminf A_n\subset\limsup A_n$。
> 两者一字之差，含义截然不同，做题时先翻译成"无穷多次发生 / 最终一直发生"再动手。

### 3.4 应用一：确定概率的上下界【了解即可】

> [!IMPORTANT] 定理（Fatou 型不等式）
> 任意事件列 $\{A_i,i=1,2,\ldots\}$，有
> 
> $$
> \mathbb{P}\left(\limsup_{n\to\infty}A_n\right)\geq\limsup_{n\to\infty}\mathbb{P}(A_n),\qquad \mathbb{P}\left(\liminf_{n\to\infty}A_n\right)\leq\liminf_{n\to\infty}\mathbb{P}(A_n)
> $$

**证明**（第一个不等式）：记 $B_n=\bigcup_{k=n}^{\infty}A_k$，则 $\{B_n\}$ 是单调减序列，由概率的连续性，

$$
\mathbb{P}\left(\limsup_{n\to\infty}A_n\right)=\mathbb{P}\left(\lim_{n\to\infty}B_n\right)=\lim_{n\to\infty}\mathbb{P}(B_n)
$$

又由概率单调性，有 $\mathbb{P}(B_n)\geq\mathbb{P}(A_k)$，$\forall k\geq n$，即有

$$
\mathbb{P}(B_n)\geq\sup_{k\geq n}\mathbb{P}(A_k)
$$

代入上面的等式即得第一个不等式。（注意，此时 $\sup_{k\geq n}\mathbb{P}(A_k)$ 是**数列**，不是事件列；该数列关于 $n$ 是单调的，从而保证了其极限存在，且其极限即 $\limsup_{n\to\infty}\mathbb{P}(A_n)$。）第二个不等式的证明是类似的。$\blacksquare$

### 3.5 应用二：Borel–Cantelli 引理【了解即可】

> [!IMPORTANT] 定理（Borel–Cantelli 引理，BC 引理）
> 设 $\{A_n\}$ 是事件列。
> 1. 如果
> 
> $$
> \sum_{n=1}^{\infty}\mathbb{P}(A_n)<\infty
> $$
> 
> 则 $\mathbb{P}\left(\limsup_{n\to\infty}A_n\right)=0$。
> 2. 如果 $\{A_n\}$ 是相互独立的，且
> 
> $$
> \sum_{n=1}^{\infty}\mathbb{P}(A_n)=\infty
> $$
> 
> 则 $\mathbb{P}\left(\limsup_{n\to\infty}A_n\right)=1$。

**直觉**：概率之和有限 ⟹ 事件几乎必然只发生有限次；概率之和发散且各次独立 ⟹ 事件几乎必然发生无穷多次。"0-1"两极分化。

> [!EXAMPLE]- 例题：BC 引理的简单应用（无穷次抛硬币）
> **题目**：试验为抛掷一枚均匀硬币无穷多次。$\Omega=?$ 正面是否无穷多次出现？是否可能从某时刻之后一直是正面？
> 
> **解**：
> $\Omega$ 为所有无穷长的正反面序列的集合（注：此步补全了 $\Omega=\{H,T\}^{\infty}$ 的含义）。
> 
> 记事件 $H_n$ 表示第 $n$ 次抛掷得到正面，则 $\mathbb{P}(H_n)=\dfrac{1}{2}$，从而
> 
> $$
> \sum_{n=1}^{\infty}\mathbb{P}(H_n)=\sum_{n=1}^{\infty}\frac{1}{2}=\infty
> $$
> 
> 且各次抛掷相互独立。则由 Borel–Cantelli 引理（第 2 条），知
> 
> $$
> \mathbb{P}\left(\limsup_{n\to\infty}H_n\right)=1
> $$
> 
> 即，以概率 1 地正面会无穷多次出现。
> 
> **那么是否可能到某时刻之后一直是正面吗？** "从某时刻起一直是正面"正是下极限事件 $\liminf_{n\to\infty}H_n$。由对偶关系（注：此步补全了 $(\liminf H_n)^c=\limsup H_n^c$，且 $H_n^c$ 同样满足 BC 引理第 2 条的条件，故 $\mathbb{P}(\limsup H_n^c)=1$）：
> 
> $$
> \mathbb{P}\left(\liminf_{n\to\infty}H_n\right)=1-\mathbb{P}\left(\limsup_{n\to\infty}H_n^c\right)=1-1=0
> $$
> 
> 所以答案是**几乎不可能**。

---

## 四、条件概率

### 4.1 引例：获取新信息后如何更新认知

> [!EXAMPLE]- 例题：扑克牌（抽到梅花的条件下抽到 5）
> **题目**：52 张扑克中任取一张，在已知抽到梅花的条件下，求抽到 5 的概率。
> 
> **解**：$A$ 表示抽到梅花，$B$ 表示抽到 5。
> - 如果去除条件，则 $\mathbb{P}(A)=13/52$，$\mathbb{P}(A\cap B)=1/52$（注：此步补全了——梅花共 13 张，"梅花 5"只有 1 张）；
> - 已知事件 $A$ 发生后，**样本空间缩小为** $\{1,2,\ldots,13\}$（13 张梅花），且每个样本点具有等可能性。此时抽到 5 的概率为 $1/13$；
> - 如下关系：
> 
> $$
> \mathbb{P}(B\mid A)=\frac{1}{13}=\frac{1/52}{13/52}=\frac{\mathbb{P}(A\cap B)}{\mathbb{P}(A)}
> $$

从上例中可以看到：给定"一个试验、与这个试验所对应的样本空间和概率（测度）"，假设已经知道给定的事件 $A$ 发生了，而希望知道另外一个给定的事件 $B$ 发生的可能性，则可以构造一个新的概率（测度），它刻画了事件 $A$ 发生的信息，求出任何事件 $B$ 发生的概率。这个概率就是给定 $A$ 发生条件下事件 $B$ 发生的**条件概率**，记作 $\mathbb{P}(B\mid A)$。

### 4.2 条件概率的定义

> [!IMPORTANT] 定义（条件概率，conditional probability）【常用】
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$A,B\in\mathcal{F}$，且 $\mathbb{P}(A)>0$，则在事件 $A$ 发生的条件下，事件 $B$ 发生的**条件概率**定义为
> 
> $$
> \mathbb{P}(B\mid A)=\frac{\mathbb{P}(A\cap B)}{\mathbb{P}(A)}
> $$

**直觉**：条件概率就是把样本空间"压缩"到 $A$ 上之后重新归一化——$A$ 之外的结果被排除，$A$ 内部各结果的相对比例不变。

> [!NOTE] 备注
> 当 $\mathbb{P}(A)=0$ 时，相应的条件概率**没有定义**。（有时候可以假设把 $\mathbb{P}(B\mid A)$ 定义为 $[0,1]$ 中的任意常数。）

> [!EXAMPLE]- 例题：连掷两次四面体骰子（供练习巩固）
> **题目**：连续抛掷两次均匀的 4 面体试验，假定所有 16 种试验结果是等可能的，分别记 $X$ 和 $Y$ 为第一次和第二次抛掷的结果。计算条件概率 $\mathbb{P}(A\mid B)$，其中 $A=\{\max(X,Y)=m\}$，$m=1,2,3,4$，$B=\{\min(X,Y)=2\}$。
> 
> **解**：$\Omega=\{(i,j):i,j=1,2,3,4\}$。由于两次均匀，可以假定这 16 个试验结果是等可能的。
> 
> $B=\{(i,j):\min(i,j)=2\}$。（注：此步补全了枚举——$B=\{(2,2),(2,3),(2,4),(3,2),(4,2)\}$。）故 $\#(B)=5$。
> 
> $A\cap B=\{(i,j):\max(i,j)=m,\min(i,j)=2\}$，逐个枚举：
> 
> $$
> \#(A\cap B)=\begin{cases}0,&\text{若 }m=1\\ 1,&\text{若 }m=2\\ 2,&\text{若 }m=3\text{ 或 }4\end{cases}
> $$
> 
> （注：此步补全了——$m=2$ 时只有 $(2,2)$；$m=3$ 时是 $(2,3),(3,2)$；$m=4$ 时是 $(2,4),(4,2)$；$m=1$ 时 $\max<\min$ 不可能。）
> 
> 因此（注：此步补全了公式 $\mathbb{P}(A\mid B)=\#(A\cap B)/\#(B)$，因为在 $B$ 内各点仍等可能）：
> 
> $$
> \mathbb{P}(A\mid B)=\begin{cases}0,&\text{若 }m=1\\ 1/5,&\text{若 }m=2\\ 2/5,&\text{若 }m=3\text{ 或 }4\end{cases}
> $$

### 4.3 条件概率依然是一个概率测度

> [!IMPORTANT] 定理（条件概率是概率测度）【常用】
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$A\in\mathcal{F}$，且 $\mathbb{P}(A)>0$，则
> 1. 对任意的 $B\in\mathcal{F}$，$\mathbb{P}(B\mid A)\geq 0$；
> 2. $\mathbb{P}(\Omega\mid A)=1$；
> 3. 对互不相容的事件列 $\{B_i\}$，有
> 
> $$
> \mathbb{P}\left(\bigcup_{i=1}^{\infty}B_i\,\middle|\,A\right)=\sum_{i=1}^{\infty}\mathbb{P}(B_i\mid A)
> $$

**证明思路**：逐条用定义验证。如第 3 条：$\mathbb{P}(\bigcup_iB_i\mid A)=\mathbb{P}(\bigcup_i(B_i\cap A))/\mathbb{P}(A)$，而 $\{B_i\cap A\}$ 仍互不相容，用 $\mathbb{P}$ 的可列可加性即得。

- 用 $\mathbb{P}_A(\cdot)$ 表示在事件 $A$ 发生时的条件概率，即 $\mathbb{P}_A(\cdot)=\mathbb{P}(\cdot\mid A)$，则 $(\Omega,\mathcal{F},\mathbb{P}_A)$ 也是一个概率空间。
- 注意到，在 $\mathbb{P}_A$ 下，条件概率完全集中在 $A$ 上。这样，我们也可以把 $A$ 以外的结果排除掉，并将 $A$ 看成新的样本空间 $(A,A\cap\mathcal{F},\mathbb{P}_A)$。
- **条件概率依然是一个概率测度**；关于概率的性质对条件概率都成立。

> [!EXAMPLE]- 例题：条件概率 vs 无条件概率（古典概型对照）
> **题目**：$\Omega=\{1,2,3\}$，古典概型，$A=\{1,2\}$。写出条件概率测度 $\mathbb{P}_A$。
> 
> **解**：条件化之后新的样本空间 $\widetilde{\Omega}=\{1,2\}=A$，新事件域 $\widetilde{\mathcal{F}}=A\cap\mathcal{F}$。对照如下：
> 
> | 事件 | $\mathbb{P}$（无条件） | 事件（条件化后） | $\mathbb{P}_A$（条件） |
> | --- | --- | --- | --- |
> | $\{1,2\}$ | $2/3$ | $\{1,2\}$ | $1$ |
> | $\{2\}$ | $1/3$ | $\{2\}$ | $1/2$ |
> | $\{3\}$ | $1/3$ | $\emptyset$ | $0$ |
> 
> （注：此步补全了计算，如 $\mathbb{P}_A(\{2\})=\mathbb{P}(\{2\}\cap A)/\mathbb{P}(A)=(1/3)/(2/3)=1/2$。）

### 4.4 $\mathbb{P}(B\mid A)$ 与 $\mathbb{P}(B)$ 的大小关系

> [!WARNING] 辨析
> 条件化之后概率可大可小，$\mathbb{P}(B\mid A)$ 和 $\mathbb{P}(B)$ 的大小关系**不确定**：
> 1. 当 $B\subset A$ 时，
> 
> $$
> \mathbb{P}(B\mid A)=\frac{\mathbb{P}(A\cap B)}{\mathbb{P}(A)}=\frac{\mathbb{P}(B)}{\mathbb{P}(A)}\geq\mathbb{P}(B)
> $$
> 
> （条件信息"利好" $B$，概率被放大）；
> 2. 当 $A\cap B=\emptyset$ 时，$\mathbb{P}(B\mid A)=0\leq\mathbb{P}(B)$（条件信息直接否定了 $B$）。

### 4.5 基于条件概率的概率模型

> [!EXAMPLE]- 例题：雷达探测
> **题目**：有一台雷达探测设备在探测是否其上空区域有飞机。分别标记两个事件 $A=\{\text{飞机出现}\}$，$B=\{\text{雷达报警}\}$。已知 $\mathbb{P}(A)=0.05$，$\mathbb{P}(B\mid A)=0.99$，$\mathbb{P}(B^c\mid A)=0.01$，$\mathbb{P}(A^c)=0.95$，$\mathbb{P}(B\mid A^c)=0.10$，$\mathbb{P}(B^c\mid A^c)=0.90$（序贯树形图的四个叶子为 $A\cap B,A\cap B^c,A^c\cap B,A^c\cap B^c$）。
> 
> **解**：
> 
> $$
> \mathbb{P}(A\cap B)=\mathbb{P}(A)\mathbb{P}(B\mid A)=0.05\times 0.99=0.0495
> $$
> 
> $$
> \mathbb{P}(B)=0.05\times 0.99+0.95\times 0.1=0.1445
> $$
> 
> （注：此步补全了依据——对分割 $\{A,A^c\}$ 用全概率公式，见第六节。）
> 
> $$
> \mathbb{P}(A\mid B)=\frac{\mathbb{P}(A\cap B)}{\mathbb{P}(B)}=\frac{0.0495}{0.1445}\approx 0.34
> $$
> 
> 即：雷达报警时，真有飞机的概率只有约 34%——条件概率把"先验" 5% 更新到了"后验" 34%。

---

## 五、乘法公式

### 5.1 序贯树形图

利用**序贯树形图**计算概率，规则如下：
1. 设立一个序贯树形图，让关心的事件处于图的末端（叶子）。由根节点一直到树的子树的路径上每一个节点代表一个事件，我们关心的事件的发生是由根节点一直到叶子的一系列事件发生的结果；
2. 在路径的每个分枝上写上相应的条件概率；
3. 叶子所代表的事件发生的概率是相应的分枝上的条件概率的**乘积**。

**例：统计语言模型**。一句话 $S=\text{Where are we going}$ 的概率，按"前文（context）→ 待预测词"逐词分解：

$$
\mathbb{P}(S)=\mathbb{P}(\text{Where})\times\mathbb{P}(\text{are}\mid\text{Where})\times\mathbb{P}(\text{we}\mid\text{Where are})\times\mathbb{P}(\text{going}\mid\text{Where are we})
$$

这正是现代语言模型逐词生成文本的概率基础。

### 5.2 乘法公式

> [!IMPORTANT] 定理（乘法公式）【常用】
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$A_i\in\mathcal{F}$，$i=1,\ldots,n$，且 $\mathbb{P}(A_1\cap A_2\cap\cdots\cap A_{n-1})>0$，则
> 
> $$
> \mathbb{P}\left(\bigcap_{i=1}^{n}A_i\right)=\mathbb{P}(A_1)\prod_{i=2}^{n}\mathbb{P}(A_i\mid A_1\cap A_2\cap\cdots\cap A_{i-1})
> $$

**证明**：因为 $\mathbb{P}(A_1\cap\cdots\cap A_{n-1})>0$，所以

$$
\mathbb{P}(A_1)\geq\mathbb{P}(A_1\cap A_2)\geq\cdots\geq\mathbb{P}(A_1\cap\cdots\cap A_{n-1})>0
$$

即定理中的条件概率都有意义。由条件概率的定义（注：此步补全了——右端逐项展开为 $\mathbb{P}(A_1)\cdot\frac{\mathbb{P}(A_1A_2)}{\mathbb{P}(A_1)}\cdot\frac{\mathbb{P}(A_1A_2A_3)}{\mathbb{P}(A_1A_2)}\cdots\frac{\mathbb{P}(A_1\cdots A_n)}{\mathbb{P}(A_1\cdots A_{n-1})}$，相邻分子分母依次相消），可知结论成立。$\blacksquare$

> [!NOTE] 备注
> 事件可任意换序，所以其实是 $n!$ 个公式。什么是合适的顺序？——选择的艺术（通常按信息的自然获得顺序条件化，使每个条件概率好算）。

### 5.3 例题：配对问题

> [!EXAMPLE]- 例题：配对问题（信封装信）
> **题目**：某人写了 $n$ 封信，将其装入 $n$ 个信封，并在每个信封上分别任意地写上 $n$ 个收信人的一个地址（不重复），求：
> （1）没有一个信封上所写的地址正确的概率 $q_0$；
> （2）恰有 $r$ 个信封上所写的地址正确的概率 $q_r$（$r\leq n$）。
> 
> **解（1）**：设 $A_i=$ "第 $i$ 个信封上所写的地址正确"，$i=1,2,\ldots,n$，则 $\bigcup_{i=1}^{n}A_i$ 表示"$n$ 个信封上至少有一个信封上所写地址正确"，故 $q_0=1-\mathbb{P}\left(\bigcup_{i=1}^{n}A_i\right)$。
> 
> 利用乘法公式逐层计算交事件概率：
> - 对任意的 $1\leq i\leq n$，有 $\mathbb{P}(A_i)=\dfrac{(n-1)!}{n!}=\dfrac{1}{n}$；
> - 对任意的 $1\leq i<j\leq n$，有
> 
> $$
> \mathbb{P}(A_iA_j)=\mathbb{P}(A_i)\mathbb{P}(A_j\mid A_i)=\frac{1}{n}\cdot\frac{1}{n-1}=\frac{(n-2)!}{n!}
> $$
> 
> - 对任意的 $1\leq i<j<k\leq n$，有 $\mathbb{P}(A_iA_jA_k)=\dfrac{(n-3)!}{n!}$（注：此步补全了——$\mathbb{P}(A_iA_jA_k)=\frac{1}{n}\cdot\frac{1}{n-1}\cdot\frac{1}{n-2}$，乘法公式连乘三层）；
> - 一般地，$\mathbb{P}(A_1A_2\cdots A_n)=\dfrac{1}{n!}$。
> 
> 从而由容斥原理：
> 
> $$
> \begin{align}
> \mathbb{P}\left(\bigcup_{i=1}^{n}A_i\right)&=\sum_{i=1}^{n}\mathbb{P}(A_i)-\sum_{1\leq i<j\leq n}\mathbb{P}(A_iA_j)+\sum_{1\leq i<j<k\leq n}\mathbb{P}(A_iA_jA_k)-\cdots+(-1)^{n-1}\mathbb{P}\left(\bigcap_{i=1}^{n}A_i\right)\\
> &=\binom{n}{1}\mathbb{P}(A_1)-\binom{n}{2}\mathbb{P}(A_1A_2)+\cdots+(-1)^{n-1}\mathbb{P}\left(\bigcap_{i=1}^{n}A_i\right)\\
> &=\binom{n}{1}\frac{1}{n}-\binom{n}{2}\frac{(n-2)!}{n!}+\cdots+(-1)^{n-1}\frac{1}{n!}\\
> &=1-\frac{1}{2!}+\frac{1}{3!}-\cdots+(-1)^{n-1}\frac{1}{n!}
> \end{align}
> $$
> 
> （注：此步补全了通项化简——$\binom{n}{k}\dfrac{(n-k)!}{n!}=\dfrac{n!}{k!(n-k)!}\cdot\dfrac{(n-k)!}{n!}=\dfrac{1}{k!}$。）
> 
> 因此
> 
> $$
> q_0=1-\mathbb{P}\left(\bigcup_{i=1}^{n}A_i\right)=\frac{1}{2!}-\frac{1}{3!}+\cdots+(-1)^{n}\frac{1}{n!}=\sum_{k=0}^{n}\frac{(-1)^k}{k!}
> $$
> 
> 进一步，由于 $q_0$ 跟 $n$ 有关，故一般记为 $q_0(n)$。从而
> 
> $$
> \lim_{n\to\infty}q_0(n)=e^{-1}=0.36787944117144233\cdots
> $$
> 
> 即，当 $n$ 非常大的时候，$q_0\approx 0.37$。
> 
> **解（2）**：因为在指定的"某 $r$ 个（不妨设前 $r$ 个）信封上所写的地址是正确的"这一事件的概率相当于"从 $n$ 个不同编号的球中**无放回**摸取 $r$ 个正好依次摸得前 $r$ 号的概率"，即
> 
> $$
> \frac{1}{n(n-1)\cdots(n-r+1)}
> $$
> 
> 而其余 $(n-r)$ 个信封上所写地址都不正确的概率为（由（1），把问题缩小到剩下的 $n-r$ 封信上）
> 
> $$
> q_0(n-r)=\sum_{k=0}^{n-r}\frac{(-1)^k}{k!}
> $$
> 
> 又从 $n$ 个信封里取 $r$ 个组合，共 $\binom{n}{r}$ 种取法，故所求概率为
> 
> $$
> q_r=\binom{n}{r}\cdot\frac{1}{n(n-1)\cdots(n-r+1)}\cdot\sum_{k=0}^{n-r}\frac{(-1)^k}{k!}=\frac{1}{r!}\sum_{k=0}^{n-r}\frac{(-1)^k}{k!}
> $$
> 
> （注：此步补全了化简——$\binom{n}{r}=\dfrac{n(n-1)\cdots(n-r+1)}{r!}$，与中间因子相消只剩 $\dfrac{1}{r!}$。当 $n$ 大时 $q_r\approx\dfrac{e^{-1}}{r!}$，即正确配对数近似服从 $\mathcal{P}(1)$。）

---

## 六、全概率公式

**想法**：将 $\Omega$ 分割成事件 $A_1,A_2,A_3$ 的并；对每个 $i$，得到 $\mathbb{P}(B\mid A_i)$；计算 $\mathbb{P}(B)$ 的方法之一：$\mathbb{P}(B)=\sum_{i=1}^{3}\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)$（Venn 图上 $B$ 被分割切成三块，树形图上 $B$ 是三条路径的叶子之和）。

### 6.1 全概率公式

> [!IMPORTANT] 定理（Total Probability Theorem 全概率公式）【常用】
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$B,A_i\in\mathcal{F}$，$i=1,\ldots,n$，且 $\mathbb{P}(A_i)>0$，$\{A_i\}$ 是 $\Omega$ 的一个**分割**，则
> 
> $$
> \mathbb{P}(B)=\mathbb{P}(A_1)\mathbb{P}(B\mid A_1)+\cdots+\mathbb{P}(A_n)\mathbb{P}(B\mid A_n)
> $$
> 
> 其中 $\{A_i\}$ 是 $\Omega$ 的一个分割指：$\Omega=\bigcup_{i=1}^{n}A_i$，且 $A_i\cap A_j=\emptyset$，$\forall i\neq j$，$i,j\in\{1,\ldots,n\}$。

**直觉**：把"$B$ 发生"按"它经由哪种情形发生"分门别类，每一类贡献 $\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)$，加总即得整体概率——"分而治之"。

> [!NOTE] 备注
> - 特别地，如果 $0<\mathbb{P}(A)<1$，则 $\mathbb{P}(B)=\mathbb{P}(A)\mathbb{P}(B\mid A)+\mathbb{P}(A^c)\mathbb{P}(B\mid A^c)$；
> - 在定理中，$n$ 可以换成 $\infty$；
> - 该定理的一个主要应用：计算事件 $B$ 的概率。关键是找到**合适的分割** $A_1,\ldots,A_n$。通常，分割跟实际问题的背景有关。什么是合适的分割？——选择的艺术。

### 6.2 例题：无放回摸球（抽签公平性）

> [!EXAMPLE]- 例题：第 k 次取得黑球的概率
> **题目**：设一袋中有 $n$ 个白球与 $m$ 个黑球，现从中**无放回**连续抽取 $k$ 个球，求第 $k$ 次取得黑球的概率（$1\leq k\leq n+m$）。设 $A_k=$ "第 $k$ 次摸得黑球"，$k=1,2,\ldots,n+m$。
> 
> **解法 1（排列计数）**：把球看成是编号了的，从 $n+m$ 个球中摸取 $k$ 个排成一行，有
> 
> $$
> P_{n+m}^{k}=(n+m)(n+m-1)\cdots(n+m-k+1)
> $$
> 
> 种取法，即该试验的基本事件总数为 $P_{n+m}^{k}$。因为第 $k$ 个位置上是黑球，有 $P_m^1$ 种取法，而前 $k-1$ 个位置上可以是其余 $n+m-1$ 个球中任意 $k-1$ 个球，共有 $P_{n+m-1}^{k-1}$ 种取法；于是 $A_k$ 包含的基本事件数为 $P_{n+m-1}^{k-1}\cdot P_m^1$，从而所求概率为
> 
> $$
> \mathbb{P}(A_k)=\frac{P_{n+m-1}^{k-1}\,P_m^1}{P_{n+m}^{k}}=\frac{m}{n+m}
> $$
> 
> （注：此步补全了约分——$\dfrac{P_{n+m-1}^{k-1}\cdot m}{P_{n+m}^{k}}=\dfrac{(n+m-1)!/(n+m-k)!\cdot m}{(n+m)!/(n+m-k)!}=\dfrac{m}{n+m}$。）
> 
> **解法 2（归纳法 + 全概率公式）**：显然 $\mathbb{P}(A_1)=\dfrac{m}{n+m}$；
> 
> $$
> \mathbb{P}(A_2)=\mathbb{P}(A_1)\mathbb{P}(A_2\mid A_1)+\mathbb{P}(A_1^c)\mathbb{P}(A_2\mid A_1^c)=\frac{m}{n+m}\cdot\frac{m-1}{n+m-1}+\frac{n}{n+m}\cdot\frac{m}{n+m-1}=\frac{m}{n+m}
> $$
> 
> （注：此步补全了通分——分子为 $m(m-1)+nm=m(n+m-1)$，与分母 $(n+m)(n+m-1)$ 约去 $(n+m-1)$。）
> 
> **归纳假设**："无论开始黑球、白球个数是多少，无放回抽到第 $i$ 次时，抽到黑球的概率都是初始状态中黑球的比例"。
> 
> **往证**："无放回抽到第 $i+1$ 次时，抽到黑球的概率是初始状态中黑球的比例"，即 $\mathbb{P}(A_{i+1})=\dfrac{m}{n+m}$，$i+1\leq n+m$。
> 
> 因为（按第 1 次摸球结果分割，用全概率公式）
> 
> $$
> \mathbb{P}(A_{i+1})=\mathbb{P}(A_1)\mathbb{P}(A_{i+1}\mid A_1)+\mathbb{P}(A_1^c)\mathbb{P}(A_{i+1}\mid A_1^c)=\frac{m}{n+m}\mathbb{P}(A_{i+1}\mid A_1)+\frac{n}{n+m}\mathbb{P}(A_{i+1}\mid A_1^c)
> $$
> 
> 由于 $\mathbb{P}(A_{i+1}\mid A_1)$ 表示在 $m-1$ 个黑球与 $n$ 个白球的袋中第 $i$ 次摸得黑球的概率，根据假设有
> 
> $$
> \mathbb{P}(A_{i+1}\mid A_1)=\frac{m-1}{n+m-1}
> $$
> 
> 同理，
> 
> $$
> \mathbb{P}(A_{i+1}\mid A_1^c)=\frac{m}{n+m-1}
> $$
> 
> 所以
> 
> $$
> \mathbb{P}(A_{i+1})=\frac{m}{n+m}\cdot\frac{m-1}{n+m-1}+\frac{n}{n+m}\cdot\frac{m}{n+m-1}=\frac{m}{n+m}
> $$
> 
> 故对一切 $k$，$\mathbb{P}(A_k)=\dfrac{m}{n+m}$。这就是**抽签与次序无关**（抽签公平性）的数学表述。

### 6.3 全概率公式的实际应用：敏感问题调查

> [!EXAMPLE]- 例题：敏感问题调查（随机化回答）
> **题目**：在调查家庭暴力（或服用兴奋剂、吸毒等敏感问题）所占家庭的比例 $p$ 时，被调查者往往不愿回答真相，这使得调查数据失真。为得到实际的 $p$ 同时又不侵犯个人隐私，调查人员将一些球放入袋中，其中红球比例为 $p_0$、白球比例为 $q_0=1-p_0$。被调查者在袋中任取一球窥视后放回，并承诺取得红球就讲真话、取到白球就讲假话。被调查者只需在匿名调查表中选"是"（有家庭暴力）或"否"，然后将表放入投票箱。没人能知道被调查者是否讲真话和回答的是什么。如果每个家庭回答"是"的概率为 $p_1$，求 $p$。
> 
> **解**：对任选的一个家庭，用 $B$ 表示回答"是"，用 $A$ 表示取到红球。利用全概率公式得
> 
> $$
> \begin{align}
> p_1=\mathbb{P}(B)&=\mathbb{P}(A)\mathbb{P}(B\mid A)+\mathbb{P}(A^c)\mathbb{P}(B\mid A^c)\\
> &=p\,p_0+(1-p)q_0\\
> &=q_0+(p_0-q_0)p
> \end{align}
> $$
> 
> （注：此步补全了两个条件概率的来历——取到红球讲真话，有暴力才答"是"，故 $\mathbb{P}(B\mid A)=p$；取到白球讲假话，**没有**暴力反而答"是"，故 $\mathbb{P}(B\mid A^c)=1-p$。）
> 
> 于是，只要 $p_0\neq q_0$，
> 
> $$
> p=\frac{p_1-q_0}{p_0-q_0}
> $$
> 
> 在实际问题中，$p_1$ 是未知的，需要经过调查得到。假设调查了 $n$ 个家庭，其中有 $k$ 个家庭回答"是"，则可以用 $\hat{p}_1=k/n$ 估计 $p_1$，于是可以用
> 
> $$
> \hat{p}=\frac{\hat{p}_1-q_0}{p_0-q_0}
> $$
> 
> 去估计 $p$。
> 
> **数值例**：如果袋中放 30 个红球、50 个白球，调查了 320 个家庭，其中有 195 个家庭回答"是"，则 $p_0=3/8$，$q_0=5/8$，$\hat{p}_1=195/320$，
> 
> $$
> \hat{p}=\frac{195/320-5/8}{3/8-5/8}=\frac{-0.015625}{-0.25}=6.25\%
> $$
> 
> （注：此步补全了数值——$195/320=0.609375$，$5/8=0.625$。）
> 
> 可以证明 $|p_0-q_0|$ 越大，得到的结论越可靠；但是 $|p_0-q_0|$ 越大，调查方法越不易被被调查者接受（红白球比例悬殊时，回答暴露真相的风险变大）。

---

## 七、Bayes 准则

**问题**：已知 $\mathbb{P}(B\mid A_i)$，$\forall i$，求 $\mathbb{P}(A_i\mid B)$。（给定 $B$ 发生了，我们要修正对各"原因" $A_i$ 的**信念程度**。）

$$
\mathbb{P}(A_i\mid B)=\frac{\mathbb{P}(A_i\cap B)}{\mathbb{P}(B)}=\frac{\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)}{\sum_{j=1}^{n}\mathbb{P}(A_j)\mathbb{P}(B\mid A_j)},\quad i=1,\ldots,n
$$

Bayes 准则可以用来进行**推理**：由"原因 $\to$ 结果"的正向概率（似然），反推"结果 $\to$ 原因"的逆向概率。$\mathbb{P}(A_i)$ 称为**先验概率**，$\mathbb{P}(A_i\mid B)$ 称为**后验概率**。

### 7.1 Bayes 准则

> [!IMPORTANT] 定理（Bayes' Rule）【常用】
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$B,A_i\in\mathcal{F}$，$i=1,\ldots,n$，且 $\mathbb{P}(B)>0$，$\mathbb{P}(A_i)>0$，$\{A_i\}$ 是 $\Omega$ 的一个分割，则
> 
> $$
> \mathbb{P}(A_i\mid B)=\frac{\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)}{\sum_{j=1}^{n}\mathbb{P}(A_j)\mathbb{P}(B\mid A_j)},\quad i=1,\ldots,n
> $$
> 
> 特别地，当 $\mathbb{P}(B)>0$ 时，有
> 
> $$
> \mathbb{P}(A\mid B)=\frac{\mathbb{P}(A)\mathbb{P}(B\mid A)}{\mathbb{P}(A)\mathbb{P}(B\mid A)+\mathbb{P}(A^c)\mathbb{P}(B\mid A^c)}
> $$

**证明思路**：分子用条件概率定义（乘法公式）$\mathbb{P}(A_i\cap B)=\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)$，分母用全概率公式展开 $\mathbb{P}(B)$，两步合并即得。

> [!NOTE] 备注
> 课件思考题："信息的先后顺序影响结果么？"——Bayes 公式表明，后验只取决于先验与似然的乘积，与信息到达的先后顺序无关（多条信息可逐次更新，结果一致）。Thomas Bayes（1702–1761）。

> [!WARNING] 辨析
> - **先验概率** $\mathbb{P}(A_i)$：观察到证据 $B$ **之前**对原因的信念；
> - **后验概率** $\mathbb{P}(A_i\mid B)$：观察到证据 $B$ **之后**修正过的信念；
> - 切勿混淆 $\mathbb{P}(A\mid B)$ 与 $\mathbb{P}(B\mid A)$（"检验阳性者患病的概率"与"患病者检验阳性的概率"完全是两码事，见下例）。

### 7.2 例题：假阳性之谜

> [!EXAMPLE]- 例题：The False-Positive Puzzle（假阳性之谜）
> **题目**：设对于某种少见的疾病，假定某一人群中患有这种病的概率为 0.001。医院推出某检验方法的准确率为 95%：如果一个被检的人有这种疾病，其检查结果为阳性的概率为 95%；如果该人没有这种疾病，其检查结果为阳性的概率为 5%。现在从这个总体中随机抽取一个人进行检测，检查结果为阳性。问这个人患这种疾病的概率有多大？
> 
> **解**：记 $A$ 为这个人有这种疾病，$B$ 为检验结果为阳性。利用 Bayes 准则
> 
> $$
> \begin{align}
> \mathbb{P}(A\mid B)&=\frac{\mathbb{P}(A)\mathbb{P}(B\mid A)}{\mathbb{P}(A)\mathbb{P}(B\mid A)+\mathbb{P}(A^c)\mathbb{P}(B\mid A^c)}\\
> &=\frac{0.001\times 0.95}{0.001\times 0.95+(1-0.001)\times(1-0.95)}\\
> &=\frac{0.00095}{0.00095+0.04995}\\
> &=0.01866405\cdots\approx 1.87\%
> \end{align}
> $$
> 
> （注：此步补全了中间数值——分母第二项 $0.999\times 0.05=0.04995$，分母合计 $0.0509$。）
> 
> **结论**：检验呈阳性，真正患病的概率竟然不到 2%！造成这个结果的原因是**发病率较低**（先验太小）和**诊断的准确性不够高**（5% 的假阳性率在庞大的健康人群中制造了大量假阳性）。

### 7.3 Bayes 准则的实际应用

- **贝叶斯统计**（Bayesian Statistics）：如 Lancet（Wu et al. 2020）对 2019-nCoV 疫情在武汉的国内外潜在传播进行 nowcasting / forecasting 的建模研究，核心就是用观测数据不断更新参数（如基本再生数）的后验分布。
- **贝叶斯网络**（Bayesian networks）：用有向图组织大量随机变量之间的条件概率关系进行推理（如三层 BN 疾病诊断模型）；其奠基人 Judea Pearl 获 2011 年图灵奖。

---

## 八、小结（课件原文）

**知识点**：
- 概率空间（事件域、概率是一种测度）；
- 概率的性质（续）：极限（抓住主要矛盾）；
- 条件概率：基于条件概率的三大法则——乘法法则、全概率公式、Bayes 准则（学术规范很重要；发现正确的问题比解决问题更重要）。

**三大法则速查表**：

| 法则 | 公式 | 用途 |
| --- | --- | --- |
| 乘法公式 | $\mathbb{P}(\bigcap_{i=1}^{n}A_i)=\mathbb{P}(A_1)\prod_{i=2}^{n}\mathbb{P}(A_i\mid A_1\cdots A_{i-1})$ | 算"一连串事件都发生"的概率 |
| 全概率公式 | $\mathbb{P}(B)=\sum_{i}\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)$ | 由"原因"算"结果"的概率 |
| Bayes 准则 | $\mathbb{P}(A_i\mid B)=\dfrac{\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)}{\sum_j\mathbb{P}(A_j)\mathbb{P}(B\mid A_j)}$ | 由"结果"反推"原因"（更新信念） |

**技巧**：
- 类比熟悉的概念/技巧，理解、掌握新概念（e.g. 数列的极限 → 集合的极限）；
- 复杂概念/定理，找简单例子，通过逐层拆解进行理解（e.g. 集合的上下极限）；
- 把复杂的大问题拆分成简单的小问题；
- 根据经验挑选好简化计算的条件概率的顺序、样本空间的分割。

---

## 九、附录：不可测集举例（不要求掌握）

（不要求，略。内容梗概：以一维几何概型 $\Omega=[-2,2]$、$\mathbb{P}(A)=\text{length}(A)/\text{length}(\Omega)$ 为例，在 $[0,1]$ 上用"$x\sim y\iff x-y\in\mathbb{Q}$"定义等价类，借助**选择公理**从每个等价类各取一个代表元构成集合 $E$（Vitali 集）；再用 $\mathbb{Q}$ 的可数性把 $E$ 平移出可数个互不相交的副本 $E_n=r_n+E$，满足 $[0,1]\subseteq\bigcup_{n=1}^{\infty}E_n\subseteq[-1,2]$；最后反证：若 $\mathbb{P}(E)$ 存在，由平移不变性与可列可加性得 $0<\sum_{n=1}^{\infty}\mathbb{P}(E)<\infty$，而该级数要么为 0 要么为 $\infty$，矛盾——故 $E$ 不可分配概率，即不可列样本空间上确实存在不可测集。）

---

## 本讲方法/题型清单

- **判断一个集合系是否为 σ-域** → 证伪用封闭性、证实用定义 → 证伪：找两个成员，其并/补不在集合系中（如 $\mathcal{F}\cup\mathcal{G}$ 反例）；证实：逐条验证 $\Omega\in\mathcal{F}$、对补封闭、对可列并封闭。
- **由若干事件生成 σ-域** → 原子法 → 先求 $A,B$ 的全部"原子"（$AB,AB^c,A^cB,A^cB^c$），σ-域 = 原子的一切并，共 $2^{\text{原子数}}$ 个元素。
- **求单调事件列极限的概率** → 概率的连续性 → 先认定单调增/减，写出 $\lim A_n=\bigcup A_i$ 或 $\bigcap B_i$，再交换 $\mathbb{P}$ 与 $\lim$。
- **判断"事件无穷多次发生 / 最终一直发生"的概率** → 上下极限 + Borel–Cantelli 引理 → 把问题翻译为 $\limsup A_n$ 或 $\liminf A_n$；验证 $\sum\mathbb{P}(A_n)$ 收敛（结论概率 0）或发散且独立（结论概率 1）；"最终一直发生"用对偶 $\mathbb{P}(\liminf A_n)=1-\mathbb{P}(\limsup A_n^c)$。
- **求"已知 A 发生时 B 的概率"** → 条件概率定义 → 算 $\mathbb{P}(A\cap B)$ 与 $\mathbb{P}(A)$ 后相除；古典概型下可直接缩小样本空间数数：$\mathbb{P}(B\mid A)=\#(A\cap B)/\#(A)$。
- **求"一连串事件依次发生"的概率（无放回抽取、逐词生成等）** → 乘法公式 / 序贯树形图 → 按时间顺序条件化逐层相乘；树形图上叶子概率 = 路径上分枝条件概率之积；顺序可换，选条件概率好算的顺序。
- **求"至少一个 / 恰好 r 个"型概率（配对问题）** → 乘法公式算交事件 + 容斥原理 → 算 $\mathbb{P}(A_{i_1}\cdots A_{i_k})=(n-k)!/n!$，代入容斥，利用 $\binom{n}{k}\frac{(n-k)!}{n!}=\frac{1}{k!}$ 化简；"恰好 r 个"= 选位置 × 指定位置全对 × 其余全错。
- **所求事件概率难直接算，但分情形后好算** → 全概率公式 → 找合适分割 $\{A_i\}$（常按第一步结果、所属类别等分），$\mathbb{P}(B)=\sum_i\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)$；情形无穷时 $n$ 换 $\infty$。
- **证明与次序无关的抽取概率（抽签公平性）** → 归纳法 + 全概率公式 → 对第 1 次结果分割，归纳假设"比例不变"，验证递推后比例仍为初始比例。
- **已知"原因→结果"概率，反求"结果→原因"概率** → Bayes 准则 → 分子 = 先验 × 似然，分母 = 全概率公式；警惕低先验下的"假阳性之谜"，勿混淆 $\mathbb{P}(A\mid B)$ 与 $\mathbb{P}(B\mid A)$。
- **敏感问题调查（隐私保护下估计比例）** → 随机化回答 + 全概率公式 → 设计随机装置（红/白球），列 $p_1=q_0+(p_0-q_0)p$，解出 $p=(p_1-q_0)/(p_0-q_0)$，用频率 $\hat{p}_1=k/n$ 代入估计。
