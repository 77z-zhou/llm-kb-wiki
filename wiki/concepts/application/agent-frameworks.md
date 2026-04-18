---
type: concept
title: "Agent 框架选型与微调"
category: application
sources: [extra01-4.6, extra01-4.12, extra01-4.13]
interview_frequency: 中频
interview_difficulty: 中等
related: [agent-overview, tool-use, rag-overview]
---

# Agent 框架选型与微调

## LangChain vs LlamaIndex

| 维度 | LangChain | LlamaIndex |
|:-----|:----------|:-----------|
| **核心定位** | 通用 LLM 应用编排框架 | 专注外部数据的数据框架 |
| **最擅长** | 复杂多步骤 Agent | 高性能 RAG 系统 |
| **核心抽象** | Chains, Agents, Memory | Data Connectors, Indexes, Retrievers |
| **选型建议** | 逻辑编排驱动 → 选 LangChain | 数据驱动 → 选 LlamaIndex |

**实际开发中常结合使用**：LlamaIndex 构建知识库检索工具 → 接入 LangChain Agent

## Agent 评估指标

1. **任务成功率**：能否完整完成最终任务
2. **过程效率**：Token 消耗、延迟、步骤数
3. **鲁棒性**：错误处理能力、输出一致性、安全评估

## Agent 微调

微调 Agent 的核心是**教会模型如何更好地"思考"和"使用工具"**——本质是行为克隆。

**数据集收集方法**：
1. **教师模型合成**（主流）：用 GPT-4o 在 ReAct 框架下执行任务 → 记录完整轨迹 → 过滤清洗
2. **人工编写/修正轨迹**
3. **从真实用户交互中收集**

## 补充见解

- **框架选型的真正考量是生态和社区**：LangChain 的工具集成最丰富，LlamaIndex 的数据处理最专业
- **微调 Agent 不如微调底层能力**：更好的做法是微调 LLM 的工具调用格式和推理能力，而非特定的任务轨迹
- **Agent 框架正在从"代码库"向"平台"演进**：如 RAGFlow、Dify 等，降低非专家的使用门槛
