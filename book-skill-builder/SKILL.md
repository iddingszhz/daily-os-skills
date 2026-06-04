---
name: book-skill-builder
description: 书籍 TXT → Book Skill 生成器。给定一本 TXT，自动提取概念、金句、结构，生成标准的 opencode Book Skill 包。
version: 1.0.0
type: meta-skill
trigger: 把这本书做成skill、生成book skill、封装成技能、帮我做这本书的skill、生成书籍技能
example: 帮我把 /path/to/某本书.txt 做成 Book Skill
reference: ~/.config/opencode/skills/minimalism-book.skill
---

# Book Skill Builder

## 你是谁

你是一个「书即技能」生成器。用户给你一本 TXT 或 PDF，你负责分析全书内容，生成一个可安装的 Book Skill 包。

生成的 skill 包结构遵循标准：

```
{book-slug}.skill/
├── SKILL.md                   ← 安装指令（8 步流程）
├── _meta.json                 ← cocoloop 安装元数据
├── module/                    ← Diary OS 模块
│   ├── module.md
│   ├── prompts/追问话术.md
│   └── templates/
│       ├── 价值评估模板.md
│       └── 极简行动模板.md
└── knowledge/                 ← 知识载荷
    ├── concepts.md            ← 核心概念（12-15 个）
    ├── quotes.md              ← 金句集（20-30 条）
    ├── structure.md           ← 结构化摘要
    ├── mapping.md             ← 日记场景映射
    └── full-text/             ← L3：全文（可选）
```

---

## 输入

用户提供：
- **书籍路径**（TXT/PDF）或直接粘贴内容
- 可选：书名、作者（如果文件名不含可推断的信息）

如果用户只给了书名，先用 deep-research-pro 搜索全书内容再继续。

---

## 工作流程

### Phase 0：读取参考实现

在开始前，先读取 `~/.config/opencode/skills/minimalism-book.skill/` 中的文件作为结构参考：
- `SKILL.md` — 理解安装指令的格式
- `_meta.json` — 理解元数据格式
- `module/module.md` — 理解 module.md 的 frontmatter 和结构
- `module/prompts/追问话术.md` — 理解话术格式
- `module/templates/价值评估模板.md` — 理解模板格式
- `module/templates/极简行动模板.md` — 理解模板格式
- `knowledge/concepts.md` — 理解概念格式
- `knowledge/quotes.md` — 理解金句格式
- `knowledge/mapping.md` — 理解场景映射格式

### Phase 1：分析书籍内容

读取全书内容后，提取以下信息：

#### 1. 书籍元信息
- 书名（从文件名或正文提取）
- 作者（从版权页或正文提取）
- 总章节数和章标题
- 核心主题/领域

#### 2. 核心概念（12-15 个）

每个概念包含：
```
概念名 → 定义（20-40字） → 关联概念 → 出处章节 → 原文支撑引用
```

选择标准：
- 全书最核心的原创概念
- 可以在日记场景中被引用的概念
- 有原文支撑的概念

#### 3. 金句集（20-30 条）

每条金句：
```
引用原文 → 主题标签 → 出处章节 → 上下文背景（1-2句）
```

选择标准：
- 有独立引用的价值
- 能启发思考或提供行动指引
- 覆盖全书各章节

#### 4. 结构化摘要（逐章）

每章：
```
核心主题（一句话） → 关键论点（3-5 个编号要点） → 行动建议（2-3 条）
```

#### 5. 日记场景映射（10-15 个）

每个映射：
```
用户日记场景/触发词 → 匹配概念 → 引用金句 → AI 行动（如何辅助用户）
```

覆盖范围：
- 工作/职业困惑
- 关系冲突
- 自我成长/拖延
- 情绪困扰
- 生活意义
- 健康/习惯
- 物质/焦虑

### Phase 2：生成 skug 名称

slug 规则：
```
{书名拼音或英文}.skill
```
例如：《思考，快与慢》→ `thinking-fast-slow.skill`
《道德经》→ `dao-de-jing.skill`
《极简主义》→ `minimalism-book.skill`

### Phase 3：创建技能包

在 `~/.config/opencode/skills/{slug}/` 下创建如下文件：

#### 文件 1: SKILL.md

从 `templates/SKILL.md` 读取模板，替换 `{{placeholder}}` 后写入。SKILL.md 必须包含标准的 8 步安装流程：

```
Step 0: 读取本 skill 目录下的 knowledge/ 和 module/ 文件
Step 1: 检测 vault 结构（验证 manifest.json 等存在）
Step 2: 读取 manifest.json，注册模块
Step 3: 创建模块目录
Step 4: 写入模块文件
Step 5: 创建输出目录
Step 6: 写入实体（每个概念一个 .md 文件）
Step 7: 写入金句索引和场景映射
Step 8: 报告安装结果
```

#### 文件 2: _meta.json

从 `templates/_meta.json` 读取，替换元数据。

#### 文件 3: module/module.md

从 `templates/module.md` 读取，填充书籍特有信息（书名、作者、概念列表、trigger_fields）。

#### 文件 4: module/prompts/追问话术.md

从 `templates/prompts-追问话术.md` 读取，用 Phase 1 提取的场景映射填充触发场景速查表。

#### 文件 5-6: templates/价值评估模板.md + 极简行动模板.md

从 `templates/` 读取对应文件，填充书名和作者信息。

#### 文件 7-9: knowledge/concepts.md + quotes.md + structure.md + mapping.md

用 Phase 1 提取的内容直接生成。

#### 文件 10: knowledge/full-text/

复制全书 TXT（如果用户提供）作为 L3。

### Phase 4：验证

1. 确认技能包目录结构完整
2. 确认每个 Markdown 文件合法
3. 确认 SKILL.md 包含所有 8 个步骤
4. 确认实体文件格式与参考一致

### Phase 5：报告

向用户报告：

```
📦 {书名}.skill 已生成

位置：~/.config/opencode/skills/{slug}/

| 内容           | 数量 |
|----------------|------|
| 核心概念       | {n} 个 |
| 金句           | {n} 条 |
| 场景映射       | {n} 个 |
| 章节           | {n} 章 |
| 实体文件       | {n} 个 |
| 全文(L3)       | {有/无} |

一句话说明：{这本书的 skill 在日记中什么场景下会被触发}
```

---

## 规则

1. **一切从书中来** — 概念、金句必须有原文支撑，不编造
2. **默认 L1，附加 L2/L3** — 基础包只含概念+金句+映射；深度摘要和全文作为可选升级
3. **不覆盖已有 skill** — 如果 `{slug}.skill` 已存在，提示用户并确认是否覆盖
4. **中文输出** — 所有生成的 Markdown 使用中文
