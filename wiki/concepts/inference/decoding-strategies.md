---
type: concept
title: "解码策略: Greedy, Beam Search, Top-K, Top-P"
aliases: [Greedy Search, Beam Search, Top-K Sampling, Nucleus Sampling, Top-P]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [transformer]
tags: [解码, 推理, 采样]
status: active
confidence: high
interview_frequency: medium
interview_difficulty: medium
---

# 解码策略

推理阶段如何从词元概率分布中选择下一个词元。

## 确定性策略

### Greedy Search
- 每步选概率最高的词元
- **优点**：速度最快
- **缺点**：局部最优、缺乏多样性、输出确定性

### Beam Search
- 保留 K 个最优候选序列，最终选累计概率最高的
- **优点**：质量优于贪心
- **缺点**：计算 K 倍、仍偏保守、长文本易重复

## 随机策略

### Top-K Sampling
- 从概率最高的 K 个词元中按概率采样
- **优点**：增加多样性、过滤低概率词
- **缺点**：K 固定，不适应不同分布形状

### Top-P / Nucleus Sampling (当前主流)
- 从累积概率达到 P 的最小词元集中采样
- **优点**：候选集大小自适应，分布尖锐时集合小（精确），平坦时集合大（探索）
- **缺点**：P 值仍需调优

## 补充见解

1. **temperature 的作用**：通常与 Top-P/Top-K 配合使用。T<1 使分布更尖锐（更确定），T>1 使分布更平坦（更随机）。面试中要能解释 temperature 和 Top-P 的协同效果。

2. **实际应用中的组合**：大多数 LLM API 同时支持 temperature + Top-P + Top-K，三者叠加使用。理解它们各自的作用和交互非常重要。

3. **Beam Search 在 LLM 中的衰退**：Beam Search 在翻译等 Seq2Seq 任务中仍广泛使用，但在开放式生成中几乎被采样策略取代，因为它倾向于生成"安全但无聊"的文本。

---

*来源：[[sources/extra01-llm-interview-reference]]*
