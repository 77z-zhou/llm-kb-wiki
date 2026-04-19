---
type: concept
title: "RoPE 旋转位置编码"
aliases: [Rotary Position Embedding, 旋转位置编码]
created: 2026-04-17
updated: 2026-04-19
sources: [extra01-llm-interview-reference]
related: [positional-encoding, transformer, attention-variants]
tags: [RoPE, 位置编码, 架构]
status: active
confidence: high
interview_frequency: high
interview_difficulty: hard
---

# RoPE 旋转位置编码

## 一、要解决什么问题？

Transformer 的 Self-Attention 本身是**位置无关**的——它只看 token 之间的相似度，不知道谁在前谁在后。所以必须注入位置信息。

传统做法（正弦位置编码、可学习位置编码）是在输入层**加上**一个位置向量，但这只能编码绝对位置，注意力分数无法自然反映**相对距离**。

RoPE 的目标：**用绝对位置信息编码 Q 和 K，使得它们的点积天然只依赖相对位置 $(m-n)$。**

## 二、核心直觉：旋转

RoPE 把 Q/K 向量的维度两两分组，每组看作一个**二维向量**（复平面上的一个点），然后根据 token 的位置**旋转**这个向量。

- 位置 $m$ 的 token → Q 向量旋转角度 = $m \times \theta$
- 位置 $n$ 的 token → K 向量旋转角度 = $n \times \theta$

两个旋转后的向量做点积时，结果只含 $(m-n)$ 项，绝对位置被消掉了。这就是 RoPE 的精髓——**用绝对位置的旋转操作，自然得到相对位置的表达**。

## 三、数学推导（从动机出发，逐步推导）

### 第一步：明确我们要什么

注意力分数的本质是 Q 和 K 的**点积**。假设位置 $m$ 的 token 的 Q 向量为 $\mathbf{q}$，位置 $n$ 的 token 的 K 向量为 $\mathbf{k}$。

我们需要找到一个**位置编码函数** $f$，作用于 $\mathbf{q}$ 和 $\mathbf{k}$，使得编码后的点积：

$$
\langle f(\mathbf{q}, m),\; f(\mathbf{k}, n) \rangle = g(\mathbf{q}, \mathbf{k}, m - n)
$$

即：**点积只依赖于 $\mathbf{q}$、$\mathbf{k}$ 的内容，以及它们的相对位置 $(m-n)$，而不单独依赖绝对位置 $m$ 或 $n$。**

这就是 RoPE 要满足的核心约束。

### 第二步：从 2D 情况入手

先只考虑 2 维向量（$d=2$），这样推导更清晰。

设 $\mathbf{q} = (q_1, q_2)$，$\mathbf{k} = (k_1, k_2)$。

**为什么从 2D 开始？** 因为后续我们会把高维向量拆成若干个 2D 子空间分别处理，所以先搞清楚 2D 的情况就够了。

### 第三步：为什么旋转是唯一解？（关键推导）

#### 3.1 假设 f 是线性变换

最简单的编码方式是用一个矩阵乘法。设位置 $m$ 的编码矩阵为 $T_m$，即 $f(\mathbf{x}, m) = T_m \mathbf{x}$。

用 $2 \times 2$ 矩阵的一般形式：

$$
T_m = \begin{bmatrix} a_m & b_m \\ c_m & d_m \end{bmatrix}
$$

编码后的向量：

$$
f(\mathbf{q}, m) = T_m \mathbf{q} = \begin{bmatrix} a_m q_1 + b_m q_2 \\ c_m q_1 + d_m q_2 \end{bmatrix}
$$

$$
f(\mathbf{k}, n) = T_n \mathbf{k} = \begin{bmatrix} a_n k_1 + b_n k_2 \\ c_n k_1 + d_n k_2 \end{bmatrix}
$$

#### 3.2 写出点积并施加约束

计算编码后的点积：

$$
\langle T_m \mathbf{q},\; T_n \mathbf{k} \rangle = (a_m q_1 + b_m q_2)(a_n k_1 + b_n k_2) + (c_m q_1 + d_m q_2)(c_n k_1 + d_n k_2)
$$

