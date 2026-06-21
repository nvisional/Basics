---
title: Overview — 全局知识状态
type: overview
subject: cross
tags: [cross, meta, overview]
created: 2026-06-16
updated: 2026-06-21
status: in-progress
confidence: high
---

# Overview · 计算机基础 知识全景

## 学习进度

### 操作系统

```
Memory Management     ████░░░░░░ 10%  二级页表 ✅ → 分配策略 ✅ → 虚拟内存 ⏳
Process & Concurrency ███░░░░░░░  7%  进程上下文 ✅ → 同步前驱 ✅ → 线程模型 ⏳
File System           ████░░░░░░ 10%  inode ✅ → dentry/dcache ✅ → FCB ✅ → 逻辑块翻译 ✅
I/O & Device          ░░░░░░░░░░  0%  远期
```

### 计算机组成原理

```
全模块                ░░░░░░░░░░  0%  待开始
```

### 计算机网络

```
全模块                ░░░░░░░░░░  0%  待开始
```

### 数据结构

```
全模块                ░░░░░░░░░░  0%  待开始
```

---

## 已掌握的核心概念

| 学科 | 概念 | 一句话 |
|------|------|--------|
| OS | [[concepts/os/two-level-page-table]] | 页表是内存里的数组；CR3 存字节地址，PDE/PTE 存页框号 |
| OS | [[concepts/os/page-allocation-replacement]] | 固定/可变 × 局部/全局 = 3 种有效策略 |
| OS | [[concepts/os/process-context]] | 硬件寄存器 + 地址空间 + PCB；CR3 一换全切 |
| OS | [[concepts/os/sync-vs-precedence]] | 前驱关系定义约束，同步是实现机制 |
| OS | [[concepts/os/dentry-inode-dcache]] | 索引结点=inode；目录项磁盘 vs dcache 的差异 |
| OS | [[concepts/os/inode-block-structure]] | inode 号是身份证，块号是坐标 |
| OS | [[concepts/os/fcb]] | FCB 是 struct；一个 inode 多 FCB 引用 |
| OS | [[concepts/os/logical-to-physical]] | 逻辑偏移→inode→物理块号，与 MMU 类比 |
| Cross | [[concepts/cross/file-block-vs-cache-block]] | 文件块号(磁盘) vs Cache 块号(CPU) |

---

## 知识缺口

| 缺口 | 学科 | 严重程度 |
|------|------|---------|
| 虚拟内存完整流程 | OS | 🔴 关键 |
| TLB 刷新策略 | OS/CA | 🟡 重要 |
| 多级页表（x86-64） | OS/CA | 🟡 重要 |
| 线程模型 | OS | 🟡 重要 |
| 调度算法 | OS | 🟡 重要 |

---

*Claude 每次 ingest 后更新本文。*
