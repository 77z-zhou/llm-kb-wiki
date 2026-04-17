---
type: concept
title: "Agent 记忆系统"
category: application
sources: [extra01-4.4]
interview_frequency: 中频
interview_difficulty: 中等
related: [agent-overview, rag-overview]
---

# Agent 记忆系统

记忆模块是 Agent 打破 LLM 上下文窗口限制、实现持续学习和个性化的关键。

## 短期记忆

**作用**：存储当前任务的上下文（对话历史、中间步骤、工具返回结果）

| 实现方式 | 说明 |
|:---------|:-----|
| LLM 上下文窗口 | 最直接的载体，所有最近交互放入 Prompt |
| ConversationBufferMemory | 存储完整对话历史 |
| ConversationBufferWindowMemory | 只保留最近 K 轮对话 |
| ConversationSummaryBufferMemory | 历史过长时用 LLM 动态总结 |
| Scratchpad（暂存器） | 记录 ReAct 的 Thought-Action-Observation 轨迹 |

## 长期记忆

**作用**：存储跨任务/时间维度的信息（用户偏好、经验、领域知识）

核心是 **RAG 范式**：存储 → 检索 → 使用

| 环节 | 技术 | 工具 |
|:-----|:-----|:-----|
| 存储 | 嵌入模型将文本 → 向量，存入向量数据库 | Pinecone, ChromaDB, FAISS |
| 检索 | 当前问题 → 查询向量 → 相似度搜索 | 余弦相似度/ANN |
| 使用 | 检索到的记忆插入 Prompt 作为额外上下文 | |

**其他长期记忆技术**：
- 传统 SQL 数据库：结构化数据精确查询
- 知识图谱（Neo4j）：实体关系推理

## 补充见解

- **记忆管理是 Agent 工程的核心难点之一**：什么时候写入记忆、写入什么、如何去重、如何遗忘过时信息——这些问题没有标准答案
- **MemGPT 论文**提出了虚拟内存管理的思路：将 LLM 上下文类比为 RAM，外部存储类比为磁盘，由 LLM 自主决定何时"换页"
- **短期记忆的 Token 消耗是成本大头**：长对话场景下，仅 Scratchpad 就可能消耗大量 Token
