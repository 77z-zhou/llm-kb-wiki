---
type: log
title: "知识库操作日志"
created: 2026-04-17
updated: 2026-04-17
---

# 知识库操作日志

## 2026-04-17 初始化导入

### 第一阶段：核心概念导入（第1-3章）
- 导入第1章 LLM 基础 (1.1-1.16)：9 个概念页 + 架构/训练/推理题目
- 跳过第2章 VLM (2.1-2.11)：按用户要求排除
- 导入第3章 RLHF (3.1-3.6)：6 个概念页 + RLHF 题目
- 创建 wiki/index.md 索引页
- 创建 raw/interview-exp/extra01-reference-answers.md 原始引用

### 第二阶段：补全遗漏章节（第4-6章）
- 导入第4章 Agent (4.1-4.13)：8 个概念页 + 13 道面试题
- 导入第5章 RAG (5.1-5.12)：6 个概念页 + 12 道面试题
- 导入第6章 评估 (6.1-6.10)：4 个概念页 + 10 道面试题
- 更新 index.md 统计（29 概念 + 55 题目）

### 第三阶段：补全知识库结构
- 创建 CLAUDE.md Schema 配置文件
- 创建 5 个实体页面：Qwen、DeepSeek、vLLM、LangChain、LlamaIndex
- 创建 3 个对比页面：MoE vs Dense、RAG vs 微调、MHA vs MQA vs GQA
- 创建 2 个知识地图：模型架构、应用系统
- 创建 interview/weak-points.md 薄弱点追踪
- 创建 interview/review-schedule.md 4 周复习计划
- 创建 by-difficulty/ 难度分类：基础(3题)、中等(32题)、高级(12题)
- 更新 index.md 完整索引（113行）

## 当前统计

| 类别 | 数量 | 说明 |
|------|------|------|
| 概念页面 | 29 | 架构9 + 训练6 + 推理1 + 应用14 + 评估4 |
| 实体页面 | 5 | Qwen/DeepSeek/vLLM/LangChain/LlamaIndex |
| 对比页面 | 3 | MoE vs Dense / RAG vs 微调 / MHA vs GQA |
| 知识地图 | 2 | 模型架构 / 应用系统 |
| 面试题 | 55 | 基础3 + 中等32 + 高级12（另8题未明确分档） |
| 复习管理 | 2 | 薄弱点追踪 + 4周复习计划 |
| 来源文档 | 1 | Extra01 面试参考答案 |

---

*此文件记录知识库所有变更操作，每次重要更新后追加条目。*
