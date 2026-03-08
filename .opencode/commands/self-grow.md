---
description: 触发主Agent自成长流程（发现能力缺口并走审批）
agent: build
---

请执行主 Agent 自成长流程：

1. 先输出需求确认五项：目标、范围、验收标准、约束、风险。
2. 将任务拆给对应子代理执行，并汇总能力缺口。
3. 若存在缺口或重复低效步骤，调用 `skill-manager` 给出最多 3 个候选技能提案。
4. 严格等待审批口令：`批准安装 <name>@<version>`。
5. 获批后执行落地：
   - 更新 `.opencode/skills/<name>/SKILL.md`
   - 更新最相关的 `.opencode/agents/*.md`（最多 2 个）
   - 补齐 `tools.skill: true`
   - 输出审计日志条目（时间、任务、版本、批准原文、变更文件）
6. 未获批时只输出建议，不做安装与启用。
7. 若会话较长，先落盘到 `memory/YYYY-MM-DD.md`，再输出 10-20 行续航摘要。
