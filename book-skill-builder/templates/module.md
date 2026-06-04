---
name: {{book_short_name}}
type: knowledge-source
version: 1.0.0
book_title: {{book_title}}
book_author: {{book_author}}
description: {{description}}
trigger_fields:
{{trigger_fields}}
depends_on: []
output_dir: user/wiki/{{book_short_name}}/
concepts:
{{concepts_list}}
knowledge_base: {{slug}}
---

# {{book_short_name}} — 知识源模块

## 触发逻辑

1. 写日记时扫描用户输入，匹配 mapping.md 中定义的场景关键词
2. 匹配成功 → 读取对应概念和金句 → 以自然方式融入回应
3. 匹配失败但用户 mood ≤ 3 或写了相关情绪词 → 主动建议自评
4. 周报/月报时纳入 {{book_short_name}} 维度分析

## 输出目录

- `user/wiki/{{book_short_name}}/概念分析/`
- `user/wiki/{{book_short_name}}/价值评估/`
- `user/wiki/{{book_short_name}}/金句引用/`

## 交互边界

- 不主动推销书中观点（只有在用户话题匹配时才引用）
- 引用必须标明出处（标注章节）
- 不做价值判断
