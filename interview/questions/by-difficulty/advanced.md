---
type: interview-questions
title: "高级面试题 (Hard)"
difficulty: advanced
created: 2026-04-17
updated: 2026-04-17
total: 12
---

# 高级面试题 (Hard)

> 高难度题和开放题，考察深度理解和工程经验。用于区分候选人水平。

---

## 架构类 (2 题)

### Q1: 详细介绍 RoPE，对比绝对位置编码的优劣
- **来源**: [architecture](by-topic/architecture.md) Q3
- **概念页**: [[concepts/architecture/rope]]
- **要点**: 向量旋转编码位置 → 注意力分数只依赖相对位置；外推能力、无参数、远距离衰减
- **深度提示**: 能推导旋转矩阵公式、解释为什么 RoPE 的相对位置编码是通过内积自然实现的

### Q2: MoE 如何在不增加推理成本情况下扩大参数规模？
- **来源**: [architecture](by-topic/architecture.md) Q6
- **概念页**: [[concepts/architecture/moe]]
- **要点**: 稀疏激活 + Top-K 路由；总参数量 vs 推理 FLOPs 解耦
- **深度提示**: Mixtral 8x7B 计算题 (47B 总参, 13B 推理成本)、DeepSeek 细粒度 MoE 创新

## 训练类 (2 题)

### Q3: 什么是 Scaling Laws？揭示了什么关系？
- **来源**: [training](by-topic/training.md) Q1
- **概念页**: [[concepts/training/scaling-laws]]
- **要点**: 性能与 N/D/C 的幂律关系；Chinchilla 1:20 比例
- **深度提示**: 能写出幂律公式 $L(N) \propto N^{-\alpha}$、解释计算最优 vs 数据最优边界

### Q4: 训练百亿/千亿参数 LLM 面临哪些主要挑战？
- **来源**: [training](by-topic/training.md) Q2
- **概念页**: [[concepts/training/large-scale-training]]
- **要点**: 显存(3D并行+ZeRO)→通信(NVLink/IB)→稳定性(BF16/梯度裁剪)
- **深度提示**: 能说清 3D 并行 (TP+PP+DP) 各自解决什么瓶颈

## RLHF 类 (3 题)

### Q5: 详述 RLHF 三阶段，每阶段的输入/输出/目标
- **来源**: [rlhf](by-topic/rlhf.md) Q2
- **概念页**: [[concepts/training/rlhf]]
- **要点**: SFT→初始策略；RM→人类偏好代理函数；PPO→对齐后模型
- **深度提示**: 能画完整数据流图、说清为什么需要 KL 散度约束

### Q6: 奖励模型架构如何选择？损失函数是什么？
- **来源**: [rlhf](by-topic/rlhf.md) Q3
- **概念页**: [[concepts/training/reward-model]]
- **要点**: 同架构+回归头；Bradley-Terry 模型；负对数似然
- **深度提示**: 能写出 BT 模型的 loss 公式 $P(y_w > y_l) = \sigma(r(x, y_w) - r(x, y_l))$

### Q7: 为什么选 PPO？β 系数如何调参？
- **来源**: [rlhf](by-topic/rlhf.md) Q4 + Q6
- **概念页**: [[concepts/training/ppo]]
- **要点**: vs REINFORCE(方差)、vs Q-learning(动作空间)；β 过大/过小问题
- **深度提示**: 能解释 PPO-clip 公式、自适应 KL 调整策略

## Agent 类 (2 题)

### Q8: 了解 A2A 框架吗？解决了什么问题？
- **来源**: [agent](by-topic/agent.md) Q11
- **概念页**: [[concepts/application/multi-agent]]
- **要点**: 个体实现 vs 群体交互标准、应用层 vs 协议层
- **深度提示**: 对比 A2A 与 HTTP 的类比，理解协议层的标准化价值

### Q9: 如何微调 Agent 能力？数据集如何收集？
- **来源**: [agent](by-topic/agent.md) Q13
- **概念页**: [[concepts/application/agent-frameworks]]
- **要点**: 行为克隆、教师模型合成轨迹、轨迹数据收集三法
- **深度提示**: 能讨论 SFT vs RL 在 Agent 微调中的对比、数据质量 vs 数量权衡

## RAG 类 (2 题)

### Q10: 除了基础向量检索，还有哪些提升检索质量的技术？
- **来源**: [rag](by-topic/rag.md) Q4
- **概念页**: [[concepts/application/retrieval-enhancement]]
- **要点**: 混合搜索、Cross-Encoder 重排序、Multi-Query/HyDE/Sub-Query
- **深度提示**: 能画出从基础 RAG → 进阶 RAG 的技术栈层次图

### Q11: 了解哪些高级 RAG 范式？
- **来源**: [rag](by-topic/rag.md) Q10
- **概念页**: [[concepts/application/advanced-rag]]
- **要点**: 迭代式(Self-RAG)、自适应(FLARE)、GraphRAG
- **深度提示**: 能对比 Self-RAG 的 Critique 机制和 FLARE 的主动检索策略

## 评估类 (1 题)

### Q12: 如何设计评估方案衡量特定能力？(6.4)
- **来源**: [evaluation](by-topic/evaluation.md) Q4
- **概念页**: [[concepts/evaluation/llm-as-judge]]
- **要点**: 事实性(知识库QA+LLM Judge)、推理(结果+过程)、安全性(拒绝率+误伤率)
- **深度提示**: 能设计完整的评估 Pipeline，包括指标选择、数据构造、评分标准

---

## 答题策略

- 高级题不需要完美回答，展示思考过程比给出标准答案更有价值
- **结构化回答**: 定义 → 核心机制 → 工程挑战 → 解决方案 → 个人见解
- 遇到不会的可以坦诚说"这方面我了解不深，但我的理解是..."然后展示相关知识
- 准备一些 **数字** 和 **对比** 在回答中引用（如 Mixtral 参数量、Scaling Laws 指数）
- 开放题没有标准答案，重点展示分析框架和工程思维
