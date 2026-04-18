# LLM 面试知识库 Schema

## 目录结构

```
llm-kb-wiki/
├── CLAUDE.md                 # 本文件 - Schema 配置
├── raw/                      # 原始资料（只读）
│   ├── articles/             # 技术文章
│   ├── papers/               # 论文
│   ├── videos/               # 视频转录
│   ├── interview-exp/        # 面经
│   └── code/                 # 代码示例
├── wiki/                     # 结构化知识
│   ├── index.md              # 总索引
│   ├── log.md                # 操作日志
│   ├── concepts/             # 概念页面
│   │   ├── architecture/     # 架构相关
│   │   ├── training/         # 训练相关
│   │   ├── inference/        # 推理相关
│   │   ├── application/      # 应用相关（Agent/RAG）
│   │   └── evaluation/       # 评估相关
│   ├── entities/             # 实体页面（模型/工具/框架）
│   ├── sources/              # 来源摘要
│   ├── comparisons/          # 对比分析
│   └── maps/                 # 主题导航
└── interview/                # 面试专项
    ├── questions/            # 面试题库
    │   ├── by-topic/         # 按主题分类
    │   └── by-difficulty/    # 按难度分类
    ├── weak-points.md        # 薄弱点追踪
    ├── review-schedule.md    # 复习计划
    └── mock-records/         # 模拟面试记录
```

## Frontmatter 规范

### Wiki 页面通用字段

```yaml
---
type: <concept|entity|source|comparison|map>
title: "页面标题"
aliases: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: []
related: []
tags: []
status: <active|stub|needs-update|deprecated>
interview_frequency: <high|medium|low>
interview_difficulty: <easy|medium|hard>
---
```

### 面试题页面字段

```yaml
---
type: interview-questions
title: "面试题集标题"
category: <topic>
source: "来源标识"
total: 0
---
```

## 工作流

### 1. Ingest（知识摄入）

1. **保存原始文档** → `raw/` 对应目录（只读）
2. **创建来源摘要** → `wiki/sources/`
3. **提取概念页面** → `wiki/concepts/` 按分类存放
4. **提取实体页面** → `wiki/entities/`（模型/工具/框架）
5. **提取面试题** → `interview/questions/by-topic/`
6. **更新索引** → `wiki/index.md`
7. **记录日志** → `wiki/log.md`

### 2. Query（知识查询）

1. 查阅 `wiki/index.md` 了解结构
2. 定位相关概念/实体页面
3. 检查 `interview/questions/` 相关题目
4. 综合回答，标注面试重点
5. 发现薄弱点时提示记录

### 3. Review（复习模式）

1. 查阅 `interview/weak-points.md`
2. 根据复习计划推荐内容
3. 生成复习清单和自测题

### 4. Mock（模拟面试）

1. 确定范围和难度 → 从题库抽题
2. 逐题提问并记录
3. 评估回答 → 识别薄弱点 → 更新复习计划

### 5. Lint（维护检查）

- 链接检查：验证所有 wikilinks
- 孤立页面：找出无入链页面
- 过期内容：标记长期未更新页面
- 薄弱点：提醒长期未复习项

## 写作规范

### Wikilink 格式

- 基本：`[[concepts/architecture/transformer]]`
- 带别名：`[[concepts/architecture/transformer|Transformer]]`

### 面试频率标记

- 🔥 高频：面试几乎必问
- 🟡 中频：经常出现
- 🟢 低频：偶尔出现

### 薄弱点优先级

- 🔴 高优先级：面试重点且掌握不牢
- 🟡 中优先级：了解但不深入
- 🟢 已掌握：通过验证

## 页面类型

| 类型 | 用途 | 示例 |
|------|------|------|
| `concept` | 概念/理论/方法论 | `concepts/architecture/transformer.md` |
| `entity` | 模型/工具/框架 | `entities/qwen.md`, `entities/vllm.md` |
| `source` | 来源文档摘要 | `sources/extra01-llm-interview-reference.md` |
| `comparison` | 对比分析 | `comparisons/moe-vs-dense.md` |
| `map` | 主题导航 | `maps/model-architecture.md` |

## 不可变规则

- `raw/` 目录只读，不得修改
- 所有生成内容放入 `wiki/` 和 `interview/`
- 来源可追溯：所有信息链接到原始资料

## 当前知识库统计

- 概念页面: 29 个
- 面试题: 55 道
- 来源文档: 1 份
- 创建时间: 2026-04-17
