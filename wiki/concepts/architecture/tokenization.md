---
type: concept
title: "词元化 (Tokenization): BPE vs WordPiece"
aliases: [Tokenization, BPE, WordPiece, 子词切分]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [transformer]
tags: [tokenization, 预处理]
status: active
confidence: high
interview_frequency: medium
interview_difficulty: medium
---

# 词元化 (Tokenization)

词元化是将文本分解为词元并映射到整数 ID 的过程，是模型处理文本的第一步。

## 为什么用子词 (Subword)？

1. **处理未登录词 (OOV)**：罕见词可拆为已知子词组合
2. **平衡词表大小与序列长度**：比词级词表小，比字符级序列短
3. **保留形态信息**：running/runner 共享 "run"

## BPE vs WordPiece

| 特性 | BPE | WordPiece |
|------|-----|-----------|
| **合并标准** | **频率驱动**：合并出现最多的相邻子词对 | **似然驱动**：合并能最大化语料库似然的子词对 |
| **理论基础** | 数据压缩算法 | 概率语言模型 |
| **代表模型** | GPT, Llama, RoBERTa | BERT, T5 |
| **子词标记** | 无特殊标记 | 非起始部分加 `##` |

### BPE 流程

1. 初始化词表为所有基本字符
2. 统计所有相邻词元对频率
3. 合并频率最高的对为新词元
4. 重复直到达到目标词表大小

### WordPiece 流程

1. 初始化词表为所有基本字符
2. 尝试所有可能合并
3. 选择能**最大提升训练数据似然**的合并
4. 重复直到达到目标词表大小

## 补充见解

1. **Byte-level BPE**：GPT-2 引入的改进，先将文本转为 UTF-8 字节序列再做 BPE，词表基础单元是 256 个字节而非 Unicode 字符，完全消除 OOV 问题。现在几乎所有主流 LLM 都用此方案。

2. **SentencePiece**：Google 的统一分词框架，支持 BPE 和 Unigram 两种算法，直接在原始文本上操作无需预分词，Llama 系列使用它。

3. **Tokenizer 对模型性能的影响常被低估**：词表大小、分词粒度直接影响模型的序列长度效率和多语言能力。中文分词的颗粒度差异尤其明显。

---

*来源：[[sources/extra01-llm-interview-reference]]*
