# Daily OS Skills

**Diary OS 的外置知识源（Skill）合集。**

每个 Skill 是一个完整的书籍/方法论知识包，包含概念定义、追问话术、金句库和日记场景映射。安装后 AI 自动在你的日记中引用书中概念辅助深化分析。

---

## 可用 Skill

| Skill | 类型 | 来源/用途 | 核心内容 |
|-------|------|-----------|----------|
| [minimalism-book](./minimalism-book.skill/) | 知识源 | 《极简主义》米尔本 & 尼科迪默斯 | 五大价值、锚、打包派对、简单成功方程 |
| [delay-gratification](./delay-gratification.skill/) | 知识源 | 《延迟满足》沃尔特·米歇尔 | 双系统理论、如果—就计划、心理距离、自我疏离 |
| [book-skill-builder](./book-skill-builder.skill/) | 工具 | 书籍 TXT → Book Skill 生成器 | 自动提取概念、金句、结构，生成标准 Skill 包 |

## 安装方法

### 知识源型（minimalism-book, delay-gratification）

```bash
# 1. 下载到 opencode skills 目录
cp -r minimalism-book.skill ~/.config/opencode/skills/

# 2. 在 Diary OS 中启用
# 编辑 modules/manifest.json 的 enabled 数组，加入对应模块名
```

### 工具型（book-skill-builder）

```bash
# 复制到 opencode skills 目录
cp -r book-skill-builder.skill ~/.config/opencode/skills/
```

工具型 Skill 使用时直接触发即可（如"帮我把这本书做成 Skill"），无需在 manifest.json 注册。

安装后 AI 在下次写日记时自动生效，无需额外配置。

## 结构说明

### 知识源型（Diary OS 模块）

```
XXX.skill/
├── _meta.json          ← 元信息（名称、版本、依赖检测）
├── SKILL.md            ← 行为定义（触发条件、概念关联、追问话术）
├── module/             ← Diary OS 模块文件
│   ├── module.md
│   ├── prompts/
│   │   └── 追问话术.md
│   └── templates/
└── knowledge/          ← 知识源（概念、金句、场景映射、结构说明）
    ├── concepts.md
    ├── quotes.md
    ├── mapping.md
    └── structure.md
```

### 工具型（opencode tool）

```
XXX.skill/
├── _meta.json          ← 元信息
├── SKILL.md            ← 行为定义（完整工作流）
├── templates/          ← 生成新项目用的模板文件
└── references/         ← 参考实现
```

> 注意：`knowledge/full-text/`（书籍全文）因版权原因未包含在此仓库中，如需请自行获取。

---


