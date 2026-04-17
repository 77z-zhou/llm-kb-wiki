---
type: concept
title: "高级 RAG 范式与知识图谱"
category: application
sources: [extra01-5.8, extra01-5.9, extra01-5.12]
interview_frequency: 中频
interview_difficulty: 中高
related: [rag-overview, retrieval-enhancement, rag-eval]
---

# 高级 RAG 范式与知识图谱

## 知识图谱增强 RAG

**向量数据库 vs 知识图谱**：语义相似度模糊匹配 vs 实体与关系精确查询

### 适用场景

| 场景 | 举例 | 为什么用 KG |
|:-----|:-----|:-----------|
| **多跳推理** | "Llama 2 作者所在公司的CEO是谁？" | 需要沿关系链跳转 |
| **强结构数据** | 金融股权、药物-基因关系 | 最大化利用结构信息 |
| **高可解释性** | 风控、医疗 | 查询路径即证据链 |

### 实际应用：混合增强
1. LLM 分析问题 → 查询知识图谱（结构化事实）
2. 图谱结果构建更精确查询 → 检索向量数据库（非结构化文本）
3. 两方面信息汇总 → LLM 生成答案

## 高级 RAG 范式

### 1. 迭代式检索 (Self-RAG / Corrective-RAG)
- 首次检索+生成 → LLM 反思评估 → 信息不足则二次检索 → 整合精炼
- **核心**：将 RAG 从单向流水线变为**循环自我修正**

### 2. 自适应检索 (FLARE / Self-Ask)
- LLM 一边生成一边预测不确定性 → 不确定时暂停 → 主动提问+检索 → 继续
- **核心**：按需检索（just-in-time），避免预先检索无关信息

### 3. 多源数据 RAG
- Agent 判断问题需要哪些信息源 → 向量DB/知识图谱/SQL/搜索引擎 → 综合生成
- **核心**：Agent 驱动的 RAG

## RAG 开源框架选择

| 需求 | 推荐 |
|:-----|:-----|
| 高度定制化、灵活控制 | LangChain / LlamaIndex |
| 快速原型、开箱即用 | RAGFlow / Dify |

**最佳实践**：先用 RAGFlow 搭建基线 → 验证后用 LlamaIndex 精细化重构

## 补充见解

- **GraphRAG (微软)** 是知识图谱+RAG 的代表性工作：通过 LLM 自动构建社区图谱，支持全局性摘要查询
- **自适应检索代表了 RAG 的进化方向**：从"被动检索"到"主动按需获取"
- **多源 RAG 本质上是 Agent + RAG 的融合**，是当前工程实践的前沿
