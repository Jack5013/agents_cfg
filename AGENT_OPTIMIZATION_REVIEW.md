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

---

## 追加优化（规则审阅后合并）

### 审核结果
- 用户已审核并确认：`research/governance/proposals/2026-03-08-agents-optimization-proposal.md` 全部通过。

### 合并内容
- daily-reflection 增加备份失败降级条款。
- 安全分层增加 `git push` 外部操作例外说明。
- 项目编排增加门禁记录模板。
- 技能缺口处理中增加安装节流（单阶段最多 3 个）。
- 仓库拆分策略增加提交规范。
- 计划执行一致性增加偏离说明模板。

### 本次变更文件
- `AGENTS.md`
- `AGENT_VERSION.md`
- `AGENT_OPTIMIZATION_REVIEW.md`

---

## 追加优化（联合评审 + 优质 Agent 写法并入）

### 背景
- 用户要求：不仅安装 skill，还要把优秀 Agent 写法与功能并入子代理与主 Agent 规则。

### 改动点
- 在 `AGENTS.md` 增加“多子代理联合评审（强制）”章节。
- 为所有子代理补充统一评审输出卡（立场/证据/风险/回滚/阻塞项）。
- 新增并接入 3 个审批通过技能：`vitest`、`webapp-testing`、`turborepo`。
- 将技能接入与完整性校验结果写入 `memory/skill_audit.jsonl` 与当日记忆。

### 相关文件
- `AGENTS.md`
- `.opencode/agents/project-analyst.md`
- `.opencode/agents/system-architect.md`
- `.opencode/agents/sw-engineer.md`
- `.opencode/agents/sw-qa.md`
- `.opencode/agents/devops-ci.md`
- `.opencode/agents/embedded-engineer.md`
- `.opencode/agents/fpga-engineer.md`
- `.opencode/agents/hw-qa.md`
- `.opencode/agents/skill-manager.md`
- `.opencode/skills/vitest/SKILL.md`
- `.opencode/skills/webapp-testing/SKILL.md`
- `.opencode/skills/turborepo/SKILL.md`
- `AGENT_VERSION.md`
- `memory/2026-03-09.md`
- `memory/skill_audit.jsonl`

### 风险
- 评审流程更严格后，短平快任务可能增加沟通成本。
- 新增技能需会话重载后在运行时技能列表中可见。

### 回滚路径
1. 删除新增技能目录并回退子代理技能引用。
2. 回退 `AGENTS.md` 的联合评审章节与各子代理新增评审卡。
3. 保留审计日志，追加一条回滚记录说明原因与影响。

---

## 追加优化（白名单优秀 Agent 写法迁移）

### 背景
- 用户要求：不仅装 skill，还要把白名单中的优秀 agent 写法按分工迁移到对应子代理。

### 来源
- `anthropics/skills`：强调触发描述、步骤化说明、结果呈现与排障。
- `vercel-labs/skills`：强调技能结构标准、发现路径与兼容约束。
- `antfu/skills`：强调决策树、反模式、输出模板与证据导向。

### 改动点
- 新增 `research/agentskills/style-maps/whitelist-map-v1.md` 记录来源与分工映射。
- 为所有子代理增加“高质量写法迁移（白名单）”段：
  - 触发词
  - 标准流程
  - 输出模板
  - 反模式

### 相关文件
- `research/agentskills/style-maps/whitelist-map-v1.md`
- `.opencode/agents/project-analyst.md`
- `.opencode/agents/system-architect.md`
- `.opencode/agents/sw-engineer.md`
- `.opencode/agents/sw-qa.md`
- `.opencode/agents/devops-ci.md`
- `.opencode/agents/embedded-engineer.md`
- `.opencode/agents/fpga-engineer.md`
- `.opencode/agents/hw-qa.md`
- `.opencode/agents/skill-manager.md`
- `AGENT_VERSION.md`

### 风险
- 子代理提示词长度增加，可能略增首次决策延时。
- 若模板过强，个别探索性任务灵活度可能下降。

### 回滚路径
1. 删除各子代理的“高质量写法迁移（白名单）”段。
2. 删除 `research/agentskills/style-maps/whitelist-map-v1.md`。
3. 在 `AGENT_VERSION.md` 与本审阅文件记录回滚说明。

---

## 追加优化（agentskills.me 热门写法 + 本地缓存分类）

### 背景
- 用户要求：参考 agentskills.me 的热门技能与规范，并将可复用写法并入主 Agent 与 subagent。
- 用户要求：考虑联网成本，整理并本地分类保存资料。

### 改动点
- 增加热门技能筛选文档：`research/agentskills/selections/2026-03-09.md`。
- 在 `AGENTS.md` 增加“热门 Agent 写法迁移（agentskills.me）”章节。
- 在相关子代理增加热门写法条款（计划先行、完成前验证、提交边界）。
- 新建 `research/agentskills/` 本地资料库并按规范/榜单/策略分类。

### 相关文件
- `research/agentskills/selections/2026-03-09.md`
- `AGENTS.md`
- `.opencode/agents/project-analyst.md`
- `.opencode/agents/sw-engineer.md`
- `.opencode/agents/sw-qa.md`
- `.opencode/agents/devops-ci.md`
- `research/agentskills/README.md`
- `research/agentskills/specification-summary.md`
- `research/agentskills/popular-process-skills-2026-03-09.md`
- `research/agentskills/cache-policy.md`
- `AGENT_VERSION.md`

### 风险
- 规则持续增强会提高执行门槛，极小任务可能显得流程偏重。

### 回滚路径
1. 回退 `AGENTS.md` 新增章节与子代理新增条款。
2. 删除 `research/agentskills/` 与热门筛选文档。
3. 更新版本与审阅文件记录回滚原因。

---

## 追加优化（每周巡检候选正式采纳）

### 背景
- 用户确认将本周巡检候选写法正式添加到主 Agent 与分工子代理。

### 改动点
- `AGENTS.md`：新增已采纳写法
  - `executing-plans`
  - `requirements-clarity`
  - `systematic-debugging`
- `project-analyst`：新增 `requirements-clarity` 条款。
- `sw-engineer`：新增 `systematic-debugging` 条款。
- 更新 `research/agentskills/selections/2026-03-09.md` 候选状态为“已采纳”。

### 相关文件
- `AGENTS.md`
- `.opencode/agents/project-analyst.md`
- `.opencode/agents/sw-engineer.md`
- `research/agentskills/selections/2026-03-09.md`
- `research/agentskills/weekly-reviews/2026-03-09.md`
- `AGENT_VERSION.md`

### 风险
- 规则密度上升，简单任务可能感觉流程更重。

### 回滚路径
1. 回退上述文件本次新增条款。
2. 将候选状态改回“待确认”并保留周巡检记录。
