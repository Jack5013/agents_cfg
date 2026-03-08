# AGENT_STYLE_WHITELIST_MAP

## 目标
- 从白名单仓库提炼“高质量 agent 写法”，并按分工映射到本地子代理提示词。

## 白名单来源（本轮采样）
- `https://github.com/anthropics/skills`
- `https://github.com/vercel-labs/skills`
- `https://github.com/antfu/skills`
- `https://github.com/vercel-labs/agent-skills`（由 `antfu/skills` README 引用）

## 提炼出的通用写法
- 触发明确：每个 agent 都应写清“何时介入/触发词”。
- 流程清晰：采用固定步骤，减少漏项（先定义标准，再执行，再回报）。
- 输出结构化：给固定输出模板，便于跨角色汇总与评审。
- 反模式前置：显式写“不要做什么”，避免常见误操作。
- 证据驱动：结论必须绑定命令、日志、报告或可复现步骤。

## 分工映射
- `project-analyst`：六段式立项输出（目标/范围/非目标/验收/约束风险/阻塞项）。
- `system-architect`：方案矩阵 + 主备方案 + 切换与回滚条件。
- `sw-engineer`：最小可运行验证优先，输出改动与验证证据。
- `sw-qa`：门禁标准先行，输出可复现失败证据与覆盖缺口。
- `devops-ci`：可复现优先于提速，输出耗时/失败率/制品追溯。
- `embedded-engineer`：最小 bring-up 链路与固件回退包要求。
- `fpga-engineer`：仿真/时序/CDC 证据链与 bitstream 回滚。
- `hw-qa`：判据与仪器先行，异常分级和复现实验闭环。
- `skill-manager`：候选筛选、审批语法、完整性校验、dry-run、启用回报。

## 变更落点
- `AGENTS.md`（联合评审机制）
- `.opencode/agents/*.md`（各角色新增“高质量写法迁移”段）

## 备注
- 本轮只迁移“写法与流程模板”，未新增自动安装逻辑。
- 新技能仍遵循严格审批语法与白名单来源约束。
