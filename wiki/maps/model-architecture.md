---
type: map
title: "模型架构知识地图"
created: 2026-04-17
updated: 2026-04-17
status: active
---

# 模型架构知识地图

## 学习路径

```
Transformer 基础
├── 自注意力机制
│   ├── MHA / MQA / GQA 演进
│   └── FlashAttention 优化
├── 位置编码
│   ├── 正弦/余弦编码
│   ├── 可学习绝对编码
│   └── RoPE (旋转位置编码) ← 当前主流
├── FFN 层
│   ├── 激活函数: GeLU → SwiGLU
│   └── MoE: 稠密FFN → 稀疏专家
└── 整体架构
    ├── Encoder-Only (BERT)
    ├── Decoder-Only (GPT/Qwen/LLaMA) ← 当前主流
    └── Encoder-Decoder (T5)
```

## 按面试频率排序

### 🔥 必须掌握
1. [[concepts/architecture/transformer|Transformer 自注意力]]
2. [[concepts/architecture/rope|RoPE]]
3. [[concepts/architecture/attention-variants|MHA/MQA/GQA]]
4. [[concepts/architecture/llm-architectures|三大架构对比]]
5. [[concepts/architecture/moe|MoE]]

### 🟡 建议了解
6. [[concepts/architecture/positional-encoding|位置编码]]
7. [[concepts/architecture/activation-functions|激活函数]]
8. [[concepts/architecture/emergent-abilities|涌现能力]]
9. [[concepts/architecture/tokenization|词元化]]

## 对比分析

- [[comparisons/mha-vs-mqa-vs-gqa|MHA vs MQA vs GQA]]
- [[comparisons/moe-vs-dense|MoE vs Dense]]

## 实体模型

- [[entities/qwen|Qwen]]
- [[entities/deepseek|DeepSeek]]

## 面试题

- [[interview/questions/by-topic/architecture|架构类面试题 (10题)]]
