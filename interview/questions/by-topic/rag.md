---
type: interview-questions
title: "RAG 面试题"
category: rag
source: extra01-第5章
total: 12
---

# RAG 面试题

## 🔥 高频题

### Q1. 请解释 RAG 的工作原理。与微调相比有什么优势？(5.1)
- **难度**：中等
- **概念页**：[rag-overview](../../wiki/concepts/application/rag-overview.md)
- **要点**：先检索后生成、解决知识过时/幻觉/缺乏领域知识、RAG vs 微调对比

### Q2. 完整的 RAG 流水线包含哪些关键步骤？(5.2)
- **难度**：中等
- **概念页**：[rag-pipeline](../../wiki/concepts/application/rag-pipeline.md)
- **要点**：离线索引(加载→切块→嵌入→存储) + 在线推理(查询→检索→重排→生成)

### Q3. 如何选择合适的切块大小和重叠长度？(5.3)
- **难度**：中等
- **概念页**：[rag-pipeline](../../wiki/concepts/application/rag-pipeline.md)
- **要点**：依据嵌入模型/数据类型/查询类型，大块vs小块权衡，重叠10%-20%

### Q4. 除了基础向量检索，还有哪些提升检索质量的技术？(5.5)
- **难度**：中高
- **概念页**：[retrieval-enhancement](../../wiki/concepts/application/retrieval-enhancement.md)
- **要点**：混合搜索、重排序(Cross-Encoder)、Query改写(Multi-Query/HyDE/Sub-Query)、小块引用大块

### Q5. 什么是"Lost in the Middle"问题？(5.6)
- **难度**：中等
- **概念页**：[retrieval-enhancement](../../wiki/concepts/application/retrieval-enhancement.md)
- **要点**：LLM 忽略长上下文中间信息、文档重排序/减少数量/指令化提示/微调

### Q6. 搜索系统和 RAG 有什么区别？(5.11)
- **难度**：低
- **概念页**：[rag-overview](../../wiki/concepts/application/rag-overview.md)
- **要点**：找文档 vs 给答案、文档列表 vs 自然语言答案、搜索系统是 RAG 的子集

## 🟡 中频题

### Q7. 如何选择嵌入模型？评估指标有哪些？(5.4)
- **难度**：中等
- **概念页**：[embedding-models](../../wiki/concepts/application/embedding-models.md)
- **要点**：MTEB/C-MTEB 排行榜、nDCG@k/Recall/MRR、私有vs开源

### Q8. 如何全面评估 RAG 系统性能？(5.7)
- **难度**：中等
- **概念页**：[rag-eval](../../wiki/concepts/application/rag-eval.md)
- **要点**：检索评估(Precision/Recall/nDCG) + 生成评估(Faithfulness/Relevancy)

### Q9. 什么时候用知识图谱替代向量数据库？(5.8)
- **难度**：中高
- **概念页**：[advanced-rag](../../wiki/concepts/application/advanced-rag.md)
- **要点**：多跳推理/强结构数据/高可解释性、通常是互补增强而非替代

### Q10. 了解哪些高级 RAG 范式？(5.9)
- **难度**：高
- **概念页**：[advanced-rag](../../wiki/concepts/application/advanced-rag.md)
- **要点**：迭代式(Self-RAG)、自适应(FLARE)、多源数据 RAG

### Q11. RAG 系统实际部署面临哪些挑战？(5.10)
- **难度**：中等
- **概念页**：[rag-pipeline](../../wiki/concepts/application/rag-pipeline.md)
- **要点**：数据管道复杂/实时更新/延迟成本/无答案处理/安全隐私

### Q12. 知道哪些开源 RAG 框架？如何选？(5.12)
- **难度**：中等
- **概念页**：[advanced-rag](../../wiki/concepts/application/advanced-rag.md)
- **要点**：定制→LangChain/LlamaIndex、快速原型→RAGFlow/Dify
