# AGENT_VERSION

## Current
- version: `0.2.7`
- date: `2026-03-10`
- scope: `agent_cfg` 治理与执行解耦、审批默认拒绝兜底、阶段状态机标准化

## Changelog

### 0.2.7
- 修复 `AGENTS.md` 头部格式，移除误放的 command frontmatter，恢复为纯治理文档。
- 在 skill 审批协议补充“语法不匹配即 NO-OP”默认拒绝兜底规则。
- 新增阶段状态机（DISCOVERY -> PLAN_APPROVED -> POC_VALIDATED -> BUILD -> VERIFY -> RELEASE）与迁移记录要求。
- 明确 `daily-reflection` 的执行模板以 `.opencode/commands/daily-reflection.md` 为准，AGENTS 仅保留治理边界。

### 0.2.6
- 在 `AGENTS.md` 的热门写法章节新增：`executing-plans`、`requirements-clarity`、`systematic-debugging`。
- 在 `project-analyst` 提示词新增需求澄清前置（Why/KISS）。
- 在 `sw-engineer` 提示词新增系统化调试证据链（现象->假设->实验->结论）。
- 将每周巡检候选状态从“待确认”更新为“已采纳”。

### 0.2.5
- 新增 `research/agentskills/selections/2026-03-09.md`，沉淀 agentskills.me 热门流程技能筛选与适配结论。
- `AGENTS.md` 新增“热门 Agent 写法迁移（agentskills.me）”章节。
- 为 `project-analyst/sw-engineer/sw-qa/devops-ci` 补充热门流程写法落地条款。
- 新增 `research/agentskills/` 本地资料库，包含规范摘要、热门清单与缓存策略。

### 0.2.4
- 新增 `research/agentskills/style-maps/whitelist-map-v1.md`，沉淀白名单来源与分工映射规则。
- 为全部子代理补充“高质量写法迁移”段，统一触发词、标准流程、输出模板与反模式。

### 0.2.3
- 新增“多子代理联合评审（强制）”规则，明确触发场景、参与角色与通过条件。
- 为全部子代理补充统一评审输出卡（立场/证据/风险/回滚/阻塞项）。
- 按审批落地 `vitest`、`webapp-testing`、`turborepo` 技能并写入审计。

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
