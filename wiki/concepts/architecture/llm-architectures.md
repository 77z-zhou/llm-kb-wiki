---
type: concept
title: "LLM 架构对比: Encoder-Only vs Decoder-Only vs Encoder-Decoder"
aliases: [Encoder-Only, Decoder-Only, Encoder-Decoder, Causal LM]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [transformer]
tags: [架构, LLM]
status: active
confidence: high
interview_frequency: high
interview_difficulty: medium
---

# LLM 架构对比

## 三种架构

### 1. Encoder-Only (BERT, RoBERTa)
- **注意力**：双向自注意力，每个词同时看到左右所有词
- **擅长**：自然语言理解 (NLU) — 分类、NER、NLI、完形填空
- **原因**：双向上下文对准确理解至关重要

### 2. Decoder-Only (GPT系列, Llama, Qwen)
- **注意力**：单向因果自注意力 (Causal)，只能看到左侧
- **擅长**：自然语言生成 (NLG) — 文本生成、对话、代码生成、ICL
- **原因**：单向注意力完美模拟语言从左到右的生成过程
- **地位**：当前绝大多数通用 LLM 都采用此架构

### 3. Encoder-Decoder (T5, BART)
- **注意力**：Encoder 双向 + Decoder 单向 + 交叉注意力
- **擅长**：Seq2Seq — 翻译、摘要、问答
- **原因**：先全局理解输入，再有条件地生成输出

## 补充见解

1. **为什么 Decoder-Only 一统天下？** 因为在足够大的规模下，Decoder-Only 模型通过 ICL 和 instruction following 也能很好地完成理解任务。统一的架构意味着统一的 scaling、统一的基础设施，工程成本大幅降低。

2. **Encoder-Only 并未消亡**：在实际生产中，BERT 类模型在文本分类、信息检索 embedding 等特定场景仍然是性价比最高的选择，因为它们小、快、精准。

3. **面试技巧**：被问到这个问题时，不要只列举三种架构的区别，更重要的是能解释**为什么业界最终收敛到了 Decoder-Only**。

---

*来源：[[sources/extra01-llm-interview-reference]]*
