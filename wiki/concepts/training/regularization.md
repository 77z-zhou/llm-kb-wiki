---
type: concept
title: "L1/L2 正则化"
aliases: [Lasso, Ridge, Weight Decay]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [large-scale-training]
tags: [正则化, 基础]
status: active
confidence: high
interview_frequency: low
interview_difficulty: easy
---

# L1/L2 正则化

在损失函数中添加惩罚项防止过拟合。

## L1 正则化 (Lasso)

- `Loss_L1 = Original Loss + λ·Σ|w_i|`
- **效果**：权重稀疏化，部分权重变为精确 0
- **适用**：特征选择，当存在大量冗余特征时

## L2 正则化 (Ridge / Weight Decay)

- `Loss_L2 = Original Loss + λ·Σw_i²`
- **效果**：权重趋近于 0 但不为 0，分布更平滑
- **适用**：通用过拟合防治，深度学习中最常用

## 对比

| 对比项 | L1 | L2 |
|--------|----|----|
| **效果** | 稀疏化，部分权重=0 | 平滑化，权重趋近0 |
| **用途** | 特征选择 | 通用防过拟合 |
| **解的稳定性** | 不稳定 | 稳定，唯一解 |

## 补充

在现代 LLM 训练中，L2 正则化（Weight Decay）几乎是标配，通常配合 AdamW 优化器使用。AdamW 将 weight decay 从梯度更新中解耦，是目前主流做法。

---

*来源：[[sources/extra01-llm-interview-reference]]*
