# OpenClaw Add Agent

帮助你在 OpenClaw 中添加新的 Telegram 机器人代理。

## 功能

引导你完成在 OpenClaw 中添加新的 Telegram 机器人代理 —— 收集 bot token、设置 agent ID、配置 binding，然后自动更新 `openclaw.json` 并创建工作目录。

## 安装

### Prompt

复制以下内容到 OpenClaw：

```
Install the skill "openclaw-add-agent" (gaoxiaowei2117/openclaw-add-agent) from GitHub.
Skill page: https://github.com/gaoxiaowei2117/openclaw-add-agent
Keep the work scoped to this skill only.
After install, inspect the skill metadata and help me finish setup.
Required binaries: none
Use only the metadata you can verify from the repository; do not invent missing requirements.
Ask before making any broader environment changes.
```

### 手动安装

```bash
git clone https://github.com/gaoxiaowei2117/openclaw-add-agent.git ~/skills/openclaw-add-agent
```

## 使用方法

安装后，告诉你的 OpenClaw agent：

- "添加一个新的 agent"
- "添加一个 Telegram bot"
- 或调用 `/openclaw-add-agent`

agent 会依次询问：
1. **Bot token** — Telegram bot token（从 @BotFather 获取）
2. **Agent ID** — 唯一标识符（如 `translator`、`customer_support`）
3. **名称** — 显示名称（可选）
4. **允许用户** — 可以访问此 bot 的 Telegram 用户 ID

然后会：
- 更新 `~/.openclaw/openclaw.json`
- 创建工作目录
- 询问是否需要内存隔离

最后重启 OpenClaw：`openclaw restart`

## 要求

- 已安装 OpenClaw
- OpenClaw 配置文件位于 `~/.openclaw/openclaw.json`
- 从 [@BotFather](https://t.me/BotFather) 获取的 Telegram bot token

## 配置示例

运行 skill 后，`openclaw.json` 会添加如下配置：

```json
// agents.list
{ "id": "translator", "name": "translator", "workspace": "/home/xgao/clawd-workspace/translator" }

// bindings
{ "agentId": "translator", "match": { "channel": "telegram", "accountId": "translator" } }

// channels.telegram.accounts
"translator": { "enabled": true, "dmPolicy": "allowlist", "botToken": "123456789:ABCdef...", "allowFrom": ["8538882690"], "groupPolicy": "allowlist", "streaming": "partial" }
```

## License

MIT
