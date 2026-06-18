# CLAUDE.md — 计算机基础 Wiki Schema

本文件是 Wiki 的 Schema 层，Claude Code 在进入本目录时自动加载。
定义了 Claude 在本知识库中的行为规则、工作流程和维护约定。

---

## 三层架构

```
Raw Sources（不可变）→ Wiki（LLM 维护）→ Schema（本文件 + wiki-schema.md + wiki-purpose.md）
     raw/                  wiki/
```

- **Raw Sources**：原始教材、讲义、文章。Claude 可读，绝不修改。
- **Wiki**：Claude 维护的结构化 Markdown 知识库。
- **Schema**：本文件 + `wiki-schema.md` + `wiki-purpose.md`。

---

## 四大学科

| 代号 | 学科 | 目录 |
|------|------|------|
| `os` | 操作系统 | `wiki/concepts/os/` |
| `ca` | 计算机组成原理 | `wiki/concepts/ca/` |
| `net` | 计算机网络 | `wiki/concepts/net/` |
| `ds` | 数据结构 | `wiki/concepts/ds/` |
| `cross` | 跨学科概念 | 任意，标注 `subject: cross` |

---

## 核心操作流程

### 1. Ingest（消化新内容）

当用户讨论或提供新内容时：

1. **读 `wiki-purpose.md`** — 理解学习目标和当前进度
2. **读 `wiki/index.md`** — 定位相关已有概念（必要时跨学科）
3. **分析内容** — 识别实体、概念、所属学科、与已有知识的关联、矛盾
4. **更新 Wiki**：
   - 创建/更新概念页到对应学科子目录
   - 使用 surgical edit，不整页重写
   - 更新 `wiki/index.md`、追加 `wiki/log.md`、必要时更新 `wiki/overview.md`
5. **跨学科连接** — 同一概念在多个学科的视角用 `[[wikilinks]]` 互联
6. **不确定项** → 写入 `wiki/review-queue.md`

### 2. Query（查询知识）

1. **先读 `wiki/index.md`** — 从一行简述定位候选页面
2. **只读候选页面** — 不扫描全 Wiki
3. **合成回答** — 附带 `[[wikilink]]` 引用
4. 回答值得保留 → 写入对应学科的概念页或 synthesis 页

### 3. Lint（健康检查）

- **确定性**：断链、缺失 frontmatter、页面超限（>800 行）、孤儿页
- **语义（LLM 辅助）**：矛盾声明、过时内容、缺失交叉引用、跨学科链接遗漏

---

## Claude 的职责

| 应该做 | 不应该做 |
|--------|---------|
| 维护 Wiki：将讨论整理为结构化概念页 | 擅自修改 raw/ 下的源文件 |
| 每次操作后更新 index 和 log | 整页重写已有概念（用 surgical edit） |
| 用 `[[wikilinks]]` 交叉引用，跨学科互联 | 修改 wiki-purpose.md 或 wiki-schema.md（除非用户要求） |
| 不确定时标记 `confidence: low` + 写入 review-queue | 把推测当事实 |
| 解释：直觉 → 细节 → 公式/代码 → 设计权衡 | 直接给答案而不解释原理 |

---

## 写作规范

- **先给直觉，再给公式，最后给代码**
- 代码注释写"为什么"而不是"是什么"
- 每个概念页末尾必须有 `## 关联` 部分
- 如果概念涉及其他学科，添加 `## 跨学科` 部分
- 预留节点（尚未创建的 `[[wikilink]]`）合法，lint 会列出
- 文件名：`{subject}/小写英文-连字符.md`

## 学习偏好

- 如果用户应该自己想，提示方向而不是直接给答案
- 强调设计权衡：为什么不选 B 而选 A
- 关联已学过的概念，跨学科建立知识网络
