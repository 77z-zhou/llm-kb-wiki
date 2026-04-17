---
type: concept
title: "Scaling Laws 尺度定律"
aliases: [尺度定律, Chinchilla定律]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [large-scale-training, emergent-abilities]
tags: [scaling, 训练]
status: active
confidence: high
interview_frequency: high
interview_difficulty: hard
---

# Scaling Laws 尺度定律

## 核心发现

LLM 性能（Loss）与三个要素存在**幂律关系**：
- **N**：模型参数规模
- **D**：训练数据集大小
- **C**：计算量 (FLOPs)

`L(N) ∝ N^(-α)`，性能随规模增大平滑、可预测地下降。

## 关键结论

1. **性能可预测**：小规模实验可外推大模型性能
2. **瓶颈效应**：N/D/C 中最受限的因素决定上限
3. **资源最优分配 (Chinchilla)**：计算最优条件下，参数量与数据量应约 **1:20** 比例扩展（70B 模型 ≈ 1.4T tokens）

## 研发指导意义

1. **科学规划**：先在小规模拟合 Scaling Law，再预测大模型性能和投资回报
2. **避免浪费**：Chinchilla 定律纠正了"一味堆参数"的做法，强调参数与数据的平衡
3. **数据为王**：高质量大规模数据与参数规模同等重要

## 补充见解

1. **Chinchilla 之后的变化**：实际上 Llama 系列"故意"违反了 Chinchilla 最优——用更多数据训练更小的模型（over-training），因为部署成本与模型大小正相关。这说明 Chinchilla 最优是"训练成本最优"而非"部署成本最优"。面试中能讲清这个区别非常加分。

2. **Scaling Laws 的局限**：它预测的是 Loss，但 Loss 的改善不一定线性映射到下游任务的改善。同时，它假设数据质量恒定，实际中数据质量才是最关键的变量。

3. **推理时 Scaling (Test-time Compute)**：近期研究（如 OpenAI o1）表明，在推理阶段投入更多计算（如更长的思维链）也能提升性能，这是 Scaling Laws 的新维度。

---

*来源：[[sources/extra01-llm-interview-reference]]*
