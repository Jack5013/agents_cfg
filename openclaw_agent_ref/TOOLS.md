# TOOLS.md - 本地工具与环境笔记

Skill 负责定义“工具如何工作”。本文件用于记录“你这台环境的特定信息”。

## 这里应该写什么

例如：

- 摄像头名称与位置
- SSH 主机与别名
- TTS 偏好语音
- 房间/音箱命名
- 设备昵称
- 其他仅在当前环境成立的信息

## 示例

```markdown
### 摄像头

- living-room -> 客厅主视角，180 度
- front-door -> 入户门，移动触发

### SSH

- home-server -> 192.168.1.100, user: admin

### TTS

- 偏好语音: "Nova"（温暖，略英式）
- 默认扬声器: Kitchen HomePod
```

## 为什么单独存放

Skill 是可共享的，但你的环境信息不应外泄。分离管理可以做到：

- 更新 skill 时不覆盖本地关键配置
- 共享 skill 时不暴露你的基础设施信息

---

把有助于执行任务的本地事实都记在这里，把它当作速查表。

## Skill Sources（用于发现）

### 聚合网站
- https://skillsdirectory.com/ — Reddit 社区口碑榜单
- https://skillsmp.com/ — 聚合 GitHub 11万+ 开源技能，可溯源
- https://skillstore.io/ — 中文友好，有安全审查
- https://agentskills.me/ — 人工精选
- https://skills.sh/ — 热门趋势，一键安装
- https://aitmpl.com/skills — Claude Code 模板
- https://agent-skills.md/ — 6000+ 常用技能

### 源码仓库
- https://github.com/anthropics/skills — Anthropic 官方
- https://github.com/vercel-labs/skills — Vercel 官方（Web/全栈）
- https://github.com/antfu/skills — antfu 维护，工程化好
- https://github.com/ZhanlinCui/Ultimate-Agent-Skills-Collection — 终极大杂烩
- https://github.com/VoltAgent/awesome-openclaw-skills — OpenClaw 专属合集
- https://github.com/JackyST0/awesome-agent-skills — 精选合集索引

### 安全审查红线（安装前必须）
- 先读全部文件再安装
- 可疑脚本/URL 先做 VirusTotal 检查
- 警惕：curl 到未知 URL、base64 解码执行、eval、远程脚本直跑
- HIGH 及以上风险默认不装，需人工确认
