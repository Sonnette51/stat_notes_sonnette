---
title: "Lecture01 概率模型与性质"
tags:
  - 概率论
  - 前半学期
  - 概率模型
  - 样本空间
  - 概率公理
---

# Lecture01 概率模型与性质

> [!ABSTRACT] 本讲概要
> 概率论的出发点是给"随机试验"建一个数学模型：先把所有可能结果收进一个集合（样本空间），再给结果的集合（事件）分配一个表示"信念程度"的数（概率）。本讲（Bertsekas & Tsitsiklis Ch1 1.2, 1.6）围绕概率模型的两大构件、概率公理及其推论性质、随机抽样的四种基本模式展开。

## 一、概率模型

### 1.1 概率模型的基本构成

引入例：我们关心一门课的成绩（A, B, C, …），这就是一个随机试验。

> [!IMPORTANT] 概率模型的基本构成
> 
> 一个概率模型由两部分组成：
> 
> 1. **样本空间 $\Omega$**：一个试验的所有可能结果的集合；
> 2. **概率**：为试验结果的集合 $A$（称之为事件）确定一个非负数 $\mathbb{P}(A)$（称为事件 $A$ 的概率）。此非负数刻画了我们对事件 $A$ 的认识或所产生的信念程度。

**直觉**：样本空间回答"会发生什么"，概率回答"各种情况发生的可能性多大"。两者合起来才是一个完整的模型。

---

### 1.2 样本空间

> [!INFO] 定义（样本空间）
> 
> 样本空间是一个**集合**：每一个概率模型都关联着一个试验，这个试验将产生一个试验结果，该试验的**所有可能结果**形成样本空间，记作 $\Omega$。

**直觉**：样本空间就是把"所有可能发生的事"一个不漏、互不重复地列成清单。

样本空间必须满足的要求：
- 试验结果必须**互斥**（不同结果不能同时发生），并且**完整**（穷尽所有可能）。
- 试验结果**可能是有限**的，也**可能是无限**多个试验结果组成。

> [!NOTE] 备注
> 
> 一个试验由什么构成，并没有什么限制。然而我们讨论的概率模型的问题中，只涉及一个试验。所以"连续抛三次硬币"的试验，只能作为**一次**试验，不能认为是三次试验。

### 1.3 样本空间——选择的艺术

选择样本空间的原则：
- 即便对同一个试验，根据我们的兴趣也可以确定**不同的模型**。
- 在确定 $\Omega$ 时，既要有足够多的细节，又要避免不必要的繁琐。

> [!EXAMPLE]- 例子 1：两个抛硬币游戏（样本空间的不同选法）
> 
> 考虑两个不同的游戏，它们都涉及连续抛掷 10 次硬币：
> 
> - **游戏一**：每次抛掷硬币只要出现正面向上，甲就赢 1 元钱。（只与 10 次抛掷中正面向上的次数有关）
> - **游戏二**：每次抛掷硬币甲都赢 1 元钱，直到出现第一次正面向上（包括这一次）；继续抛掷，甲每次赢 2 元钱，直到第二次正面向上；每次抛掷得到正面向上的时候，以后每次抛掷硬币所赢的钱数比以前每次抛掷硬币所赢的钱数加倍。（不仅跟正面出现的次数有关，还跟出现的顺序有关）
> 
> **解**（注：此处补全了课件未明写的结论）：
> 
> - 游戏一的收益只依赖正面次数，取样本空间 $\Omega_1 = \lbrace 0, 1, 2, \ldots, 10 \rbrace$（正面向上的次数）就足够了，共 11 个结果。
> - 游戏二的收益依赖正面出现的具体位置（顺序），必须取完整的序列样本空间 $\Omega_2 = \lbrace \text{正}, \text{反} \rbrace^{10}$，共 $2^{10} = 1024$ 个结果。
> 
> 同一个物理试验，因关心的问题不同，合理的样本空间可以完全不同——这就是"选择的艺术"。

### 1.4 离散例（序贯模型）

很多试验本身具有**有序性**的特征，比如连续抛掷一枚四面体的骰子，一共抛两次；或者连续观测一只股票，共观测五天。常用**序贯树形图**来刻画样本空间中的试验结果：从根 (Root) 出发，每一层对应一次观测，叶子 (Leaves) 对应一个完整的试验结果。例如四面体骰子掷两次，样本空间可以画成 $4 \times 4$ 的格点图，也可以画成两层的树形图，共 16 个叶子。

### 1.5 连续例

> [!EXAMPLE]- 例子 2：约会延迟的样本空间
> 
> 甲和乙约定在某时刻见面，而每个人到达约会地点的时间都会有延迟，延迟时间在 0~1 小时。
> 
> **解**：考虑直角坐标系的单位正方形
> 
> $$\Omega = [0,1] \times [0,1] = \lbrace (x,y) \mid 0 \leq x, y \leq 1 \rbrace$$
> 
> 正方形中的每一个点的两个坐标分别表示他们各自可能的延迟时间。这是一个典型的**连续（不可数）样本空间**。

