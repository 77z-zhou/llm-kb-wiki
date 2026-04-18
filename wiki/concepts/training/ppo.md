---
type: concept
title: "PPO 近端策略优化"
aliases: [Proximal Policy Optimization, KL散度惩罚]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [rlhf, reward-model]
tags: [PPO, 强化学习, 对齐]
status: active
confidence: high
interview_frequency: high
interview_difficulty: hard
---

# PPO 近端策略优化

## 为什么选 PPO？

### vs REINFORCE (简单策略梯度)
- REINFORCE **方差极高**，用整序列奖励更新，梯度不稳定
- PPO 通过价值函数基线和优势函数**显著降低方差**

### vs Q-learning (DQN)
- Q-learning 为**离散低维**动作空间设计
- LLM 动作空间 = 词汇表在每步的组合，极其巨大
- PPO 作为策略梯度方法**天然适用巨大动作空间**

## KL 散度惩罚项

```
Objective(π_RL) = E[Reward] - β · KL(π_RL || π_SFT)
```

### 两个关键作用

1. **防止策略崩溃 (Policy Collapse)**
   - 没有 KL 约束 → 模型找 RM 漏洞"作弊" → 生成无意义/重复文本
   - KL 惩罚将优化限制在 SFT 模型附近的"安全区域"

2. **保证探索效率和多样性**
   - 避免过早收敛到高奖励但低质的局部最优
   - 在有意义的语言分布附近探索

## β 系数的调参

### β 过大
- 模型过于保守，策略几乎不更新
- 最终模型 ≈ SFT 模型，RLHF 白做

### β 过小
- 约束不足，策略过于激进
- **奖励作弊 (Reward Hacking)**：找 RM 漏洞获高分
- **模式崩溃 (Mode Collapse)**：输出单一重复
- 语言能力退化

### 调参方法

1. **监控 KL 散度**：应在合理范围内波动（≈0 太大，急剧增大太小）
2. **监控奖励分数**：应稳步提升，突然暴涨可能是作弊
3. **人工评估**：定期抽样检查输出质量
4. **自适应 β**：根据 KL 散度动态调整（KL 偏高则增大 β，反之减小）

## 补充见解

1. **PPO 的实际替代方案**：由于 PPO 工程复杂性高（需要 4 个模型），业界越来越倾向于使用 DPO、GRPO 等更简单的替代方案。但理解 PPO 仍然是面试的基础。

2. **PPO-clip vs PPO-penalty**：PPO 有两种形式——clip 版通过裁剪比率来限制更新幅度，penalty 版通过 KL 惩罚。RLHF 中通常用 penalty 版或两者结合。

3. **Reward shaping 技巧**：在实践中通常对 RM 输出做归一化处理（如减均值除标准差），避免奖励尺度不稳定影响训练。

---

*来源：[[sources/extra01-llm-interview-reference]]*
