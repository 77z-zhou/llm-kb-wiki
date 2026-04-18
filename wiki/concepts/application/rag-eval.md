---
type: concept
title: "RAG 评估"
category: application
sources: [extra01-5.7]
interview_frequency: 中频
interview_difficulty: 中等
related: [rag-overview, retrieval-enhancement]
---

# RAG 评估

## 两大评估阶段

### 检索性能评估 — "找得对、找得全"

| 指标 | 衡量内容 |
|:-----|:---------|
| **Context Precision** | 检索结果中有多少是真正相关的（信噪比） |
| **Context Recall** | 所有相关文档中找回了多少（全面性） |
| **Hit Rate** | 是否至少包含一个相关文档 |
| **MRR** | 第一个相关文档的排名倒数 |
| **nDCG@k** | 综合考虑相关性和排名 |

### 生成性能评估 — "忠实、准确、有用"

| 指标 | 衡量内容 |
|:-----|:---------|
| **Faithfulness（忠实度）** | 答案是否基于提供的上下文？有无幻觉？ |
| **Answer Relevancy（相关性）** | 答案是否直接回答了用户问题？ |
| **Answer Correctness（正确性）** | 答案信息是否事实准确？ |

## 自动化评估框架

- **RAGAS**：使用 LLM-as-a-Judge 自动计算 Faithfulness, Relevancy 等指标
- **ARES**：自动化 RAG 评估系统
- **TruLens**：开源评估和追踪框架

## 补充见解

- **检索评估和生成评估要分开做**：答案不好可能是检索问题，也可能是生成问题
- **RAGAS 是目前最流行的 RAG 评估框架**，建议重点了解
- **评估数据集的质量决定评估结果的可信度**：需要覆盖多种问题类型和难度