---

## 二、概率与概率公理

### 2.1 事件与概率

> [!INFO] 定义（事件）
> 
> **事件**：样本空间的子集，即某些试验结果的集合。事件"发生"，或者事件"不发生"。

**直觉**：事件就是"我们关心的一类结果"打包成的集合；试验结果落在这个集合里，就说事件发生了。

> [!INFO] 定义（概率的含义）
> 
> **概率**：分配到事件上的数。它是一种"信念"，例如"百分百确定"、"不可能"。

### 2.2 概率公理

> [!IMPORTANT] 概率公理
> 
> 1. **（非负性）** 对一切事件 $A$，满足 $\mathbb{P}(A) \geq 0$。
> 2. **（归一化）** $\mathbb{P}(\Omega) = 1$。
> 3. **（可加性）** 若 $A \cap B = \emptyset$，那么 $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B)$。

**直觉**：概率像"质量"——总质量为 1，分到互不重叠的块上可以直接相加，且每块质量非负。

**课件中的讨论（四个问题）**：
- 需要增加一条公理 $\mathbb{P}(A) \leq 1$ 么？（注：不需要，后面性质 4 的推论 2 表明它可以由三条公理推出。）
- 有限可加性：例如 $\mathbb{P}(\lbrace s_1, s_2, \ldots, s_k \rbrace) = \mathbb{P}(\lbrace s_1 \rbrace) + \cdots + \mathbb{P}(\lbrace s_k \rbrace) = \mathbb{P}(s_1) + \cdots + \mathbb{P}(s_k)$，即有限个互斥事件可以逐个相加。
- 公理 3 需要加强。（→ 见第五部分：加强为可列可加性）
- 任意样本空间的子集都可以分配概率么？（注：一般不行，这涉及可测性问题，本课不深入。）

---

## 三、离散模型与连续模型

### 3.1 离散模型

离散样本空间上，给每个样本点赋概率，事件的概率即其中样本点概率之和。

> [!EXAMPLE]- 例题 1：均匀四面体骰子掷两次
> 
> 假设骰子是均匀的，每一面出现的机会是相同的。连续抛掷一枚四面体骰子两次，记第一次、第二次的点数为 $X, Y$。求：
> 
> 1. $\mathbb{P}\big((X,Y) \text{ 是 } (1,1) \text{ 或 } (1,2)\big)$；
> 2. $\mathbb{P}(X = 1)$；
> 3. $\mathbb{P}(X + Y \text{ 是奇数})$；
> 4. $\mathbb{P}\big(\min(X,Y) = 2\big)$。
> 
> **解**（注：课件将答案留作"?"，此处补全全部计算）：
> 
> 样本空间 $\Omega = \lbrace (i,j) \mid i, j = 1,2,3,4 \rbrace$，共 16 个等可能结果，每个概率 $\frac{1}{16}$。
> 
> 1. 事件含 2 个样本点 $(1,1), (1,2)$，故概率为 $\frac{2}{16} = \frac{1}{8}$。
> 2. $X = 1$ 对应 $(1,1), (1,2), (1,3), (1,4)$ 共 4 个点，概率 $\frac{4}{16} = \frac{1}{4}$。
> 3. $X+Y$ 为奇数当且仅当一个为奇数、一个为偶数。$\lbrace 1,2,3,4 \rbrace$ 中奇数 2 个、偶数 2 个，故样本点数为 $2 \times 2 + 2 \times 2 = 8$，概率 $\frac{8}{16} = \frac{1}{2}$。
> 4. $\min(X,Y) = 2$ 即两数均 $\geq 2$ 且至少一个等于 2。均 $\geq 2$ 的点有 $3 \times 3 = 9$ 个，均 $\geq 3$ 的点有 $2 \times 2 = 4$ 个，故恰好 $\min = 2$ 的点有 $9 - 4 = 5$ 个，概率 $\frac{5}{16}$。

### 3.2 离散模型特例：古典概型

> [!IMPORTANT] 古典概型（离散均匀概率）
> 
> 设样本空间 $\Omega$ 由 $n$ 个**等可能性**的试验结果组成，因此每个试验结果组成的事件（称为基本事件）的概率是相等的。由此得到
> 
> $$\mathbb{P}(A) = \frac{\text{含于事件 } A \text{ 的试验结果数}}{n}$$

**直觉**：当每个结果"一视同仁"时，算概率就退化为数数——数 $A$ 里有几个结果，再除以总数。

### 3.3 连续模型

