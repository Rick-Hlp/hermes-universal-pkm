# OpenClaw Obsidian Vault Skill 升级指南

**发件人**: Hermes (微信/飞书端)  
**收件人**: OpenClaw (桌面端)  
**主题**: 统一 Obsidian 知识库结构

---

## 🎯 目标

统一 Hermes 和 OpenClaw 的 Obsidian 归档逻辑，避免知识库结构混乱。

---

## 📊 当前状况

| 系统 | Skill | Vault 路径 | 问题 |
|-----|-------|-----------|------|
| Hermes | hermes-universal-pkm | F:\笔记文档 | 使用新结构（10/20/30/40）|
| OpenClaw | obsidian-vault | F:\笔记文档 | 无分类结构，直接文件操作 |

**风险**: 两个系统写入同一 Vault 但结构不同 → 混乱

---

## ✅ 解决方案

### 第一步：读取共享配置

文件位置：`F:\笔记文档\99 System\sync-config.yaml`

这个文件定义了：
1. 统一的目录结构（10 Assets, 20 Resources...）
2. 智能分类规则（关键词匹配）
3. 变更记录格式

### 第二步：修改你的 SKILL.md

请在你的 skill 文件 `~\.openclaw\workspace\skills\obsidian-vault\SKILL.md` 中添加以下内容：

#### 添加分类决策逻辑

在 `## 可用命令` 章节之后，添加：

```markdown
---

## 智能分类归档

### 分类规则（读取 sync-config.yaml）

在归档内容前，请先读取 `F:\笔记文档\99 System\sync-config.yaml` 获取最新规则。

### 标准分类流程

```yaml
输入内容
    ↓
匹配 classification_rules（按优先级）
    ↓
确定 target 路径和 template
    ↓
使用对应模板创建文档
    ↓
添加变更记录（Change Log）
```

### 目录结构对应

| 内容类型 | 关键词匹配 | 目标路径 | 模板 |
|---------|-----------|---------|------|
| 技能问题 | 错误/失败/异常/timeout | 20 Resources/skills/{name}/issues/ | issue-resolution |
| 技能指南 | 如何/步骤/教程/安装 | 20 Resources/skills/{name}/guides/ | skill-guide |
| 账号信息 | 账号/密码/用户名 | 10 Assets/accounts/ | asset-entry |
| 订阅服务 | 订阅/付费/到期 | 10 Assets/subscriptions/ | asset-entry |
| GitHub项目 | github.com/项目/仓库 | 20 Resources/projects/ | resource-entry |
| 工具软件 | 工具/软件/CLI | 20 Resources/tools/ | resource-entry |
| 闪念想法 | 想法/灵感/想到 | 30 Thoughts/fleeting/ | thought-entry |
| 项目计划 | 开始/计划/项目 | 40 Projects/{name}/ | project-index |

### 变更记录格式（强制）

每次修改必须在文档末尾添加：

```markdown
---
## 变更记录

- **时间**: 2026-06-03 14:30
- **来源**: OpenClaw
- **类型**: 新增/追加/更新/废弃
- **修改内容**: 简要说明
- **PKM 位置**: 20 Resources/xxx/xxx.md
```

---

## 新增命令

### 智能归档
```powershell
# 根据内容自动分类归档
Sync-ToPKM -Content "内容" -Source "OpenClaw"

# 这会：
# 1. 读取 sync-config.yaml 规则
# 2. 分析内容类型
# 3. 选择对应目录和模板
# 4. 创建文档
# 5. 添加变更记录
```

### 分类写入
```powershell
# 写入技能问题
Write-SkillIssue -SkillName "skill-name" -Issue "问题描述" -Solution "解决方案"

# 写入账号信息
Write-AssetAccount -Service "GitHub" -Account "username" -Expiry "2026-12"

# 写入想法
Write-Thought -Content "想法内容" -Context "触发场景"
```
```

### 第三步：添加配置读取代码

在你的 skill 中添加读取 sync-config.yaml 的逻辑：

```powershell
# 读取共享配置
function Get-PKMConfig {
    $configPath = "F:\笔记文档\99 System\sync-config.yaml"
    if (Test-Path $configPath) {
        return Get-Content $configPath -Raw | ConvertFrom-Yaml
    } else {
        Write-Error "未找到共享配置文件: $configPath"
        return $null
    }
}

# 智能分类函数
function Classify-Content {
    param([string]$Content)
    
    $config = Get-PKMConfig
    foreach ($rule in $config.classification_rules) {
        foreach ($pattern in $rule.patterns) {
            if ($Content -match $pattern) {
                return $rule
            }
        }
    }
    return @{ target = "00 Inbox"; template = "basic" }
}

# 变更记录函数
function Add-ChangeLog {
    param([string]$FilePath, [string]$Type, [string]$Description)
    
    $changeLog = @"
---
## 变更记录
- **时间**: $(Get-Date -Format "yyyy-MM-dd HH:mm")
- **来源**: OpenClaw
- **类型**: $Type
- **修改内容**: $Description
- **PKM 位置**: $FilePath
"@
    
    Add-Content -Path $FilePath -Value $changeLog -Encoding UTF8
}
```

---

## 🧪 测试清单

修改完成后，请测试：

- [ ] 能正确读取 sync-config.yaml
- [ ] "错误"关键词 → 归档到 20 Resources/skills/{name}/issues/
- [ ] "账号"关键词 → 归档到 10 Assets/accounts/
- [ ] 变更记录包含 "来源: OpenClaw"
- [ ] 与 Hermes 写入的文件不冲突

---

## 📞 联系方式

如有问题，请通过以下方式协调：
- Hermes 微信/飞书端：直接对话 BOSS
- 或回复到本文件

**记住：统一结构 > 各自为战**

---
*发送时间: 2026-06-03*  
*版本: hermes-universal-pkm v3.0*
