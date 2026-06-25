---
title: "Lecture03 独立性、随机变量"
tags:
  - 概率论
  - 前半学期
  - 独立性
  - 随机变量
---

# Lecture03 独立性、随机变量

> [!ABSTRACT] 本讲概要
> 本讲两条主线：一是把"$B$ 的发生不给 $A$ 带来新信息"这一直觉数学化为**事件的独立性**（含条件独立、相互独立、两两独立的层层辨析）；二是引入概率论的核心语言——**随机变量**，并定义随机变量的独立性。教材对应 Bertsekas & Tsitsiklis Ch2 2.1, 2.7, Ch3 3.5.4。

## 一、事件的独立性

### 1.1 引例：有偏硬币连掷三次

有一枚有偏的硬币，连续抛掷 3 次：$\mathbb{P}(H)=p$，$\mathbb{P}(T)=1-p$。课件用树状图列出 8 个结果（HHH, HHT, HTH, HTT, THH, THT, TTH, TTT），每条树枝标注 $p$ 或 $1-p$。

记 $H_k$ 为"第 $k$ 次正面向上"，$T_k$ 为"第 $k$ 次反面向上"，则：

- $\mathbb{P}(H_2\mid H_1)=p$；
- $\mathbb{P}(H_2\mid T_1)=p$；
- $\mathbb{P}(H_2)=\mathbb{P}(H_2\mid H_1)\mathbb{P}(H_1)+\mathbb{P}(H_2\mid T_1)\mathbb{P}(T_1)=p$。

**直觉**：无论第一次结果如何，第二次正面的概率都还是 $p$——第一次的结果没有给第二次带来任何信息，这就是"独立"。

---

### 1.2 两个事件的独立性（定义）

**"独立性"的直观定义**：事件 $B$ 的发生并没有给事件 $A$ 带来新的信息，它没有改变事件 $A$ 发生的概率，即 $\mathbb{P}(A\mid B)=\mathbb{P}(A)$。

> [!IMPORTANT] 定义（独立性 independence）【常用】
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$A,B\in\mathcal{F}$。如果
>
> $$
> \mathbb{P}(A\cap B)=\mathbb{P}(A)\mathbb{P}(B),
> $$
>
> 则称 $A$ 与 $B$ **相互独立**，简称**独立**。

**直觉**：交事件的概率恰好等于概率的乘积，意味着两个事件互相不提供任何信息。

**几点备注（课件逐条）：**

- 乘积式定义对 $A$、$B$ **对称**；对 $\mathbb{P}(B)=0$ 的情形同样适用；它**蕴含**直观定义 $\mathbb{P}(A\mid B)=\mathbb{P}(A)$（当 $\mathbb{P}(B)>0$ 时两者等价）。
- 显然，**不可能事件、必然事件与任何事件独立**。
- 若 $A$ 与 $B$ 独立，则：(i) $A$ 与 $B^c$ 独立；(ii) $A^c$ 与 $B$ 独立；(iii) $A^c$ 与 $B^c$ 独立。

**性质 (i)–(iii) 的证明思路**（注：此步补全了课件未写出的推导）：以 (i) 为例，

$$
\mathbb{P}(A\cap B^c)=\mathbb{P}(A)-\mathbb{P}(A\cap B)=\mathbb{P}(A)-\mathbb{P}(A)\mathbb{P}(B)=\mathbb{P}(A)\big(1-\mathbb{P}(B)\big)=\mathbb{P}(A)\mathbb{P}(B^c).
$$

(ii) 由对称性即得；(iii) 对 (i) 再用一次 (ii) 即得。

> [!WARNING] 辨析：独立 ≠ 不相交
> 注意独立性与**不相交（互斥）**的区别：互斥是集合关系 $A\cap B=\varnothing$，此时 $\mathbb{P}(A\cap B)=0$；若 $\mathbb{P}(A)>0,\mathbb{P}(B)>0$，互斥的两个事件**必不独立**（一个发生则另一个必不发生，信息量极大）。独立是概率（测度）关系，与集合是否相交无关。

**什么情况可能出现独立？**

- 同一试验可以有相互独立的事件；
- 不同试验也可以有相互独立的事件。

> [!EXAMPLE]- 例题 1：两个互不相干试验中的事件独立
> 用 $\Omega_1$ 和 $\Omega_2$ 分别表示互不相干的试验 $S_1$ 和 $S_2$ 的样本空间，设 $\Omega_1$ 和 $\Omega_2$ 的样本点分别是等可能的，并且
>
> $$
> \Omega_1=\{\mu_i\mid 1\le i\le n\},\qquad \Omega_2=\{\eta_j\mid 1\le j\le m\}.
> $$
>
> 则对 $A\subset\Omega_1$，$B\subset\Omega_2$，有 $A,B$ 独立。
>
> **解**（注：此步补全了课件未展开的验证）：把两个试验合在一起看，复合试验的样本空间为 $\Omega_1\times\Omega_2$，共 $nm$ 个等可能样本点。
>
> 事件 $A$ 在复合试验中对应 $A\times\Omega_2$，含 $|A|\cdot m$ 个点，故 $\mathbb{P}(A)=\dfrac{|A|m}{nm}=\dfrac{|A|}{n}$；同理 $\mathbb{P}(B)=\dfrac{|B|}{m}$。
>
> 事件 $A\cap B$ 对应 $A\times B$，含 $|A|\cdot|B|$ 个点，故
>
> $$
> \mathbb{P}(A\cap B)=\frac{|A||B|}{nm}=\frac{|A|}{n}\cdot\frac{|B|}{m}=\mathbb{P}(A)\mathbb{P}(B),
> $$
>
> 即 $A$ 与 $B$ 独立。

---

### 1.3 两个事件的条件独立性（定义）

