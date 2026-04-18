---
type: interview-questions
title: "Agent 面试题"
category: agent
source: extra01-第4章
total: 13
---

# Agent 面试题

## 🔥 高频题

### Q1. 你如何定义一个基于 LLM 的 Agent？它通常由哪些核心组件构成？(4.1)
- **难度**：中等
- **概念页**：[agent-overview](../../wiki/concepts/application/agent-overview.md)
- **要点**：四大组件（大脑/规划/记忆/工具）、自主性+循环执行

### Q2. 请详细解释 ReAct 框架 (4.2)
- **难度**：中等
- **概念页**：[react](../../wiki/concepts/application/react.md)
- **要点**：Thought-Action-Observation 循环、与纯 CoT 的区别、动态推理+工具交互

### Q3. 如何赋予 LLM 规划能力？(4.3)
- **难度**：中等
- **概念页**：[planning-methods](../../wiki/concepts/application/planning-methods.md)
- **要点**：CoT → ReAct → ToT → GoT 三个层次，搜索式 vs 提示式

### Q4. LLM 如何学会调用外部工具？(4.5)
- **难度**：中等
- **概念页**：[tool-use](../../wiki/concepts/application/tool-use.md)
- **要点**：Function Calling 五步流程、JSON Schema 工具定义、结构化输出

### Q5. 构建复杂 Agent 的主要挑战？(4.7)
- **难度**：中等
- **概念页**：[agent-overview](../../wiki/concepts/application/agent-overview.md)
- **要点**：规划鲁棒性、评估困难、成本延迟、安全可控

## 🟡 中频题

### Q6. 如何设计 Agent 的短期和长期记忆？(4.4)
- **难度**：中等
- **概念页**：[agent-memory](../../wiki/concepts/application/agent-memory.md)
- **要点**：短期(上下文窗口/Buffer) vs 长期(向量DB/RAG)

### Q7. 比较两个 Agent 开发框架（如 LangChain 和 LlamaIndex）(4.6)
- **难度**：中等
- **概念页**：[agent-frameworks](../../wiki/concepts/application/agent-frameworks.md)
- **要点**：编排驱动 vs 数据驱动、灵活控制 vs 开箱即用

### Q8. 什么是多智能体系统？优势和新复杂性？(4.8)
- **难度**：中等
- **概念页**：[multi-agent](../../wiki/concepts/application/multi-agent.md)
- **要点**：分工/并行/鲁棒 vs 通信/协调/信用分配

### Q9. 如何确保 Agent 行为安全可控？(4.10)
- **难度**：中等
- **概念页**：[agent-safety](../../wiki/concepts/application/agent-safety.md)
- **要点**：六层保障（模型对齐/权限管理/HITL/沙箱/护栏/红队）

### Q10. 软件 Agent vs 具身 Agent 的本质区别？(4.9)
- **难度**：中等
- **概念页**：[agent-overview](../../wiki/concepts/application/agent-overview.md)
- **要点**：感知/可观测性/行动空间/实时性/安全性五个维度

### Q11. 了解 A2A 框架吗？(4.11)
- **难度**：中高
- **概念页**：[multi-agent](../../wiki/concepts/application/multi-agent.md)
- **要点**：个体实现 vs 群体交互标准、应用层 vs 协议层

### Q12. 用过哪些 Agent 框架？选型？评价指标？(4.12)
- **难度**：中高（开放题）
- **概念页**：[agent-frameworks](../../wiki/concepts/application/agent-frameworks.md)
- **要点**：逻辑驱动→LangChain / 数据驱动→LlamaIndex；成功率/效率/鲁棒性

### Q13. 如何微调 Agent 能力？数据集如何收集？(4.13)
- **难度**：高（开放题）
- **概念页**：[agent-frameworks](../../wiki/concepts/application/agent-frameworks.md)
- **要点**：行为克隆、教师模型合成轨迹、轨迹数据收集三法
