# OpenClaw Add Agent

A skill for OpenClaw that helps you add new Telegram bot agents to your OpenClaw configuration.

## What It Does

Walks you through adding a new Telegram bot agent to OpenClaw — collecting the bot token, agent ID, and configuring the binding — then updates `openclaw.json` and creates the workspace directory automatically.

## Installation

### Prompt

```
Install the skill "openclaw-add-agent" (gaoxiaowei2117/openclaw-add-agent) from GitHub.
Skill page: https://github.com/gaoxiaowei2117/openclaw-add-agent
Keep the work scoped to this skill only.
After install, inspect the skill metadata and help me finish setup.
Required binaries: none
Use only the metadata you can verify from the repository; do not invent missing requirements.
Ask before making any broader environment changes.
```

### Manually

```bash
git clone https://github.com/gaoxiaowei2117/openclaw-add-agent.git ~/skills/openclaw-add-agent
```

## Usage

After installation, tell your OpenClaw agent:

- "add a new agent"
- "add a Telegram bot"
- invoke `/openclaw-add-agent`

The agent will ask for:
1. **Bot token** — Telegram bot token (from @BotFather)
2. **Agent ID** — unique identifier (e.g., `translator`, `customer_support`)
3. **Purpose/Name** — display name (optional)
4. **Allow users** — Telegram user IDs that can access this bot

Then it will:
- Update `~/.openclaw/openclaw.json`
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
