# agents_cfg

OpenCode agent configuration workspace for multi-role engineering collaboration.

## What this repo contains

- `AGENTS.md` - Core governance rules (skill approval, safety boundaries, daily reflection)
- `opencode.json` - OpenCode runtime permissions and agent/task policies
- `.opencode/agents/` - Subagent definitions (software, FPGA, embedded, QA, DevOps, skill-manager)
- `.opencode/commands/` - Reusable commands (`daily-reflection`, `self-grow`)
- `.opencode/skills/` - Local skill definitions and governance templates
- `TEAM_REQUIREMENTS_V1.md` - Team requirement analysis baseline
- `openclaw_agent_ref/` - Chinese-localized OpenClaw reference documents

## Design goals

1. Safe self-evolution: discover skills proactively, install only after explicit approval
2. Least privilege: skill access is restricted per subagent domain
3. Auditable operations: proposal, approval, execution, and rollback are traceable
4. Practical workflow: daily reflection with idempotency and failure downgrade

## Approval contract

Skill installation must use strict commands:

- `批准安装 <name>@<version>`
- `拒绝安装 <name>@<version>`
- `稍后提醒 <name>`

Ambiguous approvals are treated as invalid.

## Usage

Run OpenCode in this repository root:

```bash
opencode
```

Useful commands:

- `/self-grow` - Trigger capability-gap analysis and skill proposal flow
- `/daily-reflection` - Run daily sync + reflection workflow

## Notes

- This repository is configuration-focused.
- Do not auto-install high-risk skills.
- Keep changes small and commit frequently for rollback safety.
