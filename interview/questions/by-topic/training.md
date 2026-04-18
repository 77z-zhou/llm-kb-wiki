---
type: interview-question-set
title: "训练类面试题"
created: 2026-04-17
updated: 2026-04-17
topic: training
source: extra01-llm-interview-reference
question_count: 3
---

# 训练类面试题

## 🔥 高频题

### Q1: 什么是 Scaling Laws？揭示了什么关系？对研发有什么指导？
- **难度**: Hard
- **概念页**: [[concepts/training/scaling-laws]]
- **要点**: 性能与 N/D/C 的幂律关系；Chinchilla 1:20 比例；可预测性指导资源分配

### Q2: 训练百亿/千亿参数 LLM 面临哪些主要挑战？
- **难度**: Hard
- **概念页**: [[concepts/training/large-scale-training]]
- **要点**: 显存(3D并行+ZeRO)→通信(NVLink/IB)→稳定性(BF16/梯度裁剪/Warmup)

## 🟢 低频题

### Q3: L1 和 L2 正则化分别是什么？适用场景？
- **难度**: Easy
- **概念页**: [[concepts/training/regularization]]
- **要点**: L1 稀疏化做特征选择；L2 平滑化防过拟合(Weight Decay)
