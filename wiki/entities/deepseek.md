---
type: entity
title: "DeepSeek 系列"
category: model
created: 2026-04-17
updated: 2026-04-17
status: active
tags: [深度求索, 开源模型, LLM, MoE, RL]
interview_frequency: high
related_concepts: [moe, rlhf, ppo]
---

# DeepSeek 系列

## 基本信息

- **开发者**：深度求索 (DeepSeek)
- **开源协议**：MIT（大部分版本）
- **定位**：高性价比开源模型，以创新架构著称

## 关键版本与创新

| 版本 | 参数量 | 核心创新 |
|:-----|:-------|:---------|
| DeepSeek-V2 | 236B (21B激活) | MLA (Multi-head Latent Attention)、DeepSeekMoE |
| DeepSeek-V3 | 671B (37B激活) | 辅助无损负载均衡、多 token 预测 |
| DeepSeek-R1 | 671B | 纯 RL 训练推理能力、蒸馏到小模型 |

## 核心创新点

### MLA (Multi-head Latent Attention)
- 将 KV Cache 压缩到低秩潜在向量
- 大幅降低推理显存占用，同时保持性能
- **面试热点**：MLA 和 GQA 的区别？

### DeepSeekMoE
- 细粒度专家（更多小专家而非少大专家）
- 共享专家 + 路由专家分离
- 辅助无损负载均衡策略

### GRPO (Group Relative Policy Optimization)
- 不需要单独的 Reward Model
- 组内相对排序作为奖励信号
- **面试热点**：GRPO vs PPO 的区别？

## 面试常见问题

- DeepSeek-V2 的 MLA 是如何降低 KV Cache 的？
- GRPO 和 PPO 有什么区别？为什么 DeepSeek 选择 GRPO？
- DeepSeekMoE 的"细粒度专家"和 Mixtral 有什么不同？
- DeepSeek-R1 是如何用纯 RL 训练出推理能力的？

## 相关概念

- [[concepts/architecture/moe|MoE]]
- [[concepts/training/rlhf|RLHF]]
- [[concepts/training/ppo|PPO]]
- [[concepts/architecture/attention-variants|MHA/MQA/GQA]]
