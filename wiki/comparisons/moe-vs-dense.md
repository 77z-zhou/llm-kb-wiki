---
type: comparison
title: "MoE vs Dense 模型"
created: 2026-04-17
updated: 2026-04-17
status: active
interview_frequency: high
---

# MoE vs Dense 模型对比

## 核心区别

| 维度 | Dense (稠密) | MoE (稀疏) |
|:-----|:-------------|:-----------|
| 参数激活 | 每个token激活所有参数 | 每个token只激活部分专家 |
| 推理成本 | 与参数量成正比 | 远低于总参数量对应成本 |
| 模型容量 | 受限 | 大幅扩展知识容量 |
| 训练难度 | 相对简单 | 负载均衡、路由策略、通信开销 |
| 代表模型 | GPT-4, Qwen-72B | Mixtral-8x7B, DeepSeek-V3 |

## MoE 的优势

- **解耦参数量和计算成本**：用小模型成本获得大模型知识
- **更好的 Scaling 效率**：增加专家数量比增加单模型参数更高效

## MoE 的挑战

- **路由负载均衡**：避免所有 token 都涌向少数专家
- **All-to-All 通信**：跨 GPU 的专家调度通信开销大
- **显存占用**：总参数仍需全部加载到显存

## 面试要点

- MoE 如何实现"参数大但推理成本低"？
- Mixtral 8x7B 的 47B 总参和 13B 推理成本如何计算？
- DeepSeekMoE 的"细粒度专家"和 Mixtral 有什么不同？

## 相关概念

- [[concepts/architecture/moe|MoE 概念页]]
- [[entities/deepseek|DeepSeek]]
