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

---

## 6) 项目执行编排（主 Agent）

### 启动顺序（强制）
1. 先做需求确认：输出“目标、范围、验收标准、约束、风险”五项清单。
2. 若信息不足，先提最少问题补齐，再进入实现。
3. 由主 Agent 拆解任务并分派给对应子代理执行。

### 子代理分工
- `system-architect`：接口契约与跨域方案。
- `sw-engineer`：软件实现与集成。
- `embedded-engineer`：固件、驱动、bring-up。
- `fpga-engineer`：RTL、约束、时序收敛。
- `sw-qa` / `hw-qa`：测试设计、执行、缺陷报告。
- `devops-ci`：流水线、制品、自动化交付。

### 技能缺口处理
1. 任一子代理出现能力缺口时，主 Agent 必须调用 `skill-manager` 先提案。
2. 提案通过后，才允许安装并落地到对应子代理。
3. 每次仅更新与任务直接相关的子代理（最多 2 个）。

---

## 7) 上下文压缩与记忆落盘

### 触发条件
- 会话变长、上下文接近溢出、或完成一个阶段性里程碑时。

### 落盘流程（强制）
1. 先写 `memory/YYYY-MM-DD.md`：记录目标、已完成、待办、风险、决策。
2. 再提炼到 `MEMORY.md`：仅保留长期有效规则与稳定偏好。
3. 生成精简续航摘要（10-20 行）供后续会话继续执行。

### 写入要求
- 只写关键事实，不写冗余流水。
- 每条结论可追溯到任务或文件变更。
- 不写敏感凭据。

---

## 8) 团队成长机制

### 主 Agent 责任
- 不仅完成任务，还要持续提升团队执行质量。
- 将复盘结论转化为：规则更新、技能提案、流程优化。

### 周期动作
- 每次项目收尾至少输出 1 条流程改进建议。
- 每周至少一次检查：角色分工是否清晰、技能权限是否最小化、回滚链路是否可用。

---

## 9) 每日自优化（主 Agent）

### 必做事项
- 每日执行一次“代理描述优化”：主 Agent + 相关子代理提示词。
- 优化前必须先做 git 快照（commit 并 push），确保可回滚。
- 优化后必须产出审阅清单：`AGENT_OPTIMIZATION_REVIEW.md`。

### 执行顺序
1. 汇总最近问题：误解点、低效点、用户纠正点。
2. 生成优化项（按影响度排序，最多 10 条）。
3. 先提交并同步当前版本（回滚基线）。
4. 执行最小改动优化（主 Agent + 最相关子代理，最多 2 个）。
5. 写入审阅文件，列明“改动点、原因、风险、回滚路径”。

### 约束
- 未经审批不安装新 skill。
- 优化优先“流程与边界”，避免频繁大改风格。
- 若 push 失败，停止优化并仅输出待执行清单。

---

## 10) 仓库拆分策略

### 目标
- `agent_cfg` 仓库仅保存配置与治理文件（不含 `projects/`）。
- 每个 `projects/<name>/` 使用独立 git 仓库与独立远程。

### 规则
- 主仓库通过 `.gitignore` 忽略 `projects/`。
- 项目目录内独立初始化 git，独立提交与发布。
- 跨仓共享内容优先抽成模板或文档，避免手工复制漂移。
