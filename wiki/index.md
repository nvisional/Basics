---
title: Wiki Index — 计算机基础知识图谱
type: index
subject: cross
tags: [cross, meta, index]
created: 2026-06-16
updated: 2026-06-23
status: in-progress
confidence: high
---

# Wiki Index · 计算机基础

> **索引优先导航 (Index-First)**：Claude 每次查询必须先读本索引，从一行简述定位候选页面，再读候选内容。不扫描全 Wiki。
>
> **矢量版骨架**：原始教材为扫描图片 PDF，见 [[sources]] 获取按考纲的知识骨架与各章消化进度，**不要默认重开 raw/ PDF**。

---

## 全局统计

| 指标 | 数值 |
|------|------|
| 总页面数 | 11 |
| 操作系统 | 8 |
| 组成原理 | 2 |
| 计算机网络 | 0 |
| 数据结构 | 0 |
| 跨学科 | 1 |
| 最后更新 | 2026-06-23 |

---

## 一、操作系统  `os`

| 模块 | 进度 |
|------|------|
| Memory Management | 🔴 进行中 |
| Process & Concurrency | 🟢 已开始 |
| File System | 🟢 已开始 |
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
| [[concepts/os/sync-vs-precedence]] | done | 前驱关系定义"谁在前"，同步是实现手段 |

### File System

| 节点 | 状态 | 简述 |
|------|------|------|
| [[concepts/os/dentry-inode-dcache]] | done | 目录项、目录文件、inode 三者在磁盘和内存中的位置 |
| [[concepts/os/inode-block-structure]] | done | inode 号 vs 起始块号，索引表区/项/块号 |
| [[concepts/os/fcb]] | done | FCB(struct file) 与 inode/dentry 的关系，多 FCB 共享 inode |
| [[concepts/os/logical-to-physical]] | done | 逻辑地址 → inode 块指针 → 物理块号，与 MMU 翻译类比 |

---

## 二、计算机组成原理  `ca`

| 模块 | 进度 |
|------|------|
| Instruction Set | 🟢 已开始 |
| Data & ALU | 🟢 已开始 |

### 指令系统

| 节点 | 状态 | 简述 |
|------|------|------|
| [[concepts/ca/instruction-set-mindset]] | done | ISA 是契约/约束；三大母题：扩展操作码=哈夫曼、寻址=三角权衡、格式=时间换空间 |

### 数据的表示与运算

| 节点 | 状态 | 简述 |
|------|------|------|
| [[concepts/ca/flags-cf-of-addsub]] | done | CF=C_out⊕Sub(无符号借位) vs OF=C_out⊕C_in(有符号溢出)；统一加减 ALU；3−5 例 |

---

## 三、计算机网络  `net`

| 节点 | 状态 | 简述 |
|------|------|------|
| *(待添加)* | — | — |

---

## 四、数据结构  `ds`

| 节点 | 状态 | 简述 |
|------|------|------|
| *(待添加)* | — | — |

---

## 跨学科  `cross`

| 节点 | 状态 | 简述 |
|------|------|------|
| [[concepts/cross/file-block-vs-cache-block]] | done | 文件系统块号(磁盘) vs Cache 块号(CPU)，两次翻译完全解耦 |

---

*Claude Code 每次新增概念时更新本索引。*
