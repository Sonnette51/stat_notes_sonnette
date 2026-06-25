---
title: "Lecture10 协方差、相关"
tags:
  - 概率论
  - 后半学期
  - 协方差
  - 相关系数
---

# Lecture10 协方差、相关


## 二、协方差（Covariance）

### 2.1 定义（定义 1.1）

$$\boxed{\text{cov}(X, Y) \triangleq E[(X-EX)(Y-EY)]}$$

（前提：$EX$、$EY$ 存在，且 $E|(X-EX)(Y-EY)| < \infty$）

**符号含义：**

- $\text{cov}(X,Y) > 0$：正相关（等高线沿主对角线方向）
- $\text{cov}(X,Y) = 0$：不相关（等高线为圆形或轴对称椭圆）
- $\text{cov}(X,Y) < 0$：负相关（等高线沿副对角线方向）

---

### 2.2 性质（性质 1.1）

以下性质本质上都来自于**期望的线性性质**。

| 编号    | 性质                                                                                            | 说明               |
| ----- | --------------------------------------------------------------------------------------------- | ---------------- |
| 1     | $\text{cov}(X, X) = \text{var}(X)$                                                            | 方差是协方差的特例        |
| 2     | $\text{cov}(X, Y) = \text{cov}(Y, X)$                                                         | 对称性              |
| **3** | $\text{cov}(X,Y) = E(XY) - (EX)(EY)$                                                          | **最常用计算公式**      |
| 4     | $\text{cov}(X, c) = 0$（$c$ 为常数）                                                               | 常数与任何随机变量协方差为零   |
| **5** | $\text{cov}(cX, Y) = c\text{cov}(X,Y)$；$\text{cov}(X+Z, Y) = \text{cov}(X,Y)+\text{cov}(Z,Y)$ | **双线性**（最常用运算规则） |
| **6** | $\text{var}(X_1+X_2) = \text{var}(X_1) + \text{var}(X_2) + 2\text{cov}(X_1,X_2)$              | 方差和公式            |

---

### 2.3 双线性的推广

由双线性反复应用，可得更一般的公式：

**（1）两个和的协方差：** $$\text{cov}(X+Y, Z+W) = \text{cov}(X,Z) + \text{cov}(X,W) + \text{cov}(Y,Z) + \text{cov}(Y,W)$$

**（2）一般线性组合的协方差：** $$\text{cov}\left(\sum_{i=1}^m a_i X_i,\sum_{j=1}^n b_j Y_j\right) = \sum_{i=1}^m \sum_{j=1}^n a_i b_j ,\text{cov}(X_i, Y_j)$$

**（3）方差的展开公式（重要）：** $$\text{var}\left(\sum_i X_i\right) = \sum_i \text{var}(X_i) + \sum_{i \neq j} \text{cov}(X_i, X_j)$$

> **记忆口诀：** 展开协方差就像展开乘法——"每一对都配对，系数相乘"。特别地，若 $X_i$ 两两不相关，则 $\text{var}(\sum_i X_i) = \sum_i \text{var}(X_i)$（方差可加）。

---

### 2.4 协方差的局限性

协方差有一个缺陷：**受量纲影响，不可比**。

**例：** 设 $X = 10Z$，$Y = 10W$（$Z, W$ 标准化，$\text{var}(Z)=\text{var}(W)=1$）。由双线性：

$$\text{cov}(X, Y) = \text{cov}(10Z, 10W) = 100 \cdot \text{cov}(Z, W)$$

若 $\text{cov}(Z,W) = 0.42$，则 $\text{cov}(X,Y) = 42$。但 $X,Y$ 与 $Z,W$ 的**关系强度完全一样**，只是单位放大了10倍，协方差却变成了100倍——因此协方差数值本身不能直接比较。这促使我们引入相关系数。

---

## 三、相关系数（Correlation Coefficient）

### 3.1 定义（定义 1.2）

**思路：** 先对 $X, Y$ 标准化（消除量纲），再计算标准化后的协方差。

标准化：$X^* = \dfrac{X-EX}{\sqrt{\text{var}(X)}}$，$Y^* = \dfrac{Y-EY}{\sqrt{\text{var}(Y)}}$