> [!EXAMPLE]- 例子 4：约会相遇问题
> 
> 甲和乙约定在某时刻见面，而每个人到达约会地点的时间都会有延迟，延迟时间在 0~1 小时。第一个到达约会地点的人会在那儿等待 15 分钟，等了 15 分钟后若对方还没有出现，先到者会离开约会地点。问他们能够相会的概率有多大？
> 
> **解**：
> 
> 将 $\Omega$ 的子集出现的概率定义为这个子集的**面积**。此定义符合概率的三条公理（非负、$\Omega$ 面积为 1、不相交集合面积可加）。
> 
> 两人相会当且仅当延迟时间之差不超过 15 分钟（$\frac{1}{4}$ 小时），即事件
> 
> $$M = \left\lbrace (x,y) \ \middle| \ |x - y| \leq \frac{1}{4},\ 0 \leq x \leq 1,\ 0 \leq y \leq 1 \right\rbrace$$
> 
> 所求的概率即为 $M$ 的面积。（注：此步补全了面积的具体计算）$M$ 是单位正方形去掉两个直角边长为 $\frac{3}{4}$ 的等腰直角三角形后剩下的斜带形区域，故
> 
> $$\mathbb{P}(M) = 1 - 2 \times \frac{1}{2} \times \left(\frac{3}{4}\right)^2 = 1 - \frac{9}{16} = \frac{7}{16}$$

### 3.4 连续模型特例：几何概型

用 $\mathbb{R}^r$ 表示 $r$ 维向量空间，$\mathbb{R}^r = \lbrace (x_1, x_2, \ldots, x_r) \mid x_i \in (-\infty, \infty), 1 \leq i \leq r \rbrace$。对于 $\mathbb{R}^r$ 的子集 $A$，用

$$m(A) = \int_A dx_1 dx_2 \cdots dx_r$$

表示集合 $A$ 的体积。

> [!IMPORTANT] 几何概率模型（连续均匀概率）
> 
> 设样本空间 $\Omega \subset \mathbb{R}^r$ 的体积 $m(\Omega)$ 是正数，且 $\Omega$ 中的每个试验结果发生的**可能性相同**，则对于事件 $A \subset \Omega$，其发生的概率为
> 
> $$\mathbb{P}(A) = \frac{m(A)}{m(\Omega)}$$

**直觉**：几何概型是古典概型的连续版本——"数个数"换成"量体积（长度、面积）"。

> [!WARNING] 辨析
> 
> 古典概型要求**有限个等可能结果**、用"个数之比"；几何概型要求**连续区域上均匀**、用"体积之比"。两者都依赖"等可能"假设，但等可能的含义（计数测度 vs 体积测度）完全不同，不可混用。

---

## 四、模型与现实：Bertrand 悖论

不同的"等可能"假设可以导致不同的概率模型，进而得到不同的答案——建模时必须明确随机机制。

> [!EXAMPLE]- 例子 5（Bertrand 悖论）：随机弦的长度
> 
> 在半径为 1 的圆内任取一条弦，求弦长大于等于 $\sqrt{3}$ 的概率。
> 
> （注：圆的内接等边三角形的边长为 $\sqrt{3}$。）用 $\Omega$ 表示试验的样本空间，用 $A$ 表示得到的弦长大于等于 $\sqrt{3}$。
> 
> **解法 (1)**：如果认为弦的端点等可能的落在圆周上，则点 $x_0$ 确定后另一点 $y$ 也等可能的落在圆周上。因为 $\Omega = \lbrace y \mid y \in [0, 2\pi) \rbrace$，$A = \left\lbrace y \ \middle| \ \dfrac{2\pi}{3} \leq y \leq \dfrac{4\pi}{3} \right\rbrace$。于是
> 
> $$\mathbb{P}(A) = \frac{1}{3}$$
> 
> （注：此步补全直觉——固定一个端点后，弦长 $\geq \sqrt{3}$ 当且仅当另一端点落在对侧三分之一圆弧上，弧长 $\frac{2\pi}{3}$ 占全圆 $2\pi$ 的 $\frac{1}{3}$。）
> 
> **解法 (2)**：如果认为弦的中点等可能的落在与之垂直的直径上：当且仅当其中点与圆心的距离小于 $\frac{1}{2}$ 时，它的弦长才大于 $\sqrt{3}$。因此
> 
> $$\mathbb{P}(A) = \frac{1}{2}$$
> 
> （注：此步补全直觉——直径长为 2，中点离圆心距离 $< \frac{1}{2}$ 的部分总长为 1，占比 $\frac{1}{2}$。）
> 
> **解法 (3)**：如果认为弦的中点等可能的落在圆内，则 $\Omega$ 是大圆盘，$A$ 是半径 $\frac{1}{2}$ 的小圆盘。因此
> 
> $$\mathbb{P}(A) = \frac{\pi (1/2)^2}{\pi \cdot 1^2} = \frac{1}{4}$$

> [!WARNING] 易错
> 
> 从 Bertrand 悖论可以看出：**不同的等可能假设可以导致不同的计算结果**。"随机取一条弦"这句话本身没有唯一确定概率模型；做几何概型题目时，必须先明确"什么东西在什么集合上均匀分布"。

---

## 五、概率公理 3：加强为可列可加性

