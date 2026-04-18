---
type: concept
title: "嵌入模型选择与评估"
category: application
sources: [extra01-5.4]
interview_frequency: 中频
interview_difficulty: 中等
related: [rag-overview, rag-pipeline]
---

# 嵌入模型选择与评估

## 选择方法

### 1. 参考排行榜
- **MTEB** (Massive Text Embedding Benchmark)：最权威的英文排行榜
- **C-MTEB**：中文专用排行榜
- 关注 **Retrieval 任务**的得分

### 2. 考虑具体场景
- **领域特异性**：专业领域可用领域微调的嵌入模型
- **语言支持**：确保覆盖业务语言
- **模型大小 vs 速度**：大模型效果好但推理慢

### 3. 私有 vs 开源

| 类型 | 代表 | 优点 | 缺点 |
|:-----|:-----|:-----|:-----|
| 私有 | OpenAI Ada | 性能强，使用方便 | 数据隐私风险，成本高 |
| 开源 | BGE, M3E, Jina | 本地部署，安全可控 | 需自行维护 |

## 评估指标

| 任务 | 核心指标 | 衡量内容 |
|:-----|:---------|:---------|
| **检索** | nDCG@k, Recall@k, MRR | 检索结果的相关性和排名 |
| 语义相似度 | Spearman/Pearson 相关系数 | 向量相似度与人类判断的一致性 |
| 分类 | Accuracy | 嵌入向量作为特征的质量 |
| 聚类 | V-measure | 语义相似文本能否自然聚集 |

## 补充见解

- **嵌入模型是 RAG 的基石**：检索质量的上限由嵌入模型决定
- **中文场景推荐 BGE 系列**（智源）：在 C-MTEB 上表现优秀且开源
- **多语言场景考虑 multilingual-e5 或 M3E**：跨语言检索能力好
