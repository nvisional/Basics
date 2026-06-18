---
title: Wiki Index — 操作系统知识图谱
type: index
tags: [os, meta, index]
created: 2026-06-16
updated: 2026-06-18
status: in-progress
confidence: high
---

# Wiki Index · 操作系统

> **索引优先导航 (Index-First)**：Claude 每次查询必须先读本索引，从一行简述定位候选页面，再读候选页面内容。不扫描全 Wiki。
>
> 学习路线：自底向上，从硬件接口（MMU、中断）到内核抽象（进程、文件系统）。

---

## 统计

| 指标 | 数值 |
|------|------|
| 总页面数 | 3 |
| 概念节点 | 3 |
| 综合页 | 0 |
| 待审核项 | 0 |
| 最后更新 | 2026-06-18 |

---

## Memory Management · 内存管理  🔴 进行中

| 节点 | 状态 | 置信度 | 简述 |
|------|------|--------|------|
| [[concepts/two-level-page-table]] | done | high | 二级页表地址转换：CR3 → PDE → PTE → 物理地址，偏移量本质，TLB 必要性，页表即约束 |
| [[concepts/page-allocation-replacement]] | done | high | 固定/可变分配 × 局部/全局置换：三维正交矩阵，Linux 的选择 |

---

## Process & Concurrency · 进程与并发  🟢 已开始

| 节点 | 状态 | 置信度 | 简述 |
|------|------|--------|------|
| [[concepts/process-context]] | done | high | 进程上下文三大块：硬件寄存器、地址空间、内核元数据；CR3 切换成本 |

---

## File System · 文件系统  🟡 待开始

| 节点 | 状态 | 置信度 | 简述 |
|------|------|--------|------|
| *(待添加)* | — | — | — |

---

## I/O & Device · 输入输出与设备  ⚪ 远期

| 节点 | 状态 | 置信度 | 简述 |
|------|------|--------|------|
| *(待添加)* | — | — | — |

---

## Networking · 网络  ⚪ 远期

| 节点 | 状态 | 置信度 | 简述 |
|------|------|--------|------|
| *(待添加)* | — | — | — |

---

## Virtualization · 虚拟化  ⚪ 远期

| 节点 | 状态 | 置信度 | 简述 |
|------|------|--------|------|
| *(待添加)* | — | — | — |

---

## Synthesis · 综合与对比

| 节点 | 状态 | 简述 |
|------|------|------|
| *(每个模块完成后写 synthesis)* | — | — |

---

## 索引扩容计划

当前 < 150 页，使用单 `index.md`。当页面数超过 150 时，自动分片到 `wiki/indexes/`：

```
wiki/indexes/
  ├── memory-management.md
  ├── process-concurrency.md
  ├── file-system.md
  └── ...
```

顶层 index.md 变为目录指向各分片。

---

*Claude Code 每次新增概念时更新本索引。*
