---
type: map
title: "应用与系统知识地图"
created: 2026-04-17
updated: 2026-04-17
status: active
---

# 应用与系统知识地图

## Agent 学习路径

```
Agent 基础
├── 核心组件: 大脑/规划/记忆/工具
├── 行为框架
│   └── ReAct (Thought-Action-Observation)
├── 规划方法
│   ├── CoT (线性)
│   ├── ToT (树形搜索)
│   └── GoT (图形)
├── 记忆系统
│   ├── 短期: 上下文窗口 / Buffer / Scratchpad
│   └── 长期: 向量数据库 / RAG
├── 工具使用
│   └── Function Calling
├── 多智能体
│   └── A2A 协议
└── 安全与对齐
    └── 六层保障体系
```

## RAG 学习路径

```
RAG 基础
├── 核心流程: 检索 → 增强 → 生成
├── 数据准备
│   ├── 文本切块策略
│   └── 嵌入模型选择
├── 检索优化
│   ├── 混合搜索 (BM25 + 向量)
│   ├── 重排序 (Cross-Encoder)
│   └── Query 改写 (Multi-Query / HyDE)
├── 高级范式
│   ├── 迭代式 (Self-RAG)
│   ├── 自适应 (FLARE)
│   └── 知识图谱增强 (GraphRAG)
├── 评估
│   └── RAGAS 框架
└── 部署挑战
```

## 按面试频率排序

### 🔥 必须掌握
1. [[concepts/application/agent-overview|Agent 概述]]
2. [[concepts/application/react|ReAct]]
3. [[concepts/application/rag-overview|RAG 概述]]
4. [[concepts/application/rag-pipeline|RAG 流水线]]
5. [[concepts/application/retrieval-enhancement|检索增强]]
6. [[concepts/application/tool-use|Function Calling]]

### 🟡 建议了解
7. [[concepts/application/planning-methods|规划方法]]
8. [[concepts/application/rag-eval|RAG 评估]]
9. [[concepts/application/advanced-rag|高级 RAG]]
10. [[concepts/application/agent-safety|Agent 安全]]

## 面试题

- [[interview/questions/by-topic/agent|Agent 面试题 (13题)]]
- [[interview/questions/by-topic/rag|RAG 面试题 (12题)]]
