---
title: FCB — 文件控制块
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

# FCB — 文件控制块

## 直觉

FCB 不是代码，是**内核内存里记录"这个文件当前读写状态"的结构体**。打开时创建，关闭时销毁。同一文件被打开多次有多个 FCB，各自维护独立读写位置。

---

## Linux 里的 FCB

```c
struct file {
    loff_t    f_pos;           // 当前读写位置
    fmode_t   f_mode;          // 读写模式
    struct dentry  *f_dentry;  // 指向目录项
    struct file_operations *f_op; // 操作函数集
    atomic_t  f_count;         // 引用计数
};
```

---

## 从磁盘到用户视角

```
磁盘                              内存
────                              ────
inode 表 ──→ inode cache ──→ struct inode   ← 元数据
目录数据块 ──→ dcache ──→ struct dentry   ← 文件名
❌ 磁盘没有 ────────────→ struct file (FCB)  ← 读写状态
```

| 结构 | 磁盘上有吗 | 有几个 |
|------|-----------|--------|
| inode | ✅ | 每个文件 1 个 |
| dentry | ❌ | 每级路径 1 个 |
| FCB | ❌ | 每打开一次 1 个 |

---

## 一个 inode 可被多个 FCB 引用

```
  fd=3 → FCB-A (f_pos=0)    ┐
                             ├→ inode=42 → 数据块
  fd=5 → FCB-B (f_pos=1024) ┘
```

各自维护独立 f_pos。

---

## FCB 与 inode 的分工

```
read(fd, buf, 100)
    ├→ FCB: f_pos 在哪 (读到哪了)
    └→ inode: 块号在哪 (数据在哪)
```

---

## 关联

- [[concepts/os/dentry-inode-dcache]] — 目录项、dcache、inode cache
- [[concepts/os/inode-block-structure]] — inode 号、起始块号、索引表
- [[concepts/os/logical-to-physical]] — 逻辑地址到物理地址的翻译链
