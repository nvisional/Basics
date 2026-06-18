# Wiki Schema — 页面类型、命名与约定

本文档定义 Wiki 的页面类型、frontmatter 规范、命名约定和交叉引用规则。
Schema 由人和 LLM 共同演化。

---

## 仓库结构

```
os/                         # 仓库根目录，也是 Obsidian Vault 根
├── CLAUDE.md               # Schema 层（Claude Code 自动加载）
├── wiki-purpose.md         # Wiki 目标与学习范围
├── wiki-schema.md          # 本文件
├── raw/                    # Raw Sources（不可变，按 YYYY-MM-DD 组织）
├── wiki/
│   ├── index.md            # 中枢索引（四大学科）
│   ├── log.md              # 追加式操作日志
│   ├── overview.md         # 全局知识状态摘要
│   ├── review-queue.md     # 待人工审核条目
│   ├── concepts/           # 概念节点
│   │   ├── os/             #   操作系统
│   │   ├── ca/            #   计算机组成原理
│   │   ├── net/            #   计算机网络
│   │   └── ds/             #   数据结构
│   ├── synthesis/          # 跨概念总结与对比
│   │   ├── os/
│   │   ├── ca/
│   │   ├── net/
│   │   └── ds/
│   └── indexes/            # 未来索引分片（>150 页时启用）
└── .gitignore
```

---

## 页面类型

| 类型 | 目录 | 说明 |
|------|------|------|
| `concept` | `wiki/concepts/{subject}/` | 单一知识原子 |
| `synthesis` | `wiki/synthesis/{subject}/` | 跨概念总结、对比、综述 |
| `index` | `wiki/index.md` | 总索引，LLM 每次查询入口 |
| `overview` | `wiki/overview.md` | 全局知识状态摘要 |
| `log` | `wiki/log.md` | 追加式操作日志 |
| `review` | `wiki/review-queue.md` | 待人工审核条目 |

### 页面大小限制

- 概念页软上限：**400 行**，硬上限：**800 行**
- 超过软上限时考虑拆分为多个概念节点

---

## Frontmatter 规范

```yaml
---
title: "页面标题"
type: concept | synthesis | index | overview | log | review
subject: os | ca | net | ds | cross
tags: [os, memory-management, ...]
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: draft | in-progress | done
confidence: high | medium | low
sources: []
contested: false
---
```

### 字段说明

| 字段 | 必填 | 说明 |
|------|------|------|
| `title` | ✅ | 页面标题 |
| `type` | ✅ | 页面类型 |
| `subject` | ✅ | os / ca / net / ds / cross |
| `tags` | ✅ | 至少包含学科标签 + 模块标签 |
| `created` | ✅ | 创建日期 |
| `updated` | ✅ | 最后更新日期 |
| `status` | ✅ | draft / in-progress / done |
| `confidence` | ✅ | high / medium / low |
| `sources` | 推荐 | 来源列表 |
| `contested` | 可选 | 存在矛盾观点时 true |

---

## 学科代号

| 代号 | 含义 |
|------|------|
| `os` | 操作系统 |
| `ca` | 计算机组成原理 |
| `net` | 计算机网络 |
| `ds` | 数据结构 |
| `cross` | 跨学科概念 |

---

## 标签分类

### 学科标签
`os` `ca` `net` `ds` `cross`

### 操作系统
`memory-management` `process-concurrency` `file-system` `io-device`

### 计算机组成原理
`data-representation` `isa` `processor` `memory-hiercay` `cache` `pipeline`

### 计算机网络
`physical-link` `network-layer` `transport-layer` `application-layer` `routing`

### 数据结构
`linear` `tree` `graph` `hash` `advanced-ds`

### 通用
`x86` `arm` `riscv` `linux` `design-tradeoff` `meta`

---

## 命名约定

- **概念节点**：`{subject}/概念名.md`，如 `os/two-level-page-table.md`
- **综合页**：`{subject}/主题-overview.md`，如 `os/memory-management-overview.md`
- 文件名小写英文 + 连字符，自解释

---

## 正文结构约定

概念节点按以下结构：

1. **## 直觉** — 一句话说清概念在干什么，为什么存在
2. **## 细节** — 逐步展开机制、数据结构、流程
3. **## 关键公式/代码** — 精确的技术细节
4. **## 设计权衡** — 为什么这么做？其他方案为什么不行？
5. **## 关联** — `[[wikilinks]]` 连接相关概念
6. **## 跨学科**（可选）— 与其他三门课的联系

---

*本文件由人和 LLM 共同维护。*
