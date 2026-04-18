---
type: concept
title: "激活函数: GeLU 与 SwiGLU"
aliases: [GeLU, SwiGLU, Swish, GLU]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [transformer]
tags: [激活函数, 架构]
status: active
confidence: high
interview_frequency: medium
interview_difficulty: medium
---

# 激活函数: GeLU 与 SwiGLU

激活函数为网络引入**非线性**，没有它多层网络等价于单层线性模型。

## GeLU (Gaussian Error Linear Unit)

- $\text{GeLU}(x) = x \cdot \Phi(x)$，$\Phi(x)$ 是高斯 CDF
- 是 ReLU 的平滑近似，梯度更稳定
- **代表模型**：BERT, GPT-2
- **思想**：根据输入大小确定性地"保留或归零"

## SwiGLU (当前主流)

- 属于门控线性单元（GLU）家族
- $\text{SwiGLU}(A, B) = \text{Swish}(A) \otimes B$，其中 $\text{Swish}(x) = x \cdot \sigma(x)$
- FFN 输入分为两部分：一部分经 Swish 激活，另一部分作为"门"
- **代表模型**：Llama, PaLM, Mixtral, Gemma, Qwen

### 为什么 SwiGLU 更好？

1. **门控机制**：B 部分动态控制信息流通，增强表达力
2. **实证优越**：PaLM 实验证明替换 GeLU 后困惑度显著降低
3. **代价**：FFN 参数量增加（两个矩阵而非一个），但性能增益值得

## 补充见解

1. **面试常见追问**："SwiGLU 为什么比 GeLU 好？"——核心答案是**门控机制**，它让 FFN 能选择性地过滤信息，类似于 LSTM 的门控思想在 FFN 中的应用。

2. **参数量的变化**：标准 FFN 是 $\text{hidden} \to 4h \to \text{hidden}$，SwiGLU 通常是 $\text{hidden} \to \frac{8}{3}h \times 2 \to \text{hidden}$（两个矩阵各 $\frac{8}{3}h$），总参数量相当但结构不同。

---

*来源：[[sources/extra01-llm-interview-reference]]*
