---
name: vitest
version: 2026.1.28
description: Vitest 单元测试与回归测试规范，聚焦 mock、覆盖率与筛选执行。
source: https://github.com/antfu/skills/tree/main/skills/vitest
upstream_commit: 5cae97ca87e0dcfb5a192cd2cbf8b83a9f769e8f
integrity_sha256: 87c8cf025987d1f1a0e9c0fd0b8605946a0ebd5478676471ce296d8f0adc0f07
---

## 用途
- 统一 Vitest 测试编写与执行方式，降低回归不稳定。
- 为 `sw-qa` 提供 mock、coverage、filtering 的标准操作基线。

## 输入
- 目标模块与风险点。
- 当前测试脚本、覆盖率要求与门禁阈值。

## 输出
- 可复用的测试命令与配置建议。
- 失败定位线索与最小复现建议。

## 安全与回滚
- 仅使用白名单来源与固定 commit 内容。
- 若需回滚：删除 `.opencode/skills/vitest/`，并回退子代理技能引用。