> [!EXAMPLE]- 例 6：为什么有限可加性不够用
> 
> 抛硬币直到第一次出现正面，记所需次数为试验结果。
> 
> - 样本空间：$\lbrace 1, 2, \ldots \rbrace$；
> - $\mathbb{P}(n) = 2^{-n}$，$n = 1, 2, \ldots$；
> - 求 $\mathbb{P}(\text{outcome is even})$。
> 
> **解**：
> 
> $$\mathbb{P}(\lbrace 2, 4, 6, \ldots \rbrace) = \mathbb{P}(2) + \mathbb{P}(4) + \cdots = \frac{1}{2^2} + \frac{1}{2^4} + \cdots = \frac{1/4}{1 - 1/4} = \frac{1}{3}$$
> 
> （注：此步补全了等比级数求和，公比为 $\frac{1}{4}$。）这里把**可列无穷多个**互斥事件的概率相加，仅有"两个事件可加"的公理 3 推不出这一步，必须加强公理。

> [!IMPORTANT] 可列可加性（公理 3 的加强）
> 
> 若 $A_1, A_2, \ldots$ 是互不相交的事件，那么
> 
> $$\mathbb{P}(A_1 \cup A_2 \cup \cdots) = \mathbb{P}(A_1) + \mathbb{P}(A_2) + \cdots$$

从此概率公理的最终版本为：
1. **（非负性）** 对一切事件 $A$，满足 $\mathbb{P}(A) \geq 0$；
2. **（归一化）** $\mathbb{P}(\Omega) = 1$；
3. **（可列可加性）** 若 $A_1, A_2, \ldots$ 是互不相交的事件，那么 $\mathbb{P}(A_1 \cup A_2 \cup \cdots) = \mathbb{P}(A_1) + \mathbb{P}(A_2) + \cdots$。

---

## 六、概率的性质

### 6.1 直观的概率性质（维恩图验证）

利用维恩图可以直观验证概率的若干性质：
- 若 $A \subset B$，则 $\mathbb{P}(A) \leq \mathbb{P}(B)$。
- $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$。
- $\mathbb{P}(A \cup B) \leq \mathbb{P}(A) + \mathbb{P}(B)$。
- $\mathbb{P}(A \cup B \cup C) = \mathbb{P}(A) + \mathbb{P}(A^c \cap B) + \mathbb{P}(A^c \cap B^c \cap C)$（把并集切成互不相交的三块）。

下面从三条公理出发**严格证明**九条性质。

### 6.2 性质一览表

| 编号 | 性质 | 公式 | 重要程度 |
| --- | --- | --- | --- |
| 1 | 空集概率为零 | $\mathbb{P}(\emptyset) = 0$ | 常用 |
| 2 | 有限可加性 | $A_i$ 两两不交 $\Rightarrow \mathbb{P}\left(\bigcup_{i=1}^{n} A_i\right) = \sum_{i=1}^{n} \mathbb{P}(A_i)$ | 常用 |
| 3 | 对立事件 | $\mathbb{P}(A^c) = 1 - \mathbb{P}(A)$ | 常用 |
| 4 | 差事件 | $A \subset B \Rightarrow \mathbb{P}(B \setminus A) = \mathbb{P}(B) - \mathbb{P}(A)$ | 常用 |
| 5 | 加法公式 | $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$ | 常用 |
| 6 | 容斥恒等式 | 见 6.8 | 常用 |
| 7 | Bonferroni / Kounias 不等式 | 见 6.9 | 了解即可 |
| 8 | 可列次可加性 | $\mathbb{P}\left(\bigcup_{i=1}^{\infty} A_i\right) \leq \sum_{i=1}^{\infty} \mathbb{P}(A_i)$ | 常用 |
| 9 | 交事件下界 | $\mathbb{P}\left(\bigcap_{i=1}^{\infty} A_i\right) \geq 1 - \sum_{i=1}^{\infty} \mathbb{P}(A_i^c)$ | 了解即可 |

### 6.3 性质 1：$\mathbb{P}(\emptyset) = 0$

**证明**：因为 $\Omega = \Omega \cup \emptyset \cup \emptyset \cup \cdots$，由概率公理 (3) 得

$$\mathbb{P}(\Omega) = \mathbb{P}(\Omega \cup \emptyset \cup \emptyset \cup \cdots) = \mathbb{P}(\Omega) + \mathbb{P}(\emptyset) + \mathbb{P}(\emptyset) + \cdots$$

由概率公理 (2)，得

$$1 = 1 + \mathbb{P}(\emptyset) + \mathbb{P}(\emptyset) + \cdots$$

即 $0 = \mathbb{P}(\emptyset) + \mathbb{P}(\emptyset) + \cdots$，再由概率公理 (1)（每项非负），得 $\mathbb{P}(\emptyset) = 0$。

### 6.4 性质 2：概率的有限可加性

设有事件 $A_i$，$i = 1, \ldots, n$，且 $A_i \cap A_j = \emptyset$，$i \neq j$，则

