---
title: Wiki Log — 操作日志
type: log
subject: cross
tags: [cross, meta, log]
created: 2026-06-16
updated: 2026-06-21
status: in-progress
confidence: high
---

# Wiki Log

> 追加式操作日志。格式：`## [YYYY-MM-DD] <operation> | <标题>`
>
> Operations: `init` | `ingest` | `query` | `lint` | `restructure`

---

## [2026-06-16] init | 初始化操作系统学习 Wiki

- 创建完整 LLM Wiki 架构（三层 + 索引 + 日志 + review-queue）
- 新增 [[concepts/os/two-level-page-table]] — 二级页表地址转换全过程
- Schema: `CLAUDE.md` + `wiki-schema.md` + `wiki-purpose.md`

## [2026-06-18] ingest | 页框分配策略 + 进程上下文 + 页表约束

- 新增 [[concepts/os/page-allocation-replacement]] — 固定/可变分配 × 局部/全局置换的三维矩阵
- 新增 [[concepts/os/process-context]] — 进程上下文三大块
- 更新 [[concepts/os/two-level-page-table]] — 新增 VA/PA 先后关系和页表即约束

## [2026-06-18] restructure | 扩展为四大学科架构

- 仓库从纯 OS 扩展为 OS + 组成原理 + 网络 + 数据结构
- 重组目录、重写核心约束文件、新增 subject frontmatter

## [2026-06-21] ingest | 文件系统基础 + 同步/前驱 + 跨学科

- 新增 [[concepts/os/dentry-inode-dcache]] — 目录项、目录文件、inode 三者的磁盘与内存位置
- 新增 [[concepts/os/inode-block-structure]] — inode 号 vs 起始块号，索引表区/项/块号
- 新增 [[concepts/os/fcb]] — FCB (struct file) 与 inode/dentry 的关系
- 新增 [[concepts/os/logical-to-physical]] — 逻辑地址 → inode → 物理块号的翻译链
- 新增 [[concepts/os/sync-vs-precedence]] — 前驱关系是约束，同步是实现手段
- 新增 [[concepts/cross/file-block-vs-cache-block]] — 文件系统块号 vs Cache 块号
