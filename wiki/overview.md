---
title: Overview — 全局知识状态
type: overview
subject: cross
tags: [cross, meta, overview]
created: 2026-06-16
updated: 2026-06-18
status: in-progress
confidence: high
---

# Overview · 计算机基础 知识全景

> 全局知识状态摘要，每次 ingest 后更新。

---

## 学习进度

### 操作系统

```
Memory Management     ████░░░░░░ 10%  二级页表 ✅ → 分配策略 ✅ → 虚拟内存 ⏳
Process & Concurrency ██░░░░░░░░  5%  进程上下文 ✅ → 线程模型 ⏳
File System           ░░░░░░░░░░  0%  待开始
I/O & Device          ░░░░░░░░░░  0%  远期
```

### 计算机组成原理

```
Data Representation   ░░░░░░░░░░  0%  待开始
Instruction Set       ░░░░░░░░░░  0%  待开始
Processor             ░░░░░░░░░░  0%  待开始
Memory Hiercay      ░░░░░░░░░░  0%  待开始
```

### 计算机网络

```
Physical & Link       ░░░░░░░░░░  0%  待开始
Network               ░░░░░░░░░░  0%  待开始
Transport             ░░░░░░░░░░  0%  待开始
Application           ░░░░░░░░░░  0%  待开始
```

### 数据结构

```
Linear                ░░░░░░░░░░  0%  待开始
Tree & Graph          ░░░░░░░░░░  0%  待开始
Hash & Index          ░░░░░░░░░░  0%  待开始
Advanced              ░░░░░░░░░░  0%  待开始
```

---

## 已掌握的核心概念

| 学科 | 概念 | 一句话 |
|------|------|--------|
| OS | [[concepts/os/two-level-page-table]] | 页表是内存里的数组；CR3 存字节地址，PDE/PTE 存页框号；页表不指向别处 |
| OS | [[concepts/os/page-allocation-replacement]] | 固定/可变 × 局部/全局 = 3 种有效策略 |
| OS | [[concepts/os/process-context]] | 硬件寄存器 + 地址空间 + PCB；CR3 一换地址空间全切 |

---

## 知识缺口

| 缺口 | 学科 | 严重程度 |
|------|------|---------|
| 虚拟内存完整流程 | OS | 🔴 关键 |
| TLB 刷新策略 | OS/Arch | 🟡 重要 |
| 多级页表（x86-64） | OS/Arch | 🟡 重要 |
| 线程模型 | OS | 🟡 重要 |
| 调度算法 | OS | 🟡 重要 |

---

*Claude 每次 ingest 后更新本文。*
