---
type: concept
title: "大规模训练挑战: 显存、通信与稳定性"
aliases: [3D并行, ZeRO, 分布式训练, 训练稳定性]
created: 2026-04-17
updated: 2026-04-17
sources: [extra01-llm-interview-reference]
related: [scaling-laws, moe]
tags: [分布式训练, 并行, 工程]
status: active
confidence: high
interview_frequency: high
interview_difficulty: hard
---

# 大规模训练挑战

训练百亿/千亿参数 LLM 的三大核心挑战。

## 1. 显存挑战 (Memory Wall)

千亿参数模型的参数+梯度+优化器状态需数 TB，远超单卡（H100 80GB）。

### 解决方案：3D 并行

| 并行方式 | 原理 | 解决什么 | 代价 |
|----------|------|----------|------|
| **数据并行 (DP)** | 每卡一份完整模型，数据切分 | 提高吞吐 | 不减单卡显存 |
| **流水线并行 (PP)** | 模型层垂直切分到不同 GPU | 降低单卡显存 | 流水线气泡 |
| **张量并行 (TP)** | 单个大算子水平切分 | 降低单卡显存 | 高通信开销 |
| **ZeRO** | 在 DP 基础上切分优化器/梯度/参数 | 消除冗余 | 额外通信 |

**ZeRO 三级**：
- ZeRO-1: 切分优化器状态
- ZeRO-2: + 切分梯度
- ZeRO-3: + 切分模型参数

## 2. 通信挑战 (Communication Bottleneck)

所有并行策略都引入 GPU 间通信，可能超过计算本身成为瓶颈。

- **硬件**：NVLink（机内）+ InfiniBand（跨节点）
- **软件**：Ring All-Reduce、计算与通信重叠 (overlap)

## 3. 训练不稳定性 (Training Instability)

Loss 突然飙升为 NaN，数天训练成果可能毁于一旦。

### 关键对策

- **BF16 混合精度**：比 FP16 动态范围更大，避免下溢
- **Pre-LayerNorm**：在 Attention/FFN 前做归一化，比 Post-LN 更稳定
- **梯度裁剪 (Gradient Clipping)**：设范数上限防止梯度爆炸
- **学习率预热 (Warmup)**：训练初期小学习率，逐渐增大

## 补充见解

1. **面试回答策略**：这题涵盖面很广，建议按"显存→通信→稳定性"三条线分别展开，每条线给出"问题→解决方案"的结构，显得条理清晰。

2. **实际工程中的选择**：通常 TP 用在节点内（NVLink 带宽高），PP 用在节点间，DP 覆盖所有节点。这种"分层并行"策略是业界标准做法。

3. **FSDP vs ZeRO**：PyTorch 的 FSDP (Fully Sharded Data Parallel) 本质上就是 ZeRO-3 的 PyTorch 原生实现。面试可以提到两者的关系。

---

*来源：[[sources/extra01-llm-interview-reference]]*
