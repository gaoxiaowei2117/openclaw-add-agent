# OpenClaw Add Agent

A skill for OpenClaw that helps you add new Telegram bot agents to your OpenClaw configuration.

## What It Does

Walks you through adding a new Telegram bot agent to OpenClaw — collecting the bot token, agent ID, and configuring the binding — then updates `openclaw.json` and creates the workspace directory automatically.

## Installation

### Manually

```bash
git clone https://github.com/gaoxiaowei2117/openclaw-add-agent.git ~/.claude/skills/openclaw-add-agent
```

### From GitHub

```bash
# If you have claude-code CLI
claude skill install gaoxiaowei2117/openclaw-add-agent
```

## Usage

After installation, just tell your agent:

- "add a new agent"
- "add a Telegram bot"
- invoke `/openclaw-add-agent`

The agent will ask for:
1. **Bot token** — Telegram bot token (from @BotFather)
2. **Agent ID** — unique identifier (e.g., `translator`, `customer_support`)
3. **Purpose/Name** — display name (optional)
4. **Allow users** — Telegram user IDs that can access this bot

Then it will:
- Update `/home/xgao/.openclaw/openclaw.json`
- Create the workspace directory
- Ask if you need memory isolation

Finally, restart OpenClaw: `openclaw restart`

## Requirements

- OpenClaw installed
- Existing OpenClaw configuration at `~/.openclaw/openclaw.json`
- Telegram bot token from [@BotFather](https://t.me/BotFather)

## Minimal Config Example

After the skill runs, your `openclaw.json` will have entries like:

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
