# AGENTS.md

## 项目

个人 [pi](https://github.com/badlogic/pi-mono) coding agent 的配置目录（`~/.pi/agent`），通过 git 同步到 [EarthChen/my-pi-agent](https://github.com/EarthChen/my-pi-agent)。dotfiles 类配置仓库：无构建产物、无测试，文件改动对 pi 直接生效。

## Stack

- 纯 JSON 配置 + 少量本地 TypeScript 扩展（`extensions/*.ts`，由 pi 运行时加载）
- 扩展依赖由 pi 通过 npm 安装到 `npm/`（`package.json` + `package-lock.json` 已入库）
- 无 CI、无构建/测试/lint 命令

## 常用命令

```bash
# 新机器恢复
git clone git@github.com:EarthChen/my-pi-agent.git ~/.pi/agent
cp ~/.pi/agent/models.example.json ~/.pi/agent/models.json
# 编辑 models.json 填入真实 baseUrl / apiKey；
# pi 启动后按 settings.json 的 packages 自动安装 npm 扩展
```

## 目录结构

| 路径 | 职责 |
|------|------|
| `settings.json` | pi 主配置：`packages` 扩展列表、主题 |
| `pi-statusline.json` | `@narumitw/pi-statusline` 状态栏配置 |
| `npm/` | pi 自动维护的扩展依赖；`node_modules/` 忽略，manifest 入库 |
| `extensions/` | 本地 TS 扩展；`orca-*`（工作环境专用）不入库 |
| `skills/` | pi skills 目录，当前为空（历史 symlink 已于 9f44a26 移除） |
| `models.example.json` | 模型 provider 配置的脱敏模板 |
| `auth.json` / `models.json` / `sessions/` | 本地敏感文件，永不入库 |

## 约定

- `settings.json` 的 `packages` 与 `npm/package.json` 的 `dependencies` 一一对应；增删扩展需两处同步（`npm/` 侧通常由 pi 自动写入）
- 提交信息：英文 Conventional Commits（`chore:` / `feat:` …），正文说明动机 [推断]
- 文档（README 等）使用简体中文

## Rules

- 严禁提交 `auth.json`、`models.json`、`sessions/`——含真实 API key 与会话内容；模型配置变更只同步到 `models.example.json` 的脱敏模板
- `extensions/orca-*` 为工作环境专用，保持本地，不得从 `.gitignore` 移除
- 不要手动在 `npm/` 内运行包管理器改写 lockfile——`package-lock.json` 由 pi 生成维护（此仓库例外于"仅用 pnpm"的全局约定）
- 提交前用 `git status` 复查，确认无敏感文件被意外跟踪
