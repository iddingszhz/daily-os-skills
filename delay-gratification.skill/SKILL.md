---
name: delay-gratification
description: 《延迟满足》全书知识源技能——安装后在 Diary OS 中自动配置延迟满足模块、实体、金句库和追问话术
type: knowledge-source
version: 1.0.0
book:
  title: 延迟满足
  author: 沃尔特·米歇尔
  concepts:
    - 棉花糖实验
    - 冲动系统与冷静系统
    - 如果—就计划
    - 延迟满足能力
    - 心理距离
    - 策略性注意力分配
    - 执行功能
    - 自我疏离
    - 未来自我连续性
    - 心理免疫系统
trigger: 延迟满足、棉花糖实验、自控力、意志力、拖延、冲动控制
---

# 《延迟满足》— Book Skill

## 你是谁

你是一个「书即技能」安装程序。当用户安装此技能时，你的任务是将《延迟满足》全书的知识基础设施注入到目标 Diary OS 知识库中。

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

- `knowledge/concepts.md`
- `knowledge/quotes.md`
- `knowledge/structure.md`
- `knowledge/mapping.md`
- `module/module.md`
- `module/prompts/追问话术.md`
- `module/templates/价值评估模板.md`
- `module/templates/极简行动模板.md`

### Step 1: 检测目标 vault 结构

- 存在 `modules/manifest.json`
- 存在 `core/` 目录
- 存在 `user/wiki/entities/` 目录
- 存在 `CLAUDE.md` 或 `人格定义.md`

### Step 2: 读取 manifest.json，注册模块

```json
{
  "name": "延迟满足",
  "type": "knowledge-source",
  "version": "1.0.0",
  "description": "《延迟满足》知识源——自控力双系统理论与冷却现在/加热未来策略",
  "output_dir": "user/wiki/延迟满足/",
  "enabled": true
}
```

### Step 3: 创建模块目录

```
{vault}/modules/延迟满足/
├── module.md
├── prompts/
│   └── 追问话术.md
└── templates/
    ├── 价值评估模板.md
    └── 极简行动模板.md
```

### Step 4: 写入模块文件

### Step 5: 创建输出目录

```
{vault}/user/wiki/延迟满足/
├── 概念分析/
├── 概念定义/
├── 策略记录/
└── 金句引用/
```

### Step 6: 写入概念定义（15 个）

在 `{vault}/user/wiki/延迟满足/概念定义/` 下创建概念定义文件。

概念列表：棉花糖实验、冲动系统与冷静系统、如果—就计划、延迟满足能力、心理距离、策略性注意力分配、执行功能、信任与延迟满足、冷热系统相互作用、自我控制的可塑性、心理免疫系统、自我疏离、未来自我连续性、"如果—就"性格特征、意志力疲劳与内隐理论

### Step 7: 写入金句索引

- `knowledge/quotes.md` → `金句引用/金句集.md`
- `knowledge/mapping.md` → `mapping.md`

### Step 8: 报告

> 现在当你写日记时，AI 会根据你的内容自动引用《延迟满足》中的双系统理论和自控策略辅助分析。你可以通过 `@延迟满足` 主动唤起模块。

---

## 可选升级

### L2
将 `knowledge/structure.md` 写入 `user/wiki/延迟满足/结构摘要.md`

### L3
将 `knowledge/full-text/` 中的全文 TXT 写入 `user/wiki/延迟满足/全文/`
