---
type: resource
subtype: skill
category: hermes-skill | openclaw-skill | general-skill
tags: []
date_added: {{date:YYYY-MM-DD}}
date_updated: {{date:YYYY-MM-DD}}
status: active | deprecated
---

# {{skill-name}}

## 简介
{{one_sentence_description}}

## 目录结构
```
skills/{{skill-name}}/
├── 📋 index.md              # 本文件
├── guides/                  # 使用指南
│   ├── installation.md      # 安装配置
│   └── usage.md             # 使用教程
├── issues/                  # 问题与解决
│   └── issue-xxx.md
├── improvements/            # 优化记录
│   └── optimization-xxx.md
└── backups/                 # 备份恢复
    └── backup-strategy.md
```

## 快速导航
- [[{{skill-name}}/guides/installation|安装配置]]
- [[{{skill-name}}/guides/usage|使用指南]]
- [[{{skill-name}}/issues/index|问题排查]]
- [[{{skill-name}}/improvements/index|优化历史]]

## 基本信息
| 项目 | 内容 |
|-----|------|
| 技能类型 | {{skill-type}} |
| 版本 | {{version}} |
| 源代码 | {{repo_url}} |
| 依赖 | {{dependencies}} |

## 使用场景
- {{use_case_1}}
- {{use_case_2}}

## 相关资源
- [[{{related_skill_1}}]]
- [[{{related_skill_2}}]]
- [[{{related_project}}]]

---
## 变更记录
- **时间**：{{date:YYYY-MM-DD}}
- **来源**：{{source}}
- **类型**：新增
- **修改内容**：创建技能文档结构