$$\mathbb{P}\left(\bigcup_{i=1}^{n} A_i\right) = \sum_{i=1}^{n} \mathbb{P}(A_i)$$

**证明**：令 $A_{n+1} = A_{n+2} = \cdots = \emptyset$，则 $\bigcup_{i=1}^{n} A_i = \bigcup_{i=1}^{\infty} A_i$，且当 $i \neq j$ 时 $A_i \cap A_j = \emptyset$。由概率公理 (3) 和性质 1，可得

$$\mathbb{P}\left(\bigcup_{i=1}^{n} A_i\right) = \mathbb{P}\left(\bigcup_{i=1}^{\infty} A_i\right) = \sum_{i=1}^{\infty} \mathbb{P}(A_i) = \sum_{i=1}^{n} \mathbb{P}(A_i)$$

**直觉**：把"无穷可加"里多余的位置塞满空集即可退回有限情形。

### 6.5 性质 3：对立事件

如果有事件 $A$，则 $\mathbb{P}(A^c) = 1 - \mathbb{P}(A)$。

**证明**：因为 $A \cap A^c = \emptyset$，$A \cup A^c = \Omega$，由性质 2 和概率公理 (2) 得

$$1 = \mathbb{P}(\Omega) = \mathbb{P}(A \cup A^c) = \mathbb{P}(A) + \mathbb{P}(A^c)$$

故 $\mathbb{P}(A^c) = 1 - \mathbb{P}(A)$。

**直觉**："正难则反"的依据——事件不发生的概率等于 1 减去发生的概率。

### 6.6 性质 4：差事件公式与单调性

如果有事件 $A, B$，且 $A \subset B$，则 $\mathbb{P}(B \setminus A) = \mathbb{P}(B) - \mathbb{P}(A)$。

**证明**：因为 $B = A \cup (B \setminus A)$ 且 $A \cap (B \setminus A) = \emptyset$，由性质 2 得

$$\mathbb{P}(B) = \mathbb{P}(A) + \mathbb{P}(B \setminus A)$$

即 $\mathbb{P}(B \setminus A) = \mathbb{P}(B) - \mathbb{P}(A)$。

**推论**：
1. **（概率的单调性）** 如果有事件 $A, B$，且 $A \subset B$，则 $\mathbb{P}(A) \leq \mathbb{P}(B)$；
2. 对任意的事件 $A$，有 $0 \leq \mathbb{P}(A) \leq 1$。（这回答了 2.2 节的问题：$\mathbb{P}(A) \leq 1$ 无需作为公理。）

> [!WARNING] 易错
> 
> $\mathbb{P}(B \setminus A) = \mathbb{P}(B) - \mathbb{P}(A)$ 只在 $A \subset B$ 时成立！一般情形应为 $\mathbb{P}(B \setminus A) = \mathbb{P}(B) - \mathbb{P}(A \cap B)$。

### 6.7 性质 5：加法公式与 Boole 不等式

如果有事件 $A, B$，则 $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$。

**证明**：因为 $A \cup B = A \cup (B \setminus A)$，且 $A \cap (B \setminus A) = \emptyset$，由性质 2 和性质 4 得

$$\begin{align}
\mathbb{P}(A \cup B) &= \mathbb{P}(A) + \mathbb{P}(B \setminus A) \\
&= \mathbb{P}(A) + \mathbb{P}(B \setminus (A \cap B)) \\
&= \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)
\end{align}$$

（注：此步补全了 $B \setminus A = B \setminus (A \cap B)$ 且 $A \cap B \subset B$，故可用性质 4。）

**推论（有限次可加性，finite subadditivity，或 Boole's inequality）**：如果有事件 $A_i$，$i = 1, \ldots, n$，则

$$\mathbb{P}\left(\bigcup_{i=1}^{n} A_i\right) \leq \sum_{i=1}^{n} \mathbb{P}(A_i)$$

**直觉**：并集的概率不超过各自概率之和，因为重叠部分被重复计算了。

### 6.8 性质 6：容斥恒等式（The inclusion-exclusion formula）

如果有事件 $A_i$，$i = 1, \ldots, n$，则

$$\begin{align}
\mathbb{P}\left(\bigcup_{i=1}^{n} A_i\right) &= \sum_{1 \leq i \leq n} \mathbb{P}(A_i) - \sum_{1 \leq i < j \leq n} \mathbb{P}(A_i \cap A_j) \\
&\quad + \sum_{1 \leq i < j < k \leq n} \mathbb{P}(A_i \cap A_j \cap A_k) - \cdots + (-1)^{n-1} \mathbb{P}(A_1 \cap A_2 \cap \cdots \cap A_n)
\end{align}$$

**直觉与证明思路**：先加单个、再减两两相交、再加三三相交……"多退少补"，恰好让每个样本点被数一次。形式证明可对 $n$ 用数学归纳法，从性质 5 出发归纳推广。

### 6.9 性质 7：Bonferroni 不等式与 Kounias 不等式（了解即可）

