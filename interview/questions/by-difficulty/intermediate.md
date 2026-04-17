---
type: interview-questions
title: "中等面试题 (Medium)"
difficulty: intermediate
created: 2026-04-17
updated: 2026-04-17
total: 32
---

# 中等面试题 (Medium)

> 面试主力题，占面试题目 60%+。需要概念清晰、能展开讨论。

---

## 架构类 (7 题)

### Q1: 详细解释 Transformer 自注意力机制的工作原理
- **来源**: [architecture](by-topic/architecture.md) Q1
- **概念页**: [[concepts/architecture/transformer]]
- **要点**: Q/K/V → 点积 → 缩放 → Softmax → 加权求和；并行性 vs RNN 序列性

### Q2: 什么是位置编码？为什么必须？列举至少两种实现方式
- **来源**: [architecture](by-topic/architecture.md) Q2
- **概念页**: [[concepts/architecture/positional-encoding]]
- **要点**: 置换不变性；Sinusoidal / Learned / RoPE

### Q3: MHA、MQA、GQA 的区别？
- **来源**: [architecture](by-topic/architecture.md) Q4
- **概念页**: [[concepts/architecture/attention-variants]]
- **要点**: K/V 头共享方式；MHA N:N:N → MQA N:1:1 → GQA N:G:G

### Q4: 比较 Encoder-Only, Decoder-Only, Encoder-Decoder 架构
- **来源**: [architecture](by-topic/architecture.md) Q5
- **概念页**: [[concepts/architecture/llm-architectures]]
- **要点**: 双向 vs 因果 vs 混合；NLU vs NLG vs Seq2Seq

### Q5: 词元化是什么？比较 BPE 和 WordPiece
- **来源**: [architecture](by-topic/architecture.md) Q7
- **概念页**: [[concepts/architecture/tokenization]]
- **要点**: 频率驱动 vs 似然驱动；子词切分解决 OOV

### Q6: 涌现能力如何理解？通常在什么规模出现？
- **来源**: [architecture](by-topic/architecture.md) Q9
- **概念页**: [[concepts/architecture/emergent-abilities]]
- **要点**: 非线性相变；CoT/ICL；62B+ 开始；存在争议

### Q7: LLM 常用的激活函数？为什么选用？
- **来源**: [architecture](by-topic/architecture.md) Q10
- **概念页**: [[concepts/architecture/activation-functions]]
- **要点**: GeLU → SwiGLU；门控机制增强表达力

## RLHF 类 (2 题)

### Q8: RLHF 旨在解决什么问题？为什么 SFT 不够？
- **来源**: [rlhf](by-topic/rlhf.md) Q1
- **概念页**: [[concepts/training/rlhf]]
- **要点**: HHH 对齐原则；SFT 教模仿不教判断；偏好标注难

### Q9: RM 训练为什么用成对比较而非绝对评分？
- **来源**: [rlhf](by-topic/rlhf.md) Q5
- **概念页**: [[concepts/training/reward-model]]
- **要点**: 认知负荷低、一致性高、信号精细

## 推理类 (1 题)

### Q10: LLM 推理阶段有哪些常见解码策略？
- **来源**: [inference](by-topic/inference.md) Q1
- **概念页**: [[concepts/inference/decoding-strategies]]
- **要点**: 确定性 (Greedy/Beam) vs 随机 (Top-K/Top-P)

## Agent 类 (10 题)

### Q11: 你如何定义一个基于 LLM 的 Agent？核心组件？
- **来源**: [agent](by-topic/agent.md) Q1
- **概念页**: [[concepts/application/agent-overview]]
- **要点**: 四大组件（大脑/规划/记忆/工具）

### Q12: 请详细解释 ReAct 框架
- **来源**: [agent](by-topic/agent.md) Q2
- **概念页**: [[concepts/application/react]]
- **要点**: Thought-Action-Observation 循环

### Q13: 如何赋予 LLM 规划能力？
- **来源**: [agent](by-topic/agent.md) Q3
- **概念页**: [[concepts/application/planning-methods]]
- **要点**: CoT → ReAct → ToT → GoT

### Q14: LLM 如何学会调用外部工具？
- **来源**: [agent](by-topic/agent.md) Q4
- **概念页**: [[concepts/application/tool-use]]
- **要点**: Function Calling 五步流程、JSON Schema

### Q15: 构建复杂 Agent 的主要挑战？
- **来源**: [agent](by-topic/agent.md) Q5
- **概念页**: [[concepts/application/agent-overview]]
- **要点**: 规划鲁棒性、评估困难、成本延迟

### Q16: 如何设计 Agent 的短期和长期记忆？
- **来源**: [agent](by-topic/agent.md) Q6
- **概念页**: [[concepts/application/agent-memory]]
- **要点**: 短期(上下文) vs 长期(向量DB/RAG)

### Q17: 比较两个 Agent 开发框架
- **来源**: [agent](by-topic/agent.md) Q7
- **概念页**: [[concepts/application/agent-frameworks]]
- **要点**: 编排驱动 vs 数据驱动

