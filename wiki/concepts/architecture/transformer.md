---
type: concept
title: "Transformer 与自注意力机制"
aliases: [Self-Attention, Scaled Dot-Product Attention]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [positional-encoding, rope, attention-variants, moe]
tags: [transformer, attention, 架构基础]
status: active
confidence: high
interview_frequency: high
interview_difficulty: medium
---

# Transformer 与自注意力机制

## 核心概念

自注意力（Self-Attention）使模型能动态衡量输入序列中不同词元之间的重要性。

### 工作原理（5步）

1. **生成 Q, K, V 向量**：每个词元通过 $W^Q, W^K, W^V$ 三个权重矩阵生成：
   - **Query (Q)**: 当前词元的"查询意图"
   - **Key (K)**: 每个词元携带的"信息标签"
   - **Value (V)**: 每个词元的"实际内容"

2. **计算注意力分数**：Q 与所有 K 的点积
   - $Score(Q_i, K_j) = Q_i \cdot K_j$

3. **缩放**：除以 $\sqrt{d_k}$，防止点积过大导致 Softmax 进入饱和区
   - $Scaled = Q \cdot K^T / \sqrt{d_k}$

4. **Softmax 归一化**：转为概率分布（注意力权重）

5. **加权求和**：注意力权重 × V → 上下文感知输出

### 为什么优于 RNN？

| 维度        | Transformer   | RNN             |
| --------- | ------------- | --------------- |
| **并行性**   | 一次处理整个序列，高度并行 | 必须逐步处理，无法并行     |
| **长距离依赖** | 任意两位置路径 O(1)  | 路径 O(N)，梯度消失/爆炸 |
| **训练效率**  | 充分利用 GPU 并行   | 受限于序列长度         |

## 补充见解

1. **缩放的深层原因**：当 d_k 很大时，点积方差随之增大，Softmax 输出趋向 one-hot（几乎所有权重集中于一个位置），梯度极小。缩放让输入保持在 Softmax 的有效梯度区间。

2. **Attention 的本质**：可类比为"软性字典查找"——传统字典精确匹配 key 返回 value，Attention 对所有 key 做加权匹配返回 value 的加权组合。

3. **Multi-Head 的意义**：不同头关注不同类型的关系（语法、语义、位置等），类比"多视角看问题"。研究表明部分头确实有明确的功能分工。

4. **计算瓶颈**：Self-Attention 复杂度 O(n²·d)，这也是 FlashAttention、稀疏注意力等后续工作的核心动机。

---

*来源：[[sources/extra01-llm-interview-reference]]*
