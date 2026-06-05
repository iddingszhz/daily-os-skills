---
name: ren-sheng-de-zhi-hui.skill
description: 《人生的智慧》全书知识源技能——安装后在 Diary OS 中自动配置人生智慧模块、实体、金句库和追问话术
type: knowledge-source
version: 1.0.0
book:
  title: 人生的智慧
  author: 阿图尔·叔本华
  translator: 韦启昌
  concepts:
    - 人的自身
    - 人所拥有的财产
    - 人所展现的表象
    - 痛苦与无聊
    - 菲利斯特人
    - 内在丰富与外在贫乏
    - 闲暇是人生的精华
    - 幸福源自内在
    - 独处与庸俗
    - 意欲与认知
    - 健康的优先性
    - 虚荣与荣誉感
    - 财富作为城墙
    - 人生的不同阶段
    - 不喜与人交往
trigger: 人生智慧、叔本华、Schopenhauer、幸福、孤独、社交烦恼、读书笔记、知识源、安装模块
---

# 《人生的智慧》— Book Skill

## 你是谁

你是一个「书即技能」安装程序。当用户安装此技能时，你的任务是将《人生的智慧》全书的知识基础设施注入到目标 Diary OS 知识库中。

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

- `knowledge/concepts.md` — 15 个核心概念定义
- `knowledge/quotes.md` — 28 条金句
- `knowledge/structure.md` — 6 章结构化摘要
- `knowledge/mapping.md` — 14 个日记场景映射
- `module/module.md` — 模块定义
- `module/prompts/追问话术.md` — 追问策略
- `module/templates/价值评估模板.md` — 价值自评模板
- `module/templates/行动模板.md` — 行动记录模板

### Step 1: 检测目标 vault 结构

验证目标目录是 Diary OS 兼容结构：

- 存在 `modules/manifest.json`
- 存在 `core/` 目录（内有 `日记格式标准.md` 等）
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
  "name": "人生的智慧",
  "type": "knowledge-source",
  "version": "1.0.0",
  "description": "《人生的智慧》知识源——叔本华论幸福（人的自身、财产、表象、建议与格言、人生阶段）",
  "output_dir": "user/wiki/人生的智慧/",
  "enabled": true
}
```

### Step 3: 创建模块目录

创建以下目录结构：

```
{vault}/modules/人生的智慧/
├── module.md
├── prompts/
│   └── 追问话术.md
└── templates/
    ├── 价值评估模板.md
    └── 行动模板.md
```

### Step 4: 写入模块文件

- 将 `module/module.md` 写入 `{vault}/modules/人生的智慧/module.md`
- 将 `module/prompts/追问话术.md` 写入 `{vault}/modules/人生的智慧/prompts/追问话术.md`
- 将 `module/templates/价值评估模板.md` 写入 `{vault}/modules/人生的智慧/templates/价值评估模板.md`
- 将 `module/templates/行动模板.md` 写入 `{vault}/modules/人生的智慧/templates/行动模板.md`

### Step 5: 创建输出目录

创建：

```
{vault}/user/wiki/人生的智慧/
├── 概念分析/
├── 概念定义/
├── 价值评估/
└── 金句引用/
```

### Step 6: 写入实体

对于 `knowledge/concepts.md` 中的每个核心概念，在 `{vault}/user/wiki/人生的智慧/概念定义/` 下创建概念定义文件。

每个实体的格式：

```markdown
---
type: concept
source: 人生的智慧
book: 人生的智慧
author: 阿图尔·叔本华
chapter: 第X章
related_concepts:
  - 关联概念1
  - 关联概念2
---

# {概念名}

> {定义原文}

## 出处

- **书籍**：《人生的智慧》
- **作者**：阿图尔·叔本华
- **译者**：韦启昌
- **章节**：第X章

## 原文支撑

> "{原文引用}"

## 关联概念

- [[关联概念1]]
- [[关联概念2]]
```

写入如下实体文件（15 个）：

1. `人的自身.md`
2. `人所拥有的财产.md`
3. `人所展现的表象.md`
4. `痛苦与无聊.md`
5. `菲利斯特人.md`
6. `内在丰富与外在贫乏.md`
7. `闲暇是人生的精华.md`
8. `幸福源自内在.md`
9. `独处与庸俗.md`
10. `意欲与认知.md`
11. `健康的优先性.md`
12. `虚荣与荣誉感.md`
13. `财富作为城墙.md`
14. `人生的不同阶段.md`
15. `不喜与人交往.md`

### Step 7: 写入金句索引

将 `knowledge/quotes.md` 写入 `{vault}/user/wiki/人生的智慧/金句引用/金句集.md`。

将 `knowledge/mapping.md` 写入 `{vault}/user/wiki/人生的智慧/mapping.md`。

### Step 8: 报告安装结果

安装完成后，向用户报告：

1. **模块注册**：modules/manifest.json → 人生的智慧 (knowledge-source)
2. **模块文件**：modules/人生的智慧/ (module.md + prompts + templates)
3. **概念定义**：15 个 → user/wiki/人生的智慧/概念定义/
4. **知识载荷**：28 条金句 + 14 个日记场景映射
5. **输出目录**：user/wiki/人生的智慧/

以及一句说明：
> 现在当你写日记时，AI 会根据你的内容自动引用《人生的智慧》中的概念和金句辅助分析。你可以通过 `@人生的智慧` 主动唤起模块。

---

## 可选升级

### 升级到 L2

用户说"安装 L2"时：
- 将 `knowledge/structure.md` 写入 `{vault}/user/wiki/人生的智慧/结构摘要.md`
- 为每一章创建笔记文件：`{vault}/user/wiki/人生的智慧/章节笔记/第X章-{标题}.md`

### 升级到 L3

用户说"安装 L3"时：
- 将 `knowledge/full-text/` 中的全文 TXT 写入 `{vault}/user/wiki/人生的智慧/全文/`
- 告知用户全文索引可用于 AI 深度检索

---

## 卸载说明

1. 从 `modules/manifest.json` 中移除人生的智慧模块条目
2. 删除 `modules/人生的智慧/` 目录
3. 删除 `user/wiki/人生的智慧/` 目录
4. 删除 `user/wiki/人生的智慧/概念定义/` 中 15 个概念定义文件
5. 报告清理完成
