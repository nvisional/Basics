---
title: 文件系统块号 vs Cache 块号
type: concept
subject: cross
tags: [cross, os, ca, file-system, memory-hierarchy]
created: 2026-06-21
updated: 2026-06-21
status: done
confidence: high
sources: ["操作系统课程讨论"]
contested: false
---

# 文件系统块号 vs Cache 块号

## 直觉

虽然都叫"块号"，但**文件系统块号是磁盘坐标，Cache 块号是 CPU 内部 Cache 的行号。** 两个完全独立的编号系统。

---

## 两个独立的地址空间

```
CPU 发虚拟地址
    │
    └──→ MMU → 物理地址 (DRAM)
                │
                ├──→ Cache: [Tag][Index][Offset]
                │       单位: Cache Line (64B)
                │
                └──→ 文件系统: 逻辑块号 → 磁盘物理块号
                        单位: 磁盘块 (512B/4KB)
```

---

## 对比

| | 文件系统块号 | Cache 块号 |
|---|-------------|-----------|
| **属于** | 磁盘存储 | CPU Cache |
| **单位** | 512B/4KB | 64B (Cache Line) |
| **翻译者** | 文件系统 (内核) | Cache 控制器 (硬件) |
| **层级** | OS → 块设备驱动 | CPU → L1/L2/L3 → DRAM |

---

## 跨学科视角

### OS 侧
文件系统块号是 inode 翻译链的终点。

### 组成原理侧
Cache 块号是物理地址高位去除组索引后的 Tag，纯硬件。

### 联系点
磁盘数据读到 page cache (DRAM) 后，CPU 访问时才走 Cache 翻译。**同一个数据先经文件系统块号定位（软件），再经 Cache 块号定位（硬件），两次翻译完全解耦。**

---

## 能不能不用磁盘？

**可以。** tmpfs 把文件存在内存，inode 块指针直接指向 page cache 里的 DRAM 页，没有磁盘块号概念。

---

## 关联

- [[concepts/os/two-level-page-table]] — 虚拟地址 → 物理地址的又一套翻译
- [[concepts/os/logical-to-physical]] — 文件系统逻辑地址 → 物理块号
- [[concepts/os/inode-block-structure]] — inode 块指针与索引表
