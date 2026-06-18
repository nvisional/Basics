---
title: Wiki Log — 操作日志
type: log
subject: cross
tags: [cross, meta, log]
created: 2026-06-16
updated: 2026-06-18
status: in-progress
confidence: high
---

# Wiki Log

> 追加式操作日志（Append-Only）。格式：`## [YYYY-MM-DD] <operation> | <标题>`
>
> Operations: `init` | `ingest` | `query` | `lint` | `restructure`

---

## [2026-06-16] init | 初始化操作系统学习 Wiki

- 创建完整 LLM Wiki 架构（三层 + 索引 + 日志 + review-queue）
- 新增 [[concepts/two-level-page-table]] — 二级页表地址转换全过程
- Schema: `CLAUDE.md` + `wiki-schema.md` + `wiki-purpose.md`

## [2026-06-18] ingest | 页框分配策略 + 进程上下文 + 页表约束

- 新增 [[concepts/page-allocation-replacement]] — 固定/可变分配 × 局部/全局置换的三维矩阵
- 新增 [[concepts/process-context]] — 进程上下文三大块，线程切换 vs 进程切换的成本差异
- 更新 [[concepts/two-level-page-table]] — 新增"虚拟地址与物理地址的先后关系"和"页表即约束"两个章节
- 强化了 CR3、页框分配、进程上下文之间的交叉引用

## [2026-06-18] restructure | 扩展为四大学科架构

- 仓库从纯 OS 扩展为 OS + 组成原理 + 网络 + 数据结构
- 重组目录：`concepts/{os,ca,net,ds}/` + `synthesis/{os,ca,net,ds}/`
- 重写 `CLAUDE.md`、`wiki-purpose.md`、`wiki-schema.md`、`index.md`、`overview.md`
- 新增 `subject` frontmatter 字段，统一学科代号体系
- 新增 `## 跨学科` 章节约定，同一概念多学科视角互联