**（Bonferroni's inequality）** 如果有事件 $A_i$，$i = 1, \ldots, n$，则

$$\mathbb{P}\left(\bigcup_{i=1}^{n} A_i\right) \geq \sum_{1 \leq i \leq n} \mathbb{P}(A_i) - \sum_{1 \leq i < j \leq n} \mathbb{P}(A_i \cap A_j)$$

**（Kounias's inequality）**

$$\mathbb{P}\left(\bigcup_{i=1}^{n} A_i\right) \leq \min_{k} \left\lbrace \sum_{1 \leq i \leq n} \mathbb{P}(A_i) - \sum_{i: i \neq k} \mathbb{P}(A_i \cap A_k) \right\rbrace$$

**直觉**：容斥恒等式截断到第二项给出下界（Bonferroni）；而 Kounias 只扣掉与某个固定事件 $A_k$ 的重叠，再对 $k$ 取最优，给出比 Boole 不等式更紧的上界。

### 6.10 性质 8：可列次可加性（$\sigma$-subadditivity）

如果有事件 $A_i$，$i = 1, 2, \ldots$，则

$$\mathbb{P}\left(\bigcup_{i=1}^{\infty} A_i\right) \leq \sum_{i=1}^{\infty} \mathbb{P}(A_i)$$

**证明**：令 $B_1 = A_1$，$B_n = A_n \setminus \bigcup_{i=1}^{n-1} A_i$，则 $\bigcup_{i=1}^{\infty} A_i = \bigcup_{i=1}^{\infty} B_i$ 且 $B_i \cap B_j = \emptyset$（$i \neq j$），$B_n \subset A_n$。由概率公理 (3) 和概率的单调性，得

$$\mathbb{P}\left(\bigcup_{i=1}^{\infty} A_i\right) = \mathbb{P}\left(\bigcup_{i=1}^{\infty} B_i\right) = \sum_{i=1}^{\infty} \mathbb{P}(B_i) \leq \sum_{i=1}^{\infty} \mathbb{P}(A_i)$$

**直觉**："不相交化"技巧——把并集改写成两两不交的"新增部分"$B_n$ 之并，是概率论中反复出现的标准手法。

### 6.11 性质 9：交事件的概率下界（了解即可）

如果有事件 $A_i$，$i = 1, 2, \ldots$，则

$$\mathbb{P}\left(\bigcap_{i=1}^{\infty} A_i\right) \geq 1 - \sum_{i=1}^{\infty} \mathbb{P}(A_i^c)$$

特别地，

$$\mathbb{P}(A_1 \cap A_2) \geq 1 - \mathbb{P}(A_1^c) - \mathbb{P}(A_2^c)$$

**证明**：由性质 3 和性质 8 得

$$\mathbb{P}\left(\bigcap_{i=1}^{\infty} A_i\right) = 1 - \mathbb{P}\left(\left(\bigcap_{i=1}^{\infty} A_i\right)^c\right) = 1 - \mathbb{P}\left(\bigcup_{i=1}^{\infty} A_i^c\right) \geq 1 - \sum_{i=1}^{\infty} \mathbb{P}(A_i^c)$$

特别地，令 $A_3 = A_4 = \cdots = \Omega$，由性质 1（$\mathbb{P}(\Omega^c) = \mathbb{P}(\emptyset) = 0$），可得第二个结论。

**直觉**："每个事件都几乎必然发生，则它们同时发生也几乎必然"——损失最多是各事件不发生概率的累加。

---

## 七、随机抽样与随机分配

### 7.1 排列与组合

排列与组合的基本计数公式：
1. $n$ 个对象的排列数：$n!$；
2. $n$ 个对象中取 $k$ 个对象的排列数：$P_n^k = \dfrac{n!}{(n-k)!}$；
3. $n$ 个对象中取 $k$ 个对象的组合数：$\dbinom{n}{k} = \dfrac{n!}{k!(n-k)!}$。

**讨论**：在含有 $M$ 个不同球的箱子中抽取 $n$ 个球的不同方法，课件给出三个生活化场景帮助区分排列与组合：
- 雨课堂点名（抽取并区分先后/身份 → 排列）；
- 选班长、副班长（选出的人职位不同 → 排列）；
- 一二九大合唱（只要选出一组人，不分次序 → 组合）。

### 7.2 不同方式的随机抽样

**有放回抽样与无放回抽样**：
- 如果每次将抽到的球在下一次抽球前放回箱子中，则试验称做**放回抽样**。这时，由 $n$ 个球形成的每一个样本可以表示为向量 $(a_1, \ldots, a_n)$，其中 $a_i$（$i = 1, \ldots, n$）是第 $i$ 次抽到的球的编号。易见，对于放回抽样，每个 $a_i$ 可以是 $\lbrace 1, 2, \ldots, M \rbrace$ 中的任何一个数。
- 假设 $n \leq M$，且凡是抽到的球都不再放回，则试验称做**无放回抽样**。

