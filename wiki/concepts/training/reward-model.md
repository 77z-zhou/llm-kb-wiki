---
type: concept
title: "奖励模型 (Reward Model)"
aliases: [RM, 偏好模型]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [rlhf, ppo]
tags: [RM, RLHF, 对齐]
status: active
confidence: high
interview_frequency: high
interview_difficulty: hard
---

# 奖励模型 (Reward Model)

## 架构设计

- 通常与目标 LLM **相同架构**，初始化自 SFT 模型
- 最后的 softmax 层替换为**回归头**（线性层 → 标量分数）
- 是最终 LLM 的**人类偏好代理函数**

## 为什么用成对比较而非绝对评分？

### 优势
1. **认知负荷低**：判断"哪个更好"比打精确分数容易
2. **标注一致性高**：不同标注者对相对好坏更易达成共识
3. **信号更精细**：能捕捉两个都不错的回答间的微妙差异
4. **自然归一化**：对标注者个人打分尺度不敏感

### 劣势
1. **数据效率可能较低**：每次比较只产生 1 bit 信息
2. **不传递性**：可能出现 A>B, B>C, 但 C>A 的循环偏好
3. **信息不完整**：只知道好坏，不知道差距大小

## 损失函数：Bradley-Terry 模型

假设回答 $y_w$ 优于 $y_l$ 的概率：

$$
P(y_w > y_l \mid x) = \sigma\!\left(r(y_w \mid x) - r(y_l \mid x)\right)
$$

损失函数（负对数似然）：

$$
\mathcal{L} = -\log\,\sigma\!\left(r(y_w \mid x) - r(y_l \mid x)\right)
$$

直觉：奖励分数差距越大，我们越确信一个比另一个好。

## 补充见解

1. **RM 的质量是 RLHF 的天花板**：如果 RM 有偏见或漏洞，LLM 会在 PPO 阶段"奖励作弊"（reward hacking），生成高分但低质的文本。RM 的质量决定对齐效果上限。

2. **Process RM vs Outcome RM**：Outcome RM 只给最终回答打分，Process RM 对推理的每一步打分。Process RM 在数学推理等场景更有效（OpenAI 的 "Let's Verify Step by Step" 论文）。

3. **RM 的规模选择**：业界实践中 RM 通常比策略模型小（如策略 70B，RM 7B-13B），因为 RM 只需要打分不需要生成。

---

*来源：[[sources/extra01-llm-interview-reference]]*
