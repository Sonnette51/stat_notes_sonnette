---
title: "Lecture11 概率母函数、矩母函数、特征函数"
tags:
  - 概率论
  - 后半学期
  - PGF
  - MGF
  - 特征函数
---

# Lecture11 概率母函数、矩母函数、特征函数

> [!ABSTRACT] 本讲概要
> - **概率母函数**：把概率分布"打包"进一个多项式，使得求和、求矩等操作变成简单的代数运算。
> - **矩母函数**：把所有的矩 $$E[X],E[X^2], E[X^3], \ldots $$ 按顺序打包进一个函数。

## 一、概率母函数

### 1.1 定义

设 $X$ 是取**非负整值**的随机变量，定义其**概率母函数 (probability-generating function, PGF)** 为

$$g(s) = E(s^X) = \sum_{j=0}^{\infty} s^j \mathbb{P}(X = j), \quad s \in [-1, 1]$$

> **约定**：$0^0 = 1$

**几点说明：**

- $g(s)$ 在 $[-1, 1]$ 上绝对收敛（因为 $|s^j \mathbb{P}(X=j)| \le \mathbb{P}(X=j)$，而概率之和为 1）
- $g(1) = \sum_{j=0}^{\infty} \mathbb{P}(X=j) = 1$，即在 $s=1$ 处代入得到总概率为 1

---

### 1.2 性质（一维）

设 $g(s)$ 是 $X$ 的 PGF，$g^{(k)}(s)$ 是 $g(s)$ 的 $k$ 阶导数，则：

| 性质     | 公式                                                         |
| ------ | ---------------------------------------------------------- |
| 恢复概率分布 | $\mathbb{P}(X=k) = \dfrac{g^{(k)}(0)}{k!}$                 |
| 期望     | $E(X) = g^{(1)}(1)$                                        |
| 方差     | $\text{var}(X) = g^{(2)}(1) + g^{(1)}(1) - [g^{(1)}(1)]^2$ |
| 独立和    | $g_Y(s) = g_1(s) g_2(s) \cdots g_n(s)$                     |

**证明思路：**

**性质1**：对 $g(s) = \sum_{j=0}^{\infty} s^j \mathbb{P}(X=j)$ 求 $k$ 阶导后令 $s=0$，只有 $j=k$ 项存活：

$$\frac{g^{(k)}(0)}{k!} = \frac{1}{k!} \sum_{j=k}^{\infty} \left.\frac{d^k}{ds^k}(s^j)\right|_{s=0} \mathbb{P}(X=j) = \mathbb{P}(X=k)$$

**性质2**：对 $g(s)$ 求一阶导后令 $s=1$：

$$g^{(1)}(1) = \sum_{j=0}^{\infty} j \mathbb{P}(X=j) = E(X)$$

**性质3**：方差推导展开：

$$g^{(2)}(1) + g^{(1)}(1) - [g^{(1)}(1)]^2$$ $$= \sum_{j=0}^{\infty} j(j-1)\mathbb{P}(X=j) + E(X) - (EX)^2$$ $$= E[X(X-1)] + EX - (EX)^2 = E(X^2) - (EX)^2 = \text{var}(X)$$

**性质4**：利用 $s^{X_1}, \ldots, s^{X_n}$ 的独立性：

$$g_Y(s) = E(s^{X_1+\cdots+X_n}) = E(s^{X_1})\cdots E(s^{X_n}) = g_1(s)\cdots g_n(s)$$

> **重要结论**：PGF 与概率分布列**相互唯一决定**（可逆性）

---

### 1.3 常见分布的 PGF

#### 二项分布 $B(n, p)$，其中 $q = 1-p$

$$g(s) = \sum_{j=0}^{n} s^j \binom{n}{j} p^j q^{n-j} = (q+sp)^n$$

**应用**：若 $X_1, \ldots, X_m$ 独立且 $X_i \sim B(n_i, p)$，则

$$Y = X_1 + \cdots + X_m \sim B(n_1+\cdots+n_m,\ p)$$

_证明_：$g_Y(s) = \prod_{i=1}^m (q+sp)^{n_i} = (q+sp)^{\sum n_i}$，与 $B(\sum n_i, p)$ 的 PGF 一致，由可逆性得结论。

#### Poisson 分布 $\mathcal{P}(\lambda)$

$$g(s) = \sum_{k=0}^{\infty} s^k \frac{\lambda^k}{k!} e^{-\lambda} = e^{\lambda(s-1)}$$

**应用**：若 $X_i \sim \mathcal{P}(\lambda_i)$ 独立，则

$$Y = X_1 + \cdots + X_m \sim \mathcal{P}(\lambda_1 + \cdots + \lambda_m)$$

> **课堂练习 1**：设 $X_1, X_2, \ldots, X_m$ 相互独立，且 $X_i \sim \mathcal{P}(\lambda_i)$，则 $Y = X_1 + X_2 + \cdots + X_m \sim ?$
> 
> **解**：由 Poisson 分布的 PGF，$g_{X_i}(s) = e^{\lambda_i(s-1)}$。
> 
> 由独立和性质（性质4），
> 
> $$g_Y(s) = \prod_{i=1}^{m} g_{X_i}(s) = \prod_{i=1}^{m} e^{\lambda_i(s-1)} = e^{(\lambda_1+\cdots+\lambda_m)(s-1)}$$
> 
> 这正是 $\mathcal{P}(\lambda_1+\cdots+\lambda_m)$ 的 PGF，由可逆性得 $Y \sim \mathcal{P}(\lambda_1+\lambda_2+\cdots+\lambda_m)$。

#### 几何分布 $G(p)$

$$g(s) = \sum_{k=1}^{\infty} s^k p q^{k-1} = \frac{sp}{1-sq}$$

**应用**：$m$ 个独立 $G(p)$ 随机变量之和 $S_m$ 的 PGF 为

$$g_m(s) = \left(\frac{sp}{1-sq}\right)^m$$

