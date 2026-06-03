---
name: hermes-universal-pkm
description: 整合版 - Universal PKM 框架 + Hermes/Obsidian 双向同步工作流。使用统一的目录结构，支持任何内容输入，自动归档到标准化知识库。
version: 3.0.0
platforms: [linux, macos, windows]
tags: [pkm, obsidian, hermes, sync, universal, para, knowledge-management]
author: BOSS
---

# Hermes Universal PKM - 整合版知识库

**Universal PKM 框架** + **Hermes/Obsidian 双向同步** = 一套完整、统一、可协作的个人知识管理系统。

## 设计理念

```
┌─────────────────────────────────────────────────────────┐
│                    🎯 INPUT（输入层）                    │
│  任何渠道 × 任何形式 × 任何内容                           │
│  微信/飞书/CLI/OpenClaw/手动编辑                          │
└─────────────────────────┬───────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────┐
│              ⚡ PROCESS（处理层 - 智能分类）              │
│  识别内容类型 → 匹配 PKM 位置 → 自动归档 + 变更记录      │
└─────────────────────────┬───────────────────────────────┘
                          ▼
┌─────────────────────────────────────────────────────────┐
│                    📚 OUTPUT（知识层）                   │
│  Universal PKM 统一结构                                  │
│  10 Assets | 20 Resources | 30 Thoughts | 40 Projects   │
└─────────────────────────────────────────────────────────┘
```

---

## 目录结构（统一版）

```
📦 Personal-Knowledge-Base/
│
├── 📁 00 Inbox/                           # 快速捕获（任何临时内容）
│
├── 📁 10 Assets/                          # 【数字资产】
│   ├── 📋 index.md
│   ├── accounts/                          # 各类账号
│   ├── subscriptions/                     # 订阅服务
│   ├── devices/                         # 设备配置
│   └── credentials/                       # 凭证模板（安全提醒）
│
├── 📁 20 Resources/                       # 【外部资源】
│   ├── 📋 index.md
│   ├── skills/                            # ★ 技能/方法论
│   │   └── hermes-obsidian-sync/          # ★ Hermes 同步技能（原知识库内容）
│   │       ├── 📋 index.md                #     技能总览
│   │       ├── guides/                    #     原 01-基础配置 + 02-使用指南
│   │       │   ├── installation.md
│   │       │   ├── configuration.md
│   │       │   └── deployment.md
│   │       ├── issues/                    #     原 03-问题与解决
│   │       │   ├── database-locked.md
│   │       │   └── sync-conflict.md
│   │       ├── improvements/              #     原 04-优化记录
│   │       └── backups/                   #     原 05-备份恢复
│   ├── projects/                          # 开源项目/仓库
│   ├── tools/                             # 软件/工具
│   └── articles/                          # 文章/教程
│
├── 📁 30 Thoughts/                        # 【内部想法】
│   ├── 📋 index.md
│   ├── fleeting/                          # 闪念（快速捕获）
│   ├── insights/                          # 洞察（问题解决的结晶）
│   └── journals/                          # 日记/反思
│
├── 📁 40 Projects/                        # 【当前项目】
│   ├── 📋 index.md
│   └── hermes-obsidian-sync-v3/           # 示例：技能升级项目
│       ├── 📋 project-index.md
│       └── tasks/
│
├── 📁 50 Areas/                           # 【责任领域】
│   ├── work/
│   ├── learning/
│   └── tech-stack/
│
├── 📁 60 Archives/                        # 【归档】
│   ├── completed-projects/
│   └── outdated-resources/
│
├── 📁 90 MOCs/                            # 【地图】
│   ├── 📋 start-here.md                   # 新手指引
│   ├── my-assets-moc.md
│   ├── my-resources-moc.md                  # 包含所有技能导航
│   ├── my-thoughts-moc.md
│   └── my-projects-moc.md
│
└── 📁 99 System/                          # 【系统】
    ├── templates/                         # 标准模板
    │   ├── asset-entry.md
    │   ├── resource-entry.md
    │   ├── skill-entry.md                 # ★ 技能专用模板
    │   ├── thought-entry.md
    │   ├── project-index.md
    │   └── issue-resolution.md            # ★ 问题解决模板
    └── sync-config.yaml                   # 同步配置（可选）
```

