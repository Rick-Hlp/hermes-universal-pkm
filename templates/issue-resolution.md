---
type: issue
skill: {{skill-name}}
severity: critical | high | medium | low
tags: []
date_found: {{date:YYYY-MM-DD}}
date_resolved: {{date:YYYY-MM-DD}}
status: resolved | ongoing | pending
---

# {{issue-title}}

## 问题描述
{{problem_description}}

## 环境信息
- 技能版本：{{version}}
- 操作系统：{{os}}
- 相关配置：{{config}}

## 错误信息
```
{{error_log}}
```

## 判断方法
1. {{check_step_1}}
2. {{check_step_2}}
3. {{confirmation_sign}}

## 解决方案

### 方案一（推荐）
1. {{step_1}}
2. {{step_2}}
3. {{verification}}

### 方案二（备选）
{{alternative_solution}}

## 失败处理
- 如果方案一失败：{{fallback_1}}
- 如果方案二失败：{{fallback_2}}

## 根因分析
{{root_cause}}

## 预防措施
- {{prevention_1}}
- {{prevention_2}}

## 相关链接
- [[{{related_config}}]]
- [[{{related_guide}}]]
- [[{{related_improvement}}]]

---
## 变更记录
- **时间**：{{date:YYYY-MM-DD}}
- **来源**：{{source}}
- **类型**：新增
- **修改内容**：首次记录该问题及解决方案
