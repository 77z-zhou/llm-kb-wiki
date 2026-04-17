---
type: comparison
title: "MHA vs MQA vs GQA"
created: 2026-04-17
updated: 2026-04-17
status: active
interview_frequency: high
---

# MHA vs MQA vs GQA 对比

| 特性 | MHA | MQA | GQA |
|:-----|:----|:----|:----|
| **结构** | N个Q头, N个K头, N个V头 | N个Q头, 1个K头, 1个V头 | N个Q头, G个K头, G个V头 |
| **模型质量** | 最高 | 可能下降 | 接近MHA，优于MQA |
| **推理效率** | 最低(KV Cache大) | 最高(KV Cache小) | 居中 |
| **代表模型** | BERT, GPT-3 | PaLM | Llama 2, Qwen, Mixtral |

## 关键关系

- GQA 是 MHA 和 MQA 的折中
- 当 G=N 时，GQA 等价于 MHA
- 当 G=1 时，GQA 等价于 MQA
- **GQA 已成为事实标准**：Llama 2 之后的模型几乎都用 GQA

## 面试要点

- 核心动机是降低 KV Cache 显存占用
- 为什么不直接用 MQA？→ 性能损失过大
- GQA 的 uptraining 技巧：从 MHA 模型转换为 GQA

## 相关概念

- [[concepts/architecture/attention-variants|MHA/MQA/GQA 概念页]]
