---
type: concept
title: "Agent 安全与对齐"
category: application
sources: [extra01-4.10]
interview_frequency: 中频
interview_difficulty: 中等
related: [agent-overview, multi-agent, rlhf]
---

# Agent 安全与对齐

确保 Agent 行为安全、可控且符合人类意图是系统性工程，需多层面设计。

## 六层保障体系

### 1. 核心模型对齐
LLM 本身必须经过 RLHF/DPO/Constitutional AI 等对齐训练，遵循 HHH 原则

### 2. 工具与权限管理
- **最小权限原则**：只给完成任务所必需的最少工具和权限
- **工具白名单** + 读写执行权限控制
- **资源限制**：计算资源/API 调用次数/执行时间上限

### 3. 人类在环 (Human-in-the-Loop)
- 高风险操作前必须暂停等待人类批准
- 人类可实时监控、干预、终止 Agent 行为

### 4. 沙箱化执行
Agent 代码/命令在 Docker 容器或 VM 中执行，限制破坏范围

### 5. 硬编码护栏
- 正则过滤器禁止危险命令（如 `rm -rf /`）
- 输入/输出安全审查层

### 6. 红队测试与审计
- 主动攻击发现安全漏洞（Prompt Injection、越狱等）
- 详细记录所有行为轨迹，事后审计分析

## 补充见解

- **Prompt Injection 是 Agent 最大的安全威胁**：恶意用户或被索引的文档中的恶意指令可能劫持 Agent 控制流
- **Agent 安全 = LLM 安全 + 系统工程安全**：即使 LLM 本身安全，工具调用层面也可能被利用
- **防御深度（Defense in Depth）是关键原则**：不要依赖单一安全层
