---
type: concept
title: "工具使用与 Function Calling"
category: application
sources: [extra01-4.5]
interview_frequency: 高频
interview_difficulty: 中等
related: [agent-overview, react]
---

# 工具使用与 Function Calling

## Function Calling 工作流程（5步）

### 1. 工具定义与注册
以 JSON Schema 向 LLM 描述可用工具：
- **函数名称**：如 `get_current_weather`
- **函数描述**：自然语言说明功能（LLM 据此判断何时调用）
- **参数列表**：名称、类型、描述、是否必填

### 2. LLM 决策与意图识别
用户提问 + 所有工具描述 → LLM 分析意图 → 判断是否需要调用工具

### 3. 生成结构化调用指令
输出不再是自然语言，而是结构化 JSON：
```json
{
  "tool_call": {
    "name": "get_current_weather",
    "arguments": {"location": "Singapore", "unit": "celsius"}
  }
}
```

### 4. 外部执行与结果返回
Agent 控制代码（Orchestrator）解析 JSON → 实际调用 API → 返回结果

### 5. 整合结果生成最终回复
工具返回结果 + 对话历史 → LLM 生成流畅自然语言回答

## 关键设计要点

- **函数描述的质量直接决定工具选择准确率**：描述要具体、无歧义，覆盖典型使用场景
- **参数校验必不可少**：LLM 可能生成不合法参数，需后端校验+错误反馈
- **并行工具调用**：现代 API（如 OpenAI）支持一次返回多个 tool_call，可并行执行

## 补充见解

- **Function Calling 不是唯一的工具调用方式**：早期用正则解析文本（如 ReAct 的 `Action: [tool, input]`），现在主流是结构化 JSON
- **工具数量过多会降低选择准确率**：实践中建议单次可用工具不超过 20 个，或采用分层路由
- **MCP (Model Context Protocol)** 正在成为工具标准化的方向，类似"AI 的 USB 接口"