$$\text{cov}(X^*, Y^*) = E\!\left[\frac{X-EX}{\sqrt{\text{var}(X)}} \cdot \frac{Y-EY}{\sqrt{\text{var}(Y)}}\right] = \frac{\text{cov}(X,Y)}{\sqrt{\text{var}(X)}\sqrt{\text{var}(Y)}}$$

**定义：** 当 $0 < \text{var}(X) \cdot \text{var}(Y) < \infty$ 时，称

$$\boxed{\text{corr}(X, Y) \triangleq \frac{\text{cov}(X,Y)}{\sqrt{\text{var}(X)}\sqrt{\text{var}(Y)}}}$$

为 $X, Y$ 的**相关系数**（Pearson's correlation），记作 $\rho_{XY}$ 或 $\text{corr}(X,Y)$。

---

### 3.2 例 1.3：二元正态分布的相关系数

**命题：** 若 $(X,Y) \sim \mathcal{N}(\mu_1,\mu_2,\sigma_1^2,\sigma_2^2,\rho)$，则 $\text{corr}(X,Y) = \rho$。

**这解释了二元正态分布中参数 $\rho$ 的概率意义：它就是 $X$ 与 $Y$ 的相关系数，也是为什么常用 $\rho_{XY}$ 记号的原因。**

**证明（不失一般性考虑标准情形 $\mathcal{N}(0,0,1,1,\rho)$）：**

$$\text{cov}(X,Y) = E(XY) - EX \cdot EY = \iint_{\mathbb{R}^2} xy, f(x,y),dx,dy - 0 \cdot 0$$

其中 $f(x,y) = \frac{1}{2\pi\sqrt{1-\rho^2}}\exp\!\left\{-\frac{x^2-2\rho xy+y^2}{2(1-\rho^2)}\right\}$。

计算此二重积分得 $\text{cov}(X,Y) = \rho$（计算过程利用正态分布的矩计算技巧），从而：

$$\text{corr}(X,Y) = \frac{\rho}{\sqrt{1}\cdot\sqrt{1}} = \rho$$

> **计算 $E(XY)$ 的技巧（补充步骤）：** 利用条件期望，$E(XY) = E[X \cdot E(Y\mid X)]$。由二元正态的条件分布，$E(Y\mid X=x) = \mu_2 + \rho\frac{\sigma_2}{\sigma_1}(x-\mu_1)$。在标准情形下 $E(Y\mid X=x) = \rho x$，故 $E(XY) = E[X \cdot \rho X] = \rho E(X^2) = \rho \cdot 1 = \rho$。

---

## 四、例 1.1：多项分布的协方差（重要例题）

### 4.1 多项分布回顾（例 3.2）

进行 $n$ 次独立有放回试验，每次结果属于 $r$ 个类别之一，类别 $i$ 的概率为 $p_i$（$\sum p_i = 1$）。设 $X_i$ = 类别 $i$ 出现的次数，则 $(X_1, \ldots, X_r) \sim \text{Multinomial}(n, \vec{p})$，联合分布为：

$$\mathbb{P}(X_1=k_1,\ldots,X_r=k_r) = \frac{n!}{k_1!\cdots k_r!} p_1^{k_1}\cdots p_r^{k_r}, \quad \sum k_i = n$$

### 4.2 求 $\text{cov}(X_i, X_j)$

**情形一：$i = j$，即求 $\text{var}(X_i)$**

注意到 $X_i \sim B(n, p_i)$（二项分布），故：

$$\text{cov}(X_i, X_i) = \text{var}(X_i) = np_i(1-p_i)$$

**情形二：$i \neq j$，以求 $\text{cov}(X_1, X_2)$ 为例**

**方法：利用性质3（$\text{cov}(X,Y) = E(XY) - EX\cdot EY$）和辅助变量法。**

引入每次试验的指示变量：设第 $k$ 次试验中，$A_k$ = "第 $k$ 次点到类别1"，$B_k$ = "第 $k$ 次点到类别2"，则：

$$X_1 = \sum_{k=1}^n \mathbf{1}_{A_k}, \quad X_2 = \sum_{k=1}^n \mathbf{1}_{B_k}$$

利用双线性展开：

$$\text{cov}(X_1, X_2) = \text{cov}\left(\sum_k \mathbf{1}_{A_k}, \sum_l \mathbf{1}_{B_l}\right) = \sum_k \sum_l \text{cov}(\mathbf{1}_{A_k}, \mathbf{1}_{B_l})$$

