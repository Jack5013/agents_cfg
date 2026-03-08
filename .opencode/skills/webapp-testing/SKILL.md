---
name: webapp-testing
version: latest
description: 基于 Playwright 的 Web UI 自动化测试流程，适用于页面行为验证与故障排查。
source: https://github.com/anthropics/skills/tree/main/skills/webapp-testing
upstream_commit: ef740771ac901e03fbca3ce4e1c453a96010f30a
integrity_sha256: 51b7349e77ec63b7744a6f63647e7566a0b4d2e301121cc10e8c2113af6556a2
---

## 用途
- 为动态页面提供 reconnaissance-then-action 测试路径。
- 统一浏览器截图、日志采集与交互验证步骤。

## 输入
- 目标页面地址与关键业务流程。
- 预期交互路径、断言条件和失败判据。

## 输出
- 可执行的 Playwright 测试流程建议。
- UI 故障证据（截图、日志、定位信息）生成规范。

## 安全与回滚
- 来源固定为白名单仓库并锁定 commit。
- 若需回滚：删除 `.opencode/skills/webapp-testing/`，并回退子代理技能引用。
