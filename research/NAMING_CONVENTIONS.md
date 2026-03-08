# 文档命名规范

## 通用规则
- 统一使用小写字母、数字、连字符（kebab-case）。
- 日期前缀使用 `YYYY-MM-DD`。
- 主题明确，避免 `new`、`final`、`v2-new` 这类模糊命名。

## 推荐格式
- 提案：`YYYY-MM-DD-<topic>-proposal.md`
- 巡检：`YYYY-MM-DD.md`（置于 `weekly-reviews/`）
- 选择结论：`YYYY-MM-DD.md`（置于 `selections/`）
- 映射文档：`<topic>-map-vN.md`

## 不推荐
- `temp.md` / `draft.md` / `untitled.md`
- 根目录新增一次性分析文档（应归档到 `research/`）

## 迁移策略
- 若历史文件命名不规范，优先“移动并改名”，再更新引用。
- 保留可追溯性：在评审/版本文档中记录迁移路径。
