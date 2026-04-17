---
type: source
title: "LLM & Agent 面试回答参考 (Extra01)"
created: 2026-04-17
updated: 2026-04-17
source_type: interview-reference
raw_path: "raw/interview-exp/extra01-reference-answers.md"
tags: [面试题, LLM, RLHF, Transformer, MoE, Agent, RAG, 评估]
status: active
---

# LLM & Agent 面试回答参考 (Extra01)

## 来源信息

- **类型**: 面试参考答案文档
- **导入时间**: 2026-04-17
- **排除内容**: VLM 部分（第2章）

## 导入题目索引

### 第1章: LLM 八股 (16题)

| 编号 | 主题 | 频率 | 概念页 |
|------|------|------|--------|
| 1.1 | 自注意力机制 | 🔥高 | [[concepts/architecture/transformer]] |
| 1.2 | 位置编码 | 🔥高 | [[concepts/architecture/positional-encoding]] |
| 1.3 | RoPE | 🔥高 | [[concepts/architecture/rope]] |
| 1.4 | MHA/MQA/GQA | 🔥高 | [[concepts/architecture/attention-variants]] |
| 1.5 | LLM架构对比 | 🔥高 | [[concepts/architecture/llm-architectures]] |
| 1.6 | Scaling Laws | 🔥高 | [[concepts/training/scaling-laws]] |
| 1.7 | 解码策略 | 🟡中 | [[concepts/inference/decoding-strategies]] |
| 1.8 | 词元化 | 🟡中 | [[concepts/architecture/tokenization]] |
| 1.9 | NLP vs LLM | 🟡中 | — |
| 1.10 | L1/L2正则化 | 🟢低 | [[concepts/training/regularization]] |
| 1.11 | 涌现能力 | 🟡中 | [[concepts/architecture/emergent-abilities]] |
| 1.12 | 激活函数 | 🟡中 | [[concepts/architecture/activation-functions]] |
| 1.13 | MoE | 🔥高 | [[concepts/architecture/moe]] |
| 1.14 | 大规模训练挑战 | 🔥高 | [[concepts/training/large-scale-training]] |
| 1.15 | 开源框架与模型 | 🟡中 | — |
| 1.16 | 前沿论文 | 开放 | — |

### 第3章: RLHF 八股 (6题)

| 编号 | 主题 | 频率 | 概念页 |
|------|------|------|--------|
| 3.1 | RLHF vs SFT | 🔥高 | [[concepts/training/rlhf]] |
| 3.2 | RLHF三阶段 | 🔥高 | [[concepts/training/rlhf]] |
| 3.3 | 成对比较数据 | 🟡中 | [[concepts/training/reward-model]] |
| 3.4 | 奖励模型设计 | 🔥高 | [[concepts/training/reward-model]] |
| 3.5 | PPO算法 | 🔥高 | [[concepts/training/ppo]] |
| 3.6 | KL散度调参 | 🟡中 | [[concepts/training/ppo]] |

### 第4章: Agent (13题)

| 编号 | 主题 | 频率 | 概念页 |
|------|------|------|--------|
| 4.1 | Agent 定义与组件 | 🔥高 | [[concepts/application/agent-overview]] |
| 4.2 | ReAct 框架 | 🔥高 | [[concepts/application/react]] |
| 4.3 | 规划方法(CoT/ToT/GoT) | 🔥高 | [[concepts/application/planning-methods]] |
| 4.4 | Agent 记忆系统 | 🟡中 | [[concepts/application/agent-memory]] |
| 4.5 | 工具使用/Function Calling | 🔥高 | [[concepts/application/tool-use]] |
| 4.6 | LangChain vs LlamaIndex | 🟡中 | [[concepts/application/agent-frameworks]] |
| 4.7 | Agent 构建挑战 | 🔥高 | [[concepts/application/agent-overview]] |
| 4.8 | 多智能体系统 | 🟡中 | [[concepts/application/multi-agent]] |
| 4.9 | 软件 vs 具身 Agent | 🟡中 | [[concepts/application/agent-overview]] |
| 4.10 | Agent 安全与对齐 | 🟡中 | [[concepts/application/agent-safety]] |
| 4.11 | A2A 框架 | 🟡中 | [[concepts/application/multi-agent]] |
| 4.12 | 框架选型实践 | 开放 | [[concepts/application/agent-frameworks]] |
| 4.13 | Agent 微调 | 开放 | [[concepts/application/agent-frameworks]] |

### 第5章: RAG (12题)

| 编号 | 主题 | 频率 | 概念页 |
|------|------|------|--------|
| 5.1 | RAG 工作原理与优势 | 🔥高 | [[concepts/application/rag-overview]] |
| 5.2 | RAG 完整流水线 | 🔥高 | [[concepts/application/rag-pipeline]] |
| 5.3 | 文本切块策略 | 🔥高 | [[concepts/application/rag-pipeline]] |
| 5.4 | 嵌入模型选择 | 🟡中 | [[concepts/application/embedding-models]] |
| 5.5 | 检索增强技术 | 🔥高 | [[concepts/application/retrieval-enhancement]] |
| 5.6 | Lost in the Middle | 🔥高 | [[concepts/application/retrieval-enhancement]] |
| 5.7 | RAG 评估 | 🟡中 | [[concepts/application/rag-eval]] |
| 5.8 | 知识图谱增强 | 🟡中 | [[concepts/application/advanced-rag]] |
| 5.9 | 高级 RAG 范式 | 🟡中 | [[concepts/application/advanced-rag]] |
| 5.10 | RAG 部署挑战 | 🟡中 | [[concepts/application/rag-pipeline]] |
| 5.11 | 搜索系统 vs RAG | 🔥高 | [[concepts/application/rag-overview]] |
| 5.12 | 开源 RAG 框架 | 🟡中 | [[concepts/application/advanced-rag]] |

### 第6章: 模型评估与 Agent 评估 (10题)

| 编号 | 主题 | 频率 | 概念页 |
|------|------|------|--------|
| 6.1 | BLEU/ROUGE 局限性 | 🔥高 | [[concepts/evaluation/eval-metrics]] |
| 6.2 | LLM 综合基准 | 🔥高 | [[concepts/evaluation/eval-metrics]] |
| 6.3 | LLM-as-a-Judge | 🔥高 | [[concepts/evaluation/llm-as-judge]] |
| 6.4 | 专项能力评估 | 🟡中 | [[concepts/evaluation/llm-as-judge]] |
| 6.5 | Agent 评估难点 | 🟡中 | [[concepts/evaluation/agent-eval]] |
| 6.6 | Agent 基准测试 | 🟡中 | [[concepts/evaluation/agent-eval]] |
| 6.7 | 过程指标 | 🟡中 | [[concepts/evaluation/agent-eval]] |
| 6.8 | 红队测试 | 🟡中 | [[concepts/evaluation/red-teaming]] |
| 6.9 | 人工评估设计 | 🟡中 | [[concepts/evaluation/red-teaming]] |
| 6.10 | 持续监控 | 🟡中 | [[concepts/evaluation/red-teaming]] |
