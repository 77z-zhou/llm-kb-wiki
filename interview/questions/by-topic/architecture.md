---
type: interview-question-set
title: "架构类面试题"
created: 2026-04-17
updated: 2026-04-17
topic: architecture
source: extra01-llm-interview-reference
question_count: 10
---

# 架构类面试题

## 🔥 高频题

### Q1: 详细解释 Transformer 自注意力机制的工作原理，为什么比 RNN 更适合处理长序列？
- **难度**: Medium
- **概念页**: [[concepts/architecture/transformer]]
- **要点**: Q/K/V 生成 → 点积 → 缩放 → Softmax → 加权求和；并行性 $O(1)$ vs $O(N)$ 长距离依赖

### Q2: 什么是位置编码？为什么必须？列举至少两种实现方式。
- **难度**: Medium
- **概念页**: [[concepts/architecture/positional-encoding]]
- **要点**: 置换不变性；Sinusoidal PE / Learned PE / RoPE

### Q3: 详细介绍 RoPE，对比绝对位置编码的优劣。
- **难度**: Hard
- **概念页**: [[concepts/architecture/rope]]
- **要点**: 向量旋转编码位置 → 注意力分数只依赖相对位置；外推能力、无参数、远距离衰减

### Q4: MHA、MQA、GQA 的区别？
- **难度**: Medium
- **概念页**: [[concepts/architecture/attention-variants]]
- **要点**: K/V 头共享方式不同；MHA N:N:N → MQA N:1:1 → GQA N:G:G；核心动机是 KV Cache

### Q5: 比较 Encoder-Only, Decoder-Only, Encoder-Decoder 架构。
- **难度**: Medium
- **概念页**: [[concepts/architecture/llm-architectures]]
- **要点**: 双向 vs 因果 vs 混合注意力；NLU vs NLG vs Seq2Seq；为什么 Decoder-Only 成为主流

### Q6: MoE 如何在不增加推理成本情况下扩大参数规模？
- **难度**: Hard
- **概念页**: [[concepts/architecture/moe]]
- **要点**: 稀疏激活 + Top-K 路由；总参数量 vs 推理 FLOPs 解耦；Mixtral 8x7B 的例子

## 🟡 中频题

### Q7: 词元化是什么？比较 BPE 和 WordPiece。
- **难度**: Medium
- **概念页**: [[concepts/architecture/tokenization]]
- **要点**: 频率驱动 vs 似然驱动；子词切分解决 OOV

### Q8: NLP 和 LLM 最大的区别是什么？
- **难度**: Easy
- **要点**: 从"每个任务一个模型"到"一个模型所有任务"；涌现能力；ICL/zero-shot

### Q9: 涌现能力如何理解？通常在什么规模出现？
- **难度**: Medium
- **概念页**: [[concepts/architecture/emergent-abilities]]
- **要点**: 非线性相变；CoT/ICL/复杂指令；62B+开始；存在争议

### Q10: LLM 常用的激活函数？为什么选用？
- **难度**: Medium
- **概念页**: [[concepts/architecture/activation-functions]]
- **要点**: GeLU → SwiGLU；门控机制增强表达力
