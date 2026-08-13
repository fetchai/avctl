# IDE setup with AVCTL

> **Status**: Active  
> **Audience**: Agent builders using Cursor, Claude Code, or similar AI IDEs  
> **Last Verified**: 2026-08-13

Use **AVCTL** (Agentverse Control) from your IDE so an AI assistant can create, deploy, inspect logs, and iterate on hosted agents. Install the released binary — do **not** clone `agentverse-core` or run `make build` unless you are developing AVCTL itself.

## Install AVCTL

**macOS / Linux (Homebrew):**

```bash
brew tap fetchai/avctl
brew install avctl
```

**Windows (Chocolatey):**

```bash
choco install avctl
```

Confirm:

```bash
avctl version
```

## Authenticate

```bash
avctl auth login
avctl auth status
```

## Get a local project

**New agent:**

```bash
mkdir myagent && cd myagent
avctl hosting init
```

**Existing Agentverse agent** (copy the address from the Agentverse UI):

```bash
mkdir myagent && cd myagent
avctl hosting pull -a <agent_address>
```

List your agents:

```bash
avctl hosting get agents
```

Open that folder in Cursor (or your AI IDE).

## AI iteration loop

Tell the assistant to use AVCTL (not invent Agentverse HTTP calls by hand):

1. Edit local files (`agent.py`, `.env`, `pyproject.toml`, README).
2. `avctl hosting deploy` (or `push` / `sync` when updating code only).
3. `avctl hosting run -l` if the agent is stopped and you want logs.
4. `avctl hosting logs -f` to follow runtime output.
5. Fix from logs → deploy/push again → repeat.

Useful commands:

| Command | Purpose |
|---------|---------|
| `avctl hosting deploy` | Create or update + restart |
| `avctl hosting push` | Upload local code |
| `avctl hosting pull` | Download remote code |
| `avctl hosting sync` | Push or pull based on newer side |
| `avctl hosting logs -f` | Follow logs |
| `avctl hosting run` / `stop` | Start / stop |
| `avctl hosting packages` | Allowed hosted dependencies |
| `avctl hosting get secrets` | List secret names |

Full command reference: [AVCTL README](../README.md).

## Rules and agent-writing knowledge (Approach C)

Do **not** expect `init` / `pull` to download the full hosted-agent generation corpus onto disk. That knowledge stays central:

- **In-product generation** uses `services/hosting-api/hosting/agent_generation/` (see [agent-knowledge.md](./agent-knowledge.md)).
- **IDE assistants** should use a **thin** project rule ([`assets/avctl-ide.mdc`](../assets/avctl-ide.mdc)) plus **Agentverse MCP** for live hosting tools and docs-backed patterns:
  - MCP docs: [Agentverse MCP](https://docs.agentverse.ai) (search “Agentverse MCP”)
  - Remote MCP: `https://mcp-lite.agentverse.ai/mcp` (Cursor) or `https://mcp.agentverse.ai/sse`
  - Optional chat-protocol Cursor pack: see Agentverse MCP docs / `av-mcp.mdc`

Copy the thin rule into your agent project:

```bash
mkdir -p .cursor/rules
curl -fsSL -o .cursor/rules/avctl-ide.mdc \
  https://raw.githubusercontent.com/fetchai/avctl/main/assets/avctl-ide.mdc
```

(Or copy [`assets/avctl-ide.mdc`](../assets/avctl-ide.mdc) from this repo until a future `avctl ide setup` command writes it for you.)

## From the Agentverse UI

On the agent editor, use **Develop with AVCTL** to open this guide, then:

```bash
avctl hosting pull -a <your_agent_address>
```

and continue the loop above in your IDE.

## Contributor note

Building AVCTL from source (`make build` in `tools/cli`) is for maintainers only. End-user docs and the UI link must describe Brew / Chocolatey only.