展开：

$$
= (a_m a_n + c_m c_n)\, q_1 k_1
+ (a_m b_n + c_m d_n)\, q_1 k_2
+ (b_m a_n + d_m c_n)\, q_2 k_1
+ (b_m b_n + d_m d_n)\, q_2 k_2
$$

现在施加约束：**这个结果必须只依赖于 $(m-n)$，不能单独出现 $m$ 或 $n$。**

这意味着所有矩阵元素的乘积组合（$a_m a_n + c_m c_n$ 等）都必须只是 $(m-n)$ 的函数。

#### 3.3 解约束 → 旋转矩阵

什么样的矩阵族 $\{T_m\}$ 满足这个条件？

回顾线性代数：**正交矩阵保持内积**，即 $\langle T \mathbf{u}, T \mathbf{v} \rangle = \langle \mathbf{u}, \mathbf{v} \rangle$。这太强了——编码后点积跟位置无关，不是我们想要的。

但如果我们用**不同的**矩阵 $T_m$ 和 $T_n$ 分别作用于 $\mathbf{q}$ 和 $\mathbf{k}$，并且要求：

$$
T_m^T T_n = T_{n-m}
$$

即"左矩阵的转置乘右矩阵"等于一个只跟 $(n-m)$ 有关的矩阵，那么点积 $\langle T_m \mathbf{q}, T_n \mathbf{k} \rangle = \mathbf{q}^T T_m^T T_n \mathbf{k} = \mathbf{q}^T T_{n-m} \mathbf{k}$ 就只依赖 $(n-m)$ 了。

**什么样的矩阵族满足 $T_m^T T_n = T_{n-m}$？**

答案：**旋转矩阵族**。

设 $T_m = R(m\theta)$，即旋转 $m\theta$ 角度的旋转矩阵：

$$
T_m = \begin{bmatrix} \cos(m\theta) & -\sin(m\theta) \\ \sin(m\theta) & \cos(m\theta) \end{bmatrix}
$$

验证：

$$
T_m^T T_n = R(m\theta)^T R(n\theta)
$$

旋转矩阵是正交矩阵（$R^T = R^{-1}$），所以：

$$
R(m\theta)^T R(n\theta) = R(-m\theta) R(n\theta) = R((n-m)\theta) = T_{n-m}
$$

**成立！** 这就是为什么旋转是解——旋转矩阵族天然满足"转置相乘消掉一个绝对位置"的性质。

### 第四步：复数视角（让直觉更清晰）

2D 旋转用矩阵表示有些繁琐。但如果把 2D 向量看作**复数**，一切变得非常简洁。

#### 4.1 2D 向量 → 复数

$$
(q_1, q_2) \longrightarrow q_1 + i \cdot q_2 \quad \text{（记为} \; z_q\text{）}
$$

#### 4.2 旋转 → 乘以 $e^{im\theta}$

复数乘以 $e^{i\alpha}$ 就是旋转 $\alpha$ 角度（欧拉公式）：

$$
e^{i\alpha} = \cos\alpha + i\sin\alpha
$$

所以编码操作变成：

$$
f(z_q, m) = z_q \cdot e^{im\theta}
$$

$$
f(z_k, n) = z_k \cdot e^{in\theta}
$$

#### 4.3 点积 → 复数乘法取实部

两个 2D 向量的点积，等价于对应复数乘积的实部：

$$
\langle \mathbf{q}, \mathbf{k} \rangle = \text{Re}(z_q \cdot \overline{z_k})
$$

其中 $\overline{z_k}$ 是 $z_k$ 的共轭复数。那么编码后的点积：

$$
\langle f(\mathbf{q},m), f(\mathbf{k},n) \rangle
= \text{Re}\!\big(z_q \cdot e^{im\theta} \cdot \overline{z_k \cdot e^{in\theta}}\big)
$$

共轭的性质 $\overline{z \cdot w} = \overline{z} \cdot \overline{w}$，且 $\overline{e^{in\theta}} = e^{-in\theta}$，所以：

$$
= \text{Re}\!\big(z_q \cdot e^{im\theta} \cdot \overline{z_k} \cdot e^{-in\theta}\big)
$$