- **当 $k \neq l$ 时：** 第 $k$ 次与第 $l$ 次试验独立，故 $\text{cov}(\mathbf{1}_{A_k}, \mathbf{1}_{B_l}) = 0$。
- **当 $k = l$ 时：** 同一次试验中，$A_k$ 与 $B_k$ 互斥（一次试验只能属于一个类别），故： $$E(\mathbf{1}_{A_k}\mathbf{1}_{B_k}) = \mathbb{P}(A_k \cap B_k) = 0$$ $$\text{cov}(\mathbf{1}_{A_k}, \mathbf{1}_{B_k}) = E(\mathbf{1}_{A_k}\mathbf{1}_{B_k}) - E(\mathbf{1}_{A_k})E(\mathbf{1}_{B_k}) = 0 - p_1 p_2 = -p_1 p_2$$
因此（共 $n$ 个 $k=l$ 的项）：

$$\boxed{\text{cov}(X_1, X_2) = n \cdot (-p_1 p_2) = -np_1 p_2}$$

**结论：** $$\text{cov}(X_i, X_j) = \begin{cases} np_i(1-p_i), & i = j \\ -np_ip_j, & i \neq j \end{cases}$$

> **直观理解：** $\text{cov}(X_i, X_j) < 0$（$i\neq j$）是合理的——总次数固定为 $n$，某类别出现多了，其他类别自然出现少，所以两者负相关。

---
## 七、题型总结与应对策略

### 题型一：直接计算 $\text{cov}(X,Y)$

**应对方法：** 优先使用性质3（计算公式）： $$\text{cov}(X,Y) = E(XY) - (EX)(EY)$$

步骤：① 算 $EX$，$EY$；② 算 $E(XY)$（按联合分布求和/积分，或用条件期望：$E(XY) = E[X \cdot E(Y|X)]$）；③ 相减。

---

### 题型二：利用双线性化简复杂协方差

**适用场景：** $X$ 或 $Y$ 可以写成多个随机变量之和（如多项分布、二项分布等）。

**应对方法：**

1. 将 $X = \sum_i X_i$，$Y = \sum_j Y_j$ 写成指示变量之和
2. 应用 $\text{cov}(\sum_i X_i, \sum_j Y_j) = \sum_i\sum_j \text{cov}(X_i, Y_j)$
3. 利用**独立性**（协方差为0）消去大量交叉项

---

### 题型三：计算 $\text{var}(\sum_i X_i)$

**应对方法：** $$\text{var}!\left(\sum_i X_i\right) = \sum_i \text{var}(X_i) + \sum_{i\neq j} \text{cov}(X_i, X_j)$$

若 $X_i$ 两两独立（或两两不相关），则后一项为零，$\text{var}(\sum_i X_i) = \sum_i \text{var}(X_i)$。

---

### 题型四：计算相关系数 $\text{corr}(X,Y)$

**应对方法：** $$\text{corr}(X,Y) = \frac{\text{cov}(X,Y)}{\sqrt{\text{var}(X)}\cdot\sqrt{\text{var}(Y)}}$$

先算 $\text{cov}(X,Y)$（题型一），再分别算 $\text{var}(X)$ 和 $\text{var}(Y)$，最后相除。

---

### 题型五：判断不相关 vs 独立

**应对方法：**

- 若题目条件含有**独立**，则直接推出不相关，无需计算。
- 若求出 $\text{cov}(X,Y) = 0$，只能说**不相关（线性无关）**，不能说独立，需额外说明。
- 对于二元正态分布，不相关 $\Leftrightarrow$ 独立（特殊性质）。

---

## 八、核心公式汇总

| 公式                                                                                     | 名称          |
| -------------------------------------------------------------------------------------- | ----------- |
| $\text{cov}(X,Y) = E[(X-EX)(Y-EY)]$                                                    | 协方差定义       |
| $\text{cov}(X,Y) = E(XY) - (EX)(EY)$                                                   | **协方差计算公式** |
| $\text{cov}(\sum_i a_i X_i, \sum_j b_j Y_j) = \sum_i\sum_j a_ib_j,\text{cov}(X_i,Y_j)$ | 双线性展开       |
| $\text{var}(\sum_i X_i) = \sum_i\text{var}(X_i) + \sum_{i\neq j}\text{cov}(X_i,X_j)$   | 方差展开        |
| $\text{corr}(X,Y) = \dfrac{\text{cov}(X,Y)}{\sqrt{\text{var}(X)}\sqrt{\text{var}(Y)}}$ | **相关系数定义**  |


