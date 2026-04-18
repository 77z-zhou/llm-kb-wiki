---
type: concept
title: "ReAct 框架"
category: application
sources: [extra01-4.2]
interview_frequency: 高频
interview_difficulty: 中等
related: [agent-overview, planning-methods, tool-use]
---

# ReAct 框架

## 核心思想

ReAct (Reason and Act) 让 LLM 协同生成**推理轨迹**和**任务相关行动**，模仿人类 "思考→行动→观察→再思考" 的循环模式。

## 工作流程（三步循环）

```
Thought: 我需要查找今天新加坡的天气，应该使用搜索工具
Action:  [Search, "weather in Singapore today"]
Observation: "Today in Singapore, sunny, high of 32°C"
Thought: 已获得信息，可以回答用户了
Action:  [Finish, "今天新加坡晴天，最高温32°C"]
```

1. **Thought（思考）**：分析当前状态，制定策略/规划下一步
2. **Action（行动）**：生成结构化的工具调用指令 `[Tool_Name, Tool_Input]`
3. **Observation（观察）**：外部执行器调用工具，返回结果作为新上下文

## ReAct vs 纯 CoT

| 特性 | 纯 CoT | ReAct |
|:-----|:-------|:------|
| 推理方式 | 一次性生成全部推理步骤 | 每步基于最新观察动态推理 |
| 信息来源 | 仅依赖模型内部知识 | 可通过工具获取外部信息 |
| 错误修正 | 无法中途修正 | 可根据反馈调整策略 |
| 适用场景 | 纯推理/数学题 | 需要外部信息的复杂任务 |

## 补充见解

- **ReAct 是目前几乎所有 Agent 框架的基础范式**：LangChain Agent、AutoGPT 等都基于 Thought-Action-Observation 循环
- **ReAct 的局限**：线性执行，无法并行探索多条路径；遇到工具连续失败时容易陷入死循环
- **实践技巧**：为 Agent 设置最大循环次数（max_iterations）和超时机制是工程必备