将 $g_m(s)$ 作 Taylor 展开（利用广义二项式定理 $\frac{1}{(1-x)^m} = \sum_{j=0}^{\infty}\binom{m+j-1}{j}x^j$）：

$$g_m(s) = (sp)^m \sum_{j=0}^{\infty} \binom{m+j-1}{m-1}(sq)^j = \sum_{k=m}^{\infty} \binom{k-1}{m-1} p^m q^{k-m} s^k$$

读出系数即得 **Pascal 分布**：

$$\mathbb{P}(S_m = k) = \binom{k-1}{m-1} p^m q^{k-m}, \quad k = m, m+1, \ldots$$

---

### 1.4 随机数个独立随机变量之和（定理 1.1）

**设置**：

- ${X_j}$ 独立同分布，PGF 为 $g_X(s) = \sum_{k=0}^{\infty} p_k s^k$
- $N$ 为取正整数值的随机变量，PGF 为 $g_N(s) = \sum_{n=1}^{\infty} s^n \mathbb{P}(N=n)$
- $N$ 与 ${X_j}$ 相互独立

**结论**：$W = X_1 + \cdots + X_N$ 的 PGF 为

$$g_W(s) = g_N[g_X(s)]$$

即**先对 $X$ 求 PGF，再代入 $N$ 的 PGF**（复合）。

**证明**（全期望公式）：

$$g_W(s) = E(s^W) = E[E(s^W \mid N)]$$ $$= \sum_{n=1}^{\infty} E(s^{X_1+\cdots+X_n} \mid N=n) \mathbb{P}(N=n)$$

由于 $N$ 与 ${X_j}$ 独立，$E(s^{X_1+\cdots+X_n} \mid N=n) = E(s^{X_1+\cdots+X_n}) = [g_X(s)]^n$，故

$$g_W(s) = \sum_{n=1}^{\infty} [g_X(s)]^n \mathbb{P}(N=n) = g_N[g_X(s)]$$

**例 1.4（孵蛋问题）**：$N \sim \mathcal{P}(\lambda)$，$X_i \sim B(1,p)$（Bernoulli），$W = X_1+\cdots+X_N$

- $g_X(s) = q + ps$
- $g_N(s) = e^{\lambda(s-1)}$
- $g_W(s) = g_N[g_X(s)] = e^{\lambda(q+ps-1)} = e^{\lambda p(s-1)}$

由可逆性，$W \sim \mathcal{P}(\lambda p)$。

> **课堂练习 2**：设 $X_1, X_2, \ldots$ 是独立同分布的随机变量，且 $X_i \sim G(p)$，$N \sim G(\tilde{p})$，$N$ 与全部 $X_i$ 独立，则 $W = X_1 + X_2 + \cdots + X_N \sim ?$
> 
> **解**：记 $q = 1-p$，$\tilde{q} = 1-\tilde{p}$。由几何分布的 PGF：
> 
> $$g_X(s) = \frac{sp}{1-sq}, \quad g_N(s) = \frac{s\tilde{p}}{1-s\tilde{q}}$$
> 
> 由定理 1.1，$g_W(s) = g_N[g_X(s)]$，将 $g_X(s)$ 代入 $g_N$ 中的 $s$：
> 
> $$g_W(s) = \frac{g_X(s) \cdot \tilde{p}}{1 - g_X(s) \cdot \tilde{q}} = \frac{\dfrac{sp}{1-sq} \cdot \tilde{p}}{1 - \dfrac{sp}{1-sq} \cdot \tilde{q}}$$
> 
> 分子分母同乘 $(1-sq)$：
> 
> $$g_W(s) = \frac{sp\tilde{p}}{(1-sq) - sp\tilde{q}} = \frac{sp\tilde{p}}{1 - sq - sp\tilde{q}} = \frac{sp\tilde{p}}{1 - s(q + p\tilde{q})}$$
> 
> 化简分母中的系数：
> 
> $$q + p\tilde{q} = (1-p) + p(1-\tilde{p}) = 1 - p + p - p\tilde{p} = 1 - p\tilde{p}$$
> 
> 故
> 
> $$g_W(s) = \frac{s(p\tilde{p})}{1 - s(1 - p\tilde{p})}$$
> 
> 这正是参数为 $p\tilde{p}$ 的几何分布的 PGF，由可逆性得 $W \sim G(p\tilde{p})$。

---

### 1.5 二维随机向量的 PGF

设 $(X, Y)$ 是二维取非负整数值的随机向量，分布列为 $p_{ik} = \mathbb{P}(X=i, Y=k)$，定义

$$g(s,t) = E(s^X t^Y) = \sum_{i=0}^{\infty}\sum_{k=0}^{\infty} p_{ik} s^i t^k, \quad s, t \in [-1,1]$$

**性质 1.2**：设 $g(s,t)$ 是 $(X,Y)$ 的 PGF，则

1. $|g(s,t)| \le g(1,1) = 1$，$|s| \le 1$，$|t| \le 1$
2. $g_{aX+bY+c}(s) = s^c  g(s^a, s^b)$，其中 $a,b,c$ 为常数
3. **$X$ 与 $Y$ 独立** $\Longleftrightarrow$ $g(s,t) = g_X(s) g_Y(t)$，$\forall s, t$
4. 边缘 PGF：$g(s,1) = g_X(s)$，$g(1,t) = g_Y(t)$
5. 恢复分布：$p_{ik} = \dfrac{1}{i!k!} \left.\dfrac{\partial^{i+k} g(s,t)}{\partial s^i \partial t^k}\right|_{s=t=0}$
6. 期望（$EX, EY < \infty$）：

$$E(X) = \left.\frac{\partial g(s,t)}{\partial s}\right|_{s=t=1}, \quad E(Y) = \left.\frac{\partial g(s,t)}{\partial t}\right|_{s=t=1}$$

7. 二阶矩（$EX^2, EY^2 < \infty$）：

$$E(X^2) = \left.\frac{\partial^2 g}{\partial s^2}\right|_{s=t=1} + \left.\frac{\partial g}{\partial s}\right|_{s=t=1}$$

