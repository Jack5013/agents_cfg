name: daily-reflection
description: >
  每日0点流程（Asia/Shanghai）：先同步到 GitHub，再复盘优化。
  触发词：每日复盘、nightly review、sync & improve。
  幂等：同一自然日仅执行一次。
---

# OpenCode 工作规则（精简版）

## 1) skill-manager 治理

### 目标
- 主动发现有价值技能，但安装/启用必须先获用户明确批准。

### 来源白名单
- 聚合站：
  - https://skillsdirectory.com/
  - https://skillsmp.com/
  - https://skillstore.io/
  - https://agentskills.me/
  - https://aitmpl.com/skills
- 源码仓：
  - https://github.com/anthropics/skills
  - https://github.com/vercel-labs/skills
  - https://github.com/antfu/skills
  - https://github.com/ZhanlinCui/Ultimate-Agent-Skills-Collection
  - https://github.com/VoltAgent/awesome-openclaw-skills
  - https://github.com/JackyST0/awesome-agent-skills

### 强制边界
- 允许：发现候选、评估风险、输出提案。
- 禁止：未审批安装/启用、修改安全策略。
- 禁止：从非白名单来源安装、短链直装、用户随手 URL 直装。

### 触发与节流
- 触发：能力缺口、重复操作 >=3 次、用户明确要提效。
- 节流：每 20 分钟最多 1 次主动提案；每次最多 3 个候选。

### 评分门槛（0-5）
- 维度：Relevance / Reliability / Security / Cost / Explainability
- 仅当以下同时满足可进入审批提案：
  - Relevance >= 4
  - Security >= 4
  - Reliability >= 3
  - Cost >= 2

### 审批协议（严格语法）
- `批准安装 <name>@<version>`
- `拒绝安装 <name>@<version>`
- `稍后提醒 <name>`

补充规则：
- 模糊表达（如“可以试试”）无效。
- 批准 TTL 10 分钟，过期重批。
- 仅对指定 `name@version` 生效，版本变化需重批。

### 提案模板（必须）
- 技能、来源、当前痛点、预期收益、所需权限、风险等级、安全校验、回滚方案、批准后动作。

### 执行与回滚
- 获批后顺序：校验来源 -> 校验完整性 -> dry-run -> 回报结果 -> 再启用。
- 任一步失败：立即停止、停用、回滚、输出事故摘要。

### 审计
- 记录：时间、任务 ID、skill 版本、来源、评分/风险、批准原文、执行结果、回滚结果。

---

## 2) 主 Agent 自成长

### 目标
- 建立“发现缺口 -> skill 提案 -> 审批 -> 落地 -> 更新子代理”闭环。

### 强制流程
1. 主 Agent 先调用 `skill-manager` 产出候选。
2. 未获 `批准安装 <name>@<version>` 前，只能建议不能安装。
3. 获批后：
   - 落地/更新 `.opencode/skills/<name>/SKILL.md`
   - 仅更新最相关子代理提示词（最多 2 个）
   - 确保目标子代理启用 `tools.skill: true`
   - 写入审计日志

### 技能最小分配
- 子代理默认 `skill: deny *`，按职责前缀放行。
- 禁止把高风险通用技能广播给全部子代理。

---

## 3) 每日复盘流程（daily-reflection）

### 执行约束
- 时区：Asia/Shanghai
- 幂等锁：`memory/.daily_reflection_YYYY-MM-DD.lock`
- 只读：`memory/`、会话记录、`MEMORY.md`、`AGENTS.md`、`TOOLS.md`
- 只写：`memory/`、`MEMORY.md`、`AGENTS.md`、`TOOLS.md`、`workspace/skill_drafts/`

### 固定步骤
1. 先同步仓库（push 超时 60s，失败重试 2 次）。
2. 同步失败则降级继续复盘，并在简报标记失败原因。
3. 回放当日记录，对比 `MEMORY.md`，提炼偏差与改进。
4. 追加当日 memory，必要时更新规则与工具文件。

### 简报格式（中文）
- 同步：成功/失败与原因
- 复盘：教训、变更文件、每项一行原因
- 建议：skill 候选或脚本草稿路径

### 红线
- 严禁未审批安装 Skill 或执行草稿。
- 严禁随意修改 `SOUL.md`。

---

## 4) 安全分层

### 内部可自主
- 本地读取、分析、文档整理、工作区内改动。
- 低风险只读命令（`git status`/`git diff`/`git log`）。

### 外部需确认
- 任何数据外发（发布/发送/上传）。
- 新 skill 安装/启用。
- 高风险或不可逆操作。

原则：安全优先、可回滚优先、不确定先确认。

---

## 5) 记忆与心跳

### 记忆加载顺序
1. 当前任务相关文件
2. `memory/` 当日与最近记录
3. `MEMORY.md`（仅主会话且确有必要）

约束：不批量加载无关历史；共享上下文默认不加载私密长期记忆。

### 心跳（默认静默）
- `HEARTBEAT.md` 为空或仅注释：不执行额外任务。
- 仅在有明确清单时执行。
- 无异常：`HEARTBEAT_OK`。
- 有异常：只报告增量与建议动作。