合并指数部分：

$$
= \text{Re}\!\big(z_q \cdot \overline{z_k} \cdot e^{i(m-n)\theta}\big)
$$

**一目了然：绝对位置 $m$ 和 $n$ 合并为 $(m-n)$，完全消掉了。**

这就是复数视角的威力——旋转矩阵相乘消去绝对位置的推导，在复数域只需要一行。

### 第五步：从 2D 推广到 d 维

#### 5.1 分组策略

d 维向量有 d 个分量，我们两两分组：

$$
\underbrace{(q_1, q_2)}_{第0组},\;\underbrace{(q_3, q_4)}_{第1组},\;\ldots,\;\underbrace{(q_{d-1}, q_d)}_{第\frac{d}{2}-1组}
$$

共 $d/2$ 个 2D 子空间。

**为什么能分组独立处理？** 因为点积是逐元素相乘再求和：

$$
\langle \mathbf{q}, \mathbf{k} \rangle = \sum_{j=1}^{d} q_j k_j = \sum_{i=0}^{d/2-1} \Big( q_{2i+1} k_{2i+1} + q_{2i+2} k_{2i+2} \Big)
$$

每个括号内恰好是一组的点积。不同组之间是**求和关系**，互不干扰。所以每组独立旋转，不会影响其他组的结果。

#### 5.2 每组用不同的频率

第 $i$ 组的旋转角度设为 $m\theta_i$，其中频率定义为：

$$
\theta_i = 10000^{-2i/d}, \quad i = 0, 1, 2, \ldots, \tfrac{d}{2}-1
$$

**为什么不同组要不同频率？**

- 如果所有组用同一个 $\theta$，那所有组编码的是同一个尺度上的位置信息
- 用不同的 $\theta_i$ 可以让不同组捕捉不同尺度的位置关系：
  - $\theta_0 \approx 1$（最大频率）→ 旋转最快 → 捕捉相邻 token 间的精确位置
  - $\theta_{d/2-1} \approx 0$（最小频率）→ 旋转最慢 → 捕捉长距离的粗略位置

**为什么是 10000？** 这个底数来自原始 Transformer 的正弦位置编码，是一个经验值。它确保了频率从接近 1 到接近 0 的良好分布。

#### 5.3 完整的旋转矩阵

将 $d/2$ 个 2D 旋转块拼成块对角矩阵：

$$
R(\Theta, m) =
\begin{bmatrix}
\cos(m\theta_0) & -\sin(m\theta_0) & & \\
\sin(m\theta_0) &  \cos(m\theta_0) & & \\
& & \ddots & \\
& & & \cos(m\theta_{\frac{d}{2}-1}) & -\sin(m\theta_{\frac{d}{2}-1}) \\
& & & \sin(m\theta_{\frac{d}{2}-1}) &  \cos(m\theta_{\frac{d}{2}-1})
\end{bmatrix}
$$

编码操作：

$$
\hat{\mathbf{q}}_m = R(\Theta, m)\,\mathbf{q}, \qquad \hat{\mathbf{k}}_n = R(\Theta, n)\,\mathbf{k}
$$

### 第六步：完整展开验证（逐步推导，不跳步）

下面取第 $i$ 组，**完整展开**每一步，验证点积确实只含 $(m-n)$。

#### 6.1 旋转后的向量

第 $i$ 组的原始向量：

$$
\mathbf{q}^{(i)} = (q_{1}, q_{2}), \quad \mathbf{k}^{(i)} = (k_{1}, k_{2})
$$

（为简洁，省略组号下标 $i$，所有 $q_1, q_2, k_1, k_2$ 都是第 $i$ 组的分量）

旋转后：

$$
\hat{q}_{1} = q_{1}\cos(m\theta_i) - q_{2}\sin(m\theta_i)
$$

$$
\hat{q}_{2} = q_{1}\sin(m\theta_i) + q_{2}\cos(m\theta_i)
$$

$$
\hat{k}_{1} = k_{1}\cos(n\theta_i) - k_{2}\sin(n\theta_i)
$$

