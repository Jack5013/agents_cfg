---
description: 每日复盘与同步（先同步，再复盘）
agent: build
---

执行每日复盘流程（Asia/Shanghai）：

1. 检查幂等锁 `memory/.daily_reflection_YYYY-MM-DD.lock`，存在则退出。
2. 先同步 `.openclaw` 到远程仓库：push 超时 60s，失败重试 2 次（指数退避）。
3. 若同步失败，记录错误并降级继续复盘。
4. 回放当日 `memory/` 与会话记录，对比 `MEMORY.md` 基线，识别偏差与低效点。
5. 将复盘结论追加到当日 memory 文件，更新 `MEMORY.md`/`AGENTS.md`/`TOOLS.md`（如需要）。
6. 输出中文简报三段：同步、复盘、建议。
7. 每日自优化：
   - 优化前先提交并推送当前版本（回滚基线）。
   - 仅优化主 Agent 与最相关子代理描述（最多 2 个）。
   - 将优化项写入 `AGENT_OPTIMIZATION_REVIEW.md` 供用户审核。

红线：
- 严禁未经确认安装 skill。
- 严禁执行自动化草稿。
- 严禁随意修改 `SOUL.md`。