$$E(Y^2) = \left.\frac{\partial^2 g}{\partial t^2}\right|_{s=t=1} + \left.\frac{\partial g}{\partial t}\right|_{s=t=1}$$

$$E(XY) = \left.\frac{\partial^2 g}{\partial s \partial t}\right|_{s=t=1}$$

> **为什么二阶矩有额外一项？** 对 $g(s,t) = \sum_{i,k} p_{ik} s^i t^k$ 关于 $s$ 求二阶导后令 $s=t=1$，得 $\sum_{i,k} i(i-1) p_{ik} = E[X(X-1)] = E(X^2) - E(X)$，所以 $E(X^2) = g_{ss}(1,1) + g_s(1,1)$。

---

## 二、矩母函数

### 2.1 定义

设 $X$ 是随机变量，定义其**矩母函数 (moment-generating function, MGF)** 为

$$M_X(s) = E(e^{sX})$$

具体形式：

- 离散变量：$M_X(s) = \sum_j e^{s x_j} \mathbb{P}(X = x_j)$
- 连续变量：$M_X(s) = \int_{-\infty}^{+\infty} e^{sx} f_X(x), dx$

MGF 仅在 $E(e^{sX}) < \infty$ 时存在。

**为什么叫"矩母函数"？** 对 $e^{sX}$ 作 Taylor 展开：

$$E(e^{sX}) = E\left(\sum_{k=0}^{\infty} \frac{(sX)^k}{k!}\right) = \sum_{k=0}^{\infty} \frac{s^k}{k!} E(X^k)$$

因此 $E(X^k)$（即 $k$ 阶矩）是 $M(s)$ 在 $s=0$ 处展开的系数，对 $s$ 求 $k$ 阶导数后令 $s=0$ 即得各阶矩。

---

### 2.2 性质

设 $M(s)$ 是 $X$ 的 MGF，$M^{(k)}(s)$ 是 $M(s)$ 的 $k$ 阶导数，则：

1. **线性变换**：$Y = aX + b$ 的 MGF 为 $M_Y(s) = e^{sb} M(sa)$
    
    - _推导_：$E(e^{s(aX+b)}) = e^{sb} E(e^{saX}) = e^{sb} M(sa)$
    - 所以-Y可以给进-s
2. **提取各阶矩**：$E(X^k) = M^{(k)}(0)$，$k = 1, 2, \ldots$
    
3. **归一化**：$M(0) = 1$；当 $X$ 仅取非负整数值时，$\mathbb{P}(X=0) = \lim_{s \to -\infty} M(s)$
    
4. **可逆性**：若存在正数 $a$ 使得对所有 $s \in [-a, a]$ 有 $M(s) < \infty$，则 $M(s)$ **唯一决定** $X$ 的分布
    
5. **独立和**：若 $X_1, \ldots, X_n$ 相互独立，则
    

$$M_Y(s) = M_{X_1}(s) \cdots M_{X_n}(s)$$

---

### 2.3 各类分布的 MGF 计算

#### 例 2.1：离散型随机变量

|$X$|2|3|5|
|---|---|---|---|
|$\mathbb{P}$|$\frac{1}{2}$|$\frac{1}{6}$|$\frac{1}{3}$|

$$M(s) = \frac{1}{2}e^{2s} + \frac{1}{6}e^{3s} + \frac{1}{3}e^{5s}$$

$$E(X) = M^{(1)}(0) = \frac{1}{2}\cdot 2 + \frac{1}{6}\cdot 3 + \frac{1}{3}\cdot 5 = \frac{19}{6}$$

$$E(X^2) = M^{(2)}(0) = \frac{1}{2}\cdot 4 + \frac{1}{6}\cdot 9 + \frac{1}{3}\cdot 25 = \frac{71}{6}$$

#### 例 2.2：指数分布 $\mathcal{E}(\lambda)$，$f(x) = \lambda e^{-\lambda x} \mathbf{1}_{x \ge 0}$

当 $s < \lambda$ 时：

$$M(s) = \lambda \int_0^{\infty} e^{sx} e^{-\lambda x} dx = \lambda \left.\frac{e^{(s-\lambda)x}}{s-\lambda}\right|_0^{\infty} = \frac{\lambda}{\lambda - s}$$

当 $s \ge \lambda$ 时积分发散，MGF 不存在。

$$E(X) = M^{(1)}(0) = \left.\frac{\lambda}{(\lambda-s)^2}\right|_{s=0} = \frac{1}{\lambda}$$

$$E(X^2) = M^{(2)}(0) = \left.\frac{2\lambda}{(\lambda-s)^3}\right|_{s=0} = \frac{2}{\lambda^2}$$

#### 例 2.3：混合分布

三位交易员：两位快速（$\lambda=6$），一位慢速（$\lambda=4$），等概率选择。

$$f_X(x) = \left[\frac{2}{3} \cdot 6e^{-6x} + \frac{1}{3} \cdot 4e^{-4x}\right] \mathbf{1}_{x \ge 0}$$

当 $s < 4$ 时：

$$M_X(s) = \frac{2}{3} \cdot \frac{6}{6-s} + \frac{1}{3} \cdot \frac{4}{4-s}$$

**反演规则**：若 MGF 形如 $p_1 \dfrac{\lambda_1}{\lambda_1 - s} + p_2 \dfrac{\lambda_2}{\lambda_2 - s}$，则 $X$ 是 $\mathcal{E}(\lambda_1)$ 和 $\mathcal{E}(\lambda_2)$ 的混合变量，被选中概率分别为 $p_1, p_2$。

#### 例 2.4：正态分布

**步骤1**：若 $V \sim \mathcal{N}(0,1)$，则 $M_V(s) = e^{s^2/2}$（由定义直接计算）

**步骤2**：若 $W \sim \mathcal{N}(\mu, \sigma^2)$，则 $W = \sigma V + \mu$，由性质1：

$$M_W(s) = e^{\mu s} M_V(\sigma s) = e^{\mu s + \sigma^2 s^2 / 2}$$

