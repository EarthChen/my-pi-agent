# my-pi-agent

个人 [pi](https://github.com/badlogic/pi-mono) agent 配置目录（`~/.pi/agent`）。

## 内容

| 路径 | 说明 |
|------|------|
| `settings.json` | pi 主配置：已安装的扩展包列表、主题等 |
| `pi-statusline.json` | `@narumitw/pi-statusline` 状态栏配置 |
| `extensions/` | 本地 TypeScript 扩展（orca 系列） |
| `skills/` | skills 目录（含指向 `~/.agents/skills` 的符号链接） |
| `models.example.json` | 自定义模型 provider 配置模板 |

## 不纳入版本管理的内容（见 `.gitignore`）

- `auth.json` — 认证凭证
- `models.json` — 含真实 API key 的模型配置（复制 `models.example.json` 后填入自己的 key）
- `sessions/` — 会话记录
- `npm/` 内容 — pi 自动生成的扩展依赖（由其自带 `.gitignore` 忽略，`settings.json` 中的 `packages` 列表是事实来源）

## 在新机器上恢复

```bash
git clone git@github.com:EarthChen/my-pi-agent.git ~/.pi/agent
cp ~/.pi/agent/models.example.json ~/.pi/agent/models.json
# 编辑 models.json 填入真实 baseUrl / apiKey
```

pi 启动后会根据 `settings.json` 的 `packages` 自动安装 npm 扩展。
