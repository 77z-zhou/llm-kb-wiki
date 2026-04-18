---
type: entity
title: "Qwen 系列"
category: model
created: 2026-04-17
updated: 2026-04-17
status: active
tags: [阿里, 开源模型, LLM, VLM]
interview_frequency: medium
related_concepts: [transformer, rope, moe, rlhf]
---

# Qwen 系列

## 基本信息

- **开发者**：阿里云通义千问团队
- **开源协议**：Apache 2.0（大部分版本）
- **定位**：通用大语言模型家族，覆盖从小到大的多种规格

## 关键版本

| 版本 | 参数规模 | 特点 |
|:-----|:---------|:-----|
| Qwen1.5 | 0.5B-72B | 首个广泛使用的开源版本 |
| Qwen2 | 0.5B-72B | GQA、双粒度 RoPE、Tie Embedding |
| Qwen2.5 | 0.5B-72B+ | 强化数学/代码能力，多密度版本 |
| Qwen3 | 多种 | 思考模式切换、MoE与Dense并行 |

## 架构特点

- **RoPE 旋转位置编码**（双粒度频率）
- **GQA (Grouped-Query Attention)**：降低 KV Cache 开销
- **SwiGLU 激活函数**
- **Tie Embedding**：输入输出嵌入共享（部分版本）
- **MoE 变体**：Qwen2.5-MoE 等

## 面试常见问题

- Qwen 和 LLaMA 架构的主要区别？
- Qwen 使用的位置编码方案是什么？为什么选择 RoPE？
- Qwen2 相比 Qwen1.5 有哪些改进？

## 相关概念

- [[concepts/architecture/rope|RoPE]]
- [[concepts/architecture/attention-variants|MHA/MQA/GQA]]
- [[concepts/architecture/moe|MoE]]
- [[concepts/architecture/activation-functions|激活函数]]
