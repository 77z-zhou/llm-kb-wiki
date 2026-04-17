---
type: concept
title: "LLM Agent 概述"
category: application
sources: [extra01-4.1, extra01-4.7, extra01-4.9]
interview_frequency: 高频
interview_difficulty: 中等
related: [react, planning-methods, agent-memory, tool-use, multi-agent]
---

# LLM Agent 概述

## 核心定义

基于 LLM 的智能体（Agent）是一个能够**自主理解环境、进行规划决策、并执行行动**以达成特定目标的计算系统。

与传统 LLM 问答不同，Agent 具有**自主性**和**循环执行**特点——主动地、持续地与环境/工具交互直到完成任务。

## 四大核心组件

| 组件 | 作用 | 关键技术 |
|:-----|:-----|:---------|
| **大脑 (Brain)** | 认知核心，理解目标、推理、决策 | GPT-4, Llama, Qwen 等 LLM |
| **规划 (Planning)** | 将复杂目标分解为可执行子任务 | CoT, ReAct, ToT, GoT |
| **记忆 (Memory)** | 弥补有限上下文窗口 | 短期(Scratchpad) + 长期(向量DB) |
| **工具 (Tool Use)** | 扩展能力边界 | Function Calling, API调用 |

## 构建复杂 Agent 的主要挑战

1. **规划鲁棒性**：长链推理脆弱，易迷失/死循环/过早终止
2. **评估困难**：开放式任务无唯一正确答案，环境不可复现
3. **成本与延迟**：数十次 LLM 调用导致高费用和长等待
4. **安全可控**：工具权限管理、Prompt Injection 防御、行为不可预测性

## 软件 Agent vs 具身 Agent

| 维度 | 软件 Agent | 具身 Agent |
|:-----|:-----------|:-----------|
| 感知 | 结构化 JSON/API | 非结构化传感器(像素/点云) |
| 可观测性 | 完全可观测 | 部分可观测 |
| 行动空间 | 离散、确定 | 连续、随机 |
| 实时性 | 回合制/异步 | 实时反馈循环 |
| 安全性 | 错误可逆 | 物理不可逆 |

## 补充见解

- **Agent 的核心瓶颈不在 LLM 能力而在系统工程**：工具调用的错误处理、状态管理、超时重试等工程问题往往比 LLM 推理本身更棘手
- **MCP (Model Context Protocol) 的出现正在标准化工具接入**：未来 Agent 的工具生态会像 App Store 一样标准化
- **具身智能是 Agent 的终极形态**，但目前主流应用仍集中在软件 Agent（代码生成、数据分析、自动化流程）