### Q18: 什么是多智能体系统？
- **来源**: [agent](by-topic/agent.md) Q8
- **概念页**: [[concepts/application/multi-agent]]
- **要点**: 分工/并行/鲁棒 vs 通信/协调

### Q19: 如何确保 Agent 行为安全可控？
- **来源**: [agent](by-topic/agent.md) Q9
- **概念页**: [[concepts/application/agent-safety]]
- **要点**: 六层保障体系

### Q20: 软件 Agent vs 具身 Agent 的本质区别？
- **来源**: [agent](by-topic/agent.md) Q10
- **概念页**: [[concepts/application/agent-overview]]
- **要点**: 感知/行动空间/实时性五个维度

## RAG 类 (8 题)

### Q21: 请解释 RAG 的工作原理
- **来源**: [rag](by-topic/rag.md) Q1
- **概念页**: [[concepts/application/rag-overview]]
- **要点**: 先检索后生成、解决知识过时/幻觉

### Q22: 完整的 RAG 流水线包含哪些关键步骤？
- **来源**: [rag](by-topic/rag.md) Q2
- **概念页**: [[concepts/application/rag-pipeline]]
- **要点**: 离线索引 + 在线推理

### Q23: 如何选择合适的切块大小和重叠长度？
- **来源**: [rag](by-topic/rag.md) Q3
- **概念页**: [[concepts/application/rag-pipeline]]
- **要点**: 依据模型/数据/查询类型，重叠10%-20%

### Q24: 什么是"Lost in the Middle"问题？
- **来源**: [rag](by-topic/rag.md) Q5
- **概念页**: [[concepts/application/retrieval-enhancement]]
- **要点**: LLM 忽略长上下文中间信息

### Q25: 如何选择嵌入模型？评估指标有哪些？
- **来源**: [rag](by-topic/rag.md) Q7
- **概念页**: [[concepts/application/embedding-models]]
- **要点**: MTEB/C-MTEB、nDCG/Recall/MRR

### Q26: 如何全面评估 RAG 系统性能？
- **来源**: [rag](by-topic/rag.md) Q8
- **概念页**: [[concepts/application/rag-eval]]
- **要点**: 检索评估 + 生成评估

### Q27: RAG 系统实际部署面临哪些挑战？
- **来源**: [rag](by-topic/rag.md) Q11
- **概念页**: [[concepts/application/rag-pipeline]]
- **要点**: 数据管道/实时更新/延迟成本

### Q28: 知道哪些开源 RAG 框架？如何选？
- **来源**: [rag](by-topic/rag.md) Q12
- **概念页**: [[concepts/application/advanced-rag]]
- **要点**: 定制→LangChain/LlamaIndex，快速→RAGFlow/Dify

## 评估类 (7 题)

### Q29: 为什么 BLEU/ROUGE 对评估 LLM 有局限性？
- **来源**: [evaluation](by-topic/evaluation.md) Q1
- **概念页**: [[concepts/evaluation/eval-metrics]]
- **要点**: 无语义理解/无法评估事实性

### Q30: 介绍几个 LLM 综合性基准测试
- **来源**: [evaluation](by-topic/evaluation.md) Q2
- **概念页**: [[concepts/evaluation/eval-metrics]]
- **要点**: MMLU/Big-Bench/HumanEval/GSM8K

### Q31: 什么是 LLM-as-a-Judge？优缺点？
- **来源**: [evaluation](by-topic/evaluation.md) Q3
- **概念页**: [[concepts/evaluation/llm-as-judge]]
- **要点**: 自动化评估、但有位置/冗长偏见

### Q32: 评估 Agent 为什么比评估 LLM 更难？
- **来源**: [evaluation](by-topic/evaluation.md) Q5
- **概念页**: [[concepts/evaluation/agent-eval]]
- **要点**: 有状态/动态环境/非确定性

### Q33: 了解哪些 Agent 基准测试？
- **来源**: [evaluation](by-topic/evaluation.md) Q6
- **概念页**: [[concepts/evaluation/agent-eval]]
- **要点**: WebArena/AgentBench/GAIA

### Q34: 什么是红队测试？
- **来源**: [evaluation](by-topic/evaluation.md) Q8
- **概念页**: [[concepts/evaluation/red-teaming]]
- **要点**: 对抗性测试发现安全漏洞

### Q35: 如何持续监控已部署的 LLM/Agent？
- **来源**: [evaluation](by-topic/evaluation.md) Q10
- **概念页**: [[concepts/evaluation/red-teaming]]
- **要点**: 日志→自动监控→人工审核→反馈闭环

---

## 答题策略

- 这是面试得分的关键区间，占题目 60%+
- 建议采用 **STAR 回答法**：概念定义 → 核心机制 → 应用场景 → 个人理解
- 遇到不确定的细节可以主动说"我不确定具体数字，但核心思路是..."
- 准备 2-3 个实际案例（如 Qwen、DeepSeek）穿插在回答中
