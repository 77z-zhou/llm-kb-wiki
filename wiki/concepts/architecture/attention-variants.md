---
type: concept
title: "MHA / MQA / GQA 注意力机制变体"
aliases: [Multi-Head Attention, Multi-Query Attention, Grouped-Query Attention]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [transformer, rope]
tags: [attention, KV-Cache, 推理优化]
status: active
confidence: high
interview_frequency: high
interview_difficulty: medium
---

# MHA / MQA / GQA 注意力机制变体

三种方案的核心区别在于 **K/V 头的共享方式**，目标是在模型效果和推理效率（KV Cache 显存）之间做权衡。

## 对比总结

| 特性           | MHA              | MQA              | GQA              |
| ------------ | ---------------- | ---------------- | ---------------- |
| **结构**       | N个Q头, N个K头, N个V头 | N个Q头, 1个K头, 1个V头 | N个Q头, G个K头, G个V头 |
| **模型质量**     | 最高               | 可能下降             | 接近MHA，优于MQA      |
| **推理效率**     | 最低（KV Cache大）    | 最高（KV Cache小）    | 居中，远好于MHA        |
| **KV Cache** | $\propto N$              | $\propto 1$（减小N倍）        | $\propto G$              |
| **代表模型**     | BERT, GPT-3      | PaLM             | Llama 2, Mixtral |

## MHA (Multi-Head Attention)

- N 组独立的 Q, K, V 头并行计算注意力
- 多头输出拼接后线性变换回原维度
- **优点**：效果最强，每头学习不同子空间
- **缺点**：KV Cache 与头数 N 成正比，推理显存大

## MQA (Multi-Query Attention)

- N 个 Q 头共享**同一个** K 头和 V 头
- **优点**：KV Cache 缩小 N 倍
- **缺点**：表达力受限，所有 Q 被迫从同一 K/V 提取信息

## GQA (Grouped-Query Attention)

- N 个 Q 头分成 G 组，每组共享一个 K/V 头
- G=N 等价于 MHA；G=1 等价于 MQA
- **最佳平衡点**：灵活调节效率与效果

## 补充见解

1. **核心动机是 KV Cache**：面试中要强调，这三个变体的演化核心不是训练效率，而是**推理时的 KV Cache 显存瓶颈**。长序列 + 大批量推理时，KV Cache 往往比模型参数本身还占显存。

2. **GQA 已成事实标准**：Llama 2/3、Qwen、Mistral 等主流开源模型都采用 GQA，因为它在几乎不损失质量的前提下大幅降低推理成本。

3. **面试延伸**：可以主动提到 MQA→GQA 的转换技巧（uptraining），即从已训练好的 MHA 模型通过少量继续训练转为 GQA，Llama 2 论文中有详细说明。

---

*来源：[[sources/extra01-llm-interview-reference]]*
