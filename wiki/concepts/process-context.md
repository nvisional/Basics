---
title: 进程上下文
type: concept
tags: [os, process-concurrency, x86]
created: 2026-06-18
updated: 2026-06-18
status: done
confidence: high
sources: ["操作系统课程讨论"]
contested: false
---

# 进程上下文

## 直觉

进程上下文 = **切走时必须保存、切回来时必须恢复的所有状态**。

上下文切换不是在"复制"东西，而是把当前进程的寄存器值存到一个地方，再把另一个进程之前存的值装载回来。关键是 **CR3 一换，整个地址空间就切走了**——这是进程切换最贵的部分。

---

## 三大组成部分

```
进程上下文
│
├── 1. 硬件上下文 (CPU 寄存器现场)
│   ├── 通用寄存器 (EAX, EBX, ECX, EDX, ESI, EDI, R8-R15...)
│   ├── 指令指针 (EIP / RIP)
│   ├── 栈指针 (ESP / RSP)
│   ├── 标志寄存器 (EFLAGS / RFLAGS)
│   ├── 段寄存器 (CS, DS, SS, ES, FS, GS)
│   ├── 浮点/向量寄存器 (FPU, XMM, YMM, ZMM)
│   └── 控制寄存器 → CR3 (页目录基址)  ← 最关键！
│
├── 2. 内存上下文 (地址空间)
│   ├── 页表 (由 CR3 指向，决定整个虚拟→物理映射)
│   ├── 代码段 (text)
│   ├── 数据段 (data, bss)
│   ├── 堆 (heap)
│   ├── 每个线程的栈 (stack)
│   └── 共享库映射 (mmap)
│
└── 3. 内核上下文 (OS 维护的元数据)
    ├── 进程描述符 (PCB / task_struct)
    │   ├── PID, PPID
    │   ├── 进程状态 (running, ready, blocked, zombie...)
    │   ├── 优先级 (nice, rt_priority)
    │   └── 调度统计 (vruntime, CPU 时间...)
    ├── 打开文件表 (fd table → file → inode)
    ├── 信号处理 (signal handlers, pending signals, blocked mask)
    ├── 内核栈 (进程在内核态执行时使用的栈)
    ├── 内存管理信息 (VMA 链表/mm_tree)
    └── 命名空间 (namespace, cgroup)
```

---

## 线程切换 vs 进程切换：分层成本

| 切换类型 | 换什么 | 地址空间 | 成本 |
|---------|--------|---------|------|
| **线程切换** (同进程) | 通用寄存器、IP、SP | 不变（CR3 保留） | 便宜 |
| **进程切换** | 以上全部 + CR3 | 完全切换 | 贵！TLB 全部刷新 |

CR3 一换，页表根指针变了，TLB 里的旧映射全部作废。新进程开始执行时，TLB 全是空的需要重新填充——这就是进程切换比线程切换贵一个数量级的根本原因。

---

## 切换的实际流程

```
进程 A 切走:                       进程 B 切入:

1. 触发切换 (中断/系统调用/时间片到)
2. 把 A 的寄存器压入 A 的内核栈      6. 从 B 的内核栈弹出 B 的寄存器
3. 保存 A 的 CR3 → PCB_A           7. 从 PCB_B 加载 B 的 CR3 → 地址空间已切换
4. 保存 A 的 IP/SP → PCB_A         8. 加载 B 的 IP/SP
5. 选择下一个进程 (调度器)            9. 开始执行 B 的代码
```

上下文不是"复制数据"——就是**存当前、取历史、继续跑**。

---

## 设计权衡

### CR3 切换为什么贵？

| 后果 | 原因 |
|------|------|
| TLB flush | 旧地址空间的缓存全作废 |
| Cache miss 暴增 | 新进程的代码和数据还没进 L1/L2/L3 |
| 页表 walk 开销 | 冷启动，每次 TLB miss 要走完整页表遍历 |

硬件通过 **PCID（Process-Context Identifier）** 缓解：TLB 条目带上进程 ID 标签，切换时不清空 TLB，不同进程的条目共存。但最终切换时该冷的还是会冷。

### 为什么区分线程和进程？

线程共享地址空间（CR3 不变），所以线程切换只需要换寄存器上下文。这使得线程适合高频协作（同一个程序内部），进程适合隔离（不同程序之间）。两者在切换成本上的巨大差异，直接影响并发编程模型的选择。

---

## 关联

- [[concepts/two-level-page-table]] — 页表与 CR3 的关系
- [[concepts/page-allocation-replacement]] — 页框分配影响地址空间构成
- [[tlb]] — TLB 刷新策略、ASID、PCID
- [[scheduling]] — 调度器如何决定"切换谁"
- [[concurrency-thread-vs-process]] — 线程与进程的完整对比
