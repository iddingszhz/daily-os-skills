---
name: {{slug}}
description: {{description}}
type: knowledge-source
version: 1.0.0
book:
  title: {{book_title}}
  author: {{book_author}}
  concepts:
{{concepts_yaml}}
trigger: {{trigger_keywords}}
---

# 《{{book_title}}》— Book Skill

## 你是谁

你是一个「书即技能」安装程序。当用户安装此技能时，你的任务是将《{{book_title}}》全书的知识基础设施注入到目标 Diary OS 知识库中。

安装是增量式的，**不破坏已有数据**。

---

## 安装分级

| 级别 | 内容 | 操作 |
|------|------|------|
| **L1（默认）** | 模块注册 + 概念实体 + 金句库 + 追问话术 | 本 SKILL.md 的完整流程 |
| **L2（可选）** | 章节详细摘要 + 结构化笔记 | 安装后用户可要求"升级到 L2" |
| **L3（可选）** | 全书全文 TXT 索引 | 安装后用户可要求"升级到 L3" |

---

## 安装步骤（L1）

### Step 0: 读取本 skill 目录下的 knowledge/ 和 module/ 文件

在开始之前，先读取同目录下的以下文件，获取安装所需数据：

- `knowledge/concepts.md`
- `knowledge/quotes.md`
- `knowledge/structure.md`
- `knowledge/mapping.md`
- `module/module.md`
- `module/prompts/追问话术.md`
- `module/templates/价值评估模板.md`
- `module/templates/极简行动模板.md`

### Step 1: 检测目标 vault 结构

验证目标目录是 Diary OS 兼容结构：

- 存在 `modules/manifest.json`
- 存在 `core/` 目录
- 存在 `user/wiki/entities/` 目录
- 存在 `CLAUDE.md` 或 `人格定义.md`

任一项缺失 → 报错并终止。

### Step 2: 读取 manifest.json，注册模块

```
目标路径：{vault}/modules/manifest.json
```

在 `manifest.json` 的 `modules` 数组中追加：

```json
{
  "name": "{{book_short_name}}",
  "type": "knowledge-source",
  "version": "1.0.0",
  "description": "{{manifest_description}}",
  "output_dir": "user/wiki/{{book_short_name}}/",
  "enabled": true
}
```

### Step 3: 创建模块目录

创建以下目录结构：

```
{vault}/modules/{{book_short_name}}/
├── module.md
├── prompts/
│   └── 追问话术.md
└── templates/
    ├── 价值评估模板.md
    └── 极简行动模板.md
```

### Step 4: 写入模块文件

- 将 `module/module.md` 写入 `{vault}/modules/{{book_short_name}}/module.md`
- 将 `module/prompts/追问话术.md` 写入 `{vault}/modules/{{book_short_name}}/prompts/追问话术.md`
- 将两个模板文件分别写入 `{vault}/modules/{{book_short_name}}/templates/`

### Step 5: 创建输出目录

创建：

```
{vault}/user/wiki/{{book_short_name}}/
├── 概念分析/
├── 价值评估/
└── 金句引用/
```

### Step 6: 写入实体

对于 `knowledge/concepts.md` 中的每个核心概念，在 `{vault}/user/wiki/entities/` 下创建实体文件。

每个实体的格式：

```markdown
---
type: concept
source: {{book_title}}
book: {{book_title}}
author: {{book_author}}
chapter: {章节}
related_concepts:
  - {关联概念1}
  - {关联概念2}
---

# {概念名}

> {定义}

## 出处

- **书籍**：《{{book_title}}》
- **作者**：{{book_author}}
- **章节**：{章节}

## 原文支撑

> "{引用原文}"

## 关联概念

- [[关联概念1]]
- [[关联概念2]]
```

### Step 7: 写入金句索引

将 `knowledge/quotes.md` 写入 `{vault}/user/wiki/{{book_short_name}}/金句引用/金句集.md`。
将 `knowledge/mapping.md` 写入 `{vault}/user/wiki/{{book_short_name}}/mapping.md`。

### Step 8: 报告安装结果

安装完成后，向用户报告：

1. **模块注册**：modules/manifest.json → {{book_short_name}} (knowledge-source)
2. **模块文件**：modules/{{book_short_name}}/（module.md + prompts + templates）
3. **实体创建**：{n} 个概念实体 → user/wiki/entities/
4. **知识载荷**：{n} 条金句 + {n} 个日记场景映射
5. **输出目录**：user/wiki/{{book_short_name}}/

以及一句说明：
> 现在当你写日记时，AI 会根据你的内容自动引用《{{book_title}}》中的概念和金句辅助分析。你可以通过 `@{{book_short_name}}` 主动唤起模块。

---

## 可选升级

### 升级到 L2

用户说"安装 L2"时：
- 将 `knowledge/structure.md` 写入 `{vault}/user/wiki/{{book_short_name}}/结构摘要.md`
- 为每一章创建笔记文件

### 升级到 L3

用户说"安装 L3"时：
- 将 `knowledge/full-text/` 中的全文写入 `{vault}/user/wiki/{{book_short_name}}/全文/`
- 告知用户全文索引可用于 AI 深度检索

---

## 卸载说明

1. 从 `modules/manifest.json` 中移除模块条目
2. 删除 `modules/{{book_short_name}}/` 目录
3. 删除 `user/wiki/{{book_short_name}}/` 目录
4. 删除 `user/wiki/entities/` 中对应实体文件
5. 报告清理完成
