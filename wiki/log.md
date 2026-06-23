---
title: Wiki Log — 操作日志
type: log
subject: cross
tags: [cross, meta, log]
created: 2026-06-16
updated: 2026-06-23
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
- 新增 [[concepts/os/process-context]] — 进程上下文三大块，线程切换 vs 进程切换的成本差异
- 更新 [[concepts/os/two-level-page-table]] — 新增"虚拟地址与物理地址的先后关系"和"页表即约束"两个章节
- 强化了 CR3、页框分配、进程上下文之间的交叉引用

## [2026-06-18] restructure | 扩展为四大学科架构

- 重组目录：`concepts/{os,ca,net,ds}/` + `synthesis/{os,ca,net,ds}/`
- 重写 `CLAUDE.md`、`wiki-purpose.md`、`wiki-schema.md`、`index.md`、`overview.md`
- 新增 `subject` frontmatter 字段，统一学科代号体系
- 新增 `## 跨学科` 章节约定，同一概念多学科视角互联

## [2026-06-21] ingest | 登记 raw 资料 + 建立矢量版骨架 + 联网验证规则

- raw/ 新增 5 本教材 + 408 大纲，诊断为**扫描图片 PDF（无文字层，约 3700 页）**，全量读取不可行
- 新增 [[sources]] — 原始资料登记表 + 按 408 考纲的"矢量版"知识骨架（confidence: medium，待与大纲核对）
- 确立**按需消化**策略：查询时读 sources.md 定位，不默认重开 PDF；逐章消化后升级骨架状态
- `CLAUDE.md` 新增：raw 扫描图片约束、矢量版优先导航、**🌐 每次回答强制联网交叉验证**规则
- 现状：未读取任何 PDF（用户选择只搭框架）；OS 已有 3 概念页接入骨架

## [2026-06-21] ingest | 文件系统基础 + 同步/前驱 + 跨学科

- 新增 [[concepts/os/dentry-inode-dcache]] — 目录项、目录文件、inode 三者的磁盘与内存位置
- 新增 [[concepts/os/inode-block-structure]] — inode 号 vs 起始块号，索引表区/项/块号
- 新增 [[concepts/os/fcb]] — FCB (struct file) 与 inode/dentry 的关系
- 新增 [[concepts/os/logical-to-physical]] — 逻辑地址 → inode → 物理块号的翻译链
- 新增 [[concepts/os/sync-vs-precedence]] — 前驱关系是约束，同步是实现手段
- 新增 [[concepts/cross/file-block-vs-cache-block]] — 文件系统块号 vs Cache 块号

## [2026-06-23] ingest | CA 指令系统做题思想（ISA 即契约）

- 新增 [[concepts/ca/instruction-set-mindset]] — 二刷视角：ISA 是硬件/软件之间的契约与约束
- 三大母题思想：扩展操作码=哈夫曼分配、寻址方式=指令长/范围/访存三角、指令格式=时间换空间(RISC 为流水线铺路)
- 跨学科钩子：哈夫曼(ds)、地址重定位(os 页表即约束)、流水线(ca 第 5 章)
- 联网核对 408 指令系统题型分布（每年 1–2 选择 + 常出综合大题）
- sources.md：CA 第 4 章状态 ⚪→🟡（思想层已建，raw PDF 仍未消化）；首个 ca 概念页

## [2026-06-23] ingest | CA 标志位与加减运算（CF/OF + 统一加减 ALU）

- 新增 [[concepts/ca/flags-cf-of-addsub]] — 为什么无符号"减出负"看 CF，有符号溢出看 OF
- 核心区分两个异或门：**CF = C_out ⊕ Sub**（无符号借位，减法即进位取反）vs **OF = C_out ⊕ C_in(最高位⊕次高位)**（有符号溢出）；纠正"异或门属于 CF"的常见记串
- 统一加减 ALU：一根 Sub 线同时①取反 B ②补最低位 +1 ③翻转 CF
- 工作例 4 位 3−5：C_out=0 → CF=1(借位)、OF=0(无溢出)，两灯异结论
- index 组成原理新增"数据的表示与运算"模块（页面 10→11，ca 1→2）
- 联网核对 borrow 约定（Carry/Overflow flag - Wikipedia）

## [2026-06-23] ingest | 登记王道做题本 8 本 + 考频分析 md

- raw/ 新增 8 本王道做题本（四科 × 选择题/综合题），判定为扫描图片 PDF（~900KB/页），登记进 [[sources]] 新增"1a 做题本"类目
- 定位为**题源语料而非题库**：按需渲染单页抽取"权衡轴/母题"，不全量 OCR
- 登记 `raw/组成原理-考频分析.md`（有文字层，可直接读）进 sources "1b 文本资料"
- 该 md 存在总数差异（逐项 31 vs 标注 32）→ 记入 [[review-queue]] #1 待核
