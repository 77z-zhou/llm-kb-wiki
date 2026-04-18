---
type: interview-questions
title: "基础面试题 (Easy)"
difficulty: basic
created: 2026-04-17
updated: 2026-04-17
total: 3
---

# 基础面试题 (Easy)

> 面试热身题，考察基本概念理解。答不对会严重扣分。

---

## 架构类

### Q1: NLP 和 LLM 最大的区别是什么？
- **来源**: [architecture](by-topic/architecture.md) Q8
- **概念页**: [[concepts/architecture/emergent-abilities]]
- **要点**: 从"每个任务一个模型"到"一个模型所有任务"；涌现能力；ICL/zero-shot
- **一句话答案**: NLP 是任务专精范式，LLM 是通用基座范式，核心区别在于涌现能力带来的 zero-shot/ICL 能力。

## 训练类

### Q2: L1 和 L2 正则化分别是什么？适用场景？
- **来源**: [training](by-topic/training.md) Q3
- **概念页**: [[concepts/training/regularization]]
- **要点**: L1 稀疏化做特征选择；L2 平滑化防过拟合(Weight Decay)
- **一句话答案**: L1 产生稀疏解适合特征选择，L2 (Weight Decay) 限制参数幅度防止过拟合。

## RAG 类

### Q3: 搜索系统和 RAG 有什么区别？(5.11)
- **来源**: [rag](by-topic/rag.md) Q6
- **概念页**: [[concepts/application/rag-overview]]
- **要点**: 找文档 vs 给答案、文档列表 vs 自然语言答案、搜索系统是 RAG 的子集
- **一句话答案**: 搜索返回文档列表，RAG 基于检索结果生成自然语言答案，搜索是 RAG 的检索子系统。

---

## 答题技巧

- 基础题虽简单，但要简洁准确，不要啰嗦
- 可以用一句话概括 + 一句展开的结构
- 答错基础题会让面试官质疑基础功底，务必稳拿