---

## 内容映射规则（旧 → 新）

原 `hermes-obsidian-sync` 的内容如何融入新结构：

| 原分类 | 新位置 | 说明 |
|-------|--------|------|
| 01-基础配置/ | `20 Resources/skills/{skill-name}/guides/` | 技能的基础配置指南 |
| 02-使用指南/ | `20 Resources/skills/{skill-name}/guides/` | 技能的使用教程 |
| 03-问题与解决/ | `20 Resources/skills/{skill-name}/issues/` | 技能相关的问题记录 |
| 04-优化记录/ | `20 Resources/skills/{skill-name}/improvements/` | 技能的优化历史 |
| 05-备份恢复/ | `20 Resources/skills/{skill-name}/backups/` | 技能的备份策略 |
| 99-附件/quick-notes/ | `00 Inbox/` 或 `30 Thoughts/fleeting/` | 临时想法 |

**关键洞察**：每个 Skill 都有自己的子目录，保持完整上下文。

---

## 双向同步机制（保留并增强）

### 同步流程

```
Hermes/OpenClaw 实例          Obsidian 知识库
       ↓                              ↓
   发现问题                    用户手动编辑
   或解决技能                  或添加内容
       ↓                              ↓
   触发同步 ─────────────────→ 自动检测变更
       ↓                              ↓
   智能分类                              ↓
   （匹配 PKM 结构）←──────────────── 更新索引
       ↓                              ↓
   写入指定位置 ──────────────→ 冲突检测
       ↓                              ↓
   添加变更记录 ←────────────── 添加变更记录
       ↓                              ↓
   更新 MOC 索引 ←───────────── 双向通知
```

### 变更记录格式（强制）

每次修改必须在文档末尾添加：

```markdown
---
## 变更记录

- **时间**：2026-06-03 14:30
- **来源**：微信 Hermes / 飞书 Hermes / CLI Hermes / OpenClaw / 用户手动
- **类型**：新增 / 追加 / 更新 / 废弃
- **修改内容**：简要说明修改了什么
- **PKM 位置**：20 Resources/skills/xxx/issues/xxx.md
```

### 冲突解决策略

1. **用户手动修改** → 优先级最高
2. **Hermes/OpenClaw 自动同步** → 默认追加模式
3. **需要覆盖时** → 明确标记「更新」类型
4. **冲突发生** → 记录到文档「待处理」区域，人工决策

---

## 智能分类决策树

```
内容输入
    ↓
判断类型：
│
├── 账号/密码/订阅/设备
│   └── → 📁 10 Assets/
│       └── accounts/ | subscriptions/ | devices/
│
├── URL + 描述（技能/项目/工具/文章）
│   └── → 📁 20 Resources/
│       ├── skills/{skill-name}/       ← 技能类
│       │   ├── guides/              ← 指南文档
│       │   ├── issues/              ← 问题与解决
│       │   └── improvements/        ← 优化记录
│       ├── projects/                ← 开源项目
│       ├── tools/                   ← 软件工具
│       └── articles/                ← 文章教程
│
├── 想法/灵感/洞察/日记
│   └── → 📁 30 Thoughts/
│       ├── fleeting/                ← 闪念（快速记录）
│       ├── insights/                ← 洞察（深度思考）
│       └── journals/                ← 日记反思
│
├── 任务/目标/计划（有截止日期）
│   └── → 📁 40 Projects/
│       └── {project-name}/
│
└── 不明确/待分类
    └── → 📁 00 Inbox/
        └── 标记待整理
```

---

## 模板系统（统一版）

### 模板 1：技能条目（Skill）★ 核心模板

适用于：`20 Resources/skills/{skill-name}/`

```markdown
---
type: resource
subtype: skill
category: hermes-skill | openclaw-skill | general-skill
tags: []
date_added: YYYY-MM-DD
date_updated: YYYY-MM-DD
status: active | deprecated
---

# {skill-name}

## 简介
一句话描述这个技能是做什么的

## 目录结构
```
skills/{skill-name}/
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
- [[{skill-name}/guides/installation|安装配置]]
- [[{skill-name}/guides/usage|使用指南]]
- [[{skill-name}/issues/index|问题排查]]
- [[{skill-name}/improvements/index|优化历史]]

