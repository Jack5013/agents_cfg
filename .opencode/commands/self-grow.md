---
description: 触发主Agent自成长流程（发现能力缺口并走审批）
agent: build
---

请执行主 Agent 自成长流程：

1. 先评估当前任务是否存在能力缺口或重复低效步骤。
2. 若存在，调用 `skill-manager` 给出最多 3 个候选技能提案。
3. 严格等待审批口令：`批准安装 <name>@<version>`。
4. 获批后执行落地：
   - 更新 `.opencode/skills/<name>/SKILL.md`
   - 更新最相关的 `.opencode/agents/*.md`（最多 2 个）
   - 补齐 `tools.skill: true`
   - 输出审计日志条目（时间、任务、版本、批准原文、变更文件）
5. 未获批时只输出建议，不做安装与启用。
