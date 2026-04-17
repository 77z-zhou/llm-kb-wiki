---
type: concept
title: "RLHF 从人类反馈中进行强化学习"
aliases: [Reinforcement Learning from Human Feedback, 人类反馈强化学习]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [reward-model, ppo, scaling-laws]
tags: [RLHF, 对齐, 强化学习]
status: active
confidence: high
interview_frequency: high
interview_difficulty: hard
---

# RLHF 从人类反馈中进行强化学习

## 为什么需要 RLHF？SFT 不够吗？

SFT 教会模型"模仿"，但无法教会模型"判断"。RLHF 解决更深层的**对齐 (Alignment)** 问题：

**HHH 原则**：
- **Helpful** (有用)：准确、相关、信息丰富
- **Honest** (诚实)：不捏造事实，不确定时主动承认
- **Harmless** (无害)：无偏见、无歧视、无暴力内容

### SFT 的不足

1. **目标定义模糊**：HHH 概念主观、依赖上下文，难以用固定数据集定义
2. **偏好难标注**：SFT 的 (prompt, response) 格式无法表达"A比B好"的细粒度偏好
3. **行为空间巨大**：SFT 数据只覆盖极小部分，模型学到表面统计特征而非原则
4. **暴露偏差**：训练基于真实上下文，推理基于自己生成的上下文，误差累积

## 经典 RLHF 三阶段

### 阶段一：监督微调 (SFT)

- **输入**：高质量 (指令, 回答) 数据集
- **输出**：SFT 模型
- **目标**：让预训练 LLM 初步具备指令遵循能力，提供良好的初始策略

### 阶段二：训练奖励模型 (RM)

- **输入**：人类偏好比较数据 (prompt, 胜出回答 y_w, 落败回答 y_l)
  - SFT 模型对同一 prompt 生成多个回答 → 人工排序
- **输出**：奖励模型（输入任何 prompt+response，输出标量奖励分数）
- **目标**：学习模拟人类偏好的函数

### 阶段三：PPO 优化

- **输入**：SFT 模型 + RM + 新指令数据集
- **输出**：对齐后的最终 LLM
- **目标**：通过 RL 微调，让模型生成高奖励且不偏离 SFT 的回答

## 补充见解

1. **RLHF 的工程复杂性**：RLHF 需要同时管理 4 个模型（SFT 参考模型、策略模型、奖励模型、价值模型），对显存和基础设施要求很高。这也是 DPO 等替代方案出现的动机。

2. **DPO 的崛起**：DPO (Direct Preference Optimization) 跳过了 RM 训练和 PPO，直接从偏好数据优化策略。它将 RLHF 简化为一个分类损失，大大降低了实现难度。Llama 3、Qwen 等模型都用了 DPO 或其变体。

3. **GRPO (DeepSeek)**：DeepSeek 提出的 Group Relative Policy Optimization，通过组内相对奖励来优化，避免了训练单独的价值模型。这是 RLHF 领域的重要创新。

---

*来源：[[sources/extra01-llm-interview-reference]]*