> [!IMPORTANT] 定义（条件独立性 conditional independence）
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$A,B,C\in\mathcal{F}$，且 $\mathbb{P}(C)>0$。如果
>
> $$
> \mathbb{P}(A\cap B\mid C)=\mathbb{P}(A\mid C)\mathbb{P}(B\mid C),
> $$
>
> 则称 $A$ 与 $B$ 在给定 $C$ 之下**条件独立**。

**直觉**：在"已知 $C$ 发生"的新世界（条件概率测度 $\mathbb{P}(\cdot\mid C)$）里，$A$ 与 $B$ 互不提供信息。

课件提出的核心问题：**条件独立性是否蕴含独立性？反之是否成立？**——下一节用两个反例说明：**两个方向都不成立**。

---

### 1.4 独立性 vs 条件独立性

**图示反例（课件 Venn 图）**：即使假定 $A$、$B$ 相互独立，给定 $C$ 之后，$A$、$B$ 未必还相互独立——条件化会改变 $A$、$B$ 在新样本空间 $C$ 内的"比例结构"。

> [!EXAMPLE]- 例题 2：独立但不条件独立（两枚均匀硬币）
> 考虑抛掷两次均匀的硬币，这个试验的四种可能结果都是等可能的。令 $H_1=\{\text{第一枚硬币正面向上}\}$，$H_2=\{\text{第二枚硬币正面向上}\}$，$D=\{\text{两枚硬币的试验结果不同}\}$。则事件 $H_1$ 和事件 $H_2$ 是独立的，但是
>
> $$
> \mathbb{P}(H_i\mid D)=\frac{1}{2},\qquad \mathbb{P}(H_1\cap H_2\mid D)=0,\qquad i=1,2.
> $$
>
> 这样 $\mathbb{P}(H_1\cap H_2\mid D)\neq\mathbb{P}(H_1\mid D)\mathbb{P}(H_2\mid D)$，即 $H_1$ 和 $H_2$ 并不条件独立。
>
> **解**（注：此步补全了各概率的逐一验证）：样本空间 $\Omega=\{HH,HT,TH,TT\}$，每点概率 $\frac{1}{4}$。
>
> $H_1=\{HH,HT\}$，$H_2=\{HH,TH\}$，$D=\{HT,TH\}$。
>
> 独立性：$\mathbb{P}(H_1)=\mathbb{P}(H_2)=\frac{1}{2}$，$\mathbb{P}(H_1\cap H_2)=\mathbb{P}(\{HH\})=\frac{1}{4}=\frac{1}{2}\times\frac{1}{2}$，故 $H_1,H_2$ 独立。
>
> 条件概率：$\mathbb{P}(H_1\mid D)=\dfrac{\mathbb{P}(\{HT\})}{\mathbb{P}(D)}=\dfrac{1/4}{1/2}=\dfrac{1}{2}$；同理 $\mathbb{P}(H_2\mid D)=\dfrac{1}{2}$。
>
> 而 $H_1\cap H_2\cap D=\{HH\}\cap D=\varnothing$，故 $\mathbb{P}(H_1\cap H_2\mid D)=0\neq\dfrac{1}{4}=\mathbb{P}(H_1\mid D)\mathbb{P}(H_2\mid D)$。
>
> **结论**：给定 $D$ 后，知道第一枚是正面就完全确定第二枚是反面——条件之下两事件信息量拉满，不再独立。

> [!EXAMPLE]- 例题 3：条件独立但不独立（两枚不均匀硬币）
> 考虑两枚不均匀的硬币 $A$ 和 $B$：$\mathbb{P}(H\mid \text{coin }A)=0.9$，$\mathbb{P}(H\mid \text{coin }B)=0.1$。等概率选择两硬币之一进行抛掷（课件配树状图：先以 $0.5$、$0.5$ 分叉选硬币，再按 $0.9/0.1$ 分叉各次抛掷）。
>
> - 如果我们知道是硬币 $A$，不同的抛掷之间独立么？
> - 如果我们不知道是哪枚硬币，不同的抛掷之间独立么？
>
> **解**：记 $C=\{\text{选中硬币 }A\}$，$H_i=\{\text{第 }i\text{ 次正面}\}$，$\mathbb{P}(C)=\mathbb{P}(C^c)=\dfrac{1}{2}$。
>
> （1）给定选中的是硬币 $A$：每次抛掷正面概率恒为 $0.9$，且各次抛掷条件独立，
>
> $$
> \mathbb{P}(H_1\cap H_2\mid C)=0.9\times 0.9=\mathbb{P}(H_1\mid C)\mathbb{P}(H_2\mid C).
> $$
>
> 故**给定硬币后，不同抛掷之间（条件）独立**。
>
> （2）不知道是哪枚硬币时（注：此步补全了数值验证）：由全概率公式，
>
> $$
> \mathbb{P}(H_1)=\frac{1}{2}\times 0.9+\frac{1}{2}\times 0.1=0.5,\qquad \mathbb{P}(H_2)=0.5,
> $$
>
> $$
> \mathbb{P}(H_1\cap H_2)=\frac{1}{2}\times 0.9^2+\frac{1}{2}\times 0.1^2=\frac{1}{2}(0.81+0.01)=0.41\neq 0.25=\mathbb{P}(H_1)\mathbb{P}(H_2).
> $$
>
> 故**不知道硬币时，不同抛掷之间不独立**。
>
> **直觉**：第一次出现正面强烈暗示手里是硬币 $A$，从而抬高了第二次正面的概率——信息通过"是哪枚硬币"传递。

> [!WARNING] 辨析：独立与条件独立互不蕴含
> - 独立 $\not\Rightarrow$ 条件独立（例题 2：均匀硬币 + 条件 $D$）；
> - 条件独立 $\not\Rightarrow$ 独立（例题 3：不均匀硬币，给定硬币后条件独立，整体不独立）。
> 拿到题目时，"在谁的条件下独立"必须先问清楚。

---

### 1.5 一组事件的相互独立性（定义）

**直观定义**："一组事件的独立性"：任选其中一些事件，其信息不能为我们提供任何关于剩余事件的信息，或者说不改变剩余事件发生的概率。例如

