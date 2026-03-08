# agentskills 每周更新清单模板

> 用途：低成本增量更新本地资料库（不做全量重抓）。
> 周期：每周一次（建议周一）。

## 0) 本周目标
- [ ] 明确本周要补强的能力主题（最多 2 个）
- [ ] 明确是否需要新增 skill 候选（是/否）

## 1) 来源巡检（白名单）
- [ ] agentskills.me 热门榜单仅抽样前 30 条
- [ ] `anthropics/skills` 最近变更
- [ ] `antfu/skills` 最近变更
- [ ] `vercel-labs/skills` 或 `vercel-labs/agent-skills` 最近变更

记录：
- 本周巡检链接：
- 发现的高价值条目：

## 2) 迁移筛选（只迁移写法模板）
- [ ] 与当前项目强相关（自动化/测试/流水线/协作）
- [ ] 可落地到主 Agent 或现有 subagent
- [ ] 不与现有规则冲突

记录：
- 候选写法：
- 放弃原因（如不迁移）：

## 3) 本地资料更新（分类）
- [ ] 更新 `research/agentskills/specification-summary.md`（若规范有变化）
- [ ] 新增/更新当周榜单文件 `popular-process-skills-YYYY-MM-DD.md`
- [ ] 更新 `AGENT_SKILLS_SELECTION_YYYY-MM-DD.md`（若有新的迁移结论）
- [ ] 检查 `research/agentskills/cache-policy.md` 是否需调整

## 4) 规则与代理同步
- [ ] 仅将“确认采纳”的写法写入 `AGENTS.md`
- [ ] 按分工同步到对应 subagent（避免全量广播）
- [ ] 更新 `AGENT_VERSION.md` 与 `AGENT_OPTIMIZATION_REVIEW.md`

## 5) 审计与记忆
- [ ] 在 `memory/YYYY-MM-DD.md` 记录本周迁移结论
- [ ] 若涉及安装建议，写入审批指令草案（不自动安装）

## 6) 收尾检查
- [ ] 确认仅做了文档与规则更新，没有执行安装动作
- [ ] 输出 5 行内周报：新增、变更、风险、待办、建议

---

## 本周周报模板（可复制）
- 新增：
- 变更：
- 风险：
- 待办：
- 建议：