---


> [!ABSTRACT] 深入理解相关系数

---

## 一、相关系数的等价形式

**问题：** 已知

$$ \operatorname{corr}(X, Y) = \operatorname{cov}\left(\frac{X - \mu_X}{\sqrt{\operatorname{var}(X)}},\ \frac{Y - \mu_Y}{\sqrt{\operatorname{var}(Y)}}\right) $$

是否有

$$ \operatorname{cov}\left(\frac{X}{\sqrt{\operatorname{var}(X)}},\ \frac{Y}{\sqrt{\operatorname{var}(Y)}}\right) = \operatorname{corr}(X, Y)\  $$

> [!tip] 答案 **是**。协方差对常数平移不变：$\operatorname{cov}(X + c,\ Y) = \operatorname{cov}(X, Y)$，故减去均值不影响协方差，两式相等。

---

## 二、不相关与独立

### 2.1 独立 ⟹ 不相关

> [!theorem] 定理 1.1 设 $X, Y$ 相互独立，则 $X, Y$ 不相关，即 $\operatorname{cov}(X, Y) = 0$。

**证明：**

$$ \operatorname{cov}(X, Y) = E\left[(X - EX)(Y - EY)\right] \overset{\text{独立}}{=} E(X - EX) \cdot E(Y - EY) = 0 $$

$$ \boxed{\text{若独立，则不相关}} $$

### 2.2 不相关 ⟹ 独立？（一般情况：否）

反方向**不成立**（见第五节反例）。

### 2.3 特例：二元正态分布

> [!theorem] 二元正态的等价性 设 $(X, Y) \sim \mathcal{N}(\mu_1, \mu_2, \sigma_1^2, \sigma_2^2, \rho)$，则 $$\rho_{XY} = \rho, \quad \text{且}\ X, Y \text{ 独立} \iff X, Y \text{ 不相关}$$

**证明思路（以标准联合正态为例）：**

联合密度：

