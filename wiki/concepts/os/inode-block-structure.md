---
title: inode 号、起始块号与索引表结构
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

# inode 号、起始块号与索引表结构

## 直觉

**inode 号是身份证号，起始块号是 GPS 坐标，索引表区是块号指针的仓库。**

---

## inode 号

**标识符，不是地址。** 每个文件在文件系统内唯一：

```
目录项:  ["foo.txt", inode=42]

inode 磁盘地址 = inode 表起始地址 + (inode号 - 1) × inode大小
```

---

## 起始块号

**物理地址。** 存在 inode 内部：

```
inode=42:
  direct[0] = 块号 500   ← 数据从第 500 号磁盘块开始
  direct[1] = 块号 1023
```

---

## 索引表区、索引表项、索引表项的块号

### inode 的块指针结构

```
直接区:  direct[0..11]    各存一个物理块号
间接区:  indirect         → 指向一级索引表 (装满块号的磁盘块)
         double_indirect  → 指向二级索引表
         triple_indirect  → 指向三级索引表
```

### 索引表区

专门用来存块号的磁盘块，不存文件数据。一个 4KB 索引表装 1024 个 4 字节块号。

### 索引表项

索引表区里的一个槽位，存一个块号。

### 索引表项的块号

就是索引表项里存的那个数字。如 `索引表项[2] = 799` 表示文件第 14 个逻辑块在物理块 799。

---

## 三者对比

| | inode 号 | 起始块号 | 索引表项的块号 |
|---|---------|---------|-------------|
| **是什么** | 身份证号 | 数据物理坐标 | 间接物理坐标 |
| **存在哪** | 目录项里 | inode direct[] | 索引表区块里 |

---

## 为什么分两层

```
文件名 → inode号 → inode → 块号 → 数据
(目录项)  (身份)   (档案)  (物理位置) (内容)
```

分两层：移动数据块只改 inode 里的块号，文件名和 inode 号不变。

---

## 关联

- [[concepts/os/dentry-inode-dcache]] — 目录项、dcache 的内存位置
- [[concepts/os/fcb]] — FCB 与 inode 的关系
- [[concepts/os/logical-to-physical]] — 逻辑地址到物理地址的翻译链
