---
type: concept
title: "MoE 混合专家模型"
aliases: [Mixture of Experts, 稀疏激活]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [transformer, large-scale-training]
tags: [MoE, 稀疏激活, 架构]
status: active
confidence: high
interview_frequency: high
interview_difficulty: hard
---

# MoE 混合专家模型

## 核心思想

通过**稀疏激活（Sparse Activation）**解耦总参数量与推理成本：拥有巨大参数但每次只激活一小部分。

## 工作原理

### 1. 用"专家"替换 FFN 层

将 Transformer 的 FFN 层替换为 MoE 层，包含：
- **N 个"专家"**：每个都是独立的小型 FFN
- **1 个路由器（Router）**：小型线性层，决定 token 由哪些专家处理

### 2. 动态路由决策

Token → 路由器 → 输出 N 个匹配度分数 → Softmax

### 3. Top-K 稀疏激活

只激活分数最高的 **K 个专家**（通常 K=1 或 2），其余完全不参与计算。

### 4. 加权输出

被选中的 K 个专家输出按路由分数加权求和。

## 如何实现"参数大但成本低"？

以 Mixtral-8x7B 为例（N=8, K=2）：
- **总参数量**：共享部分 + 所有 8 个专家 ≈ 47B
- **推理成本**：共享部分 + 被激活的 2 个专家 ≈ 等价 13B 模型

**本质**：将**总参数量**（知识容量）和**推理计算量**（速度/成本）**解耦**。

## 补充见解

1. **路由器的训练难点**：MoE 最大的工程挑战是**负载均衡**——如果路由器总是把 token 发给少数几个"热门"专家，其他专家就会变成"死专家"。通常需要额外的 auxiliary loss（辅助损失）来鼓励均匀路由。

2. **MoE 的通信开销**：在分布式训练中，不同专家可能在不同 GPU 上，token 需要通过 All-to-All 通信发送到对应 GPU，这是 MoE 训练的主要瓶颈。

3. **DeepSeek-V2 的创新**：DeepSeek 在 MoE 上做了 DeepSeekMoE 设计，使用更多更小的专家（如 64 个细粒度专家）+ shared expert，在路由效率和专家利用率上有显著改进。面试中可以作为亮点提。

4. **MoE vs Dense 的选择**：MoE 并非总是更优。在推理时虽然单次 FLOPs 低，但因为总参数多，**显存占用**和**通信需求**都更高。适合"算力充裕但想要更强模型"的场景。

---

*来源：[[sources/extra01-llm-interview-reference]]*
