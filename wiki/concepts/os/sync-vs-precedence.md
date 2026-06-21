---
title: 同步与前驱关系
type: concept
subject: os
tags: [os, process-concurrency, design-tradeoff]
created: 2026-06-21
updated: 2026-06-21
status: done
confidence: high
sources: ["操作系统课程讨论"]
contested: false
---

# 同步与前驱关系

## 直觉

**前驱关系定义"谁必须在谁前面"，同步是实现前驱关系的手段。** 一个是约束（问题），一个是机制（解）。

---

## 前驱关系

由数据依赖天然决定的声明性约束：

```
S1: a = x + 1;
S2: b = a * 2;      ← S1 → S2 (用到 a)
S3: c = a + b;      ← S1 → S3, S2 → S3
S4: print(c);       ← S3 → S4

DAG: S1 → S2 → S4 → S6
       ↘     ↗
         → S3 → S5
```

---

## 同步

实现前驱关系的操作机制：

```
S1: 做完 → sem_post(&s);
S2: 等待 → sem_wait(&s);
```

---

## 对比

| | 前驱关系 | 同步 |
|---|---------|------|
| **是什么** | 约束 (A 在 B 前) | 机制 (怎么让 B 等 A) |
| **来源** | 数据依赖 | 程序员/编译器插入 |
| **表达** | DAG | 信号量、锁、条件变量 |

---

## 例子

```
生产者写完，消费者才能读。

前驱: write → read
同步: semaphore full = 0;
      生产者: write(data); sem_post(&full);
      消费者: sem_wait(&full); read(data);
```

---

## 关联

- [[concepts/os/process-context]] — 进程切换是同步机制的底层支撑
- [[scheduling]] — 调度影响同步等待的公平性
