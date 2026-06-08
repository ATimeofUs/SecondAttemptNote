## 1 概率基本公式

### 1.1 加法与条件概率

$$
P(A \cup B) = P(A) + P(B) - P(AB)
$$

$$
P(A \mid B) = \frac{P(AB)}{P(B)}
$$

$$
P(A \setminus B) = P(A) - P(AB) = P(AB')
$$

### 独立性

若 $A$、$B$ 独立，则：

$$
P(AB) = P(A)P(B) \quad \Longleftrightarrow \quad P(A \mid B) = P(A)
$$

> **注意**：互斥与独立是两个不同的概念。$A$、$B$ 互斥指 $AB = \varnothing$；独立指知道 $B$ 发生不影响 $A$ 的概率。两者一般不能同时成立（除非其中一个概率为 0）。

### 1.3 全概率公式与贝叶斯公式

设 $B_1, B_2, \ldots, B_n$ 是样本空间的一个**划分**（两两互斥且并集为全集），则：

$$
P(A) = \sum_{i=1}^{n} P(A \mid B_i)\,P(B_i)
$$

**贝叶斯公式**（已知结果 $A$ 发生，反推原因 $B_j$）：

$$
P(B_j \mid A) = \frac{P(A \mid B_j)\,P(B_j)}{\displaystyle\sum_{i=1}^{n} P(A \mid B_i)\,P(B_i)}
$$

---

## 2 一维随机变量

**分布函数**：$F(x) = P(X \leq x)$，单调不减，右连续，$F(-\infty)=0$，$F(+\infty)=1$。

### 2.1 常见离散型分布

| 分布 | 记号 | 分布律 $P(X=k)$ | 期望 | 方差 |
|------|------|-----------------|------|------|
| 0-1 分布 | $B(1,p)$ | $p^k(1-p)^{1-k},\ k=0,1$ | $p$ | $p(1-p)$ |
| 二项分布 | $B(n,p)$ | $\dbinom{n}{k}p^k(1-p)^{n-k}$ | $np$ | $np(1-p)$ |
| 泊松分布 | $P(\lambda)$ | $\dfrac{\lambda^k}{k!}e^{-\lambda}$ | $\lambda$ | $\lambda$ |
| 几何分布 | $G(p)$ | $(1-p)^{k-1}p,\ k=1,2,\ldots$ | $\dfrac{1}{p}$ | $\dfrac{1-p}{p^2}$ |
| 超几何分布 | $H(n,M,N)$ | $\dfrac{\binom{M}{k}\binom{N-M}{n-k}}{\binom{N}{n}}$ | $\dfrac{nM}{N}$ | $\dfrac{nM(N-M)(N-n)}{N^2(N-1)}$ |

> **注意**：当 $n$ 大、$p$ 小且 $\lambda = np$ 适中时，二项分布可用泊松分布近似：$B(n,p) \approx P(\lambda)$。

### 2.2 常见连续型分布

| 分布 | 记号 | 概率密度 $f(x)$ | 期望 | 方差 |
|------|------|-----------------|------|------|
| 均匀分布 | $U(a,b)$ | $\dfrac{1}{b-a},\ x\in[a,b]$ | $\dfrac{a+b}{2}$ | $\dfrac{(b-a)^2}{12}$ |
| 指数分布 | $E(\lambda)$ | $\lambda e^{-\lambda x},\ x>0$ | $\dfrac{1}{\lambda}$ | $\dfrac{1}{\lambda^2}$ |
| 正态分布 | $N(\mu,\sigma^2)$ | $\dfrac{1}{\sqrt{2\pi}\,\sigma}e^{-\frac{(x-\mu)^2}{2\sigma^2}}$ | $\mu$ | $\sigma^2$ |

> **注意**：指数分布具有**无记忆性**：$P(X > s+t \mid X > s) = P(X > t)$。正态分布标准化：若 $X \sim N(\mu, \sigma^2)$，则 $Z = \dfrac{X-\mu}{\sigma} \sim N(0,1)$。

---

## 3 多维随机变量

### 3.1 联合分布与边缘分布

$$
F(x, y) = P(X \leq x,\, Y \leq y)
$$

$$
F_X(x) = F(x, +\infty), \quad F_Y(y) = F(+\infty, y)
$$

**边缘概率密度**（连续型）：

$$
f_X(x) = \int_{-\infty}^{+\infty} f(x, y)\,dy, \quad f_Y(y) = \int_{-\infty}^{+\infty} f(x, y)\,dx
$$

### 3.2 条件分布

$$
f_{X \mid Y}(x \mid y) = \frac{f(x,y)}{f_Y(y)}, \quad f_{Y \mid X}(y \mid x) = \frac{f(x,y)}{f_X(x)}
$$

### 独立性

$$
X \perp Y \iff f(x,y) = f_X(x)\,f_Y(y) \iff F(x,y) = F_X(x)\,F_Y(y)
$$

### 3.3 二维正态分布

$(X,Y) \sim N(\mu_1, \mu_2, \sigma_1^2, \sigma_2^2, \rho)$，联合概率密度为：

$$
f(x,y) = \frac{1}{2\pi\sigma_1\sigma_2\sqrt{1-\rho^2}} \exp\left\{-\frac{1}{2(1-\rho^2)}\left[\frac{(x-\mu_1)^2}{\sigma_1^2} - \frac{2\rho(x-\mu_1)(y-\mu_2)}{\sigma_1\sigma_2} + \frac{(y-\mu_2)^2}{\sigma_2^2}\right]\right\}
$$

其中 $\rho$ 为相关系数。边缘分布：$X \sim N(\mu_1, \sigma_1^2)$，$Y \sim N(\mu_2, \sigma_2^2)$。

> **注意**：对二维正态分布，$X$ 与 $Y$ **独立** $\iff$ $\rho = 0$（即不相关）。这是正态分布特有的结论，一般分布不成立。

### 3.4 换元公式（变量变换）

设 $(X,Y)$ 的联合密度为 $f(x,y)$，令 $U = u(X,Y)$，$V = v(X,Y)$，反解得 $x = x(u,v)$，$y = y(u,v)$，则：

$$
f_{UV}(u,v) = f(x(u,v),\, y(u,v))\,|J|
$$

其中雅可比行列式为：

$$
J = \frac{\partial(x,y)}{\partial(u,v)} = \begin{vmatrix} \dfrac{\partial x}{\partial u} & \dfrac{\partial x}{\partial v} \\[6pt] \dfrac{\partial y}{\partial u} & \dfrac{\partial y}{\partial v} \end{vmatrix}
$$

> **注意**：换元后取值范围须由原变量范围推导出 $u, v$ 的范围，不可直接沿用。

---

## 4 数学期望与方差

### 4.1 一维随机变量

| | 离散型 | 连续型 |
|--|--------|--------|
| 期望 | $E[X] = \sum_k x_k p_k$ | $E[X] = \int_{-\infty}^{+\infty} x f(x)\,dx$ |
| 方差 | $D(X) = E[X^2] - (E[X])^2$ | 同左 |
| $E[g(X)]$ | $\sum_k g(x_k)p_k$ | $\int_{-\infty}^{+\infty} g(x)f(x)\,dx$ |

**常用性质**：

$$
E[aX + bY] = aE[X] + bE[Y]
$$

$$
D(aX + b) = a^2 D(X)
$$

$$
D(X \pm Y) = D(X) + D(Y) \pm 2\,\text{Cov}(X,Y)
$$

若 $X$、$Y$ 独立：$D(X \pm Y) = D(X) + D(Y)$，$E[XY] = E[X]E[Y]$。

### 4.2 协方差与相关系数

$$
\text{Cov}(X,Y) = E[XY] - E[X]E[Y]
$$

$$
\rho_{XY} = \frac{\text{Cov}(X,Y)}{\sqrt{D(X)}\sqrt{D(Y)}}，\quad |\rho_{XY}| \leq 1
$$

**运算性质**：

$$
\text{Cov}(aX, bY) = ab\,\text{Cov}(X,Y)
$$

$$
\text{Cov}(X+Y, Z) = \text{Cov}(X,Z) + \text{Cov}(Y,Z)
$$

$$
\text{Cov}(X,X) = D(X)
$$

> **注意**：$X$、$Y$ 独立 $\Rightarrow$ $\text{Cov}(X,Y)=0$（不相关），但反之不成立。二维正态分布是例外：不相关与独立等价。

---

## 5 大数定律与中心极限定理

### 5.1 大数定律

设 $X_1, X_2, \ldots, X_n$ 独立同分布，$E[X_i] = \mu$，则样本均值**依概率收敛**于总体均值：

$$
\bar{X} = \frac{1}{n}\sum_{i=1}^n X_i \xrightarrow{P} \mu \quad (n \to \infty)
$$

### 5.2 中心极限定理

设 $X_1, X_2, \ldots, X_n$ 独立同分布，$E[X_i]=\mu$，$D(X_i)=\sigma^2 > 0$，则当 $n$ 充分大时：

$$
\frac{\displaystyle\sum_{i=1}^n X_i - n\mu}{\sqrt{n}\,\sigma} = \frac{\bar{X} - \mu}{\sigma/\sqrt{n}} \xrightarrow{d} N(0,1)
$$

即 $\sum X_i$ 近似服从 $N(n\mu,\, n\sigma^2)$，$\bar{X}$ 近似服从 $N\!\left(\mu,\, \dfrac{\sigma^2}{n}\right)$。

> **注意**：中心极限定理说明，无论原始分布是什么形状，样本量足够大时样本均值都近似正态分布。一般 $n \geq 30$ 即可使用近似。

---



## 6 数理统计

### 6.1 常见统计量

设总体 $X \sim N(\mu, \sigma^2)$，$X_1, \ldots, X_n$ 为样本：

$$
\bar{X} = \frac{1}{n}\sum_{i=1}^n X_i, \quad E[\bar{X}] = \mu,\quad D(\bar{X}) = \frac{\sigma^2}{n}
$$

$$
S^2 = \frac{1}{n-1}\sum_{i=1}^n (X_i - \bar{X})^2, \quad E[S^2] = \sigma^2
$$

> **注意**：样本方差分母为 $n-1$（无偏估计），而非 $n$。



---



### 6.2 三大抽样分布

#### 6.2.1 卡方分布 $\chi^2(n)$

若 $X_1, \ldots, X_n \overset{iid}{\sim} N(0,1)$，则：

$$
\chi^2 = X_1^2 + X_2^2 + \cdots + X_n^2 \sim \chi^2(n)
$$

$$
E[\chi^2] = n, \quad D(\chi^2) = 2n
$$

重要结论：$\dfrac{(n-1)S^2}{\sigma^2} \sim \chi^2(n-1)$，且 $\bar{X}$ 与 $S^2$ 独立。

#### 6.2.2 $t$ 分布 $t(n)$

若 $X \sim N(0,1)$，$Y \sim \chi^2(n)$，且 $X$、$Y$ 独立，则：

$$
T = \frac{X}{\sqrt{Y/n}} \sim t(n)
$$

重要结论：$\dfrac{\bar{X} - \mu}{S/\sqrt{n}} \sim t(n-1)$（$\sigma^2$ 未知时用 $S$ 代替）。

> **注意**：$t$ 分布关于 0 对称，$n$ 较大时趋近于标准正态分布。

#### 6.2.3 $F$ 分布 $F(m,n)$

若 $U \sim \chi^2(m)$，$V \sim \chi^2(n)$，且独立，则：

$$
F = \frac{U/m}{V/n} \sim F(m,n)
$$

重要结论：$\dfrac{S_1^2/\sigma_1^2}{S_2^2/\sigma_2^2} \sim F(m-1, n-1)$，且 $F(m,n)$ 与 $F(n,m)$ 互为倒数分布。



![](/home/ping/Second_Attempt/301/概率论/assets/new.jpg)



---



### 6.3 参数估计

#### 6.3.1 矩估计法

用样本矩替换总体矩，建立方程求解参数：

$$
E[X] \approx \bar{X}, \quad E[X^2] \approx \frac{1}{n}\sum X_i^2
$$

有几个未知参数就列几个方程。

#### 6.3.2 最大似然估计法

构造似然函数 $L(\theta) = \prod_{i=1}^n f(x_i;\theta)$，求使 $L(\theta)$ 最大的 $\hat{\theta}$。

**步骤**：
1. **写出似然函数**：$L(\theta) = \prod_{i=1}^n f(x_i;\theta)$（连续型）或 $\prod p(x_i;\theta)$（离散型）
2. **取对数**：$\ln L(\theta)$（化乘为加，便于求导）
3. **求导令其为零**：$\dfrac{d\ln L}{d\theta} = 0$，解出 $\hat{\theta}$



---



### 6.4 估计量的评价标准

| 标准 | 含义 |
|------|------|
| **无偏性** | $E[\hat{\theta}] = \theta$，估计量平均值等于真实值 |
| **有效性** | 在所有无偏估计中方差最小 |
| **一致性** | $n \to \infty$ 时，$\hat{\theta} \xrightarrow{P} \theta$ |



#### 6.4.1 参数的区间估计

区间估计是在一定置信水平下，给出参数的一个可能取值范围。

已知 $\bar{X}=100$，$\sigma=10$，$n=36$，求 $\mu$ 的 95% 置信区间：

$$
100 \pm 1.96 \cdot \frac{10}{6}
= 100 \pm 3.27
$$
👉 区间为：$$(96.73,\ 103.27)$$


---



#### 6.4.1 假设检验

基本思想：**小概率事件原理（反证法）**

基本步骤：

1. **提出假设**
   
   - 原假设 $H_0$
   - 备择假设 $H_1$
   
2. **构造统计量**

3. **确定拒绝域（临界值）**

4. **作出决策**
   - 若统计量落入拒绝域 → 拒绝 $H_0$
   - 否则 → 不拒绝 $H_0$
   
   

---

#### 6.4.2 两类错误

| 类型 | 含义 |
|------|------|
| **第一类错误（弃真）** | $H_0$ 为真却被拒绝，概率为 $\alpha$ |
| **第二类错误（取伪）** | $H_0$ 为假却未拒绝，概率为 $\beta$ |

> **注意**：  
> - $\alpha$ 称为**显著性水平**（通常取 0.05 或 0.01）  
> - 检验设计通常控制第一类
> - 错误  



##### 例1：均值检验（单样本 t 检验）

某总体服从正态分布，$\sigma$ 未知。  
样本均值 $\bar{X} = 52$，样本标准差 $S = 5$，样本量 $n=25$。  
检验 $H_0:\mu=50$，显著性水平 $\alpha=0.05$。

**步骤：**

1. 构造统计量：

$$
T = \frac{52 - 50}{5/\sqrt{25}} = \frac{2}{1} = 2
$$

2. 查表：
$$
t_{0.025}(24) \approx 2.064
$$


3. 判断：
$$
|T| = 2 < 2.064
$$

👉 不拒绝 $H_0$

---