$$
\hat{k}_{2} = k_{1}\sin(n\theta_i) + k_{2}\cos(n\theta_i)
$$

#### 6.2 计算点积（展开 4 项）

$$
\hat{\mathbf{q}}^{(i)} \cdot \hat{\mathbf{k}}^{(i)} = \hat{q}_{1} \cdot \hat{k}_{1} + \hat{q}_{2} \cdot \hat{k}_{2}
$$

**第 1 项** $\hat{q}_{1} \cdot \hat{k}_{1}$：

$$
= \big(q_{1}\cos m\theta_i - q_{2}\sin m\theta_i\big)\big(k_{1}\cos n\theta_i - k_{2}\sin n\theta_i\big)
$$

展开（分配律）：

$$
= q_{1}k_{1}\cos m\theta_i\cos n\theta_i
- q_{1}k_{2}\cos m\theta_i\sin n\theta_i
- q_{2}k_{1}\sin m\theta_i\cos n\theta_i
+ q_{2}k_{2}\sin m\theta_i\sin n\theta_i
$$

**第 2 项** $\hat{q}_{2} \cdot \hat{k}_{2}$：

$$
= \big(q_{1}\sin m\theta_i + q_{2}\cos m\theta_i\big)\big(k_{1}\sin n\theta_i + k_{2}\cos n\theta_i\big)
$$

展开：

$$
= q_{1}k_{1}\sin m\theta_i\sin n\theta_i
+ q_{1}k_{2}\sin m\theta_i\cos n\theta_i
+ q_{2}k_{1}\cos m\theta_i\sin n\theta_i
+ q_{2}k_{2}\cos m\theta_i\cos n\theta_i
$$

#### 6.3 合并同类项

将第 1 项和第 2 项相加，按 $q_1k_1$、$q_1k_2$、$q_2k_1$、$q_2k_2$ 四类合并：

**$q_1k_1$ 的系数**：

$$
\cos m\theta_i\cos n\theta_i + \sin m\theta_i\sin n\theta_i
$$

利用和角公式 $\cos\alpha\cos\beta + \sin\alpha\sin\beta = \cos(\alpha - \beta)$：

$$
= \cos\big((m - n)\theta_i\big)
$$

**$q_1k_2$ 的系数**：

$$
-\cos m\theta_i\sin n\theta_i + \sin m\theta_i\cos n\theta_i
$$

利用和角公式 $\sin\alpha\cos\beta - \cos\alpha\sin\beta = \sin(\alpha - \beta)$：

$$
= \sin\big((m - n)\theta_i\big)
$$

**$q_2k_1$ 的系数**：

$$
-\sin m\theta_i\cos n\theta_i + \cos m\theta_i\sin n\theta_i
$$

$$
= -\big(\sin m\theta_i\cos n\theta_i - \cos m\theta_i\sin n\theta_i\big)
$$

$$
= -\sin\big((m - n)\theta_i\big)
$$

**$q_2k_2$ 的系数**：

$$
\sin m\theta_i\sin n\theta_i + \cos m\theta_i\cos n\theta_i
$$

$$
= \cos\big((m - n)\theta_i\big)
$$

#### 6.4 写出最终结果

$$
\hat{\mathbf{q}}^{(i)} \cdot \hat{\mathbf{k}}^{(i)}
= (q_{1}k_{1} + q_{2}k_{2})\cos\big((m{-}n)\theta_i\big)
+ (q_{1}k_{2} - q_{2}k_{1})\sin\big((m{-}n)\theta_i\big)
$$

**验证成功：所有项中的 $m$ 和 $n$ 都只以 $(m-n)$ 的形式出现。**

对所有 $d/2$ 组求和：

$$
\hat{\mathbf{q}}_m \cdot \hat{\mathbf{k}}_n
= \sum_{i=0}^{d/2-1}\Big[
(q_{2i+1}k_{2i+1} + q_{2i+2}k_{2i+2})\cos\big((m{-}n)\theta_i\big)
+ (q_{2i+1}k_{2i+2} - q_{2i+2}k_{2i+1})\sin\big((m{-}n)\theta_i\big)
\Big]
$$

