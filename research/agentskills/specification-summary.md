# Agent Skills 规范摘要（基于 agentskills.io）

## 资料来源
- `https://agentskills.io/llms.txt`
- `https://agentskills.io/specification.md`
- `https://agentskills.io/client-implementation/adding-skills-support.md`
- `https://agentskills.io/skill-creation/using-scripts.md`
- `https://agentskills.io/skill-creation/evaluating-skills.md`

## 核心格式
- 每个技能目录至少包含 `SKILL.md`。
- `SKILL.md` 必须有 YAML frontmatter：`name`、`description`。
- 可选字段：`license`、`compatibility`、`metadata`、`allowed-tools`（实验性）。

## 推荐目录
- `scripts/`：可执行脚本（应支持 `--help`、非交互、清晰错误输出）。
- `references/`：按需读取的长文档。
- `assets/`：模板、静态资源。

## 关键机制
- 渐进加载（progressive disclosure）：
  1) 启动仅加载 name/description；
  2) 激活时加载 `SKILL.md`；
  3) 需要时再加载 `scripts/references/assets`。
- 目标：降低上下文开销，避免一次性灌入全部技能正文。

## 写作与执行要点
- `description` 要写“做什么 + 何时用”。
- `SKILL.md` 建议控制在 500 行以内，细节下沉到 `references/`。
- 脚本接口应：
  - 禁止交互式输入；
  - 输出结构化数据到 stdout；
  - 诊断信息写 stderr；
  - 失败可定位（明确退出码和错误提示）。

## 评估方法（Evals）
- 建议每次迭代同时跑“with-skill / without-skill”基线对比。
- 关注三类指标：通过率、耗时、token 成本。
- 用 `assertions + human review + transcript` 三信号迭代。

## 本仓落地原则
- 仅迁移高价值“写法模板”；安装仍走白名单审批。
- 优先迁移：计划先行、子代理分派、完成前验证、会话交接、提交边界。