**步骤3**：$X \sim \mathcal{N}(\mu_1, \sigma_1^2)$，$Y \sim \mathcal{N}(\mu_2, \sigma_2^2)$ 独立，$Z = X + Y$：

$$M_Z(s) = M_X(s) M_Y(s) = e^{(\mu_1+\mu_2)s + \frac{(\sigma_1^2+\sigma_2^2)s^2}{2}}$$

由可逆性得 $Z \sim \mathcal{N}(\mu_1+\mu_2,\ \sigma_1^2+\sigma_2^2)$。

> **结论**：独立正态分布之和仍是正态分布。

**标准正态的各阶矩**：$X \sim \mathcal{N}(0,1)$，$M_X(s) = e^{s^2/2} = \sum_{k=0}^{\infty} \frac{s^{2k}}{2^k k!}$，故


$$ E(X^n) = \begin{cases} 0 & \text{$n$ 为奇数} \\ \dfrac{n!}{2^{n/2}(n/2)!} & \text{$n$ 为偶数} \end{cases} $$

---

### 2.4 随机数个独立变量之和（MGF 版本）

设 $X_1, X_2, \ldots$ 独立同分布，公共 MGF 为 $M_X(s)$，$N$ 独立于 ${X_j}$，$W = X_1 + \cdots + X_N$，则

$$M_W(s) = \sum_{n=1}^{\infty} [M_X(s)]^n \mathbb{P}(N=n)$$

**注意**：与 PGF 情形对比：

- PGF：$g_W(s) = g_N[g_X(s)]$（直接复合）
- MGF：$M_W(s) = g_N[M_X(s)]$，即对 $N$ 的 PGF 中将变量替换为 $M_X(s)$

**例 2.5（书店问题）**：$X_i \sim \mathcal{E}(\lambda)$，$N \sim G(p)$，$W = X_1 + \cdots + X_N$

- $M_{X_i}(s) = \dfrac{\lambda}{\lambda - s}$（$s < \lambda$）
- $M_N(s) = \dfrac{pe^s}{1-(1-p)e^s}$（几何分布的 MGF）
- 将  $e^s$ 替换为 $M_X(s)$：

$$M_W(s) = \frac{p \cdot M_X(s)}{1-(1-p) M_X(s)} = \frac{p \cdot \frac{\lambda}{\lambda-s}}{1 - (1-p)\frac{\lambda}{\lambda-s}} = \frac{p\lambda}{p\lambda - s}$$

由可逆性，$W \sim \mathcal{E}(p\lambda)$。

---
### 2.5 随机向量的矩母函数

### 定义

设 $\vec{X} = (X_1, \ldots, X_n)'$ 是一个 $n$ 维随机向量，$\vec{s} = (s_1, \ldots, s_n)' \in \mathbb{R}^n$，定义其**多元矩母函数**为

