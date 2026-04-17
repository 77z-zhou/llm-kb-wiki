---
type: map
title: "LLM 面试知识库索引"
created: 2026-04-17
updated: 2026-04-17
---

# LLM 面试知识库

## 核心知识领域

### 模型架构 (concepts/architecture/)
- [[concepts/architecture/transformer|Transformer 与自注意力]] 🔥高频
- [[concepts/architecture/positional-encoding|位置编码]] 🔥高频
- [[concepts/architecture/rope|RoPE 旋转位置编码]] 🔥高频
- [[concepts/architecture/attention-variants|MHA/MQA/GQA]] 🔥高频
- [[concepts/architecture/llm-architectures|LLM架构对比]] 🔥高频
- [[concepts/architecture/moe|MoE 混合专家模型]] 🔥高频
- [[concepts/architecture/activation-functions|激活函数 GeLU/SwiGLU]] 🟡中频
- [[concepts/architecture/tokenization|词元化 BPE/WordPiece]] 🟡中频
- [[concepts/architecture/emergent-abilities|涌现能力]] 🟡中频

### 训练与微调 (concepts/training/)
- [[concepts/training/scaling-laws|Scaling Laws]] 🔥高频
- [[concepts/training/large-scale-training|大规模训练挑战]] 🔥高频
- [[concepts/training/rlhf|RLHF]] 🔥高频
- [[concepts/training/reward-model|奖励模型]] 🔥高频
- [[concepts/training/ppo|PPO]] 🔥高频
- [[concepts/training/regularization|L1/L2 正则化]] 🟢低频

### 推理与部署 (concepts/inference/)
- [[concepts/inference/decoding-strategies|解码策略]] 🟡中频

### 应用与系统 (concepts/application/)
- [[concepts/application/agent-overview|LLM Agent 概述]] 🔥高频
- [[concepts/application/react|ReAct 框架]] 🔥高频
- [[concepts/application/planning-methods|Agent 规划方法]] 🔥高频
- [[concepts/application/tool-use|工具使用与 Function Calling]] 🔥高频
- [[concepts/application/agent-memory|Agent 记忆系统]] 🟡中频
- [[concepts/application/agent-safety|Agent 安全与对齐]] 🟡中频
- [[concepts/application/multi-agent|多智能体系统]] 🟡中频
- [[concepts/application/agent-frameworks|Agent 框架选型与微调]] 🟡中频
- [[concepts/application/rag-overview|RAG 概述]] 🔥高频
- [[concepts/application/rag-pipeline|RAG 完整流水线]] 🔥高频
- [[concepts/application/retrieval-enhancement|RAG 检索增强技术]] 🔥高频
- [[concepts/application/embedding-models|嵌入模型选择与评估]] 🟡中频
- [[concepts/application/rag-eval|RAG 评估]] 🟡中频
- [[concepts/application/advanced-rag|高级 RAG 范式与知识图谱]] 🟡中频

### 评估 (concepts/evaluation/)
- [[concepts/evaluation/eval-metrics|LLM 评估指标与基准]] 🔥高频
- [[concepts/evaluation/llm-as-judge|LLM-as-a-Judge 与专项评估]] 🟡中频
- [[concepts/evaluation/agent-eval|Agent 评估]] 🟡中频
- [[concepts/evaluation/red-teaming|红队测试与持续监控]] 🟡中频

## 实体与工具 (entities/)

- [[entities/qwen|Qwen 系列]] 🔥面试常考
- [[entities/deepseek|DeepSeek 系列]] 🔥面试常考
- [[entities/vllm|vLLM 推理引擎]] 🟡中频
- [[entities/langchain|LangChain 框架]] 🟡中频
- [[entities/llamaindex|LlamaIndex 框架]] 🟡中频

## 对比分析 (comparisons/)

- [[comparisons/moe-vs-dense|MoE vs Dense 模型]] 🔥高频
- [[comparisons/rag-vs-finetuning|RAG vs 微调]] 🔥高频
- [[comparisons/mha-vs-mqa-vs-gqa|MHA vs MQA vs GQA]] 🔥高频

## 知识地图 (maps/)

- [[maps/model-architecture|模型架构学习路径]]
- [[maps/application-systems|应用系统学习路径]]

## 面试题库

### 按主题

- [[interview/questions/by-topic/architecture|架构类题目]] (10题)
- [[interview/questions/by-topic/training|训练类题目]] (3题)
- [[interview/questions/by-topic/rlhf|RLHF对齐类题目]] (6题)
- [[interview/questions/by-topic/inference|推理类题目]] (1题)
- [[interview/questions/by-topic/agent|Agent类题目]] (13题)
- [[interview/questions/by-topic/rag|RAG类题目]] (12题)
- [[interview/questions/by-topic/evaluation|评估类题目]] (10题)

### 按难度

- [[interview/questions/by-difficulty/basic|基础题 Easy]] (3题)
- [[interview/questions/by-difficulty/intermediate|中等题 Medium]] (32题)
- [[interview/questions/by-difficulty/advanced|高级题 Hard]] (12题)

## 复习管理

- [[interview/weak-points|薄弱点追踪]]
- [[interview/review-schedule|复习计划 (4周)]]

## 来源文档

- [[wiki/sources/extra01-llm-interview-reference|Extra01 面试参考答案]]

## 统计

- 概念页面: 29 个 (架构9 + 训练6 + 推理1 + 应用14 + 评估4)
- 实体页面: 5 个 (Qwen/DeepSeek/vLLM/LangChain/LlamaIndex)
- 对比页面: 3 个 (MoE vs Dense/RAG vs 微调/MHA vs MQA vs GQA)
- 知识地图: 2 个 (模型架构/应用系统)
- 面试题: 55 道 (架构10 + 训练3 + RLHF6 + 推理1 + Agent13 + RAG12 + 评估10)
- 来源文档: 1 份

---

*最后更新：2026-04-17*