$$
\mathbb{P}\big(A_1\cap(A_2^c\cup A_3)\mid A_5\cap A_6^c\big)=\mathbb{P}\big(A_1\cap(A_2^c\cup A_3)\big).
$$

> [!IMPORTANT] 定义（一组事件的独立性）【常用】
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$A_1,\ldots,A_n\in\mathcal{F}$。如果对任意非空子集 $S\subset\{1,2,\ldots,n\}$，都有
>
> $$
> \mathbb{P}\Big(\bigcap_{i\in S}A_i\Big)=\prod_{i\in S}\mathbb{P}(A_i),
> $$
>
> 则称 $A_1,A_2,\ldots,A_n$ 是**相互独立**的。

**直觉**：不是只要求"全体连乘"成立，而是**任挑一撮**事件，其交的概率都要能拆成乘积——这才保证任意组合之间互不提供信息。

> [!NOTE] 思考题（课件）
> 一定要任意非空子集 $S$ 么？
> 提示（注：此为补充说明）：$|S|=1$ 时等式平凡成立，真正需要验证的是所有 $|S|\ge 2$ 的子集，共 $2^n-n-1$ 条等式；只验证"全体连乘"一条是不够的，下面的两两独立反例正说明缺少某些子集等式会出问题。

---

### 1.6 一组事件的两两独立性（定义）

> [!IMPORTANT] 定义（两两独立性 Pairwise independence）
> 设 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，$A_1,\ldots,A_n\in\mathcal{F}$。如果
>
> $$
> \mathbb{P}(A_i\cap A_j)=\mathbb{P}(A_i)\mathbb{P}(A_j),\qquad i,j\in\{1,2,\ldots,n\},
> $$
>
> 则称 $A_1,A_2,\ldots,A_n$ 是**两两独立**的。

**直觉**：只检查"任意两个"事件之间互不提供信息，不管三个及以上的组合——这是比相互独立**弱**的条件。

---

### 1.7 两两独立 vs 相互独立

> [!EXAMPLE]- 例题 4：两两独立但不相互独立（正四面体染色，Bernstein 反例）
> 将一个均匀的正四面体的第一面染上红、黄、蓝三色，将其它三面分别染上红色、黄色、蓝色。设 $A,B,C$ 分别表示掷一次四面体红色、黄色、蓝色与桌面接触的事件，则
>
> $$
> \mathbb{P}(A)=\mathbb{P}(B)=\mathbb{P}(C)=\frac{1}{2},
> $$
>
> $$
> \mathbb{P}(A\cap B)=\frac{1}{4}=\mathbb{P}(A)\mathbb{P}(B),\quad
> \mathbb{P}(B\cap C)=\frac{1}{4}=\mathbb{P}(B)\mathbb{P}(C),\quad
> \mathbb{P}(A\cap C)=\frac{1}{4}=\mathbb{P}(A)\mathbb{P}(C).
> $$
>
> 但是 $\mathbb{P}(A\cap B\cap C)=\dfrac{1}{4}\neq\dfrac{1}{8}=\mathbb{P}(A)\mathbb{P}(B)\mathbb{P}(C)$。
>
> **解**（注：此步补全了各概率的来源）：四个面等可能（各 $\frac{1}{4}$）。红色出现在"三色面"和"纯红面"上，故 $\mathbb{P}(A)=\frac{2}{4}=\frac{1}{2}$，黄、蓝同理。两种颜色同时与桌面接触只能发生在三色面落地时，故 $\mathbb{P}(A\cap B)=\mathbb{P}(B\cap C)=\mathbb{P}(A\cap C)=\frac{1}{4}$，两两独立的等式逐对成立。三色同时接触也只能是三色面落地，故 $\mathbb{P}(A\cap B\cap C)=\frac{1}{4}\neq\frac{1}{8}$。
>
> **即：两两独立并不能保证相互独立！**

> [!WARNING] 辨析：相互独立 ⊋ 两两独立
> 相互独立 $\Rightarrow$ 两两独立（取 $|S|=2$ 的子集即可），但反向不成立（例题 4）。说"$n$ 个事件独立"时务必区分是哪一种。

---

### 1.8 事件独立性的应用

> [!EXAMPLE]- 例题 5：检测纸连测 20 人
> 设某地区某时期每人携带爆炸物或毒品的概率为 $0.04\%$，用一张新的检测纸连测 20 人，求此纸条含有爆炸物或毒品的概率。
>
> **解**：设 $A_i$ 为"第 $i$ 个人携带爆炸物或毒品"，$i=1,\ldots,20$，设可以认为诸 $A_i$ 是相互独立的。则所求的概率为
>
> $$
> \begin{align}
> \mathbb{P}\Big(\bigcup_{i=1}^{20}A_i\Big)&=1-\mathbb{P}\Big(\bigcap_{i=1}^{20}A_i^c\Big)\\
> &=1-\prod_{i=1}^{20}\mathbb{P}(A_i^c)\\
> &=1-(1-0.0004)^{20}\\
> &\approx 0.008.
> \end{align}
> $$
>
> **What if 1000 persons?** 课件给出答案 $33\%$。（注：此步补全了计算）
>
> $$
> 1-(1-0.0004)^{1000}=1-e^{1000\ln 0.9996}\approx 1-e^{-0.4}\approx 0.33,
> $$
>
> 即连测 1000 人时，检测纸有约 $33\%$ 的概率沾上爆炸物或毒品——小概率事件在大量重复下几乎必然出现。

> [!TIP] 方法：至少发生一个 → 取补集拆乘积
> 求"$n$ 个独立事件至少发生一个"的概率，套路是 $\mathbb{P}(\bigcup A_i)=1-\prod(1-\mathbb{P}(A_i))$：先取补集化为"全都不发生"，再用独立性把交拆成乘积。

---

### 1.9 条件概率及相关公式的小结