注意力分数完全是相对位置 $(m-n)$ 的函数。

### 第七步：远程衰减直觉

不同组的 $\theta_i$ 跨越多个数量级（从 $\sim 1$ 到 $\sim 0.0001$），导致不同组对位置的"感知粒度"不同：

- **高频组**（$\theta_i$ 大）：位置差 1 就转很大角度，能区分相邻 token，但距离一远就快速振荡，贡献趋于零
- **低频组**（$\theta_i$ 小）：位置差 100 也只转很小角度，能感知远距离关系，但区分度低

整体效果：**近距离时多频率共同提供精确位置信息，远距离时只剩低频提供粗略信息，内积自然衰减。** 这符合语言中"远距离 token 关联更弱"的直觉。

## 四、高效计算（工程实现）

实际不需要构造 $d \times d$ 的稀疏旋转矩阵，可以用逐元素运算：

$$
q'_m = \big[\,q_1\cos(m\theta_0) - q_2\sin(m\theta_0),\;\;
q_1\sin(m\theta_0) + q_2\cos(m\theta_0),\;\;
q_3\cos(m\theta_1) - q_4\sin(m\theta_1),\;\;\ldots\,\big]
$$

等价写法（更常见于代码）：

$$
q'_m = q \odot \cos\_\text{vec} + \text{rotate\_half}(q) \odot \sin\_\text{vec}
$$

其中：

$$
\cos\_\text{vec} = [\cos(m\theta_0),\, \cos(m\theta_0),\, \cos(m\theta_1),\, \cos(m\theta_1),\, \ldots]
$$

$$
\sin\_\text{vec} = [\sin(m\theta_0),\, \sin(m\theta_0),\, \sin(m\theta_1),\, \sin(m\theta_1),\, \ldots]
$$

$$
\text{rotate\_half}(q) = [-q_2,\, q_1,\, -q_4,\, q_3,\, \ldots]
$$

## 五、与其他位置编码的对比

| 特性 | RoPE | 正弦编码 | 可学习PE | ALiBi |
|------|------|----------|----------|-------|
| 位置类型 | 绝对编码→相对感知 | 绝对 | 绝对 | 相对 |
| 编码方式 | 乘法（旋转） | 加法 | 加法 | 注意力分数加偏置 |
| 额外参数 | 无 | 无 | 有（$d$ 维向量） | 有（斜率） |
| 相对位置建模 | 天然支持 | 有限 | 无 | 直接编码 |
| 长度外推 | 较好（需增强） | 差 | 差 | 好 |
| 主流采用 | LLaMA/Qwen/DeepSeek | 原始Transformer | BERT/GPT | BLOOM/MPT |

## 六、长度外推问题

RoPE 的外推能力不是无限的。当推理长度远超训练长度时：

- 高频分量（大 $\theta_i$）在超出训练范围后会产生未见过的角度值
- 导致注意力分布混乱，性能急剧下降

**主流解决方案**：

1. **Position Interpolation (PI)**：将位置线性压缩到训练范围内
2. **NTK-aware Scaling**：调整 $\theta_i$ 的底数（$10000 \to$ 更大值），让旋转变慢
3. **YaRN**：结合 NTK scaling 和注意力温度调整，对不同频率分量分别处理

## 七、面试高频问题

1. **RoPE 的"旋转"直觉是什么？** → 把向量分量视为复数，乘以 $e^{im\theta}$，只改变方向不改变模长
2. **为什么内积只依赖相对位置？** → 旋转矩阵族满足 $R(m\theta)^T R(n\theta) = R((n{-}m)\theta)$，转置相乘消掉一个绝对位置
3. **RoPE 和正弦编码的 $\theta$ 公式一样，为什么效果不同？** → 正弦编码是加法叠加，RoPE 是乘法旋转，后者改变了 Q/K 的方向从而直接影响注意力
4. **长度外推怎么解决？** → NTK-aware scaling / YaRN / Position Interpolation
5. **RoPE 为什么有远程衰减？** → 多频率分量叠加的数学性质，高频快速振荡取平均后贡献趋零

---
*来源：[[sources/extra01-llm-interview-reference]]*
