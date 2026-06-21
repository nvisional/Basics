---
title: 逻辑地址到物理地址 — inode 翻译链
type: concept
subject: os
tags: [os, file-system]
created: 2026-06-21
updated: 2026-06-21
status: done
confidence: high
sources: ["操作系统课程讨论"]
contested: false
---

# 逻辑地址到物理地址 — inode 翻译链

## 直觉

程序从头到尾只看得见逻辑地址（文件偏移量）。物理块号藏在 inode 里。这和 MMU 翻译是两套独立的系统，但逻辑一样——**上层发偏移，下层查表找出真正的物理坐标。**

---

## 翻译过程

```
程序能拿到的                    文件系统在 inode 里查的
─────────────                  ────────────────────
fd + offset                    offset ÷ 块大小 = 逻辑块号
"从文件第 5000 字节开始读"   →   5000/4096 = 第 1 个逻辑块
                               5000%4096 = 偏移 904 字节
                                      │
                               inode 块指针[逻辑块号]
                                      │
                                      ├→ 直接区 → 拿块号
                                      ├→ 间接区 → 查索引表拿块号
                                      │
                                      └→ 物理块号 → 发起磁盘 I/O
```

## 步骤

```
1. read(fd, buf, 100)    → FCB 记录 f_pos
2. FCB → f_dentry → inode → 块指针数组
3. 计算逻辑块号 → 查直接/间接区 → 得物理块号
4. 发起 I/O → 数据返回
5. FCB.f_pos += 100
```

---

## 和虚拟地址翻译的类比

| | 虚拟地址 → 物理地址 | 文件偏移 → 磁盘块号 |
|---|-------------------|-------------------|
| **翻译器** | MMU (硬件) | 文件系统 (内核代码) |
| **页表/索引** | 页表 (PDE/PTE) | inode 块指针 + 索引表 |
| **缓存** | TLB | page cache |
| **缺页/缺块** | Page Fault | 读磁盘 |

都是"上层逻辑坐标，下层查表找物理坐标"的间接寻址。

---

## 关联

- [[concepts/os/two-level-page-table]] — 虚拟地址的页表翻译 (MMU 侧)
- [[concepts/os/inode-block-structure]] — inode 号、起始块号、索引表
- [[concepts/os/fcb]] — FCB 在翻译链中的角色
