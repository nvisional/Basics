# 操作系统学习知识库

个人操作系统学习知识库，采用 **LLM Wiki 模式**（Andrej Karpathy, 2026）。

> 核心理念：知识只编译一次，持续积累。不是每次查询重新推导（RAG），而是增量构建持久的、交叉引用的结构化 Wiki。

## 三层架构

```
Raw Sources（不可变）  →  Wiki（LLM 维护）  →  Schema（规则定义）
     raw/                    wiki/              CLAUDE.md + wiki-schema.md
```

| 层 | 目录 | 说明 |
|----|------|------|
| Raw Sources | `raw/` | 原始教材、讲义、文章，LLM 只读不写 |
| Wiki | `wiki/` | LLM 维护的结构化 Markdown 知识库 |
| Schema | `CLAUDE.md` `wiki-schema.md` `wiki-purpose.md` | 定义页面类型、命名、frontmatter、工作流 |

## 快速导航

| 文件 | 用途 |
|------|------|
| [wiki-purpose.md](./wiki-purpose.md) | Wiki 目标定义（学习范围、优先级） |
| [wiki-schema.md](./wiki-schema.md) | 页面类型、frontmatter 规范、命名约定 |
| [wiki/index.md](./wiki/index.md) | 中枢索引（LLM 查询入口） |
| [wiki/log.md](./wiki/log.md) | 追加式操作日志 |
| [wiki/overview.md](./wiki/overview.md) | 全局知识状态摘要 |
| [wiki/review-queue.md](./wiki/review-queue.md) | 待人工审核条目 |
| [wiki/concepts/](./wiki/concepts/) | 概念节点（每个知识原子一个 .md） |
| [wiki/synthesis/](./wiki/synthesis/) | 跨概念总结与对比 |

## 学习模块

| 模块 | 进度 | 状态 |
|------|------|------|
| Memory Management | 5% | 🔴 进行中 |
| Process & Concurrency | 0% | 🟡 待开始 |
| File System | 0% | 🟡 待开始 |
| I/O & Device | 0% | ⚪ 远期 |
| Networking | 0% | ⚪ 远期 |
| Virtualization | 0% | ⚪ 远期 |

## 关键设计

- **索引优先导航**：Claude 先读 index → 定位候选页 → 只读候选内容，不扫全 Wiki
- **原子页面**：一个页面 = 一个概念，软上限 400 行，硬上限 800 行
- **Surgical Edit**：更新页面时精准编辑目标段落，不整页重写
- **Human-in-the-Loop**：LLM 标记不确定项到 review-queue，人审核后入 Wiki
- **索引分片**：<150 页用单 index，超过后自动分片到 `wiki/indexes/`
- **Obsidian 兼容**：`[[wikilinks]]` + YAML frontmatter，可直接用 Obsidian 打开

---

*详细约定见 [CLAUDE.md](./CLAUDE.md)。*