课件把第 2 讲以来的核心公式汇总如下（**条件概率依然是概率测度：所有关于概率的性质对条件概率都成立**）：

| 名称 | 条件 | 公式 |
| --- | --- | --- |
| 条件概率 | $A,B\in\mathcal{F}$，$\mathbb{P}(A)>0$ | $\mathbb{P}(B\mid A)=\dfrac{\mathbb{P}(A\cap B)}{\mathbb{P}(A)}$ |
| 乘法公式 | $A_i\in\mathcal{F}$，$\mathbb{P}(A_1\cap\cdots\cap A_{n-1})>0$ | $\mathbb{P}\Big(\displaystyle\bigcap_{i=1}^{n}A_i\Big)=\mathbb{P}(A_1)\displaystyle\prod_{i=2}^{n}\mathbb{P}(A_i\mid A_1\cap A_2\cap\cdots\cap A_{i-1})$ |
| 全概率公式 | $\{A_i\}$ 是 $\Omega$ 的一个分割，$\mathbb{P}(A_i)>0$ | $\mathbb{P}(B)=\mathbb{P}(A_1)\mathbb{P}(B\mid A_1)+\cdots+\mathbb{P}(A_n)\mathbb{P}(B\mid A_n)$ |
| Bayes 公式 | $\{A_i\}$ 是 $\Omega$ 的分割，$\mathbb{P}(B)>0$，$\mathbb{P}(A_i)>0$ | $\mathbb{P}(A_i\mid B)=\dfrac{\mathbb{P}(A_i)\mathbb{P}(B\mid A_i)}{\sum_{j=1}^{n}\mathbb{P}(A_j)\mathbb{P}(B\mid A_j)}$ |
| 独立性 | $A,B\in\mathcal{F}$ | $\mathbb{P}(A\cap B)=\mathbb{P}(A)\mathbb{P}(B)$ |

---

### 1.10 赌徒破产模型

> [!EXAMPLE]- 例题 6：赌徒破产模型（递归公式 + 边界条件）
> 甲有本金 $a$ 元，决心再赢 $b$ 元停止赌博。设甲每局赢得概率是 $p=1/2$，每局输赢都是一元钱，甲输光后停止赌博，求甲输光的概率 $q(a)$。
>
> **解**：用 $A$ 表示甲第一局赢，$B_k$ 表示甲有本金 $k$ 元时最后输光。由题意，$q(0)=1$，$q(a+b)=0$（注：此步补全了边界条件的含义——本金为 $0$ 即已输光，概率为 $1$；本金达到 $a+b$ 即赢满目标后收手，再无输光可能，概率为 $0$），并且记 $q(k)=\mathbb{P}(B_k)$。
>
> **递归公式**：对第一局的结果用全概率公式：
>
> $$
> \begin{align}
> q(k)=\mathbb{P}(B_k)&=\mathbb{P}(A)\mathbb{P}(B_k\mid A)+\mathbb{P}(A^c)\mathbb{P}(B_k\mid A^c)\\
> &=\frac{1}{2}\mathbb{P}(B_{k+1})+\frac{1}{2}\mathbb{P}(B_{k-1})=\frac{1}{2}\big[q(k+1)+q(k-1)\big].
> \end{align}
> $$
>
> （注：此步补全了 $\mathbb{P}(B_k\mid A)=q(k+1)$ 的理由——第一局赢后本金变为 $k+1$ 元，且其后的赌局与之前独立，输光概率与"从 $k+1$ 元起步"相同。）
>
> 于是有 $2q(k)=q(k+1)+q(k-1)$，从而差分相等：
>
> $$
> q(k+1)-q(k)=q(k)-q(k-1)=\cdots=q(1)-q(0)=q(1)-1.
> $$
>
> 因此把差分从 $0$ 累加到 $n$（注：此步补全了叠加过程：$q(n)-q(0)=\sum_{k=0}^{n-1}[q(k+1)-q(k)]=n[q(1)-1]$）：
>
> $$
> q(n)-1=n\big[q(1)-1\big].
> $$
>
> **边界条件**：取 $n=a+b$，得到
>
> $$
> 0-1=(a+b)\big[q(1)-1\big],\quad\text{i.e.,}\quad q(1)-1=-\frac{1}{a+b}.
> $$
>
> 故
>
> $$
> q(a)=1+a\big[q(1)-1\big]=1-\frac{a}{a+b}=\frac{b}{a+b}.
> $$
>
> **此概率说明**：当甲的本金 $a$ 有限，则贪心 $b$ 越大，输光的概率越大。如果一直赌下去（$b\to\infty$），必定输光（$q(a)\to 1$）。

> [!TIP] 方法：递归 + 边界条件
> 步数或步数不确定的随机试验（赌局、随机游走），用"对第一步条件化（首步分析）"建立递归公式，再用问题给出的边界条件解出通项——这是本讲技巧"归纳法求解非有限步或步数不确定的随机试验"的典型代表。

---

## 二、随机变量

### 2.1 为什么引进"随机变量"

**动机（来自赌徒破产模型）：**

- 在赌徒破产模型中，若关心"赌徒在某个特定时间还有多少赌金"，按之前的语言只能用记号 $A_{jk}$ 表示"赌徒在 $k$ 轮赌博后刚好有 $j$ 元"这样的事件——多个时间点就需要一大堆不同的记号。
- 更复杂地，若感兴趣"赌博了多少轮输光"的事件，用上述记号表示将会很复杂。
- 而下面的记号则相对轻松许多：用 $X_k$ 表示"赌徒在 $k$ 轮赌博之后剩的赌金"，用 $R=\min\{n:\ X_n=0\ \text{or}\ X_n=a+b\}$ 表示赌博持续的时间/轮数。

**四个引例（课件逐一给出）：**