$$ f(x, y) = \frac{1}{2\pi\sqrt{1-\rho^2}} \exp\left(-\frac{x^2 - 2\rho xy + y^2}{2(1-\rho^2)}\right) $$`

计算协方差：

$$ \operatorname{cov}(X, Y) = E(XY) = \iint_{\mathbb{R}^2} xy, f(x,y), dx, dy = \rho $$

- **(⟹)** $X, Y$ 独立 $\Rightarrow \rho = E(XY) = EX \cdot EY = 0$
- **(⟸)** 当 $\rho = 0$ 时，联合密度分解为：

$$f(x, y) = \frac{1}{2\pi}\exp\!\left\{-\frac{x^2 + y^2}{2}\right\} = \underbrace{\frac{1}{\sqrt{2\pi}}e^{-x^2/2}}_{f_X(x)} \cdot \underbrace{\frac{1}{\sqrt{2\pi}}e^{-y^2/2}}_{f_Y(y)}$$
联合密度 = 边缘密度之积 ⟹ $X, Y$ 独立。$\blacksquare$

---

## 三、对期望的三重解读

下表从**代数、几何、优化**三个视角统一理解 $EY$、$E(Y|X)$、$\operatorname{corr}(X, Y)$：

|        |                             $EY$                              |                                      $E(Y \mid X)$                                       |
| :----: | :-----------------------------------------------------------: | :--------------------------------------------------------------------------------------: |
| **代数** |         $\displaystyle E(Y) = \int_\mathbb{R} ydF(y)$         |                          $E(Y\mid X)=m(X)$，$m(x)=E(Y\mid X=x)$                           |
| **几何** |                              重心                               |                                            投影                                            |
| **优化** | 常数中的最佳预测：$EY = \underset{c\in\mathbb{R}}{\arg\min}\ E(Y-c)^2$ | $g(X)$ 中的最佳预测：$E(Y\mid X) = \underset{g:\mathbb{R}\to\mathbb{R}}{\arg\min}\ E[Y-g(X)]^2$ |

|                                                       $\operatorname{corr}(X, Y)$                                                       |
| :-------------------------------------------------------------------------------------------------------------------------------------: |
|                           $\dfrac{E[(X-EX)(Y-EY)]}{\sqrt{\operatorname{var}(X)}\sqrt{\operatorname{var}(Y)}}$                           |
|                                                                  夹角余弦                                                                   |
| 拟合直线中的最佳预测：$\rho\sqrt{\dfrac{\operatorname{var}(Y)}{\operatorname{var}(X)}} = \underset{b\in\mathbb{R}}{\arg\min}\ E[(Y-EY)-b(X-EX)]^2$ |
> [!note] 关键观察 令 $\tilde{X} = X - EX,\ \tilde{Y} = Y - EY$，则 $E\tilde{X} = E\tilde{Y} = 0$，且： $$\operatorname{corr}(X,Y) = \operatorname{corr}(\tilde{X}, \tilde{Y})$$ 即相关系数在均值平移下不变。

---

## 四、相关系数的几何解释

### 类比：随机变量 ↔ 向量

|                                 随机变量空间                                 |                               欧氏向量空间                               |
| :--------------------------------------------------------------------: | :----------------------------------------------------------------: |
|                              $\tilde{X}$                               |                             $\vec{a}$                              |
|                              $\tilde{Y}$                               |                             $\vec{b}$                              |
| $\langle \tilde{X}, \tilde{Y}\rangle \triangleq E(\tilde{X}\tilde{Y})$ | $\langle \vec{a}, \vec{b}\rangle \triangleq \vec{a} \cdot \vec{b}$ |

### 核心公式

$$ \operatorname{corr}(X, Y) = \operatorname{corr}(\tilde{X}, \tilde{Y}) = \frac{\operatorname{cov}(\tilde{X},\tilde{Y})}{\sqrt{\operatorname{var}(\tilde{X})}\sqrt{\operatorname{var}(\tilde{Y})}} = \frac{E(\tilde{X}\tilde{Y})}{\sqrt{E(\tilde{X}^2)}\sqrt{E(\tilde{Y}^2)}} = \frac{\langle \tilde{X}, \tilde{Y}\rangle}{|\tilde{X}| \cdot |\tilde{Y}|} = \cos\varphi $$

其中 $\varphi$ 是两个"向量"之间的夹角。

> [!important] 重要推论（Cauchy-Schwarz 不等式） $$|\operatorname{corr}(X, Y)| \leq 1$$ 等号成立当且仅当 $X, Y$ **线性相关**（即 $\exists$ 常数 $a, b, c$ 使得 $aX + bY = c\ \text{a.s.}$）

---

## 五、不相关 ≠ 独立：反例与归纳

### 5.1 反例：单位圆上的均匀分布（例 1.4）

> [!example] 例 1.4 设 $(X, Y)$ 在单位圆 $D = {(x,y) \mid x^2 + y^2 \leq 1}$ 内均匀分布，则 $X, Y$ **不相关，但也不独立**。

**证明：**

联合密度 $f(x,y) = \dfrac{1}{\pi} \mathbf{1}_D$。

$$ E(X) = \frac{1}{\pi}\int_{-1}^{1}\left(\int_{-\sqrt{1-y^2}}^{\sqrt{1-y^2}} xdx\right) dy = 0 \quad (\text{对称性}) $$

同理 $E(Y) = 0$。因此：

$$ \operatorname{cov}(X, Y) = \frac{1}{\pi}\int_{-1}^{1} y \int_{-\sqrt{1-y^2}}^{\sqrt{1-y^2}} xdx dy = 0 $$

（内层积分关于 $x$ 为奇函数，结果为零）⟹ **不相关**。

但 $X^2 + Y^2 \leq 1$ 的约束使得两者不独立（知道 $X$ 的值限制了 $Y$ 的范围）⟹ **不独立**。$\blacksquare$

### 5.2 归纳

```
不独立 ──→ 关联 ─┬─ 线性关联  → Pearson 相关系数
               └─ 非线性关联 → Spearman 相关系数 / 互信息(MI) / …
