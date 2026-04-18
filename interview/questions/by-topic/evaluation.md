---
type: interview-questions
title: "模型评估与 Agent 评估面试题"
category: evaluation
source: extra01-第6章
total: 10
---

# 模型评估与 Agent 评估面试题

## 🔥 高频题

### Q1. 为什么 BLEU/ROUGE 对评估 LLM 有局限性？(6.1)
- **难度**：中等
- **概念页**：[eval-metrics](../../wiki/concepts/evaluation/eval-metrics.md)
- **要点**：无语义理解/无法评估事实性/忽略多样性/长文本差/无视推理

### Q2. 介绍几个 LLM 综合性基准测试 (6.2)
- **难度**：中等
- **概念页**：[eval-metrics](../../wiki/concepts/evaluation/eval-metrics.md)
- **要点**：MMLU(知识广度)/Big-Bench(能力边界)/HumanEval(代码)/GSM8K(数学)

### Q3. 什么是 LLM-as-a-Judge？优缺点？(6.3)
- **难度**：中等
- **概念页**：[llm-as-judge](../../wiki/concepts/evaluation/llm-as-judge.md)
- **要点**：自动化评估、可扩展+一致、但有位置/冗长/自我偏好偏见

## 🟡 中频题

### Q4. 如何设计评估方案衡量特定能力？(6.4)
- **难度**：中高
- **概念页**：[llm-as-judge](../../wiki/concepts/evaluation/llm-as-judge.md)
- **要点**：事实性(知识库QA+LLM Judge)、推理(结果+过程评估)、安全性(拒绝率+误伤率)

### Q5. 评估 Agent 为什么比评估 LLM 更难？(6.5)
- **难度**：中等
- **概念页**：[agent-eval](../../wiki/concepts/evaluation/agent-eval.md)
- **要点**：有状态/动态环境/非确定性/开放式任务，维度从单回答到全过程

### Q6. 了解哪些 Agent 基准测试？(6.6)
- **难度**：中等
- **概念页**：[agent-eval](../../wiki/concepts/evaluation/agent-eval.md)
- **要点**：WebArena(网页)/AgentBench(8环境)/GAIA(复杂任务)，沙箱+程序化验证

### Q7. Agent 评估除了结果正确性，还有哪些过程指标？(6.7)
- **难度**：中等
- **概念页**：[agent-eval](../../wiki/concepts/evaluation/agent-eval.md)
- **要点**：效率(Token/延迟/步骤数)、鲁棒性(错误处理/抗干扰)、自主性(干预次数)

### Q8. 什么是红队测试？(6.8)
- **难度**：中等
- **概念页**：[red-teaming](../../wiki/concepts/evaluation/red-teaming.md)
- **要点**：对抗性测试发现安全漏洞和偏见、Prompt Injection/越狱/刻板印象

### Q9. 如何设计人工评估的准则和流程？(6.9)
- **难度**：中等
- **概念页**：[red-teaming](../../wiki/concepts/evaluation/red-teaming.md)
- **要点**：原子化维度+量化评分+丰富示例、盲评+多次独立评估+仲裁

### Q10. 如何持续监控已部署的 LLM/Agent？(6.10)
- **难度**：中等
- **概念页**：[red-teaming](../../wiki/concepts/evaluation/red-teaming.md)
- **要点**：采集日志→自动化监控(LLM Judge+黄金集)→人工审核→反馈闭环+迭代