## 基本信息
| 项目 | 内容 |
|-----|------|
| 技能类型 | hermes-skill / openclaw-skill |
| 版本 | x.x.x |
| 源代码 | {{repo_url}} |
| 依赖 | {{dependencies}} |

## 使用场景
- 什么时候用这个技能？
- 解决什么问题？

## 相关资源
- [[相关技能 A]]
- [[相关技能 B]]
- [[相关项目]]

---
## 变更记录
- **时间**：YYYY-MM-DD
- **来源**：创建者
- **类型**：新增
- **修改内容**：创建技能文档结构
```

### 模板 2：问题解决（Issue Resolution）★ 核心模板

适用于：`20 Resources/skills/{skill-name}/issues/`

```markdown
---
type: issue
skill: {skill-name}
severity: critical | high | medium | low
tags: []
date_found: YYYY-MM-DD
date_resolved: YYYY-MM-DD
status: resolved | ongoing | pending
---

# {问题标题}

## 问题描述
{{问题现象的简要描述}}

## 环境信息
- 技能版本：{{version}}
- 操作系统：{{os}}
- 相关配置：{{config}}

## 错误信息
```
{{错误日志或提示}}
```

## 判断方法
1. {{检查步骤 1}}
2. {{检查步骤 2}}
3. {{确认问题的标志}}

## 解决方案

### 方案一（推荐）
1. {{步骤 1}}
2. {{步骤 2}}
3. {{验证方法}}

### 方案二（备选）
{{备选方案描述}}

## 失败处理
- 如果方案一失败：{{备选路径}}
- 如果方案二失败：{{回滚或寻求帮助的途径}}

## 根因分析
{{为什么会出现这个问题}}

## 预防措施
- {{如何避免再次出现}}
- {{配置建议}}

## 相关链接
- [[相关配置]]
- [[相关指南]]
- [[相关优化]]

---
## 变更记录
- **时间**：YYYY-MM-DD
- **来源**：{{who}}
- **类型**：新增
- **修改内容**：首次记录该问题及解决方案
```

### 模板 3：资产条目（Asset）

适用于：`10 Assets/accounts/`, `10 Assets/subscriptions/`

```markdown
---
type: asset
category: account | subscription | license | device
tags: []
date_added: YYYY-MM-DD
date_expires: YYYY-MM-DD
status: active | expired
---

# {asset-name}

## 基本信息
| 项目 | 内容 |
|-----|------|
| 服务名称 | {{name}} |
| 账号 | {{id}} |
| 密码位置 | {{password_manager}} |
| 2FA 状态 | {{enabled/disabled}} |
| 到期日期 | {{expiration}} |
| 费用 | {{cost}} |

## 恢复/备份
- 2FA 备份：{{backup_location}}
- 恢复邮箱：{{recovery_email}}

## 备注
{{notes}}

---
## 变更记录
```

### 模板 4：想法条目（Thought）

适用于：`30 Thoughts/fleeting/`, `30 Thoughts/insights/`

```markdown
---
type: thought
subtype: fleeting | insight
tags: []
date: YYYY-MM-DD
context: {{触发场景}}
---

# {想法标题}

## 原始记录
> {{原始输入}}

## 加工整理
- {{要点 1}}
- {{要点 2}}

## 连接
- [[相关资源]]
- [[相关技能]]

## 行动项
- [ ] {{待办}}

---
## 变更记录
```

### 模板 5：项目主页（Project）

适用于：`40 Projects/{project-name}/`

```markdown
---
type: project
status: planning | active | completed
date_started: YYYY-MM-DD
target_date: YYYY-MM-DD
tags: []
---

# {project-name}

## 目标
{{一句话描述}}

## 任务清单
- [ ] {{任务 1}}
- [ ] {{任务 2}}

## 相关资源
- [[技能 A]]
- [[技能 B]]

## 进度
- [YYYY-MM-DD] {{更新}}

## 复盘
{{完成后填写}}

