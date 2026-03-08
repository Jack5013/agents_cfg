# AGENT_VERSION

## Current
- version: `0.2.2`
- date: `2026-03-08`
- scope: `agent_cfg` rules, 门禁记录与偏离模板标准化, 外部动作边界补强

## Changelog

### 0.2.2
- daily-reflection 增加 push 失败降级说明与待推清单输出要求。
- 安全分层补充 `git push` 例外边界（仅复盘备份或用户明确要求）。
- 项目编排新增门禁记录模板与技能安装节流（单阶段最多 3 个）。
- 计划执行一致性新增偏离说明模板。
- 仓库策略补充提交规范：规则改动需同步更新版本与审阅文件。

### 0.2.1
- 新增“计划执行一致性”强制规则，禁止方案门通过后随意偏离。
- 为 `project-analyst` 增加阶段门检查结论输出要求。
- 为 `system-architect` 与 `sw-engineer` 增加“偏离需先确认”的执行边界。

### 0.2.0
- 新增 `project-analyst` 并接入主 Agent 调度。
- 强化立项前置门：需求确认 -> 多方案对比 -> POC -> 用户确认。
- 按审批落地 6 个本地技能包并写入审计日志。
- 增强 `system-architect/sw-engineer/sw-qa/devops-ci` 的项目特化职责。

### 0.1.0
- 初始化 OpenCode 多代理架构与 daily-reflection / self-grow 命令。
- 建立 skill 审批协议、最小权限分配、记忆与心跳机制。
