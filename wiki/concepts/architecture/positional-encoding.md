---
type: concept
title: "位置编码 (Positional Encoding)"
aliases: [PE, Sinusoidal PE, Learned PE]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [transformer, rope]
tags: [位置编码, transformer]
status: active
confidence: high
interview_frequency: high
interview_difficulty: medium
---

# 位置编码 (Positional Encoding)

## 为什么必须要位置编码？

Transformer 的自注意力是**置换不变的（Permutation-invariant）**——打乱输入顺序，每个词元自身的输出不变。但语言的语序至关重要（"我打你" ≠ "你打我"），因此必须显式注入位置信息。

## 主要实现方式

### 1. 正弦/余弦位置编码 (Sinusoidal PE)

原始 Transformer 论文方法：
- `PE(pos, 2i) = sin(pos / 10000^(2i/d_model))`
- `PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))`

**优点**：可外推到更长序列；PE(pos+k) 可表示为 PE(pos) 的线性函数

### 2. 可学习绝对位置编码 (Learned Absolute PE)

位置编码作为可训练参数，`(max_len, d_model)` 嵌入矩阵。

- **代表模型**：BERT, GPT-2
- **优点**：灵活自适应
- **缺点**：无法泛化到超出 max_len 的长度

### 3. RoPE（旋转位置编码）

当前主流方案，详见 [[rope]]

## 补充见解

1. **发展脉络**：Sinusoidal → Learned Absolute → Relative PE → RoPE → ALiBi。反映了从"绝对位置"到"相对位置"的认知转变，以及对长序列泛化的持续追求。

2. **面试追问点**："为什么不用可学习编码？"——核心在于**外推能力**，部署时经常需处理比训练更长的序列。

---

*来源：[[sources/extra01-llm-interview-reference]]*