$$M_{\vec{X}}(\vec{s}) = E\left(e^{\vec{s}'\vec{X}}\right) = E\left(e^{s_1 X_1 + \cdots + s_n X_n}\right)$$

仅当上述期望有限时，多元 MGF 存在。

### 性质

**性质1：提取边缘 MGF**

令除 $s_i$ 之外的所有分量为 0，即可得到 $X_i$ 的边缘 MGF：

$$M_{X_i}(s) = M_{\vec{X}}(0, \ldots, 0, s, 0, \ldots, 0)$$

**性质2：提取各阶混合矩**

$$E(X_1^{k_1} X_2^{k_2} \cdots X_n^{k_n}) = \left. \frac{\partial^{k_1 + k_2 + \cdots + k_n} M_{\vec{X}}(\vec{s})}{\partial s_1^{k_1} \partial s_2^{k_2} \cdots \partial s_n^{k_n}} \right|_{\vec{s} = \vec{0}}$$

特别地，令 $k_i = 1$，其余为 0，得 $E(X_i) = \left.\dfrac{\partial M_{\vec{X}}}{\partial s_i}\right|_{\vec{s}=\vec{0}}$。

**性质3：独立性刻画**

$X_1, \ldots, X_n$ 相互独立，当且仅当

$$M_{\vec{X}}(\vec{s}) = M_{X_1}(s_1) \cdot M_{X_2}(s_2) \cdots M_{X_n}(s_n)$$

即多元 MGF 可分解为各边缘 MGF 之积。

**性质4：线性变换**

设 $\vec{Y} = A\vec{X} + \vec{b}$，其中 $A$ 是 $m \times n$ 矩阵，$\vec{b} \in \mathbb{R}^m$，则

$$M_{\vec{Y}}(\vec{t}) = e^{\vec{t}'\vec{b}} \cdot M_{\vec{X}}(A'\vec{t})$$

**性质5：可逆性**

若多元 MGF 在 $\vec{0}$ 的某邻域内有限，则它唯一决定 $\vec{X}$ 的联合分布。

### 重要例子：多元正态分布

设 $\vec{X} \sim \mathcal{N}(\vec{\mu}, \Sigma)$，其中 $\vec{\mu} \in \mathbb{R}^n$ 为均值向量，$\Sigma$ 为 $n \times n$ 正定协方差矩阵，则其多元 MGF 为

$$M_{\vec{X}}(\vec{s}) = \exp\left(\vec{s}'\vec{\mu} + \frac{1}{2}\vec{s}'\Sigma\vec{s}\right)$$

**验证一维情形**：取 $n=1$，$\vec{s} = s$，$\vec{\mu} = \mu$，$\Sigma = \sigma^2$，退化为

$$M_X(s) = e^{\mu s + \sigma^2 s^2 / 2}$$

与一维正态 MGF 一致。

**利用性质4推导**：设 $\vec{Z} = (Z_1, \ldots, Z_n)'$ 各分量独立且均 $\sim \mathcal{N}(0,1)$，则

$$M_{\vec{Z}}(\vec{s}) = \prod_{i=1}^n e^{s_i^2/2} = e^{\frac{1}{2}\vec{s}'\vec{s}}$$

由于 $\vec{X} = \Sigma^{1/2}\vec{Z} + \vec{\mu}$（其中 $\Sigma^{1/2}$ 是 $\Sigma$ 的平方根矩阵），由性质4：

$$M_{\vec{X}}(\vec{s}) = e^{\vec{s}'\vec{\mu}} \cdot M_{\vec{Z}}(\Sigma^{1/2}\vec{s}) = e^{\vec{s}'\vec{\mu}} \cdot e^{\frac{1}{2}(\Sigma^{1/2}\vec{s})'(\Sigma^{1/2}\vec{s})} = e^{\vec{s}'\vec{\mu} + \frac{1}{2}\vec{s}'\Sigma\vec{s}}$$


### 与 PGF 的对比

|      | 一元 MGF                       | 多元 MGF                                                     |
| ---- | ---------------------------- | ---------------------------------------------------------- |
| 定义   | $E(e^{sX})$                  | $E(e^{\vec{s}'\vec{X}})$                                   |
| 提取矩  | $M^{(k)}(0) = E(X^k)$        | 对 $s_i$ 求偏导后令 $\vec{s}=\vec{0}$                            |
| 独立性  | 独立 $\Rightarrow$ MGF 相乘      | 独立 $\Leftrightarrow$ MGF 完全分解                              |
| 正态分布 | $e^{\mu s + \sigma^2 s^2/2}$ | $e^{\vec{s}'\vec{\mu} + \frac{1}{2}\vec{s}'\Sigma\vec{s}}$ |

---
### 2.6 矩母函数的局限性

**Cauchy 分布**的 MGF 不存在：

$$E(e^{sX}) = \int_{-\infty}^{+\infty} \frac{e^{sx}}{\pi(1+x^2)}, dx$$

对 $s > 0$，$\int_0^{+\infty} \frac{e^{sx}}{1+x^2}, dx = +\infty$（因为 $e^{sx}$ 增长远快于 $\frac{1}{1+x^2}$ 的衰减）。

因此 Cauchy 分布的 MGF 对任意 $s \ne 0$ 均不存在，这正是引入**特征函数**（将 $s$ 替换为虚数 $it$）的动机。

---

## 三、题型归纳与应对策略

### 题型一：求给定分布的 PGF / MGF

**思路**：直接代入定义计算期望 $E(s^X)$ 或 $E(e^{sX})$，尝试化为闭合形式（利用已知级数公式或积分）。

### 题型二：由 PGF / MGF 提取矩

- $E(X) = M'(0)$ 或 $g'(1)$
- $E(X^2) = M''(0)$ 或 $g''(1) + g'(1)$
- $\text{var}(X) = M''(0) - [M'(0)]^2$

**操作**：对函数求导后代入 $s=0$（MGF）或 $s=1$（PGF）。

### 题型三：独立变量和的分布

1. 分别求各变量的 PGF / MGF
2. 相乘得和的 PGF / MGF
3. 对照已知分布形式，利用**可逆性**识别分布

### 题型四：随机数个变量之和

1. 求单个 $X_i$ 的 PGF $g_X(s)$（或 MGF $M_X(s)$）
2. 求 $N$ 的 PGF $g_N(s)$
3. 代入复合：$g_W(s) = g_N[g_X(s)]$（MGF 版：$M_W(s) = g_N[M_X(s)]$）
4. 用可逆性识别 $W$ 的分布

### 题型五：混合分布的 MGF

若 MGF 可以分解为若干指数分布（或其他分布）MGF 的凸组合，则对应混合分布，各权重即为被选中的概率。

### 题型六：二维 PGF 的应用

- 检验独立性：验证 $g(s,t) = g_X(s) g_Y(t)$ 是否成立
- 求协方差：$\text{cov}(X,Y) = E(XY) - E(X)E(Y) = g_{st}(1,1) - g_s(1,1) \cdot g_t(1,1)$

---

## 四、PGF 与 MGF 对比

|       | 概率母函数 PGF                        | 矩母函数 MGF                         |
| ----- | -------------------------------- | -------------------------------- |
| 定义    | $g(s) = E(s^X)$                  | $M(s) = E(e^{sX})$               |
| 适用范围  | **非负整值**随机变量                     | 任意随机变量（如存在）                      |
| 参数范围  | $s \in [-1,1]$                   | $s$ 在某邻域内                        |
| 提取矩   | $g^{(k)}(1) / k!$ 相关             | $M^{(k)}(0) = E(X^k)$            |
| 独立和   | $g_Y = g_1 \cdot g_2 \cdots g_n$ | $M_Y = M_1 \cdot M_2 \cdots M_n$ |
| 随机数个和 | $g_W(s) = g_N[g_X(s)]$           | $M_W(s) = g_N[M_X(s)]$           |
| 局限    | 仅限整数值                            | 重尾分布可能不存在                        |

## 附：常见分布的 PGF 与 MGF 汇总

### 概率母函数 PGF（适用于非负整值随机变量）

|分布|参数|PGF $g(s) = E(s^X)$|
|---|---|---|
|退化分布 $X = c$|$c \in \mathbb{N}$|$s^c$|
|Bernoulli $B(1,p)$|$q=1-p$|$q + ps$|
|二项分布 $B(n,p)$|$q=1-p$|$(q+ps)^n$|
|Poisson $\mathcal{P}(\lambda)$|$\lambda > 0$|$e^{\lambda(s-1)}$|
|几何分布 $G(p)$|$q=1-p$|$\dfrac{sp}{1-sq}$|
|Pascal 分布（负二项）|$m \in \mathbb{N},\ q=1-p$|$\left(\dfrac{sp}{1-sq}\right)^m$|

---

### 矩母函数 MGF

|分布|参数|MGF $M(s) = E(e^{sX})$|存在条件|
|---|---|---|---|
|退化分布 $X = c$|$c \in \mathbb{R}$|$e^{cs}$|$\forall s$|
|Bernoulli $B(1,p)$|$q=1-p$|$q + pe^s$|$\forall s$|
|二项分布 $B(n,p)$|$q=1-p$|$(q+pe^s)^n$|$\forall s$|
|Poisson $\mathcal{P}(\lambda)$|$\lambda > 0$|$e^{\lambda(e^s - 1)}$|$\forall s$|
|几何分布 $G(p)$|$q=1-p$|$\dfrac{pe^s}{1-qe^s}$|$s < -\ln q$|
|均匀分布 $U(a,b)$|$a < b$|$\dfrac{e^{sb}-e^{sa}}{s(b-a)}$|$\forall s \ne 0$，$s=0$ 时为 $1$|
|指数分布 $\mathcal{E}(\lambda)$|$\lambda > 0$|$\dfrac{\lambda}{\lambda - s}$|$s < \lambda$|
|Gamma 分布 $\Gamma(\alpha, \lambda)$|$\alpha,\lambda > 0$|$\left(\dfrac{\lambda}{\lambda-s}\right)^\alpha$|$s < \lambda$|
|正态分布 $\mathcal{N}(\mu, \sigma^2)$||$e^{\mu s + \sigma^2 s^2 / 2}$|$\forall s$|
|标准正态 $\mathcal{N}(0,1)$||$e^{s^2/2}$|$\forall s$|
|Cauchy 分布||不存在|仅 $s=0$|

> **备注**：Gamma 分布 $\Gamma(\alpha, \lambda)$ 的密度为 $f(x) = \dfrac{\lambda^\alpha}{\Gamma(\alpha)} x^{\alpha-1} e^{-\lambda x}$，$x > 0$。指数分布是 $\alpha=1$ 的特例，$\chi^2(n)$ 是 $\alpha = n/2,\ \lambda = 1/2$ 的特例。

---


> [!ABSTRACT] 特征函数（Characteristic Function）

---

## 一、特征函数的定义与基本性质

### 定义 3.1（Characteristic Function，C.F.）

对随机变量 $X$，称

$$\phi(t) \coloneqq E\left(e^{itX}\right) = E\cos(tX) + iE\sin(tX), \quad t \in \mathbb{R}$$

为 $X$ 的**特征函数**，其中 $i = \sqrt{-1}$。

当 $X$ 为连续型随机变量，密度函数为 $f(x)$ 时，特征函数可显式写作：

$$\varphi_X(t) = E\left[e^{itX}\right] = \int_{-\infty}^{+\infty} e^{itx} f(x) \, dx$$

即 $\varphi_X(t)$ 是密度函数 $f(x)$ 的 **Fourier 变换**（参数取 $-t$）。

> [!note] 与 MGF 的比较 MGF 为 $M(s)=E(e^{sX})$，$s\in\mathbb{R}$（不一定存在）； C.F. 为 $\phi(t)=E(e^{itX})$，$t\in\mathbb{R}$，**对任意随机变量均存在**（因为 $|e^{itX}|=1$）。

---

### 性质 3.1

设 $\phi(t) = E(e^{itX})$，则：

| #   | 性质                                                                                        | 说明                                         |
| --- | ----------------------------------------------------------------------------------------- | ------------------------------------------ |
| 1   | $\|\phi(t)\| \le \phi(0) = 1$，$\phi(-t) = \overline{\phi(t)}$                             | 有界且共轭对称                                    |
| 2   | $\phi(t)$ 在 $(-\infty,\infty)$ 上**一致连续**                                                  | $\|\phi(t+h)-\phi(t)\| \le E\|e^{ihX}-1\|$ |
| 3   | 若 $E\|X\|^k < \infty$，则 $\phi^{(k)}(t) = i^k E(X^k e^{itX})$，$\phi^{(k)}(0) = i^k E(X^k)$ | 由导数提取矩                                     |
| 4   | $\phi_{aX+b}(t) = e^{itb}\phi_X(at)$                                                      | 线性变换                                       |
| 5   | 若 $X_1,\ldots,X_n$ **相互独立**，则 $\phi_{X_1+\cdots+X_n}(t) = \prod_{k=1}^n \phi_k(t)$        | 独立和的特征函数 = 乘积                              |

> [!important] 性质 5 的关键用途 独立随机变量之和的特征函数等于各自特征函数之积，这是证明正态分布的再生性等结论的核心工具。

---

## 二、常见分布的特征函数

> [!important] 从前面的替换就行：s替换成e^it（矩母）或it（概率母）
### 例 3.1：二项分布 $B(n,p)$

$$\phi(t) = E(e^{itX}) = \sum_{j=0}^{n} e^{itj}\binom{n}{j}p^j q^{n-j} = \left(q + pe^{it}\right)^n$$

### 例 3.2：Poisson 分布 $\mathcal{P}(\lambda)$

$$\phi(t) = E(e^{itX}) = \sum_{k=0}^{\infty} e^{itk}\frac{\lambda^k}{k!}e^{-\lambda} = e^{\lambda(e^{it}-1)}$$

### 例 3.3：几何分布 $G(p)$

$$\phi(t) = E(e^{itX}) = \sum_{k=1}^{+\infty} e^{itk}p q^{k-1} = \frac{pe^{it}}{1 - qe^{it}}$$

### 例 3.4：均匀分布 $U(a,b)$

$$\phi(t) = \frac{e^{itb} - e^{ita}}{it(b-a)}$$

特别地，$U(-c,c)$ 的特征函数为 $\dfrac{\sin(ct)}{ct}$。

### 例 3.5：指数分布 $\mathcal{E}(\lambda)$

$$\phi(t) = \left(1 - \frac{it}{\lambda}\right)^{-1}$$

> [!tip] 推导思路 类比 MGF：$M(s) = \left(1-\dfrac{s}{\lambda}\right)^{-1}$（$s<\lambda$），将 $s$ 替换为 $it$ 即得。

### 例 3.6：正态分布 $\mathcal{N}(\mu, \sigma^2)$

$$\phi(t) = \exp\left(i\mu t - \frac{1}{2}\sigma^2 t^2\right)$$

**推导（严格方法）：**

**Step 1** 先求 $\mathcal{N}(0,1)$ 的特征函数。

$$\phi(t) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty} \cos(tx)e^{-x^2/2}dx$$

对 $t$ 求导并分部积分：

$$\phi'(t) = -\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty} x\sin(tx),e^{-x^2/2}dx = -t\phi(t)$$

即 $\dfrac{d}{dt}\left[\phi(t)e^{t^2/2}\right] = 0$，故 $\phi(t)e^{t^2/2} = C = \phi(0) = 1$，得

$$\phi(t) = e^{-t^2/2}$$

**Step 2** 设 $Y \sim \mathcal{N}(\mu,\sigma^2)$，则 $Y = \mu + \sigma X$（$X\sim\mathcal{N}(0,1)$），由性质 4：

$$E(e^{itY}) = e^{it\mu}E(e^{it\sigma X}) = \exp\left(i\mu t - \frac{1}{2}\sigma^2 t^2\right)$$

**推论（正态分布的再生性）：** 设 $X_1,\ldots,X_m$ 相互独立，$X_j \sim \mathcal{N}(\mu_j, \sigma_j^2)$，则

$$Y = X_1 + \cdots + X_m \sim \mathcal{N}\left(\sum_{j=1}^m \mu_j,\sum_{j=1}^m \sigma_j^2\right)$$

### 例 3.7：Cauchy 分布（特征函数对所有变量都存在）

密度 $f(x) = \dfrac{1}{\pi(1+x^2)}$，特征函数：

$$\phi(t) = e^{-|t|}$$

### 例 3.8：Laplace 分布

密度 $f(x) = \dfrac{1}{2}e^{-|x|}$，特征函数：

$$\phi(t) = \frac{1}{1+t^2}$$
---

## 三、三种母函数对比（PGF / MGF / C.F.）

| |**PGF**（非负整数r.v.）|**MGF**（大部分r.v.）|**C.F.**（所有r.v.）|
|---|---|---|---|
|**定义**|$g(s)=Es^X$|$M(s)=Ee^{sX}$|$\phi(t)=Ee^{itX}$|
|**可逆性**|$\leftrightarrow$ PMF|$\leftrightarrow$ CDF|$\xleftrightarrow{1-1}$ CDF|
|**提取矩**|$g^{(k)}(1)/k!$ 等|$M^{(k)}(0)$|$\phi^{(k)}(0)/i^k$|
|**独立和**|$\prod g_k(s)$|$\prod M_k(s)$|$\prod \phi_k(t)$|
|**线性变换 $aX+b$**|$s^b\cdot g_X(s^a)$|$e^{sb}\cdot M_X(sa)$|$e^{itb}\cdot\phi_X(ta)$|
|**i.i.d. 之和 $S_N$**|$g_N(s)$ 中 $s\to g_X(s)$|$M_N(s)$ 中 $e^s\to M_X(s)$|$\phi_N(t)$ 中 $e^{it}\to\phi_X(t)$|
|**联合**|$E(s^X t^Y)$|$E(e^{sX}e^{tY})$|$E(e^{it_1 X}e^{it_2 Y})$|

### 各分布三种母函数汇总

| 分布                          | PGF                | MGF                                              | C.F.                                              |
| --------------------------- | ------------------ | ------------------------------------------------ | ------------------------------------------------- |
| $B(n,p)$                    | $(q+ps)^n$         | $(q+pe^s)^n$                                     | $(q+pe^{it})^n$                                   |
| $\mathcal{P}(\lambda)$      | $e^{\lambda(s-1)}$ | $e^{\lambda(e^s-1)}$                             | $e^{\lambda(e^{it}-1)}$                           |
| $G(p)$                      | $\dfrac{sp}{1-sq}$ | —                                                | $\dfrac{pe^{it}}{1-qe^{it}}$                      |
| $U(a,b)$                    | —                  | —                                                | $\dfrac{e^{itb}-e^{ita}}{it(b-a)}$                |
| $\mathcal{E}(\lambda)$      | —                  | $\left(1-\dfrac{s}{\lambda}\right)^{-1}$         | $\left(1-\dfrac{it}{\lambda}\right)^{-1}$         |
| $\mathcal{N}(\mu,\sigma^2)$ | —                  | $\exp\left(\mu s+\dfrac{\sigma^2 s^2}{2}\right)$ | $\exp\left(i\mu t-\dfrac{\sigma^2 t^2}{2}\right)$ |
| Cauchy                      | —                  | 不存在                                              | $e^{-\|t\|}$                                      |

> [!warning] Cauchy 分布没有 MGF Cauchy 分布的矩不存在（期望也不存在），因此 MGF 无法定义，但 C.F. 仍然存在。这正是 C.F. 比 MGF 更一般的体现。

---

## 四、特征函数与分布函数

> [!note] 本节不要求掌握细节

**核心结论：随机变量的特征函数和分布函数相互唯一决定。**

### 定理 3.1（逆转公式）

设 $\phi(t)$ 是 $X$ 的特征函数，$F(x)$ 是 $X$ 的分布函数。若 $F(x)$ 在 $a,b$ 处连续，则

$$\frac{1}{2\pi}\lim_{T\to\infty}\int_{-T}^{T} \frac{e^{-ita}-e^{-itb}}{it}\phi(t)dt = F(b)-F(a)$$

### 定理 3.2（由特征函数恢复密度）

若 $\int_{\mathbb{R}}|\phi(t)|dt < \infty$，则 $X$ 有连续密度函数

$$f(x) = \frac{1}{2\pi}\int_{-\infty}^{\infty} e^{-itx}\phi(t)dt$$

> [!tip] 直觉理解 这本质上是 Fourier 变换：$\phi(t)$ 是 $f(x)$ 的 Fourier 变换，$f(x)$ 是 $\phi(t)$ 的逆 Fourier 变换。

---

## 五、特征函数与矩

> [!note] 本节不要求掌握细节

**注意：** 矩不一定存在（如 Cauchy 分布），但特征函数始终存在。

### 定理 3.3（特征函数的展开）

若 $E|X|^n < \infty$，则

$$\phi(t) = \sum_{m=0}^{n} \frac{E[(itX)^m]}{m!} + o(t^n)$$

特别地，若 $E(X^2) < \infty$，则

$$\phi(t) = 1 + itE(X) - \frac{1}{2}t^2 E(X^2) + o(t^2)$$

> [!important] 思考题 **高阶矩存在，低阶矩一定存在。** （因为 $E|X|^k \le (E|X|^n)^{k/n}$ 由 Jensen 不等式，$k\le n$。）

---

## 六、混合分布的特征函数

### 定理 3.4（混合分布）

设分布函数 $F_1(x),\ldots,F_m(x)$ 的特征函数分别为 $\phi_1(t),\ldots,\phi_m(t)$。若 $\lambda_k \ge 0$ 且 $\sum_{k=1}^m \lambda_k = 1$，则混合分布 $\sum_{k=1}^m \lambda_k F_k$ 的特征函数为

$$\sum_{k=1}^m \lambda_k \phi_k(t)$$

> [!warning] 混合分布 $\ne$ 线性组合 $Y = \sum_{k=1}^m \lambda_k F_k$ 表示 $Y$ 以概率 $\lambda_k$ 服从 $F_k$，与 $\sum_{k=1}^m \lambda_k X_k$ 是**不同的**概念，对 $X_k$ 之间的独立性也无要求。

---

## 七、随机向量的特征函数

### 定义 3.2（随机向量的特征函数）

设 $\boldsymbol{X} = (X_1,\ldots,X_n)$ 是随机向量，$\boldsymbol{X}$ 的特征函数定义为

$$\phi(\boldsymbol{t}) = E\left(e^{i\boldsymbol{t}'\boldsymbol{X}}\right), \quad \boldsymbol{t} = (t_1,\ldots,t_n) \in \mathbb{R}^n$$

### 定理 3.5（独立性的充要条件）

$X_1,\ldots,X_n$ 相互独立 $\iff$

$$\phi(\boldsymbol{t}) = \phi_1(t_1)\phi_2(t_2)\cdots\phi_n(t_n)$$

其中 $\phi_k(t_k)$ 是 $X_k$ 的特征函数。

### 例 3.9（Cauchy 分布的一个反例）

设 $X$ 服从 Cauchy 分布，$Y = aX$（$a>0$）。则 $\phi_X(t) = e^{-|t|}$，

$$\phi_Y(t) = e^{-a|t|}, \quad \phi_{X+Y}(t) = e^{-(1+a)|t|} = \phi_X(t)\cdot\phi_Y(t)$$

> [!warning] 重要反例 尽管 $\phi_{X+Y}(t) = \phi_X(t)\phi_Y(t)$，但 **不能** 推出 $X$ 与 $Y$ 相互独立（因为 $Y=aX$ 是 $X$ 的函数，显然不独立）。
> 
> 即：联合特征函数分解 $\ne$ 独立。定理 3.5 中需要的是**联合**特征函数等于边际特征函数之积，而非仅仅 $\phi_{X+Y}=\phi_X\phi_Y$。

---

## 八、收敛性与连续性定理

### 定义 3.3（依分布收敛）

设 $X$ 的分布函数为 $F(x)$，$X_n$ 的分布函数为 $F_n(x)$。若在 $F(x)$ 的所有连续点 $x$ 处，

$$\lim_{n\to\infty} F_n(x) = F(x)$$

则称 $X_n$ **依分布收敛**到 $X$，记作 $X_n \xrightarrow{d} X$，或称 $F_n$ **弱收敛**到 $F$，记作 $F_n \xrightarrow{w} F$。

### 定理 3.6（连续性定理，Continuity Theorem）⭐

设 $X_n$ 的特征函数为 $\phi_n(t)$，$X$ 的特征函数为 $\phi(t)$，则

$$X_n \xrightarrow{d} X \iff \lim_{n\to\infty}\phi_n(t) = \phi(t), \quad \forall, t\in\mathbb{R}$$

> [!important] 地位 此定理是概率论中**最常用、最重要**的定理之一，是证明中心极限定理（CLT）的关键工具。

### 定理 3.7（多元收敛）

设 $\boldsymbol{X}_n$ 的特征函数 $\phi_n(\boldsymbol{t})$ 收敛到在 $\boldsymbol{t}=\boldsymbol{0}$ 处连续的函数 $\phi(\boldsymbol{t})$，则 $\phi(\boldsymbol{t})$ 是某个随机向量 $\boldsymbol{X}$ 的特征函数，且对任何同维度常数向量 $\boldsymbol{a}$，有

$$\boldsymbol{a}'\boldsymbol{X}_n \xrightarrow{d} \boldsymbol{a}'\boldsymbol{X}$$

> 此定理建立了**多元**收敛与**一元**收敛的关联。

---

## 九、三套工具总结

### 描述随机变量的完整工具

|随机变量类型|完整描述工具|
|---|---|
|离散型|PMF、CDF、C.F.|
|连续型|PDF、CDF、C.F.|
|一般随机变量|CDF、C.F.|

**独立性判定**（以连续型为例）：$\boldsymbol{X}_1$ 与 $\boldsymbol{X}_2$ 独立 $\iff$ 以下任一成立：

1. $F(\boldsymbol{x}_1,\boldsymbol{x}_2) = F_1(\boldsymbol{x}_1)F_2(\boldsymbol{x}_2)$
2. $f(\boldsymbol{x}_1,\boldsymbol{x}_2) = f_1(\boldsymbol{x}_1)f_2(\boldsymbol{x}_2)$
3. $\phi(\boldsymbol{t}_1,\boldsymbol{t}_2) = \phi_1(\boldsymbol{t}_1)\phi_2(\boldsymbol{t}_2)$

### 核心思想

> C.F. 是对随机变量**全部信息**的完整刻画，而 $EX$ 只是随机变量某一方面（一阶矩）的总结。学习了 C.F./MGF 之后，应更深刻地理解"期望"在随机变量全貌中的位置。