**有序抽样和无序抽样**：样本空间的描述，本质上与如下情形有关：诸如 $(4,1,2,1)$ 和 $(1,4,2,1)$，是认为是"不同的基本事件"，还是"同一基本事件"。因此，习惯上区分两种情形：
- 对**有序抽样**，由相同元素组成的两个样本，只要其中元素的前后顺序有所不同，就视为"不同"的样本。
- 对**无序抽样**，不管元素的顺序，只要由相同元素组成的样本，都视为"同一"样本。
- 为强调具体的样本属于哪一种，对有序样本，使用记号 $(a_1, \ldots, a_n)$，而无序样本则记作 $[a_1, \ldots, a_n]$。

> [!EXAMPLE]- 例题 2：$M = 3$，$n = 2$ 时四种抽样的基本事件列表
> 
> 自含有 $M$ 个球的箱子中作 $n$ 次抽样（$M = 3$，$n = 2$），相应基本事件的结构列表如下：
> 
> | 抽样方式 | 有序/无序 | 基本事件 |
> | --- | --- | --- |
> | 放回 | 有序 | $(i,j)$，$i,j = 1,2,3$（共 $9$ 个） |
> | 放回 | 无序 | $[1,1],[2,2],[3,3],[1,2],[1,3],[2,3]$（共 $6$ 个） |
> | 不放回 | 有序 | $(1,2),(2,1),(1,3),(3,1),(2,3),(3,2)$（共 $6$ 个） |
> | 不放回 | 无序 | $[1,2],[1,3],[2,3]$（共 $3$ 个） |
> 
> （注：个数为补全的核对，分别对应 $M^n = 9$、$\binom{M+n-1}{n} = \binom{4}{2} = 6$、$P_M^n = 6$、$\binom{M}{n} = 3$。）

### 7.3 随机抽样的样本空间与计数

**1. 有放回抽样**

**1.1 放回有序抽样**：样本空间 $\Omega$ 具有如下构造：

$$\Omega = \lbrace \omega : \omega = (a_1, \ldots, a_n),\quad a_i \in \lbrace 1, 2, \ldots, M \rbrace \rbrace$$

且 $\#(\Omega) = M^n$。

**1.2 放回无序抽样**：样本空间 $\Omega$ 具有如下构造：

$$\Omega = \lbrace \omega : \omega = [a_1, \ldots, a_n],\quad a_i \in \lbrace 1, 2, \ldots, M \rbrace \rbrace$$

且 $\#(\Omega) = \dbinom{M+n-1}{n}$。

**2. 无放回抽样**

**2.1 不放回有序抽样**：样本空间 $\Omega$ 具有如下构造：

$$\Omega = \lbrace \omega : \omega = (a_1, \ldots, a_n),\quad a_k \neq a_l,\ k \neq l,\ a_i \in \lbrace 1, 2, \ldots, M \rbrace \rbrace$$

且 $\#(\Omega) = M(M-1) \cdots (M-n+1) = P_M^n$。

**2.2 不放回无序抽样**：样本空间 $\Omega$ 具有如下构造：

$$\Omega = \lbrace \omega : \omega = [a_1, \ldots, a_n],\quad a_k \neq a_l,\ k \neq l,\ a_i \in \lbrace 1, 2, \ldots, M \rbrace \rbrace$$

且 $\#(\Omega) = \dbinom{M}{n}$。

**汇总表**（自含有 $M$ 个球的箱子中作 $n$ 次抽样，不同抽样的总数）：

| 抽样方式 | 有序 | 无序 |
| --- | --- | --- |
| 放回 | $M^n$ | $\dbinom{M+n-1}{n}$ |
| 不放回 | $P_M^n$ | $\dbinom{M}{n}$ |

> [!WARNING] 辨析
> 
> 放回有序、不放回有序、不放回无序三种样本空间中基本事件都是等可能的，可以直接套古典概型；但**放回无序抽样的 $\binom{M+n-1}{n}$ 个基本事件不是等可能的**（例如 $[1,1]$ 只对应一条有序路径，而 $[1,2]$ 对应两条），用它做古典概型分母会出错。（注：此辨析为根据例题 2 补充的提醒。）

### 7.4 随机抽样与随机分配：按箱分配质点（选修）

（不要求，略。）课件大意：将 $n$ 个质点（小球）分配到 $M$ 个箱子中，与随机抽样一一对应——（有序抽样）$\Leftrightarrow$（质点可以辨）、（无序抽样）$\Leftrightarrow$（质点不可辨）、（放回抽样）$\Leftrightarrow$（箱中可容纳任意多质点，"无抑制"）、（不放回抽样）$\Leftrightarrow$（箱中最多可容纳一个质点，"有抑制"）。此问题产生于统计物理，比如研究 $n$ 个粒子（光子、电子等）按 $M$ 种状态的分布；课件以 2 个小球分配到 3 个箱子为例列出了全部基本事件。

