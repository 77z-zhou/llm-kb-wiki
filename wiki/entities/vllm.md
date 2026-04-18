---
type: entity
title: "vLLM"
category: tool
created: 2026-04-17
updated: 2026-04-17
status: stub
tags: [推理引擎, 开源, GPU优化]
interview_frequency: medium
related_concepts: [decoding-strategies]
---

# vLLM

## 基本信息

- **开发者**：UC Berkeley 团队
- **开源协议**：Apache 2.0
- **定位**：高性能 LLM 推理和服务引擎

## 核心创新：PagedAttention

- 将 KV Cache 按"页"管理（类似操作系统虚拟内存）
- 解决传统推理中 KV Cache 的显存碎片问题
- 支持更大的 batch size，显著提升吞吐量

## 关键特性

- **Continuous Batching**：请求级别调度，新请求随时加入
- **Prefix Caching**：共享前缀的 KV Cache 复用
- **张量并行**：多 GPU 推理支持
- **多种量化支持**：AWQ, GPTQ, FP8 等

## 面试常见问题

- vLLM 的 PagedAttention 是如何工作的？
- Continuous Batching 和 Static Batching 有什么区别？
- vLLM 和 SGLang 各自的优劣势？

## 相关概念

- [[concepts/inference/decoding-strategies|解码策略]]

## 待补充

- PagedAttention 详细原理
- 与 SGLang / TensorRT-LLM 的对比
- 部署实践