- **血压**：人的血压总在不断变化之中。设甲的收缩压的变化范围是 90–180 mmHg，用 $X$ 表示甲的收缩压的测量结果，称 $X$ 是**随机变量**；$X=125$ 表示甲的收缩压是 125 mmHg。这里试验的样本空间是 $\Omega=[90,180]$，随机变量 $X$ 是 $\Omega$ 上的函数，满足 $X(\omega)=\omega$。
- **扑克**：在一副扑克的 52 张中任取 1 张，样本空间的每个点表示 1 张扑克。用 $X$ 表示所取扑克的大小，如 $X=3$ 表示所取到的扑克是 3。将 $X$ 视为样本空间上的函数 $X:\Omega\mapsto\mathbb{N}$，则
  
$$
\{X=3\}\triangleq\{\omega\mid X(\omega)=3\}=\{\clubsuit 3,\ \diamondsuit 3,\ \heartsuit 3,\ \spadesuit 3\}.
$$
  
  显然，对 $\forall x\in\mathbb{R}$，$\{X\le x\}$ 是一个事件，称 $X$ 是**随机变量**。由于 $X$ 的取值是数，可对 $X$ 进行数学运算。
- **抛硬币**：将一枚均匀的硬币连续抛掷两次，用 $X$ 表示得到正面的个数。这里试验的样本空间是 $\Omega=\{HH,HT,TH,TT\}$，随机变量 $X$ 是 $\Omega$ 上的函数，取值范围是 $\{0,1,2\}$。
- **两个孩子**：一个家庭计划连续要两个孩子，假设每个孩子的性别相互独立，且生男孩女孩是等可能的。用 $X$ 表示得到女孩的个数。样本空间是 $\Omega=\{BB,BG,GB,GG\}$，随机变量 $X$ 是 $\Omega$ 上的函数，取值范围是 $\{0,1,2\}$。

**引入随机变量的三大理由（课件强调）：**

- **（简化性）**"事件"是用来描述随机试验的某些现象是否出现的，要说明比较复杂的试验结果需要定义许多事件；随机变量让我们集中力量在关注的重点上。
- **（数值化）** 在许多概率模型中，试验结果是数值化的，比如仪器的仪表板的读数、股票的价格、气温等；还有其它的试验结果虽不是数值的，但这些试验结果与某些数值紧密相连。
- **（通用性）** 对随机试验来说，不仅关心试验出现什么结果，更重要的是要知道这些结果将以什么概率出现；可能多个场景通用一个模型，即"房子 vs 蓝图"。

---

### 2.2 "随机变量"是什么？

**给每个可能的试验结果分配一个数**。即，一个从样本空间 $\Omega$ 到实数轴 $\mathbb{R}$ 的函数（课件配图：$\Omega$ 中的样本点经 $X$ 映到数轴上的 $x$）。离散、连续均可能。

**讨论（课件三问）：**

- 随机变量也是映射，和概率（测度 $\mathbb{P}:\mathcal{F}\to[0,1]$）有什么区别？——定义域不同：随机变量定义在样本点上，概率定义在事件（集合）上。
- 随机性来自哪里？——来自 $\omega$：试验结果 $\omega$ 是随机的，$X(\omega)$ 本身是确定的函数。
- 对同一个样本空间，可以定义不同的随机变量。本质上，随机变量是一个试验某一方面的数值上的总结。

---

### 2.3 随机变量的应用

> [!EXAMPLE]- 例题 7：13 张牌中恰好 5 张梅花
> 在 52 张扑克牌中任取 13 张，求这 13 张牌中恰好有 5 张梅花的概率。
>
> **解**：
>
> **第一步（定义随机变量）**：用 $X$ 表示"这 13 张牌中梅花的张数"，则 $X=5$ 是关心的事件（**明确关心事件**）。
>
> 为了弄清 $X(\omega)$，设试验的样本空间 $\Omega=\{\omega\}$，即 $\Omega$ 由 $\binom{52}{13}$ 个样本点组成，每个样本点 $\omega$ 是不分次序的 13 张牌。$X(\omega)$ 是定义在 $\Omega$ 上的函数：
>
> $$
> X(\omega)=\text{“}\omega\text{ 中的梅花数”},\ \omega\in\Omega,\qquad \{X=5\}=\{\omega\mid\omega\text{ 中有 5 张梅花}\}.
> $$
>
> **第二步（计算对应概率）**：易得（梅花 13 张中选 5、非梅花 39 张中选 8）
>
> $$
> \mathbb{P}(X=5)=\frac{\binom{13}{5}\binom{39}{8}}{\binom{52}{13}}.
> $$
>
> 课件之问："多此一举？"——见下节：写出 $X(\omega)$ 对算出数值帮助不大，但它把"事件语言"统一成了"随机变量语言"。

---

### 2.4 随机变量的理解

- 尽管将 $X$ 的函数关系表示出来了，但对于问题 $\mathbb{P}(X=5)=?$ 的解决并没有很多的帮助。因此，人们并不十分看重函数 $X=X(\omega)$ 在 $\Omega$ 上是如何具体定义的，**只是在必要的时候才将自变元 $\omega$ 写出来**。
- 此后，相对于原始概率空间 $(\Omega,\mathcal{F},\mathbb{P})$，我们将更多关注经过 $X$ 映射后的概率空间 $(\mathbb{R},\mathcal{B},\mathbb{P})$——课件戏称"**沙子转移大法**"：把 $\Omega$ 上的概率（沙子）通过 $X$ 搬运到实数轴上。
- 思考：$\mathcal{B}$ 该如何定义？（见 2.7 节 Borel 域。）

---

### 2.5 Aside：随机变量的独立性的定义（预告）

**直观**：设 $X_1,\ldots,X_n$ 是 $(\Omega,\mathcal{F})$ 上的随机变量，如何定义随机变量间的独立性？

