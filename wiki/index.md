---
title: Wiki Index — 计算机基础知识图谱
type: index
subject: cross
tags: [cross, meta, index]
created: 2026-06-16
updated: 2026-06-18
status: in-progress
confidence: high
---

# Wiki Index · 计算机基础

> **索引优先导航 (Index-First)**：Claude 每次查询必须先读本索引，从一行简述定位候选页面，再读候选内容。不扫描全 Wiki。

---

## 全局统计

| 指标 | 数值 |
|------|------|
| 总页面数 | 3 |
| 操作系统 | 3 |
| 组成原理 | 0 |
| 计算机网络 | 0 |
| 数据结构 | 0 |
| 最后更新 | 2026-06-18 |

---

## 一、操作系统  `os`

| 模块 | 进度 |
|------|------|
| Memory Management | 🔴 进行中 |
| Process & Concurrency | 🟢 已开始 |
| File System | 🟡 待开始 |
| I/O & Device | ⚪ 远期 |

### Memory Management

| 节点 | 状态 | 简述 |
|------|------|------|
| [[concepts/os/two-level-page-table]] | done | 二级页表: CR3 → PDE → PTE → PA，偏移量本质，页表即约束 |
| [[concepts/os/page-allocation-replacement]] | done | 固定/可变分配 × 局部/全局置换，2×2 矩阵，Linux 的选择 |

### Process & Concurrency

| 节点 | 状态 | 简述 |
|------|------|------|
| [[concepts/os/process-context]] | done | 上下文三大块: 硬件寄存器 + 地址空间 + PCB，CR3 切换成本 |

---

## 二、计算机组成原理  `ca`

| 模块 | 进度 |
|------|------|
| Data Representation | ⚪ 远期 |
| Instruction Set | ⚪ 远期 |
| Processor | ⚪ 远期 |
| Memory Hiercay | ⚪ 远期 |

| 节点 | 状态 | 简述 |
|------|------|------|
| *(待添加)* | — | — |

---

## 三、计算机网络  `net`

| 模块 | 进度 |
|------|------|
| Physical & Link | ⚪ 远期 |
| Network | ⚪ 远期 |
| Transport | ⚪ 远期 |
| Application | ⚪ 远期 |

| 节点 | 状态 | 简述 |
|------|------|------|
| *(待添加)* | — | — |

---

## 四、数据结构  `ds`

| 模块 | 进度 |
|------|------|
| Linear | ⚪ 远期 |
| Tree & Graph | ⚪ 远期 |
| Hash & Index | ⚪ 远期 |
| Advanced | ⚪ 远期 |

| 节点 | 状态 | 简述 |
|------|------|------|
| *(待添加)* | — | — |

---

## Synthesis · 综合

| 节点 | 状态 | 简述 |
|------|------|------|
| *(每个模块完成后写 synthesis)* | — | — |

---

## 索引扩容计划

当前 < 150 页，使用单 `index.md`。超过时按学科分片到 `wiki/indexes/`：

```
wiki/indexes/
  ├── os.md
  ├── ca.md
  ├── net.md
  └── ds.md
```

顶层 index.md 变为分片目录。

---

*Claude Code 每次新增概念时更新本索引。*