```

> [!caution] 核心结论 $$\text{独立} \Longrightarrow \text{不相关} \qquad \text{不相关} \not\Longrightarrow \text{独立}$$

### 5.3 定理 1.2（相关系数的界）

> [!theorem] 定理 1.2 设 $\operatorname{corr}(X, Y)$ 为 $X, Y$ 的相关系数，则：
> 
> 1. $|\operatorname{corr}(X,Y)| \leq 1$
> 2. $|\operatorname{corr}(X,Y)| = 1 \iff \exists$ 不全为零的常数 $a, b, c$ 使得 $aX + bY = c\ \text{a.s.}$（此时称 $X, Y$ **线性相关**）

**证明工具：内积不等式（Cauchy-Schwarz）**

$$ |E(XY)| \leq \sqrt{EX^2 \cdot EY^2} $$

等号成立的充要条件：$\exists$ 不全为零的常数 $a, b$ 使得 $aX + bY = 0\ \text{a.s.}$

---

## 六、协方差与条件期望

> [!example] 例 1.5 设 $(X, Y)$ 服从二元正态分布，当 $E(X|Y) = \mu$（常数）时，证明 $X, Y$ 独立。

**证明：**

1. 由全期望公式：$E(X) = E[E(X|Y)] = \mu$
2. 计算 $E[(X-\mu)Y]$：

$$ E[(X-\mu)Y] = E\left[E[(X-\mu)Y \mid Y]\right] = E\left[Y \cdot E[X-\mu \mid Y]\right] = E\left[Y(\mu - \mu)\right] = 0 $$
> [!NOTE]
> **条件期望的提取已知量性质**
> 
> 在计算 $E[\,\cdot\mid Y]$ 时，$Y$ 本身视为已知常数，因此可以提到期望外面：
> 
> $$E[g(Y)\cdot h(X)\mid Y] = g(Y)\cdot E[h(X)\mid Y]$$
> 
> **例：**
> $$E[(X-\mu)Y\mid Y] = Y\cdot E[X-\mu\mid Y]$$

> [!NOTE]
> **条件期望的线性性**
>
> $$E[aX + bZ \mid Y] = a\,E[X\mid Y] + b\,E[Z\mid Y]$$
>
> 与普通期望的线性性完全类比，只是每项都多了条件 $\mid Y$。
3. 计算协方差：

$$ \operatorname{cov}(X,Y) = E[(X-\mu)(Y-EY)] = \underbrace{E[(X-\mu)Y]}_{=0} - E[(X-\mu)] \cdot EY = 0 $$

故 $X, Y$ 不相关。又因为二元正态分布下独立等价于不相关，所以 $X, Y$ **独立**。$\blacksquare$

> [!question] 思考题 对一般随机向量 $(X, Y)$，若 $E(Y \mid X)$ 为常数，是否意味着 $X, Y$ 相互独立？

---

## 七、相关与因果

### 7.1 相关 ≠ 因果

> [!warning] 经典误区 **公鸡不打鸣，太阳照常升起。** 相关系数衡量的是**线性关联强度**，不蕴含因果方向。

- 相关 ⟹ 关联，但**不蕴含**因果
- 因果 ⟹ 关联，但**不蕴含**线性相关

### 7.2 相关可以辅助探索因果

在**完全数据 + 多元正态**假设下，基于协方差矩阵可以学习有向无环图（DAG），从而发现潜在的因果路径。

**应用案例：** 小鼠 Jurkat T-细胞激活的基因调节路径，有助于认识人类急性T细胞白血病。

> 推荐阅读：_The Book of WHY_，Judea Pearl（2011年图灵奖得主） 中译本：《为什么：关于因果关系的新科学》

---

## 附：核心公式速查

| 概念       | 公式                                                                                                                     |
| :------- | :--------------------------------------------------------------------------------------------------------------------- |
| 协方差      | $\operatorname{cov}(X,Y) = E[(X-EX)(Y-EY)]$                                                                            |
| 相关系数     | $\operatorname{corr}(X,Y) = \dfrac{\operatorname{cov}(X,Y)}{\sqrt{\operatorname{var}(X)}\sqrt{\operatorname{var}(Y)}}$ |
| 独立⟹不相关   | $\operatorname{cov}(X,Y) = E(X-EX)\cdot E(Y-EY) = 0$                                                                   |
| 不相关⟹独立   | 仅在**二元正态**分布下成立                                                                                                        |
| 几何意义     | $\operatorname{corr}(X,Y) = \cos\varphi$（$\varphi$ 为去均值后的夹角）                                                           |
| 最佳线性预测斜率 | $b^* = \rho\sqrt{\dfrac{\operatorname{var}(Y)}{\operatorname{var}(X)}}$                                                |
