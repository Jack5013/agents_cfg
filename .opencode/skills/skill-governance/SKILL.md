---
name: skill-governance
description: 对候选技能执行白名单校验、风险分级、审批与回滚约束
license: MIT
compatibility: opencode
metadata:
  audience: maintainers
  safety: strict
---

## What I do
- 校验候选 skill 来源是否在白名单。
- 输出标准化提案模板（收益、风险、权限、回滚）。
- 在用户未明确批准前阻止安装。

## When to use me
- 需要从外部站点发现可用 skill 时。
- 需要严格“人工审批后安装”的流程时。

## Approval contract
- 仅接受：`批准安装 <name>@<version>`。
- 其他表达均视为未批准。
