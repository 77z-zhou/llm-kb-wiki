---
type: concept
title: "RoPE 旋转位置编码"
aliases: [Rotary Position Embedding, 旋转位置编码]
created: 2026-04-17
updated: 2026-04-18
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

## 三、数学原理

### 3.1 维度分组

Q/K 是 $d$ 维向量，分成 $d/2$ 组，每组 2 维：

$$
[x_1, x_2, x_3, x_4, \ldots, x_{d-1}, x_d]
$$

$$
\underbrace{(x_1, x_2)}_{第0组},\;\underbrace{(x_3, x_4)}_{第1组},\;\ldots,\;\underbrace{(x_{d-1}, x_d)}_{第\frac{d}{2}-1组} \quad\longrightarrow\quad \frac{d}{2} \text{ 个二维向量}
$$

### 3.2 频率定义

每组对应一个旋转基础频率：

$$
\theta_i = 10000^{-2i/d}, \quad i = 0, 1, 2, \ldots, \tfrac{d}{2}-1
$$

- $i$ 小（低维组）→ $\theta_i$ 大 → 旋转快 → 捕捉局部位置关系
- $i$ 大（高维组）→ $\theta_i$ 小 → 旋转慢 → 捕捉长距离位置关系

### 3.3 旋转操作

对位置 $m$ 的第 $i$ 组二维向量 $(x_1, x_2)$，做角度为 $m\theta_i$ 的旋转：

$$
\begin{bmatrix} x_1' \\ x_2' \end{bmatrix}
=
\begin{bmatrix}
\cos(m\theta_i) & -\sin(m\theta_i) \\
\sin(m\theta_i) &  \cos(m\theta_i)
\end{bmatrix}
\begin{bmatrix} x_1 \\ x_2 \end{bmatrix}
$$

对所有 $d/2$ 组同时旋转，写成块对角矩阵：

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

这是一个 $d \times d$ 的块对角矩阵，由 $d/2$ 个独立的 $2 \times 2$ 旋转块组成。

### 3.4 为什么内积只依赖相对位置？

设 $q$ 旋转后为 $\hat{q}_m = R(\Theta, m)\,q$，$k$ 旋转后为 $\hat{k}_n = R(\Theta, n)\,k$。

展开第 $i$ 组的点积贡献：

$$
\hat{q}_m[i] \cdot \hat{k}_n[i]
= (q_{1i}\cos m\theta_i - q_{2i}\sin m\theta_i)(k_{1i}\cos n\theta_i - k_{2i}\sin n\theta_i)
$$
$$
+ (q_{1i}\sin m\theta_i + q_{2i}\cos m\theta_i)(k_{1i}\sin n\theta_i + k_{2i}\cos n\theta_i)
$$

展开化简，利用三角恒等式 $\cos\alpha\cos\beta + \sin\alpha\sin\beta = \cos(\alpha - \beta)$：

$$
\hat{q}_m[i] \cdot \hat{k}_n[i]
= (q_{1i} k_{1i} + q_{2i} k_{2i})\cos((m{-}n)\theta_i)
+ (q_{1i} k_{2i} - q_{2i} k_{1i})\sin((m{-}n)\theta_i)
$$

**关键：结果中 $m$ 和 $n$ 只以 $(m-n)$ 的形式出现，绝对位置被完全消掉。**

全部 $d/2$ 组求和：

$$
\hat{q}_m \cdot \hat{k}_n
= \sum_{i=0}^{d/2-1}\Big[
(q_{1i} k_{1i} + q_{2i} k_{2i})\cos((m{-}n)\theta_i)
+ (q_{1i} k_{2i} - q_{2i} k_{1i})\sin((m{-}n)\theta_i)
\Big]
$$

注意力分数完全是相对位置 $(m-n)$ 的函数。

### 3.5 远程衰减特性

不同组的 $\theta_i$ 差异很大（从 $\sim 1$ 到 $\sim 0.0001$），叠加后：

- **近距离** $(m{-}n$ 小$)$：高频分量提供精确位置区分
- **远距离** $(m{-}n$ 大$)$：高频分量快速振荡趋于平均，只剩低频分量提供粗略位置信息
- **整体效果**：内积随距离增大呈衰减趋势，符合"远距离 token 关联更弱"的语言直觉

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
2. **为什么内积只依赖相对位置？** → 旋转的可结合性：旋转 $m°$ 再与旋转 $n°$ 的点积 = 旋转 $(m{-}n)°$ 的点积
3. **RoPE 和正弦编码的 $\theta$ 公式一样，为什么效果不同？** → 正弦编码是加法叠加，RoPE 是乘法旋转，后者改变了 Q/K 的方向从而直接影响注意力
4. **长度外推怎么解决？** → NTK-aware scaling / YaRN / Position Interpolation
5. **RoPE 为什么有远程衰减？** → 多频率分量叠加的数学性质，高频快速振荡取平均后贡献趋零

---
*来源：[[sources/extra01-llm-interview-reference]]*
