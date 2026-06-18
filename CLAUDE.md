# CLAUDE.md — 操作系统学习 Wiki Schema

本文件是 Wiki 的 Schema 层，Claude Code 在进入本目录时自动加载。
定义了 Claude 在本知识库中的行为规则、工作流程和维护约定。

---

## 三层架构

```
Raw Sources（不可变）→ Wiki（LLM 维护）→ Schema（本文件定规则）
     raw/                  wiki/              CLAUDE.md + wiki-schema.md
```

- **Raw Sources**：原始教材、讲义、文章。Claude 可读，但绝不修改。
- **Wiki**：Claude 维护的结构化 Markdown 知识库。
- **Schema**：本文件 + `wiki-schema.md` + `wiki-purpose.md`，定义规则和方向。

---

## 目录结构

```
os/
├── README.md
├── CLAUDE.md                  ← 本文件（自动加载）
├── wiki-purpose.md            ← Wiki 目标定义
├── wiki-schema.md             ← 页面类型、命名、frontmatter 规范
├── raw/                       ← Raw Sources（不可变）
│   └── YYYY-MM-DD/            ← 按日期组织
├── wiki/                      ← LLM 维护的知识库
│   ├── index.md               ← 中枢索引（LLM 每次查询的入口）
│   ├── log.md                 ← 追加式操作日志
│   ├── overview.md            ← 全局知识状态摘要
│   ├── review-queue.md        ← 待人工审核的条目
│   ├── concepts/              ← 概念节点（一个概念一个 .md）
│   ├── synthesis/             ← 跨概念总结、对比、综述
│   └── indexes/               ← 未来索引分片（>150 页时启用）
└── .claude/                   ← Claude Code 配置
```

---

## 核心操作流程

### 1. Ingest（消化新内容）

当用户讨论或提供新内容时：

1. **读 `wiki-purpose.md`** — 理解学习目标和范围
2. **读 `wiki/index.md`** — 找到可能相关的已有概念
3. **分析内容** — 识别实体、概念、与已有知识的关联点、矛盾
4. **更新 Wiki**：
   - 创建/更新概念页（`wiki/concepts/`）
   - 使用 surgical edit（精准编辑，不整页重写）
   - 更新 `wiki/index.md`
   - 追加 `wiki/log.md`
   - 必要时更新 `wiki/overview.md`
5. **标记待审核** — 不确定的内容写入 `wiki/review-queue.md`

### 2. Query（查询知识）

1. **先读 `wiki/index.md`** — 找到候选页面（从一行简述定位）
2. **只读候选页面** — 不扫描全 Wiki
3. **合成回答** — 附带 `[[wikilink]]` 引用
4. 如果回答值得保留，写入新的概念页或 synthesis 页

### 3. Lint（健康检查）

定期检查：
- **确定性检查**：断链、缺失 frontmatter、页面超限（>800 行）、孤儿页
- **语义检查**（LLM 辅助）：矛盾声明、过时内容、缺失交叉引用

---

## Claude 的职责

| 应该做 | 不应该做 |
|--------|---------|
| 维护 Wiki：将讨论整理为结构化概念页 | 擅自修改 raw/ 下的源文件 |
| 每次操作后更新 index 和 log | 整页重写已有概念（用 surgical edit） |
| 用 `[[wikilinks]]` 交叉引用 | 修改 wiki-purpose.md 或 wiki-schema.md（除非用户要求） |
| 不确定时标记为 `confidence: low` 并写入 review-queue | 把推测当事实（必须标注 confidence） |
| 解释时遵循：直觉 → 细节 → 公式/代码 | 直接给答案而不解释原理 |

---

## 写作规范

- **先给直觉，再给公式，最后给代码**
- 代码注释写"为什么"而不是"是什么"
- 每个概念页末尾必须有 `## 关联` 部分
- 预留节点（尚未创建的 `[[wikilink]]`）是合法的，lint 会列出
- 文件命名：小写英文 + 连字符

## 学习偏好

- 如果用户应该自己想，提示方向而不是直接给答案
- 强调设计权衡：为什么不选 B 方案而选 A
- 关联已学过的概念，帮助建立知识网络