> [!IMPORTANT] 定义（随机变量的相互独立性）【常用】
> 设 $X_1,\ldots,X_n$ 是 $(\Omega,\mathcal{F})$ 上的随机变量，如果对任意的实数 $x_1,\ldots,x_n$ 都有
>
> $$
> \mathbb{P}(X_1\le x_1,\ldots,X_n\le x_n)=\mathbb{P}(X_1\le x_1)\cdots\mathbb{P}(X_n\le x_n),
> $$
>
> 称随机变量 $X_1,\ldots,X_n$ **相互独立**。

- 思考 1：是否 $\Omega$ 上的任意函数都可以做随机变量？
- 思考 2：解决问题？例如，学生、身高、$[165,170]$ 的概率——要让 $\mathbb{P}(X\in[165,170])$ 这类问题有意义，必须保证 $\{X\in[165,170]\}$ 是 $\mathcal{F}$ 中的事件。这两问引出下面的严格定义。

---

### 2.6 Aside：集合与函数运算

> [!IMPORTANT] 定理（原像与集合运算可交换）
> 设 $A,B$ 是 $\mathbb{R}$ 上的子集，$f(\omega)$ 是 $\Omega$ 上的函数，若用 $f^{-1}(C)$ 表示 $f$ 的对应值域 $C$ 的定义域范围，则
>
> $$
> f^{-1}(A\cup B)=f^{-1}(A)\cup f^{-1}(B),
> $$
>
> $$
> f^{-1}(A\cap B)=f^{-1}(A)\cap f^{-1}(B),
> $$
>
> $$
> f^{-1}(A^c)=\big[f^{-1}(A)\big]^c.
> $$

**直觉**：取原像这个操作与并、交、补完全交换——这是后面"$\{X\in A\}$ 都是事件"的集合论引擎。（注：补充一句证明思路——逐点验证，例如 $\omega\in f^{-1}(A\cup B)\iff f(\omega)\in A\cup B\iff f(\omega)\in A$ 或 $f(\omega)\in B\iff\omega\in f^{-1}(A)\cup f^{-1}(B)$。）

---

### 2.7 随机变量的严格定义（不做考核要求）

> [!IMPORTANT] 定义（随机变量 random variable, r.v., rv）
> 设 $(\Omega,\mathcal{F})$ 为可测空间，如果 $\Omega$ 上的函数 $X(\omega)$ 满足：对 $\forall x\in\mathbb{R}$，
>
> $$
> \{\omega\mid X(\omega)\le x\}\in\mathcal{F},
> $$
>
> 则称 $X(\omega)$ 为 $(\Omega,\mathcal{F})$ 上的随机变量，简称**随机变量**。通常将随机变量 $X(\omega)$ 简记为 $X$。

**直觉**：不是任意函数都行——必须保证每个"$X$ 不超过 $x$"的集合都是合法事件，概率才有得算（回应思考 1、2）。

**记号约定**：习惯上使用大写的 $X,Y,Z,\ldots$ 或小写的 $\varepsilon,\xi,\eta$ 等表示随机变量，不够用的时候可以使用下标，如 $X_1,X_2,\ldots$；以后用 $\{X\le x\}$ 来表示事件 $\{\omega\mid X(\omega)\le x\}$。

**显然（由 $\mathcal{F}$ 是 $\sigma$-域）：**

1. $\{X>x\}=\{X\le x\}^c\in\mathcal{F}$；
2. $\{X<x\}=\bigcup_{n=1}^{\infty}\{X\le x-\frac{1}{n}\}\in\mathcal{F}$；
3. $\{X\ge x\}=\{X<x\}^c\in\mathcal{F}$。

---

### 2.8 随机变量严格定义下的性质（不做考核要求）

- 用 $\mathcal{R}$ 表示全体实数，用 $\mathcal{C}$ 表示 $\mathcal{R}$ 中左开右闭的子区间的全体，即 $\mathcal{C}=\{(a,b]\}$。令 $\mathcal{B}=\sigma(\mathcal{C})$，通常称 $\mathcal{B}$ 为 **Borel 域**，称 $\mathcal{B}$ 的元素为 **Borel 集**。
- 当 $(\Omega,\mathcal{F},\mathbb{P})$ 是概率空间，下面的定理表明，**对任何 Borel 集 $A$，$\{X\in A\}$ 都是事件，于是可以计算概率 $\mathbb{P}(X\in A)$**。

> [!IMPORTANT] 定理 1.1
> 设 $X$ 是可测空间 $(\Omega,\mathcal{F})$ 上的随机变量，则对任意的 Borel 集 $A$，有
>
> $$
> \{X\in A\}\triangleq\{\omega\mid X(\omega)\in A\}\in\mathcal{F}.
> $$

**证明**（课件注明"不要求掌握"，略）：课件思路是对 $A\subset\mathcal{R}$ 令 $X^{-1}(A)=\{\omega\mid X(\omega)\in A\}$，$\mathcal{A}=\{A\mid X^{-1}(A)\in\mathcal{F},A\subset\mathcal{R}\}$，再分 (a)(b)(c) 三步验证 $\mathcal{A}$ 是 $\sigma$-域且 $\mathcal{B}\subset\mathcal{A}$（利用 2.6 节原像与并、交、补可交换，及 $(a,b]=\{X\le b\}-\{X\le a\}$ 型分解）。（不要求，略）

- 此后，相对于原始概率空间 $(\Omega,\mathcal{F},\mathbb{P})$，我们将更多关注经过 $X$ 映射后的概率空间 $(\mathbb{R},\mathcal{B},\mathbb{P})$。

> [!NOTE] 备注
> 在随机变量的定义中，"$\{X\le x\}\in\mathcal{F}$"可用其他形式代替，如：
> 1. $\{X>x\}\in\mathcal{F}$；
> 2. $\{X<x\}\in\mathcal{F}$；
> 3. $\{X\ge x\}\in\mathcal{F}$。
> 任取其一作定义都与原定义等价（由 2.7 节的三条"显然"互推）。

---

### 2.9 随机变量的函数

