# WORKSPACE_MAP

## 根目录（核心运行与治理）
- `AGENTS.md`：主规则与执行门禁。
- `AGENT_VERSION.md`：版本与变更摘要。
- `AGENT_OPTIMIZATION_REVIEW.md`：每轮优化评审记录。
- `MEMORY.md`：长期稳定记忆。
- `README.md`：仓库总览。
- `TOOLS.md` / `HEARTBEAT.md`：工具与心跳约束。

## 代理配置
- `.opencode/agents/`：各子代理提示词与权限。
- `.opencode/skills/`：本地技能定义（已审批/在用）。
- `.opencode/commands/`：复用命令（如 daily-reflection）。

## 记忆与审计
- `memory/YYYY-MM-DD.md`：每日记忆。
- `memory/skill_audit.jsonl`：技能审批与执行审计。

## 研究与沉淀
- `research/agentskills/`：外部写法与规范摘要、本地缓存策略、周巡检。
  - `selections/`：正式筛选结论（按日期）。
  - `style-maps/`：写法来源到分工映射。
  - `weekly-reviews/`：每周巡检报告。
- `research/governance/`：治理提案与规则演进资料。

## 参考资料
- `openclaw_agent_ref/`：参考基线（只读对照，不随意改动）。

## 新文件落位规则（简版）
- 规则主文档：放根目录。
- 临时提案/调研：放 `research/` 对应主题目录。
- 审计与记忆：放 `memory/`。
- 子代理/技能：仅放 `.opencode/agents` 与 `.opencode/skills`。
