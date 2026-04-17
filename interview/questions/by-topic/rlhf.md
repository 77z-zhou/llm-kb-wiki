---
type: interview-question-set
title: "RLHF 对齐类面试题"
created: 2026-04-17
updated: 2026-04-17
topic: rlhf
source: extra01-llm-interview-reference
question_count: 6
---

# RLHF 对齐类面试题

## 🔥 高频题

### Q1: RLHF 旨在解决什么问题？为什么 SFT 不够？
- **难度**: Medium
- **概念页**: [[concepts/training/rlhf]]
- **要点**: HHH 对齐原则；SFT 教"模仿"不教"判断"；偏好难标注、行为空间巨大、暴露偏差

### Q2: 详述 RLHF 三阶段（SFT → RM → PPO），每阶段的输入/输出/目标是什么？
- **难度**: Hard
- **概念页**: [[concepts/training/rlhf]]
- **要点**: SFT→初始策略；RM→人类偏好代理函数；PPO→对齐后的模型

### Q3: 奖励模型的架构如何选择？与最终 LLM 是什么关系？损失函数是什么？
- **难度**: Hard
- **概念页**: [[concepts/training/reward-model]]
- **要点**: 同架构+回归头；Bradley-Terry 模型；负对数似然

### Q4: 为什么选 PPO？KL 散度惩罚项的作用？
- **难度**: Hard
- **概念页**: [[concepts/training/ppo]]
- **要点**: vs REINFORCE(方差)、vs Q-learning(动作空间)；防策略崩溃+保多样性

## 🟡 中频题

### Q5: RM 训练为什么用成对比较而非绝对评分？
- **难度**: Medium
- **概念页**: [[concepts/training/reward-model]]
- **要点**: 认知负荷低、一致性高、信号精细；劣势是数据效率低、可能不传递

### Q6: PPO 的 β 系数过大/过小分别导致什么问题？如何调参？
- **难度**: Hard
- **概念页**: [[concepts/training/ppo]]
- **要点**: 过大→保守白做；过小→作弊/崩溃；监控 KL/奖励分数/人工评估/自适应调整