**Borel 可测函数（简称可测函数）的定义**：若 $g:\mathbb{R}\to\mathbb{R}$ 把 Borel 集的原像仍映为 Borel 集（即 $g$ 作为 $(\mathbb{R},\mathcal{B})$ 上的"随机变量"），称 $g$ 是可测函数。

> [!IMPORTANT] 定理 1.2【常用】
> 如果 $X$ 是可测空间 $(\Omega,\mathcal{F})$ 上的随机变量，$g(x)$ 是可测函数，则 $Y=g(X)$ 是 $(\Omega,\mathcal{F})$ 上的随机变量。

**证明**（课件完整给出）：只要验证对任意的 $a\in\mathbb{R}$，有 $\{Y\le a\}\in\mathcal{F}$。对任意给定的 $a$，定义

$$
B=\{x\mid g(x)\le a\},
$$

则 $B\in\mathcal{B}$（因为 $g$ 可测）。注意到 $Y(\omega)=g\big(X(\omega)\big)$ 是 $\Omega$ 上的函数，再利用定理 1.1 得到

$$
\{Y\le a\}=\{\omega\mid Y(\omega)\le a\}=\big\{\omega\mid g\big(X(\omega)\big)\le a\big\}=\{\omega\mid X(\omega)\in B\}=\{X\in B\}\in\mathcal{F}.
$$

> [!NOTE] 备注
> **连续函数、阶梯函数、单调函数以及这些函数的线性组合都是可测函数**——实践中遇到的函数基本都可测。

**多元推广（课件）**：完全类似的可以证明，如果 $X_1,X_2,\ldots,X_n$ 都是可测空间 $(\Omega,\mathcal{F})$ 上的随机变量，$g(x_1,x_2,\ldots,x_n)$ 是 $n$ 元可测函数（$n$ 维 Borel 域意义下），则 $Y=g(X_1,X_2,\ldots,X_n)$ 是 $(\Omega,\mathcal{F})$ 上的随机变量。**无特殊说明，本课以后用到的一元和多元实函数都是指可测函数。**

**构造随机变量的方式（课件四条）：**

1. 四则运算：$aX+bY$，$XY$，$\dfrac{X}{Y}$，对任意 $a,b\in\mathbb{R}$；
2. 极限：$\sup_n X_n$，$\inf_n X_n$，$\limsup_n X_n$，$\liminf_n X_n$，$\lim_n X_n$（如果存在）；
3. 变换：$\max\{X,Y\}$，$\min\{X,Y\}$，$\sin(X)$，$e^X$，$X^+$，$X^-$，$|X|^p$ 等；
4. 函数复合。

---

## 三、随机变量的独立性

### 3.1 定义

> [!IMPORTANT] 定义（随机变量的相互独立性）【常用】
> 设 $X_1,\ldots,X_n$ 是 $(\Omega,\mathcal{F})$ 上的随机变量，如果对任意的实数 $x_1,\ldots,x_n$ 都有
>
> $$
> \mathbb{P}(X_1\le x_1,\ldots,X_n\le x_n)=\mathbb{P}(X_1\le x_1)\cdots\mathbb{P}(X_n\le x_n),
> $$
>
> 称随机变量 $X_1,\ldots,X_n$ **相互独立**。

**直觉**：$n$ 个随机变量的"联合行为"完全由各自的"个体行为"相乘而得——任何一个的取值信息都不影响其余。

> [!NOTE] 思考（课件）
> 为什么事件的独立性时（只验证全体连乘）不行，随机变量的独立性时（只验证全体 $n$ 个的联合分解）可以？
> 答案藏在下一小节：因为 $x_i$ 可以**任意取**，让某些 $x_i\to+\infty$ 就能把对应的变量"挤出"等式，自动得到所有子集版本的分解式；而事件独立性中每个事件是固定的，没有这个自由度。

---

### 3.2 关于"随机变量相互独立"定义的补充说明

**命题（课件）**：若有

$$
\mathbb{P}(X_1\le x_1,X_2\le x_2,X_3\le x_3)=\mathbb{P}(X_1\le x_1)\mathbb{P}(X_2\le x_2)\mathbb{P}(X_3\le x_3),\quad\forall x_1,x_2,x_3,
$$

则

$$
\mathbb{P}(X_1\le x_1,X_2\le x_2)=\mathbb{P}(X_1\le x_1)\mathbb{P}(X_2\le x_2),\quad\forall x_1,x_2.
$$

**证明**（课件逐行，含补注）：

$$
\begin{align}
\mathbb{P}(X_1\le x_1,X_2\le x_2)&=\mathbb{P}(X_1\le x_1,X_2\le x_2,X_3\in\mathbb{R})\\
&=\mathbb{P}\big(X_1\le x_1,X_2\le x_2,\textstyle\bigcup_{n=1}^{\infty}\{X_3\le n\}\big)\\
&=\mathbb{P}\big(\textstyle\bigcup_{n=1}^{\infty}\{X_1\le x_1,X_2\le x_2,X_3\le n\}\big)\\
&=\lim_{n\to\infty}\mathbb{P}(X_1\le x_1,X_2\le x_2,X_3\le n)\\
&=\lim_{n\to\infty}\mathbb{P}(X_1\le x_1)\mathbb{P}(X_2\le x_2)\mathbb{P}(X_3\le n)\\
&=\mathbb{P}(X_1\le x_1)\mathbb{P}(X_2\le x_2)\Big(\lim_{n\to\infty}\mathbb{P}(X_3\le n)\Big)\\
&=\mathbb{P}(X_1\le x_1)\mathbb{P}(X_2\le x_2)\mathbb{P}\big(\textstyle\bigcup_{n=1}^{\infty}\{X_3\le n\}\big)\\
&=\mathbb{P}(X_1\le x_1)\mathbb{P}(X_2\le x_2)\mathbb{P}(X_3\in\mathbb{R})\\
&=\mathbb{P}(X_1\le x_1)\mathbb{P}(X_2\le x_2).
\end{align}
$$