---

## 八、关于古典概型的补充说明

### 8.1 古典概型问题小技巧

- 不要失去常识、也不要过分依赖（常识）；
- 用最简单情形验证（公式或答案）；
- 将物体编号（即使外观相同，也先视作可辨再计数）；
- 情景证明（story proof）：用计数的双重解释证明组合恒等式。

### 8.2 情景证明的思考题

课件给出以下思考题（注：以下证明思路为补全内容，课件仅列出命题）：

- $\dbinom{m}{n} = \dbinom{m-1}{n-1} + \dbinom{m-1}{n}$。
  **思路**：从 $m$ 个物体中选 $n$ 个，按"是否选第 $m$ 个物体"分类：选它则余下从 $m-1$ 个中选 $n-1$ 个；不选它则从 $m-1$ 个中选 $n$ 个。
- $\dbinom{m}{n} = \displaystyle\sum_{k=n-1}^{m-1} \dbinom{k}{n-1}$。
  **思路**：按所选 $n$ 个物体中**编号最大者**分类：最大编号为 $k+1$（$k$ 从 $n-1$ 到 $m-1$）时，其余 $n-1$ 个须从前 $k$ 个中选取，共 $\binom{k}{n-1}$ 种。
- 证明有放回无序抽样的结论 $\dbinom{M+n-1}{n}$。
  **思路（隔板法）**：一个无序放回样本由"每个编号被抽中的次数"$(x_1, \ldots, x_M)$ 唯一决定，$x_1 + \cdots + x_M = n$，$x_i \geq 0$ 为整数。把 $n$ 个相同的星与 $M-1$ 块隔板排成一行，方案数为 $\binom{M+n-1}{n}$。
- **（多项式系数）** 有 $m$ 个球，其中共 $r$ 种不同颜色，同色球不可辨识。这 $m$ 个球的排列共有多少种？（等价地，把 $m$ 个球放入 $r$ 个盒子中，使得 $m_j$ 个球进入第 $j$ 个盒子？）
  **思路**：先把 $m$ 个球视为可辨共 $m!$ 种排列，同色（第 $j$ 色共 $m_j$ 个）内部的 $m_j!$ 种交换不产生新排列，故共

$$\frac{m!}{m_1! \, m_2! \cdots m_r!} = \binom{m}{m_1, m_2, \ldots, m_r}$$

---

## 九、小结

**知识点**：
- 概念：试验、事件、样本空间、概率（含概率的公理化定义）；
- 经典概率模型：古典概型、几何概型；
- 概率的性质（利用公理推演得到）及证明：有限、可列；等式、不等式；
- 随机抽样方式：有放回与无放回、有序与无序。

**技巧**：
- 注意定义的明确性（e.g. 样本空间、等可能——Bertrand 悖论的教训）；
- 一些小的技巧，直观化、简单化（e.g. 情景证明、应用 $e^x$ 的 Taylor 展开公式进行近似）；
- 根据概率公理 (3) 的条件需求，拆成互斥集合；归纳法；求补。（本节课主要工具）

---

## 本讲方法/题型清单

- **判断样本空间怎么取** → 看清关心的量是什么 → 既要包含足够细节（如收益依赖顺序时要记录整个序列），又避免冗余（只依赖次数时记次数即可）。
- **有限等可能结果求概率** → 古典概型 → 确定 $\Omega$ 并核对等可能；数出 $A$ 中结果数；$\mathbb{P}(A) = \#A / \#\Omega$。
- **连续区域上均匀的概率** → 几何概型 → 写出 $\Omega \subset \mathbb{R}^r$；把事件翻译为子区域（常画图）；$\mathbb{P}(A) = m(A)/m(\Omega)$，算长度/面积/体积之比。
- **题目说"随机取……"但机制含糊** → 警惕 Bertrand 悖论 → 先明确什么量在什么集合上均匀，不同假设答案不同。
- **求并集概率** → 两个事件用加法公式 $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$；多个事件用容斥恒等式；只要上界用 Boole 不等式或 Kounias 不等式；只要下界用 Bonferroni 不等式。
- **求"至少/都不/同时"型概率** → 求补技巧（性质 3）→ $\mathbb{P}(A) = 1 - \mathbb{P}(A^c)$；交事件下界用性质 9。
- **证明概率等式/不等式** → 从公理出发 → 拆成互斥集合（$B_n = A_n \setminus \bigcup_{i<n} A_i$ 不相交化）、塞空集退化到有限、求补转化、再用可列可加与单调性。
- **计数抽样问题** → 先判定"放回/不放回 × 有序/无序" → 对应 $M^n$、$P_M^n$、$\binom{M}{n}$、$\binom{M+n-1}{n}$；注意放回无序的基本事件不等可能，不能直接当古典概型分母。
- **证明组合恒等式** → 情景证明（story proof）→ 给等式两边找同一个计数问题的两种数法（按某元素是否入选、按最大编号分类、隔板法等）。
