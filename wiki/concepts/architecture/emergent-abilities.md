---
type: concept
title: "涌现能力 (Emergent Abilities)"
aliases: [Emergence, 涌现现象]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [scaling-laws]
tags: [涌现, scaling]
status: active
confidence: medium
interview_frequency: medium
interview_difficulty: medium
---

# 涌现能力 (Emergent Abilities)

## 定义

在小模型中不存在，但当模型规模达到某个临界点后**突然出现**并显著超越随机水平的能力。

核心特征：**非线性**和**不可预测性**——性能不是平滑提升，而是"相变"式跃迁。

## 典型涌现能力

1. **思维链 (Chain-of-Thought, CoT)**：提示"一步一步思考"后进行多步推理
2. **上下文学习 (In-context Learning)**：仅通过 Prompt 中的几个示例就能执行新任务
3. **复杂指令遵循**：理解多步骤、多约束、带否定逻辑的指令

## 出现的规模

没有固定数值，取决于能力、架构、数据、任务复杂性。

- 思维链推理通常在 **62B+** 开始显现（PaLM 实验）
- 在 8B/16B 模型上完全无效
- 540B 时变得更强更稳定

## 补充见解

1. **争议**：涌现能力是否"真实存在"仍有争议。有研究（如 Stanford 的论文）认为所谓"涌现"可能只是评估指标选择的假象——用连续指标替代离散指标后，性能提升往往是平滑的。面试中提到这个争议是很好的加分项。

2. **实际意义**：无论涌现是否是"真实的"，Scaling Laws 证明的"更大=更好"趋势是实在的。关键是要区分"能力的涌现"和"评估指标的跳变"。

---

*来源：[[sources/extra01-llm-interview-reference]]*