（注：此步补全了第 4 行与第 7 行用到的依据——事件列 $\{X_1\le x_1,X_2\le x_2,X_3\le n\}$ 关于 $n$ 单调上升，故由**概率的下连续性**可把概率与极限交换；末尾 $\mathbb{P}(X_3\in\mathbb{R})=1$。）

**结论**：$n$ 个变量的联合分解式自动蕴含任何子集的分解式，所以随机变量独立性的定义只需写"全体"一条。

---

### 3.3 定理 2.1：独立随机变量生成的事件独立

> [!IMPORTANT] 定理 2.1【常用】
> 设 $X_1,\ldots,X_n$ 相互独立，则对任何 Borel 集 $A_1,\ldots,A_n$，事件
>
> $$
> \{X_1\in A_1\},\ \{X_2\in A_2\},\ \ldots,\ \{X_n\in A_n\}
> $$
>
> 相互独立。

**直觉**：独立性从"半直线事件 $\{X_i\le x_i\}$"自动升级到"任意 Borel 集事件 $\{X_i\in A_i\}$"——独立随机变量身上挖出的任何事件都互相独立。（证明超出本课范围，课件未给出。）

---

### 3.4 随机变量序列或函数的独立性

#### 独立序列与独立同分布序列

> [!IMPORTANT] 定义（独立序列）
> 如果对任意的 $n$，$X_1,\ldots,X_n$ 相互独立，则称随机变量序列 $\{X_i\}$ 相互独立，此时称 $\{X_i\}$ 为**独立序列**。

> [!IMPORTANT] 定义（独立同分布序列）【常用】
> 如果随机变量 $X_1,X_2,\ldots$ 是相互独立并且有相同的**分布函数**，则称 $X_1,X_2,\cdots$ **独立同分布**（independent and identically distributed, **i.i.d.**）。

**直觉**：i.i.d. 序列就是"同一个试验独立重复无穷次"的数学模型，是后面大数定律、中心极限定理的基本设定。

#### 定理 2.2：独立随机变量的函数仍独立

> [!IMPORTANT] 定理 2.2【常用】
> 设随机变量 $X_1,\ldots,X_n$ 相互独立，$g_1(x),\ldots,g_n(x)$ 是一元实可测函数，$\varphi(x_1,x_2,\ldots,x_k)$ 是 $k$ 元实可测函数，则
> 1. 随机变量 $g_1(X_1),\ldots,g_n(X_n)$ 相互独立；
> 2. 随机变量 $\varphi(X_1,X_2,\ldots,X_k),X_{k+1},\ldots,X_n$ 相互独立。

**直觉**：各自加工各自的（每个 $g_i$ 只吃 $X_i$），或把前 $k$ 个打包加工成一个新变量，都不会"串味"——独立性沿函数加工传递。（证明思路：用定理 2.1，$\{g_i(X_i)\le y_i\}=\{X_i\in g_i^{-1}((-\infty,y_i])\}$ 是 Borel 集事件，故仍相互独立。注：此为补充思路，课件未展开。）

**应用举例（课件）**：若 $(X_1,X_2)$ 与 $(X_3,X_4)$ 独立，则 $X_2/X_1^2$ 与 $\dfrac{X_3+X_4}{X_4}$ 独立。

---

## 四、小结（课件第 40 页）

**知识点：**

- 事件的独立性：独立 vs 条件独立；相互独立 vs 两两独立。
- 随机变量：数值化、可度量概率；引申——随机变量的函数。
- 随机变量的独立性；引申——随机变量函数的独立性。
- 上述三者共同点：
    - 若未知结论，要用**定义**验证；
    - 若已知结论，可直接使用性质做后续推理！

**技巧：**

- **反例法**认识概念的细微差异（e.g. 不同独立性定义）；
- **类比法**掌握新概念（e.g. 事件的独立性 → 随机变量的独立性）；
- **归纳法**求解非有限步或步数不确定的随机试验对应问题（e.g. 赌徒破产模型）。

---

## 本讲方法/题型清单

- 验证两个/一组事件是否独立 → 回到定义逐条验证乘积式 → 算出 $\mathbb{P}(A\cap B)$ 与 $\mathbb{P}(A)\mathbb{P}(B)$ 比对；一组事件须对**所有 $\ge 2$ 元子集**验证，缺一不可（警惕只验证两两或只验证全体连乘）。
- 判断"给定 $C$ 后 $A,B$ 是否独立" → 用条件独立定义 → 在条件测度 $\mathbb{P}(\cdot\mid C)$ 下重算 $\mathbb{P}(A\cap B\mid C)$ 与 $\mathbb{P}(A\mid C)\mathbb{P}(B\mid C)$；切勿由（无条件）独立直接下结论，两者互不蕴含。
- 求"$n$ 个独立事件至少发生一个"的概率 → 补集 + 独立拆乘积 → $\mathbb{P}(\bigcup A_i)=1-\prod(1-\mathbb{P}(A_i))$；大 $n$ 时用 $(1-p)^n\approx e^{-np}$ 估算。
- 步数不确定的赌局/游走类问题（如赌徒破产） → 首步分析 + 全概率建立递归 → 写出 $q(k)$ 的差分方程，配上边界条件（$q(0)=1$，$q(a+b)=0$），叠加差分解出通项。
- 题目语言繁琐、涉及多个时刻/多种取值的事件 → 定义随机变量翻译题目 → 三步：定义随机变量 $X(\omega)$ → 明确关心事件（如 $\{X=5\}$）→ 计算对应概率。
- 判断某函数能否当随机变量、$\{X\in A\}$ 是否可算概率 → 用严格定义 $\{X\le x\}\in\mathcal{F}$ 与定理 1.1 → 可测函数加工（定理 1.2）保持随机变量身份。
- 验证/使用随机变量的独立性 → 未知时用定义（联合 $\le$ 概率分解为乘积，只需验证全体一条）；已知独立时用定理 2.1、2.2 直接推出"任意 Borel 集事件独立""函数加工后仍独立"。
