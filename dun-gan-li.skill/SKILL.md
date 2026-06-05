---
name: dun-gan-li
description: 《钝感力》全书知识源技能——安装后在 Diary OS 中自动配置钝感力模块、实体、金句库和追问话术
type: knowledge-source
version: 1.0.0
book:
  title: 钝感力
  author: 渡边淳一
  concepts:
    - 钝感力
    - 得寸进尺的才能
    - 睡眠能力
    - 自律神经
    - 有益的精神压力
    - 五大感觉的钝感
    - 唯唯诺诺对嘟嘟囔囔
    - 牙膏管效应
    - 癌症与心态
    - 恋爱的钝感力
    - 女性的强大
    - 嫉妒与讽刺的感谢
    - 适应环境的能力
    - 母爱与钝感
    - 肠胃的钝感
trigger: 钝感、迟钝的力量、钝感力、读书笔记、知识源、安装模块
---

# 《钝感力》— Book Skill

## 你是谁

你是一个「书即技能」安装程序。当用户安装此技能时，你的任务是将《钝感力》全书的知识基础设施注入到目标 Diary OS 知识库中。

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
- `knowledge/quotes.md` — 26 条金句
- `knowledge/structure.md` — 16 章结构化摘要
- `knowledge/mapping.md` — 13 个日记场景映射
- `module/module.md` — 模块定义
- `module/prompts/追问话术.md` — 追问策略
- `module/templates/价值评估模板.md` — 钝感力自评模板
- `module/templates/钝感力行动模板.md` — 行动记录模板

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
  "name": "钝感力",
  "type": "knowledge-source",
  "version": "1.0.0",
  "description": "《钝感力》知识源——迟钝的力量，不为琐事动摇的生存智慧",
  "output_dir": "user/wiki/钝感力/",
  "enabled": true
}
```

### Step 3: 创建模块目录

创建以下目录结构：

```
{vault}/modules/钝感力/
├── module.md
├── prompts/
│   └── 追问话术.md
└── templates/
    ├── 价值评估模板.md
    └── 钝感力行动模板.md
```

### Step 4: 写入模块文件

- 将 `module/module.md` 写入 `{vault}/modules/钝感力/module.md`
- 将 `module/prompts/追问话术.md` 写入 `{vault}/modules/钝感力/prompts/追问话术.md`
- 将 `module/templates/价值评估模板.md` 写入 `{vault}/modules/钝感力/templates/价值评估模板.md`
- 将 `module/templates/钝感力行动模板.md` 写入 `{vault}/modules/钝感力/templates/钝感力行动模板.md`

### Step 5: 创建输出目录

创建：

```
{vault}/user/wiki/钝感力/
├── 概念分析/
├── 概念定义/
├── 钝感力自评/
└── 金句引用/
```

### Step 6: 写入实体

对于 `knowledge/concepts.md` 中的每个核心概念，在 `{vault}/user/wiki/钝感力/概念定义/` 下创建概念定义文件。

每个实体的格式：

```markdown
---
type: concept
source: 钝感力
book: 钝感力
author: 渡边淳一
chapter: 第X部分
related_concepts:
  - 关联概念1
  - 关联概念2
---

# {概念名}

> {定义原文}

## 出处

- **书籍**：《钝感力》
- **作者**：渡边淳一
- **章节**：第X部分

## 原文支撑

> "{原文引用}"

## 关联概念

- [[关联概念1]]
- [[关联概念2]]
```

写入如下实体文件（15 个）：

1. `钝感力.md`
2. `得寸进尺的才能.md`
3. `睡眠能力.md`
4. `自律神经.md`
5. `有益的精神压力.md`
6. `五大感觉的钝感.md`
7. `唯唯诺诺对嘟嘟囔囔.md`
8. `牙膏管效应.md`
9. `癌症与心态.md`
10. `恋爱的钝感力.md`
11. `女性的强大.md`
12. `嫉妒与讽刺的感谢.md`
13. `适应环境的能力.md`
14. `母爱与钝感.md`
15. `肠胃的钝感.md`

### Step 7: 写入金句索引

将 `knowledge/quotes.md` 写入 `{vault}/user/wiki/钝感力/金句引用/金句集.md`。

将 `knowledge/mapping.md` 写入 `{vault}/user/wiki/钝感力/mapping.md`。

### Step 8: 报告安装结果

安装完成后，向用户报告：

1. **模块注册**：modules/manifest.json → 钝感力 (knowledge-source)
2. **模块文件**：modules/钝感力/ (module.md + prompts + templates)
3. **概念定义**：15 个 → user/wiki/钝感力/概念定义/
4. **知识载荷**：26 条金句 + 13 个日记场景映射
5. **输出目录**：user/wiki/钝感力/

以及一句说明：
> 现在当你写日记时，AI 会根据你的内容自动引用《钝感力》中的概念和金句辅助分析。你可以通过 `@钝感力` 主动唤起模块。

---

## 可选升级

### 升级到 L2

用户说"安装 L2"时：
- 将 `knowledge/structure.md` 写入 `{vault}/user/wiki/钝感力/结构摘要.md`
- 为每一章创建笔记文件：`{vault}/user/wiki/钝感力/章节笔记/第X部分-{标题}.md`

### 升级到 L3

用户说"安装 L3"时：
- 将 `knowledge/full-text/` 中的全文 TXT 写入 `{vault}/user/wiki/钝感力/全文/`
- 告知用户全文索引可用于 AI 深度检索

---

## 卸载说明

1. 从 `modules/manifest.json` 中移除钝感力模块条目
2. 删除 `modules/钝感力/` 目录
3. 删除 `user/wiki/钝感力/` 目录
4. 删除 `user/wiki/钝感力/概念定义/` 中 15 个概念定义文件
5. 报告清理完成
