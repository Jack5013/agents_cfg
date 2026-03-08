# AGENT_OPTIMIZATION_REVIEW

## 日期
- 2026-03-08

## 本轮优化项（按影响度）
1. 强制主 Agent 先做需求确认五项（目标/范围/验收/约束/风险）。
2. 增加“子代理先分工、缺口再 skill 提案”的执行链路。
3. 增加上下文溢出前落盘机制（`memory/` + `MEMORY.md` + 续航摘要）。
4. 增加每日自优化固定流程与回滚基线要求。
5. 增加仓库拆分策略：`agent_cfg` 与 `projects/*` 独立仓库。

## 已改动文件
- `AGENTS.md`
- `.opencode/commands/daily-reflection.md`
- `.gitignore`

## 原因
- 降低执行漂移，先对齐需求再实现。
- 让团队协作可控，减少主 Agent 单点直接编码。
- 避免长会话上下文丢失，提升连续性。
- 通过先 push 再优化保证可回滚。
- 通过仓库拆分降低配置仓与项目仓耦合。

## 风险
- 规则增强后执行步骤变多，短任务会稍增开销。
- 仓库拆分前需确认每个项目远程地址与权限。

## 回滚路径
1. `git log --oneline` 找到优化前基线提交。
2. 需要回退时切换到该提交或按文件级恢复。
3. 若已推送，优先通过新提交回滚，避免强推。

---

## 追加优化（项目重启：masterduel-daily-bot）

### 新增文件
- `projects/masterduel-daily-bot/docs/KICKOFF_EXECUTION_PLAN_V1.md`
- `projects/masterduel-daily-bot/docs/KEY_SKILLS_CANDIDATES_V1.md`
- `projects/masterduel-daily-bot/docs/RESEARCH_NOTES_V1.md`

### 更新的代理
- `.opencode/agents/project-analyst.md`
- `.opencode/agents/system-architect.md`
- `.opencode/agents/sw-engineer.md`
- `.opencode/agents/sw-qa.md`
- `.opencode/agents/devops-ci.md`

### 关键变化
- 将“复用优先 + 多方案对比 + ADR”显式写入架构代理。
- 将“POC 先行 + 任务识别/计数/领奖 dry-run”写入研发代理。
- 将“85% 成功率 / 60 分钟”写入测试门禁。
- 输出项目关键 skill 候选清单（待审批，不自动安装）。

### 审批后落地（2026-03-08）
- 已按用户审批安装并落地 6 个本地技能包到 `.opencode/skills/`。
- 已将技能使用说明同步到对应子代理提示词。
- 审计日志已写入 `memory/skill_audit.jsonl`。

---

## 追加优化（执行偏离纠偏）

### 问题
- 出现“方案门已确认但实现路径偏离主方案”的执行偏差。

### 修复
- 在 `AGENTS.md` 新增“计划执行一致性（强制）”章节。
- 强制：未触发回退条件前，不得推进备选方案实现。
- 强制：偏离前必须提交偏离说明并获得用户确认。

### 相关文件
- `AGENTS.md`
- `.opencode/agents/project-analyst.md`
- `.opencode/agents/system-architect.md`
- `.opencode/agents/sw-engineer.md`
- `AGENT_VERSION.md`
