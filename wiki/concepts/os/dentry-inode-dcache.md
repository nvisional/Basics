---
title: 目录项、目录文件与索引结点 — 从内存位置理解
type: concept
subject: os
tags: [os, file-system, linux]
created: 2026-06-21
updated: 2026-06-21
status: done
confidence: high
sources: ["操作系统课程讨论"]
contested: false
---

# 目录项、目录文件与索引结点

## 直觉

**索引结点就是 inode，同一个东西。** 目录文件是磁盘上一种特殊文件，它的"数据"就是一堆目录项（`<inode号, 文件名>` 对）。到了内存里，三者各有自己的缓存位置。

---

## 磁盘上的原始形态

```
磁盘分区:
┌──────────────────────────────────────────────┐
│ 超级块 │ inode 表                         │ 数据块区                │
│ super  │ [inode1][inode2]...[inodeN]     │ [块0][块1]...[块M]       │
└──────────────────────────────────────────────┘
              ↑                                  ↑
      索引结点 (inode)                    数据块 (含目录文件的数据)
```

### inode

```
磁盘 inode:
  权限 | 所有者 | 大小 | 时间戳 | [数据块指针数组]
  不存文件名！
```

### 目录文件

目录本身也是一个文件，有自己的 inode，有数据块。它的"数据"就是目录项：

```
目录文件的数据块:
┌──────────┬──────┬──────────┬──────┬──────────┬──────┐
│ inode=42 │"foo" │ inode=17 │"bar" │ inode=99 │"baz" │
└──────────┴──────┴──────────┴──────┴──────────┴──────┘
         ↑ 目录项 (directory entry) = <inode号, 文件名>
```

---

## 内存中的位置

```
内核内存 (RAM)
│
├── inode cache (索引结点缓存)     ← 哈希表
│   └── struct inode              ← 磁盘 inode 的升级版
│       有引用计数、锁、脏标记
│
├── dcache (目录项缓存)            ← 哈希表
│   └── struct dentry             ← 和磁盘目录项不是一回事
│       有父指针、子链表、关联 inode 指针
│
└── page cache (页缓存)            ← 目录文件数据块
    有了 dcache 后基本不再从这里读目录
```

### 三者的磁盘 vs 内存差异

| 结构 | 磁盘位置 | 内存位置 | 存什么 |
|------|---------|---------|--------|
| **inode** | 磁盘 inode 表 | inode cache | 文件元数据 |
| **目录文件数据块** | 数据块区 | page cache | `<inum, name>` 对 |
| **dentry** | ❌ 磁盘没有 | dcache | 文件名、父子指针、LRU |

### 磁盘目录项 vs 内存 dentry

```
磁盘上 (目录文件数据块里):         内存中 (dcache 里):
  只是 <inum, name> 对             完整树结构
                                   ├ parent dentry
                                   ├ child list
                                   ├ 关联 inode 指针
                                   └ LRU 链表节点
```

---

## 设计权衡

### dcache 存在的理由

加速路径名查找。打开 `/home/sun/foo.txt`，内核不走磁盘，直接查 dcache 哈希表 O(1)。没命中才读磁盘。

### 为什么 dentry 不在磁盘上？

dcache 里的父子指针、LRU 链是运行时热数据，断电丢弃，重启从磁盘目录文件重建即可。

---

## 关联

- [[concepts/os/inode-block-structure]] — inode 号、起始块号、索引表区
- [[concepts/os/fcb]] — FCB 与 inode/dentry 的关系
- [[concepts/os/logical-to-physical]] — 逻辑地址到物理地址的 inode 翻译链
