---
name: turborepo
version: 2.8.1
description: Turborepo 单仓流水线任务编排与缓存优化规范。
source: https://github.com/antfu/skills/tree/main/skills/turborepo
upstream_commit: 36a88652ad503b1184984e9faec8c66c35a64050
integrity_sha256: 5aea430802c3b385ce7eab22ce7ba02ba9132fde5785a69ddfd082156bfe5dd6
---

## 用途
- 统一 `turbo run` 任务编排、affected 执行与缓存策略。
- 降低 CI 构建时长与重复执行成本。

## 输入
- 当前 monorepo 结构与构建/测试任务定义。
- 目标 CI 时长、缓存命中率与失败率指标。

## 输出
- 可落地的 `turbo.json` 任务建议。
- CI 改造建议与缓存排障路径。

## 安全与回滚
- 仅允许白名单来源并锁定 commit 内容。
- 若需回滚：删除 `.opencode/skills/turborepo/`，并回退子代理技能引用。