---
## 变更记录
```

---

## 使用示例

### 示例 1：Hermes 发现问题并自动归档

**Hermes 输入**：
> "遇到 session file locked 错误，数据库被锁定，原因是另一个实例未释放，解决方法是删除 .session 文件并重启"

**AI 动作**：
1. 识别类型：Issue（技能问题）
2. 定位路径：`20 Resources/skills/hermes/session-file-locked.md`
3. 使用「问题解决模板」创建结构化文档
4. 添加变更记录
5. 更新技能 index.md 索引
6. 返回确认："已归档到 20 Resources/skills/hermes/issues/session-file-locked.md"

### 示例 2：用户添加新技能

**用户输入**：
> "发现个好用的 skill：https://github.com/xxx/universal-pkm，是一个通用 PKM 框架"

**AI 动作**：
1. 识别类型：Resource（技能资源）
2. 创建技能目录：`20 Resources/skills/universal-pkm/`
3. 使用「技能模板」创建 index.md
4. 创建子目录结构（guides/, issues/, improvements/）
5. 更新 20 Resources/index.md
6. 返回确认 + 快捷链接

### 示例 3：记录账号

**用户输入**：
> "GitHub Pro 订阅，账号 Rick-Hlp，到期 2026-12，$4/月，2FA 已开"

**AI 动作**：
1. 识别类型：Asset（订阅）
2. 定位路径：`10 Assets/subscriptions/github-pro.md`
3. 使用「资产模板」创建
4. 提醒："Pro 订阅 2026-12 到期"

---

## 快速命令

| 命令 | 动作 | 目标位置 |
|-----|------|---------|
| `/a` `/账号` | 添加账号 | 10 Assets/accounts/ |
| `/s` `/订阅` | 添加订阅 | 10 Assets/subscriptions/ |
| `/r` `/资源` | 添加资源 | 20 Resources/{category}/ |
| `/k` `/技能` | 添加技能 | 20 Resources/skills/{name}/ |
| `/i` `/问题` | 记录问题 | 20 Resources/skills/{name}/issues/ |
| `/t` `/想法` | 记录想法 | 30 Thoughts/fleeting/ |
| `/p` `/项目` | 创建项目 | 40 Projects/{name}/ |
| `/inbox` | 快速捕获 | 00 Inbox/ |

---

## 最佳实践

1. **统一结构**
   - 所有技能都放 `20 Resources/skills/`，保持一致的子目录结构
   - 所有问题都关联到具体技能

2. **变更记录必填**
   - 任何修改都必须添加变更记录
   - 包含来源、类型、内容、PKM 位置

3. **从 Inbox 开始**
   - 不确定分类时先放 Inbox
   - 定期（建议每日）整理 Inbox

4. **链接优于复制**
   - 一个问题解决可能在多个技能中出现 → 用链接引用
   - 保持单点真理

5. **MOC 导航**
   - 定期更新 90 MOCs/ 中的索引
   - 让每个资源都能被快速找到

---

## 迁移指南（从旧版）

如果你正在使用旧版 `hermes-obsidian-sync` 结构：

```bash
# 1. 备份现有知识库
cp -r "your-kb" "your-kb-backup"

# 2. 创建新结构（按 Universal PKM）
mkdir -p "20 Resources/skills/"

# 3. 迁移内容
mv "03-问题与解决/*" "20 Resources/skills/{skill-name}/issues/"
mv "02-使用指南/*" "20 Resources/skills/{skill-name}/guides/"
mv "04-优化记录/*" "20 Resources/skills/{skill-name}/improvements/"
mv "05-备份恢复/*" "20 Resources/skills/{skill-name}/backups/"

# 4. 更新索引
# 在每个技能的 index.md 中添加导航链接

# 5. 验证同步功能
# 测试 Hermes/OpenClaw 是否能正常写入新位置
```

---

## 版本历史

- **v3.0.0** (2026-06-03) - 整合版：Universal PKM 框架 + Hermes 双向同步
- **v2.0.0** - Hermes Obsidian Sync 增强版（双向同步、变更记录）
- **v1.0.0** - 初始版本（单向同步、基础分类）

---

**核心原则：一个结构，任何来源，统一归档，双向同步。**
