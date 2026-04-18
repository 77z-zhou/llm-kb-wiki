---
type: concept
title: "位置编码 (Positional Encoding)"
aliases: [PE, Sinusoidal PE, Learned PE]
created: 2026-04-17
updated: 2026-04-18
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

### 直觉理解：Self-Attention 只看"你是谁"，不看"你排第几"

Self-Attention 的四步操作（线性投影 → 点积 → Softmax → 加权求和）都是**基于向量内容的两两交互**，没有任何一步利用了"你是第 i 个位置"这个信息。

用一个具体例子说明。假设输入 `[我, 爱, 你]`，Self-Attention 对每个词做的事情是：

```
"我"的输出 = 0.5×"我" + 0.3×"爱" + 0.2×"你"
"爱"的输出 = 0.1×"我" + 0.6×"爱" + 0.3×"你"
"你"的输出 = 0.2×"我" + 0.3×"爱" + 0.5×"你"
```

这些系数（0.5, 0.3, 0.2...）由两个词的内容决定，和它们在第几个位置**毫无关系**。

现在打乱顺序为 `[你, 爱, 我]`，结果只是输出跟着换行：

```
第1个位置的输出 = "你"的输出（跟之前第3个位置一模一样）
第2个位置的输出 = "爱"的输出（跟之前第2个位置一模一样）
第3个位置的输出 = "我"的输出（跟之前第1个位置一模一样）
```

**每个词得到的输出完全没变**，只是在结果矩阵里换了个行。模型对"语序"没有任何感知。

### 严格术语：置换等变（Permutation Equivariant）

严格来说 Self-Attention 是**置换等变**的，不是置换不变的：

- **置换不变**：打乱输入顺序，输出完全不变（如求和、取平均）
- **置换等变**：打乱输入顺序，输出跟着同步打乱，但每个 token 自身的计算结果不变

Self-Attention 属于后者。但两者的共同点是：**模型内部没有任何机制能区分"谁在前谁在后"**。

### 位置编码做了什么？

给每个位置加上不同的"标记"：$x'[i] = x[i] + \text{PE}(i)$。这样同一个词"我"出现在位置 1 和位置 3 时变成不同的向量，模型就能区分语序了。

## 主要实现方式

### 1. 正弦/余弦位置编码 (Sinusoidal PE)

原始 Transformer 论文方法：

$$
\text{PE}(\text{pos}, 2i) = \sin\!\left(\frac{\text{pos}}{10000^{2i/d_{\text{model}}}}\right)
$$

$$
\text{PE}(\text{pos}, 2i+1) = \cos\!\left(\frac{\text{pos}}{10000^{2i/d_{\text{model}}}}\right)
$$

**优点**：可外推到更长序列；$\text{PE}(\text{pos}+k)$ 可表示为 $\text{PE}(\text{pos})$ 的线性函数

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
