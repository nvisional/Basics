# 计算机基础 · Basics

个人计算机科学基础知识库，采用 **LLM Wiki 模式**。

> 核心理念：知识只编译一次，持续积累。不是每次查询重新推导（RAG），而是增量构建持久、交叉引用的结构化 Wiki。

## 覆盖学科

| 学科 | 代号 | 进度 |
|------|------|------|
| 操作系统 | `os` | 🟢 5% |
| 计算机组成原理 | `ca` | ⚪ 0% |
| 计算机网络 | `net` | ⚪ 0% |
| 数据结构 | `ds` | ⚪ 0% |

## 三层架构

```
Raw Sources（不可变）  →  Wiki（LLM 维护）  →  Schema（规则定义）
     raw/                    wiki/              CLAUDE.md + wiki-schema.md + wiki-purpose.md
```

## 快速导航

| 文件 | 用途 |
|------|------|
| [wiki-purpose.md](./wiki-purpose.md) | Wiki 目标与学习范围（四大学科） |
| [wiki-schema.md](./wiki-schema.md) | 页面类型、frontmatter、标签、命名 |
| [wiki/index.md](./wiki/index.md) | 中枢索引（LLM 查询入口） |
| [wiki/log.md](./wiki/log.md) | 追加式操作日志 |
| [wiki/overview.md](./wiki/overview.md) | 全局知识状态摘要 |
| [wiki/review-queue.md](./wiki/review-queue.md) | 待人工审核条目 |
| [wiki/concepts/](./wiki/concepts/) | 概念节点，按学科分目录 |

## 关键设计

- **索引优先导航**：LLM 先读 index → 定位候选页 → 只读候选内容
- **原子页面**：一个页面 = 一个概念，软 400 行 / 硬 800 行
- **Surgical Edit**：精准编辑段落，不整页重写
- **Human-in-the-Loop**：不确定项写入 review-queue
- **跨学科连接**：`[[wikilinks]]` 串联同一概念在不同学科的视角
- **Obsidian 兼容**：可直接用 Obsidian 打开

---

*详细约定见 [CLAUDE.md](./CLAUDE.md)。*
