# Skill Updater

`Skill Updater` 是一个跨平台的 skill 更新工具，用于检查并更新通过两类方式安装的本地 skills：

- `git` 工作树型安装
- `.skill-lock.json` 这类锁文件驱动的展开式安装

## 支持的平台

第一版默认扫描这些平台常见目录：

- Claude Code
- Cursor
- VS Code Copilot
- Gemini CLI
- Codex CLI
- OpenCode

## 默认扫描范围

- 当前项目下的 `.claude`、`.cursor`、`.agents`、`.codex`、`.github`、`.gemini`、`.opencode`
- 用户主目录下的对应全局目录

## 命令

```bash
sh skills/skill-updater/scripts/skill-updater check
sh skills/skill-updater/scripts/skill-updater update
sh skills/skill-updater/scripts/skill-updater check --json
sh skills/skill-updater/scripts/skill-updater check --source pbakaus/impeccable
sh skills/skill-updater/scripts/skill-updater update --path ~/.agents
```

## 自然语言用法

下面这些短句都适合作为触发方式：

- 查 skill 更新
- 更新 skill
- 检查 skills
- 同步 skills
- 看看哪些 skill 要更新
- 更新 GitHub 装的 skills
- 检查全局 skills
- 只看有风险的 skill
- 输出 skill 状态 JSON
- 检查 `pbakaus/impeccable`

如果想更明确一点，也可以这样说：

- 检查当前项目和全局目录里的 skills
- 更新所有安全可更新的 skills
- 只检查 `~/.agents` 下面的 skills
- 只看 `pbakaus/impeccable` 这批 skill 的状态

## 行为说明

- `check` 只检测，不写本地内容
- `update` 只更新安全可更新项
- git 型来源仅允许 fast-forward 或 tag 切换
- 锁文件型来源默认先备份，再覆盖并刷新锁文件 hash

## 风险状态

- `dirty`
- `ahead`
- `diverged`
- `modified-locally`
- `missing-source`
- `missing-local-skill`
- `lock-invalid`
- `unsupported`

默认遇到这些状态只汇报，不覆盖。
