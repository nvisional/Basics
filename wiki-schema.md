# Wiki Schema — 页面类型、命名与约定

本文档定义 Wiki 的页面类型、frontmatter 规范、命名约定和交叉引用规则。
Schema 由人和 LLM 共同演化。

---

## 页面类型

| 类型 | 目录 | 说明 | 示例 |
|------|------|------|------|
| `concept` | `wiki/concepts/` | 单一知识原子，一个页面 = 一个概念 | `two-level-page-table.md` |
| `synthesis` | `wiki/synthesis/` | 跨概念的总结、对比、综述 | `memory-management-overview.md` |
| `index` | `wiki/index.md` | 中枢索引，LLM 每次查询的入口 | — |
| `overview` | `wiki/overview.md` | 全局知识状态摘要，ingest 后自动更新 | — |
| `log` | `wiki/log.md` | 追加式操作日志，记录每次操作 | — |
| `review` | `wiki/review-queue.md` | 待人工审核的条目（歧义、冲突、不确定项） | — |

### 页面大小限制

- 概念页软上限：**400 行**，硬上限：**800 行**
- 超过软上限时考虑拆分为多个概念节点
- Lint 强制检查硬上限

---

## Frontmatter 规范

每个页面必须包含 YAML frontmatter：

```yaml
---
title: "页面标题（中文或英文）"
type: concept | synthesis | index | overview | log | review
tags: [os, memory-management, ...]
created: YYYY-MM-DD
updated: YYYY-MM-DD
status: draft | in-progress | done
confidence: high | medium | low
sources: []           # 来源列表，尽量填写
contested: false      # 是否存在矛盾观点
---
```

### 字段说明

| 字段 | 必填 | 说明 |
|------|------|------|
| `title` | ✅ | 页面标题 |
| `type` | ✅ | 页面类型 |
| `tags` | ✅ | 标签，至少包含模块标签 |
| `created` | ✅ | 创建日期 |
| `updated` | ✅ | 最后更新日期 |
| `status` | ✅ | draft / in-progress / done |
| `confidence` | ✅ | 对内容正确性的信心 |
| `sources` | 推荐 | 来源列表，如 `["教材第3章", "讲义 p10-15"]` |
| `contested` | 可选 | 存在矛盾或争议观点时设为 true |

---

## 标签分类

| 标签 | 含义 |
|------|------|
| `os` | 操作系统核心概念 |
| `memory-management` | 内存管理 |
| `process-concurrency` | 进程与并发 |
| `file-system` | 文件系统 |
| `io-device` | I/O 与设备 |
| `networking` | 网络 |
| `virtualization` | 虚拟化 |
| `x86` | x86 架构相关 |
| `arm` | ARM 架构相关 |
| `linux` | Linux 内核实现 |
| `design-tradeoff` | 设计权衡 |
| `meta` | Wiki 元信息 |

---

## 命名约定

- **概念节点**：小写英文 + 连字符，如 `two-level-page-table.md`
- **综合页**：`模块名-overview.md`，如 `memory-management-overview.md`
- 文件名应自解释，一眼能看出内容

---

## 交叉引用规则

- 使用 `[[wikilink]]` 语法做交叉引用（Obsidian 兼容）
- 每个概念页末尾应有 `## 关联` 部分，列出相关节点
- 链接不存在的页面是合法的（预留节点），但 Lint 会列出

---

## 正文结构约定

概念节点按以下结构组织：

1. **## 直觉** — 一句话说清楚这个概念在干什么，为什么存在
2. **## 细节** — 逐步展开机制、数据结构、流程
3. **## 关键公式/代码** — 精确的技术细节
4. **## 设计权衡** — 为什么这么做？其他方案为什么不行？
5. **## 关联** — `[[wikilinks]]` 连接相关概念

---

*本文件由人和 LLM 共同维护。每次新增页面类型或修改约定时更新。*
