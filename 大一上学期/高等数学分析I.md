# 高等数学分析 I

> 大一上学期 | 东南大学吴健雄学院 | 电子信息类

---

## 目录

1. [函数与极限](#1-函数与极限)
2. [导数与微分](#2-导数与微分)
3. [微分中值定理与导数应用](#3-微分中值定理与导数应用)
4. [不定积分](#4-不定积分)
5. [定积分](#5-定积分)

---

## 1. 函数与极限

### 1.1 函数的基本性质

| 性质 | 定义 | 记号 |
|------|------|------|
| 有界性 | $\exists M > 0, \forall x \in I, |f(x)| \leq M$ | 上界、下界 |
| 单调性 | $x_1 < x_2 \Rightarrow f(x_1) \leq f(x_2)$ | 递增/递减 |
| 奇偶性 | $f(-x) = f(x)$ 或 $f(-x) = -f(x)$ | 偶函数/奇函数 |
| 周期性 | $\exists T > 0, f(x+T) = f(x)$ | 最小正周期 |

### 1.2 常用函数类型

- **幂函数**: $y = x^a$
- **指数函数**: $y = a^x \quad (a > 0, a \neq 1)$
- **对数函数**: $y = \log_a x$
- **三角函数**: $\sin x, \cos x, \tan x, \cot x$
- **反三角函数**: $\arcsin x, \arccos x, \arctan x$

### 1.3 数列极限

#### 定义（ε-N语言）
$$\lim_{n \to \infty} a_n = A \Leftrightarrow \forall \varepsilon > 0, \exists N \in \mathbb{N}, \forall n > N: |a_n - A| < \varepsilon$$

#### 收敛数列的性质
- **唯一性**: 收敛数列极限唯一
- **有界性**: 收敛数列必为有界数列
- **保号性**: 若 $\lim a_n = A > 0$，则 $\exists N, \forall n > N: a_n > 0$
- **四则运算**: 极限的四则运算律

#### 重要极限
$$\lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^n = e \quad \text{（自然对数底）}$$

### 1.4 函数极限

#### 定义（ε-δ语言）
$$\lim_{x \to x_0} f(x) = A \Leftrightarrow \forall \varepsilon > 0, \exists \delta > 0, \forall x: 0 < |x - x_0| < \delta \Rightarrow |f(x) - A| < \varepsilon$$

#### 单侧极限
- **左极限**: $\lim_{x \to x_0^-} f(x) = A$
- **右极限**: $\lim_{x \to x_0^+} f(x) = A$
- 极限存在的充要条件：左极限 = 右极限

#### 重要极限公式
$$\boxed{\lim_{x \to 0} \frac{\sin x}{x} = 1}$$

$$\boxed{\lim_{x \to \infty} \left(1 + \frac{1}{x}\right)^x = e}$$

### 1.5 无穷小与无穷大

#### 无穷小
- **定义**: 当 $x \to x_0$ 时，若 $\lim f(x) = 0$，则称 $f(x)$ 为无穷小
- **性质**: 
  - 有限个无穷小的和、积仍为无穷小
  - 有界函数与无穷小的乘积为无穷小

#### 无穷小的比较
设 $\lim \alpha(x) = 0, \lim \beta(x) = 0$

| 关系 | 条件 | 记号 |
|------|------|------|
| 高阶 | $\lim \frac{\alpha}{\beta} = 0$ | $\alpha = o(\beta)$ |
| 低阶 | $\lim \frac{\alpha}{\beta} = \infty$ | $\beta = o(\alpha)$ |
| 同阶 | $\lim \frac{\alpha}{\beta} = c \neq 0$ | $\alpha \sim c\beta$ |
| 等价 | $\lim \frac{\alpha}{\beta} = 1$ | $\alpha \sim \beta$ |

#### 常用等价无穷小（当 $x \to 0$ 时）
$$\sin x \sim x \sim \tan x \sim \arcsin x \sim \arctan x$$
$$\ln(1+x) \sim x \quad e^x - 1 \sim x$$
$$a^x - 1 \sim x\ln a \quad (1+x)^\alpha - 1 \sim \alpha x$$
$$1 - \cos x \sim \frac{x^2}{2}$$

### 1.6 函数的连续性

#### 定义
$$\lim_{x \to x_0} f(x) = f(x_0)$$

#### 间断点分类
| 类型 | 左、右极限 | 与函数值 |
|------|-----------|---------|
| **可去间断点** | 存在且相等 | 不存在或不相等 |
| **跳跃间断点** | 存在但不相等 | — |
| **第二类间断点** | 至少一个不存在 | — |

#### 闭区间连续函数的性质
- **最大最小值定理**: 闭区间连续函数必有最大值和最小值
- **介值定理**: 若 $f(a) \cdot f(b) < 0$，则 $\exists \xi \in (a,b)$ 使 $f(\xi) = 0$
- **一致连续性**: 闭区间连续函数必定一致连续

---

## 2. 导数与微分

### 2.1 导数定义

$$f'(x_0) = \lim_{\Delta x \to 0} \frac{f(x_0 + \Delta x) - f(x_0)}{\Delta x} = \lim_{x \to x_0} \frac{f(x) - f(x_0)}{x - x_0}$$

#### 左、右导数
$$f'_-(x_0) = \lim_{\Delta x \to 0^-} \frac{f(x_0 + \Delta x) - f(x_0)}{\Delta x}$$
$$f'_+(x_0) = \lim_{\Delta x \to 0^+} \frac{f(x_0 + \Delta x) - f(x_0)}{\Delta x}$$

> **导数存在 $\Leftrightarrow$ 左导数 = 右导数**

### 2.2 导数的几何意义

- 导数 $f'(x_0)$ = 曲线在点 $(x_0, f(x_0))$ 处的切线斜率
- **切线方程**: $y - f(x_0) = f'(x_0)(x - x_0)$
- **法线方程**: $y - f(x_0) = -\frac{1}{f'(x_0)}(x - x_0)$

### 2.3 基本求导公式

| 函数 | 导数 |
|------|------|
| $C$（常数） | $0$ |
| $x^n$ | $nx^{n-1}$ |
| $\sin x$ | $\cos x$ |
| $\cos x$ | $-\sin x$ |
| $\tan x$ | $\sec^2 x$ |
| $\cot x$ | $-\csc^2 x$ |
| $\sec x$ | $\sec x \tan x$ |
| $\csc x$ | $-\csc x \cot x$ |
| $a^x$ | $a^x \ln a$ |
| $e^x$ | $e^x$ |
| $\log_a x$ | $\frac{1}{x \ln a}$ |
| $\ln x$ | $\frac{1}{x}$ |
| $\arcsin x$ | $\frac{1}{\sqrt{1-x^2}}$ |
| $\arccos x$ | $-\frac{1}{\sqrt{1-x^2}}$ |
| $\arctan x$ | $\frac{1}{1+x^2}$ |
| $\text{arccot } x$ | $-\frac{1}{1+x^2}$ |

### 2.4 求导法则

#### 四则运算
$$\boxed{(u \pm v)' = u' \pm v'}$$
$$\boxed{(uv)' = u'v + uv'}$$
$$\boxed{\left(\frac{u}{v}\right)' = \frac{u'v - uv'}{v^2}}$$

#### 复合函数求导（链式法则）
$$\boxed{[f(g(x))]' = f'(g(x)) \cdot g'(x)}$$

#### 反函数求导
$$\boxed{\frac{dx}{dy} = \frac{1}{\frac{dy}{dx}}} \quad \Rightarrow \quad (\arcsin x)' = \frac{1}{\sqrt{1-x^2}}$$

#### 隐函数求导
1. 方程两边对 $x$ 求导
2. 遇到 $y$ 时视为 $x$ 的函数，使用链式法则
3. 解出 $y'$

#### 对数求导法
适用于幂指函数或多个因式乘除的函数：
$$\ln y = \ln[f(x)] \Rightarrow \frac{y'}{y} = [\ln f(x)]'$$

### 2.5 高阶导数

$$f^{(n)}(x) = \frac{d^n f(x)}{dx^n}$$

#### 莱布尼茨公式
$$\boxed{(uv)^{(n)} = \sum_{k=0}^{n} C_n^k u^{(k)} v^{(n-k)}}$$

#### 常见高阶导数
$$(x^n)^{(n)} = n!$$
$$(\sin x)^{(n)} = \sin\left(x + \frac{n\pi}{2}\right)$$
$$(\cos x)^{(n)} = \cos\left(x + \frac{n\pi}{2}\right)$$
$$(e^x)^{(n)} = e^x$$
$$[\ln(1+x)]^{(n)} = (-1)^{n-1}\frac{(n-1)!}{(1+x)^n}$$

### 2.6 微分

#### 定义
$$dy = f'(x_0) \cdot dx = f'(x_0) \Delta x$$

#### 微分与导数的关系
$$f'(x) = \frac{dy}{dx}$$

#### 微分公式
| $u$ | $du$ |
|-----|------|
| $u \pm v$ | $du \pm dv$ |
| $uv$ | $v\,du + u\,dv$ |
| $\frac{u}{v}$ | $\frac{v\,du - u\,dv}{v^2}$ |

#### 一阶微分形式不变性
$$dF(u) = F'(u)\,du$$ （$u$ 为自变量或中间变量均成立）

---

## 3. 微分中值定理与导数应用

### 3.1 微分中值定理

#### 罗尔定理
若 $f(x)$ 满足：
1. 在 $[a,b]$ 上连续
2. 在 $(a,b)$ 内可导
3. $f(a) = f(b)$

则 $\exists \xi \in (a,b)$，使 $f'(\xi) = 0$

#### 拉格朗日中值定理
若 $f(x)$ 满足：
1. 在 $[a,b]$ 上连续
2. 在 $(a,b)$ 内可导

则 $\exists \xi \in (a,b)$，使
$$\boxed{f(b) - f(a) = f'(\xi)(b - a)}$$

> **重要推论**: 若 $f'(x) \equiv 0$，则 $f(x) \equiv C$（常数）

#### 柯西中值定理
若 $f(x), g(x)$ 满足：
1. 在 $[a,b]$ 上连续
2. 在 $(a,b)$ 内可导
3. $g'(x) \neq 0$

则 $\exists \xi \in (a,b)$，使
$$\frac{f(b) - f(a)}{g(b) - g(a)} = \frac{f'(\xi)}{g'(\xi)}$$

### 3.2 洛必达法则

$$\boxed{\lim \frac{f(x)}{g(x)} = \lim \frac{f'(x)}{g'(x)}}$$
（前提：$\frac{0}{0}$ 或 $\frac{\infty}{\infty}$ 型，且右边极限存在或为无穷大）

> **注意**: 每次使用前需验证分子分母极限是否为 $0$ 或 $\infty$

#### 其他可转化为 $\frac{0}{0}$ 或 $\frac{\infty}{\infty}$ 的类型
- $0 \cdot \infty \Rightarrow \frac{1}{\infty} \cdot \infty$ 或 $\frac{0}{1/0}$
- $\infty - \infty \Rightarrow$ 通分或根式有理化
- $0^0, \infty^0, 1^\infty \Rightarrow$ 取对数

### 3.3 泰勒公式

#### 泰勒中值定理
若 $f(x)$ 在 $x_0$ 的某邻域内有 $n+1$ 阶导数，则：
$$f(x) = f(x_0) + f'(x_0)(x-x_0) + \frac{f''(x_0)}{2!}(x-x_0)^2 + \cdots + \frac{f^{(n)}(x_0)}{n!}(x-x_0)^n + R_n(x)$$

#### 拉格朗日余项
$$R_n(x) = \frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1}, \quad \xi \text{ 在 } x_0 \text{ 与 } x \text{ 之间}$$

#### 麦克劳林公式（$x_0 = 0$）
$$e^x = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots + \frac{x^n}{n!} + R_n(x)$$
$$\sin x = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots + (-1)^n\frac{x^{2n+1}}{(2n+1)!} + R_{2n+1}(x)$$
$$\cos x = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \cdots + (-1)^n\frac{x^{2n}}{(2n)!} + R_{2n}(x)$$
$$\ln(1+x) = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots + (-1)^{n-1}\frac{x^n}{n} + R_n(x)$$
$$(1+x)^\alpha = 1 + \alpha x + \frac{\alpha(\alpha-1)}{2!}x^2 + \cdots + \frac{\alpha(\alpha-1)\cdots(\alpha-n+1)}{n!}x^n + R_n(x)$$

### 3.4 函数的单调性与极值

#### 单调性判定
- $f'(x) > 0 \Rightarrow f(x)$ 在区间上单调递增
- $f'(x) < 0 \Rightarrow f(x)$ 在区间上单调递减

#### 极值必要条件
若 $x_0$ 为极值点且 $f'(x_0)$ 存在，则 $f'(x_0) = 0$

#### 极值判别法（第一充分条件）
若 $f(x)$ 在 $x_0$ 连续，在 $x_0$ 某去心邻域可导：
- $x < x_0$ 时 $f' > 0$，$x > x_0$ 时 $f' < 0$ $\Rightarrow$ $x_0$ 为极大值点
- $x < x_0$ 时 $f' < 0$，$x > x_0$ 时 $f' > 0$ $\Rightarrow$ $x_0$ 为极小值点

#### 极值判别法（第二充分条件）
若 $f'(x_0) = 0$，$f''(x_0) \neq 0$：
- $f''(x_0) < 0 \Rightarrow$ 极大值
- $f''(x_0) > 0 \Rightarrow$ 极小值

### 3.5 曲线的凹凸性与拐点

#### 凹凸性定义
- **凹函数**: $f\left(\frac{x_1+x_2}{2}\right) < \frac{f(x_1)+f(x_2)}{2}$
- **凸函数**: $f\left(\frac{x_1+x_2}{2}\right) > \frac{f(x_1)+f(x_2)}{2}$

#### 凹凸性判定
- $f''(x) > 0 \Rightarrow$ 曲线在区间上为凹
- $f''(x) < 0 \Rightarrow$ 曲线在区间上为凸

#### 拐点必要条件
若 $(x_0, f(x_0))$ 为拐点且 $f''(x_0)$ 存在，则 $f''(x_0) = 0$

### 3.6 最值问题

闭区间 $[a,b]$ 上连续函数的最值：
1. 求导得驻点 $f'(x) = 0$
2. 考察不可导点
3. 比较 $f(a), f(b), f(\text{驻点}), f(\text{不可导点})$
4. 最大者为最大值，最小者为最小值

### 3.7 曲率

$$K = \frac{|y''|}{[1+(y')^2]^{3/2}}$$

曲率半径：$\rho = \frac{1}{K}$

---

## 4. 不定积分

### 4.1 原函数与不定积分

#### 定义
若 $F'(x) = f(x)$，则 $F(x)$ 为 $f(x)$ 的一个原函数
$$\int f(x)\,dx = F(x) + C$$

### 4.2 基本积分公式

| 原函数 | 导数 |
|--------|------|
| $\frac{x^{\alpha+1}}{\alpha+1}$ | $x^\alpha$ |
| $\ln|x|$ | $\frac{1}{x}$ |
| $\frac{a^x}{\ln a}$ | $a^x$ |
| $e^x$ | $e^x$ |
| $-\cos x$ | $\sin x$ |
| $\sin x$ | $\cos x$ |
| $\tan x$ | $\sec^2 x$ |
| $-\cot x$ | $\csc^2 x$ |
| $\ln|\sec x + \tan x|$ | $\sec x$ |
| $\ln|\csc x - \cot x|$ | $\csc x$ |
| $\arcsin x$ | $\frac{1}{\sqrt{1-x^2}}$ |
| $\arctan x$ | $\frac{1}{1+x^2}$ |

### 4.3 不定积分法则

#### 第一换元法（凑微分法）
$$\int f[\varphi(x)]\varphi'(x)\,dx = \left[\int f(u)\,du\right]_{u=\varphi(x)}$$

#### 第二换元法
$$\int f(x)\,dx = \left[\int f[\varphi(t)]\varphi'(t)\,dt\right]_{t=\varphi^{-1}(x)}$$

**常用代换**：
- 根号下一次式：$t = \sqrt{ax+b}$
- 三角代换：$x = a\sin t, x = a\tan t, x = a\sec t$
- 倒代换：$x = \frac{1}{t}$

#### 分部积分法
$$\boxed{\int u\,dv = uv - \int v\,du}$$

**适用类型**：
- $\int x^n e^x dx, \int x^n \sin x dx, \int x^n \cos x dx$：$u = x^n$
- $\int x^n \ln x dx$：$u = \ln x$
- $\int e^x \sin x dx, \int e^x \cos x dx$：需两次分部后移项求解

### 4.4 有理函数积分

#### 部分分式分解
真分式可分解为：
$$\frac{P(x)}{Q(x)} = \frac{A}{x-a} + \frac{B}{(x-a)^2} + \cdots + \frac{Cx+D}{x^2+px+q} + \cdots$$

### 4.5 三角函数积分

#### 降幂公式
$$\sin^2 x = \frac{1-\cos 2x}{2}, \quad \cos^2 x = \frac{1+\cos 2x}{2}$$

#### 万能代换
令 $t = \tan\frac{x}{2}$：
$$\sin x = \frac{2t}{1+t^2}, \quad \cos x = \frac{1-t^2}{1+t^2}, \quad dx = \frac{2\,dt}{1+t^2}$$

---

## 5. 定积分

### 5.1 定积分定义

$$\int_a^b f(x)\,dx = \lim_{\lambda \to 0} \sum_{i=1}^{n} f(\xi_i)\Delta x_i$$

其中 $\lambda = \max\{\Delta x_i\}$

> 定积分的值只与被积函数和积分区间有关，与积分变量无关

### 5.2 定积分的性质

| 性质 | 公式 |
|------|------|
| 线性性 | $\int_a^b [kf(x) + mg(x)]dx = k\int_a^b f(x)dx + m\int_a^b g(x)dx$ |
| 可加性 | $\int_a^b f(x)dx = \int_a^c f(x)dx + \int_c^b f(x)dx$ |
| 比较 | $f(x) \geq g(x) \Rightarrow \int_a^b f(x)dx \geq \int_a^b g(x)dx$ |
| 估值 | $m(b-a) \leq \int_a^b f(x)dx \leq M(b-a)$ |
| 中值定理 | $\exists \xi \in [a,b], \int_a^b f(x)dx = f(\xi)(b-a)$ |

### 5.3 微积分基本定理

#### 原函数存在定理
若 $f(x)$ 在 $[a,b]$ 连续，则 $\Phi(x) = \int_a^x f(t)dt$ 在 $[a,b]$ 可导，且
$$\Phi'(x) = f(x)$$

#### 牛顿-莱布尼茨公式
$$\boxed{\int_a^b f(x)dx = F(b) - F(a)}$$

其中 $F(x)$ 为 $f(x)$ 的任一原函数

### 5.4 定积分换元法

$$\int_a^b f(x)\,dx = \int_{\alpha}^{\beta} f[\varphi(t)]\varphi'(t)\,dt$$

> **注意**：换元必换限，且 $t = \varphi^{-1}(x)$

### 5.5 定积分分部积分

$$\boxed{\int_a^b u\,dv = \left[uv\right]_a^b - \int_a^b v\,du}$$

### 5.6 奇偶函数积分

- $f(x)$ 为奇函数：$\int_{-a}^a f(x)dx = 0$
- $f(x)$ 为偶函数：$\int_{-a}^a f(x)dx = 2\int_0^a f(x)dx$

### 5.7 定积分的几何应用

#### 平面图形面积
- **直角坐标**: $A = \int_a^b |f(x) - g(x)|dx$
- **参数方程**: $A = \int_\alpha^\beta y(t)x'(t)dt$
- **极坐标**: $A = \frac{1}{2}\int_\alpha^\beta r^2(\theta)d\theta$

#### 旋转体体积
- **绕x轴**: $V_x = \pi\int_a^b f^2(x)dx$
- **绕y轴**: $V_y = 2\pi\int_a^b x|f(x)|dx$

#### 曲线弧长
- **直角坐标**: $s = \int_a^b \sqrt{1+[f'(x)]^2}dx$
- **参数方程**: $s = \int_\alpha^\beta \sqrt{[x'(t)]^2+[y'(t)]^2}dt$
- **极坐标**: $s = \int_\alpha^\beta \sqrt{r^2+[r'(\theta)]^2}d\theta$

### 5.8 定积分的物理应用

- **做功**: $W = \int_a^b F(x)dx$
- **液体压力**: $P = \int_a^b \rho g x f(x)dx$
- **引力**: 利用微元法分析

---

## 典型例题

### 例1：洛必达法则
$$\lim_{x \to 0} \frac{x - \sin x}{x^3}$$

**解**：
$$\lim_{x \to 0} \frac{x - \sin x}{x^3} = \lim_{x \to 0} \frac{1 - \cos x}{3x^2} = \lim_{x \to 0} \frac{\sin x}{6x} = \frac{1}{6}$$

### 例2：泰勒公式应用
$$\lim_{x \to 0} \frac{\sin x - x\cos x}{x^3}$$

**解**：使用麦克劳林展开：
$$\sin x = x - \frac{x^3}{6} + o(x^3)$$
$$\cos x = 1 - \frac{x^2}{2} + o(x^2)$$

$$x\cos x = x - \frac{x^3}{2} + o(x^3)$$

$$\sin x - x\cos x = \left(x - \frac{x^3}{6}\right) - \left(x - \frac{x^3}{2}\right) + o(x^3) = \frac{x^3}{3} + o(x^3)$$

$$\lim_{x \to 0} \frac{\sin x - x\cos x}{x^3} = \frac{1}{3}$$

### 例3：分部积分
$$\int x^2 e^x dx$$

**解**：
$$= x^2 e^x - \int 2x e^x dx = x^2 e^x - 2(xe^x - \int e^x dx)$$
$$= x^2 e^x - 2xe^x + 2e^x + C = e^x(x^2 - 2x + 2) + C$$

### 例4：定积分几何应用
求曲线 $y = \sqrt{x}$，$x = 4$，$x$ 轴所围图形绕 $y$ 轴旋转的体积

**解**：
$$V_y = 2\pi \int_0^4 x \cdot \sqrt{x}\,dx = 2\pi \int_0^4 x^{3/2}dx = 2\pi \cdot \frac{2}{5}x^{5/2}\Big|_0^4 = \frac{4\pi}{5} \cdot 32 = \frac{128\pi}{5}$$

---

## 易错点提示

> ⚠️ **极限计算**
> - 分子分母同时趋近于0或无穷大时才能用洛必达
> - 等价无穷小替换只能在乘除中使用，加减法不可乱用

> ⚠️ **导数与微分**
> - 可导必连续，但连续不一定可导（如 $|x|$ 在 $x=0$ 处）
> - 复合函数求导不要遗漏链式法则
> - 隐函数求导时，$y$ 的函数要乘以 $y'$

> ⚠️ **积分计算**
> - 不定积分最后要加常数 $C$
> - 定积分换元必须换限
> - 分部积分中 $u$ 和 $dv$ 的选择要合理

> ⚠️ **泰勒公式**
> - 展开到足够阶数，余项不可忽略
> - 不同点展开公式不同

> ⚠️ **中值定理**
> - 三个中值定理都有前提条件，使用前先验证
> - 构造辅助函数是中值定理证明题的关键

---

**整理时间**：大一上学期末  
**适用教材**：《高等数学》（同济大学版）  
**重要程度**：⭐⭐⭐⭐⭐
