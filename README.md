# Hermes Universal PKM

**Universal Personal Knowledge Management** + **Hermes/Obsidian Bidirectional Sync**

整合版知识库框架：统一目录结构 + 双向同步 + 智能分类

---

## 🎯 核心理念

```
任何输入 → 智能分类 → 统一归档 → 双向同步
```

- **Universal PKM**：一套目录结构，任何内容都能归档
- **Hermes Sync**：Hermes/OpenClaw 多实例自动同步
- **统一整合**：技能文档、问题解决、资源收集都在同一框架

---

## 📦 目录结构

```
Personal-Knowledge-Base/
├── 00 Inbox/                    # 快速捕获
├── 10 Assets/                   # 数字资产
│   ├── accounts/
│   ├── subscriptions/
│   └── devices/
├── 20 Resources/                # 外部资源 ⭐
│   ├── skills/                  #   技能库
│   │   └── {skill-name}/        #     每个技能独立目录
│   │       ├── guides/          #       使用指南
│   │       ├── issues/          #       问题与解决
│   │       ├── improvements/    #       优化记录
│   │       └── backups/         #       备份策略
│   ├── projects/
│   ├── tools/
│   └── articles/
├── 30 Thoughts/                 # 内部想法
│   ├── fleeting/
│   └── insights/
├── 40 Projects/                 # 当前项目
├── 50 Areas/                    # 责任领域
├── 60 Archives/                 # 归档
├── 90 MOCs/                     # 地图导航
└── 99 System/                   # 模板和配置
```

---

## 🚀 核心特性

| 特性 | 说明 |
|-----|------|
| **四大核心库** | Assets + Resources + Thoughts + Projects |
| **技能子目录** | 每个技能有自己的 guides/issues/improvements |
| **双向同步** | Hermes/OpenClaw ↔ Obsidian 自动同步 |
| **变更记录** | 每次修改强制记录来源和类型 |
| **智能分类** | AI 自动识别内容类型并归档 |
| **快速命令** | `/技能` `/问题` `/想法` `/账号` 等快捷指令 |

---

## 📋 包含模板

- `skill-entry.md` - 技能主页模板
- `issue-resolution.md` - 问题解决模板（含根因分析）
- `asset-entry.md` - 账号/订阅模板
- `resource-entry.md` - 通用资源模板
- `thought-entry.md` - 想法模板
- `project-index.md` - 项目模板

---

## 🔄 内容映射（旧版迁移）

| 旧版结构 | 新版位置 |
|---------|---------|
| 01-基础配置/ | 20 Resources/skills/{name}/guides/ |
| 02-使用指南/ | 20 Resources/skills/{name}/guides/ |
| 03-问题与解决/ | 20 Resources/skills/{name}/issues/ |
| 04-优化记录/ | 20 Resources/skills/{name}/improvements/ |
| 05-备份恢复/ | 20 Resources/skills/{name}/backups/ |

---

## 📚 相关项目

- [universal-pkm](https://github.com/Rick-Hlp/universal-pkm) - 基础 PKM 框架
- [hermes-obsidian-sync](https://github.com/Rick-Hlp/hermes-obsidian-sync) - 原版同步 skill

---

## 📜 License

MIT License
