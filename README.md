# AI Registry — Atlassian (Inferred)

> **Inferred vendor repository.** This repo is maintained by the [AI Registry](https://github.com/eclipsefdn-ai-registry/ai-registry-core) project, not by Atlassian. It pre-seeds the registry with MCP servers, Agent Skills, and an Agent Plugin published by Atlassian at [github.com/atlassian](https://github.com/atlassian) and [github.com/atlassian-labs](https://github.com/atlassian-labs).
>
> *This entry is based solely on information published through Atlassian's official public channels. Atlassian has not endorsed, approved or validated this listing, and is not necessarily participating in the AI Registry.*

## What this repo contains

### MCP servers

- **Atlassian Rovo MCP Server** (`com.atlassian/atlassian-mcp-server`) — the official remote MCP server for Jira, Confluence, Jira Service Management, Bitbucket, and Compass. Listed in the official MCP registry (`registry.modelcontextprotocol.io`) under `com.atlassian`, so name/description/version are enriched automatically; a generic `config` (`{"type": "http", "url": "https://mcp.atlassian.com/v1/mcp"}`) is included too, taken from the registry's own `streamable-http` remote entry (latest version, 1.1.3).
- **Trello MCP Server** (`com.atlassian/trello-mcp-server`) — the official remote MCP server for Trello, maintained in [atlassian/trello-mcp-server](https://github.com/atlassian/trello-mcp-server) (README: "The official Model Context Protocol (MCP) server for Trello"). Not listed in the official MCP registry under that name, so this approval supplies its own `metadata` (fallback name/description) and a `config` built from the repo's documented connection (`{"type": "http", "url": "https://mcp.trello.com/v1"}`, OAuth 2.0). Marked `selfPublished: true` since Atlassian owns and maintains Trello and this repo directly.

### Agent Skills

- **`trello-use`** — the usage skill shipped alongside the Trello MCP server in [atlassian/trello-mcp-server](https://github.com/atlassian/trello-mcp-server) (`skills/trello-use/SKILL.md`), which teaches an agent the ARI id format and cross-cutting rules the Trello MCP tools require.
- **`twg-*` skills** — all skill folders under `skills/*` in [atlassian/twg-cli](https://github.com/atlassian/twg-cli) ("Public home for Atlassian Teamwork Graph CLI users, release notes, issue tracking, agent skills, and marketplace plugin integration notes"), e.g. `twg-jira`, `twg-confluence`, `twg-context-discovery`, `twg-engineering-work`, and others — official Atlassian GitHub org repo, each with its own `SKILL.md`. The glob picks up newly added skills automatically.

### Agent Plugins

- **Forge Skills** (`io.github.atlassian/forge-skills`) — an [agent-plugins.org](https://agent-plugins.org)-conformant plugin at the root of [atlassian/forge-skills](https://github.com/atlassian/forge-skills) (`plugin.json`, author "Atlassian Developer"), bundling six Forge-focused skills (app builder, review, cost optimizer, debugger, connector, security review) plus two MCP servers (Forge docs/tooling, Atlassian Design System lookup) declared in `.mcp.json`. Consolidation surfaces the bundled skills and MCP servers as read-only `containedSkills`/`containedMcpServers` on this single plugin entry, not as separate standalone approvals.

### Considered and excluded

- **`atlassian-labs/twg-plugins`** — a "skills-only plugin repository with thin adapters" that re-packages the `twg` CLI setup flow (a single `twg-setup` skill) for host-specific plugin loaders (Claude Code marketplace, Codex, Cursor, Devin, Qoder). Its manifest lives at `.claude-plugin/plugin.json` (a Claude-Code-specific format), not a repo-root `plugin.json` alongside a `skills/` folder and `mcp.json` the way [agent-plugins.org](https://agent-plugins.org) and this registry's Agent Plugin consolidation expect (see `atlassian/forge-skills` for what that looks like) — so it doesn't qualify as an Agent Plugin approval here. Its one skill is installer glue for the CLI already covered by the `atlassian/twg-cli` skills approval, so it isn't approved separately either.
- **A2A agents** — no Atlassian-published `agent_card.json` or equivalent A2A Agent Card was found. Atlassian is a listed A2A protocol launch partner, and a third-party MCP-to-A2A bridge exists for the Rovo Dev CLI, but neither is a first-party Atlassian Agent Card. No agent approval is included.
- **Rovo MCP Server (IDE/product-bundled variants)** — Atlassian's Rovo MCP server is already covered by the registry-listed `com.atlassian/atlassian-mcp-server` approval above; no separate approval was added for product-specific bundling.

## Documentation

See the [Vendor Guide](https://github.com/eclipsefdn-ai-registry/ai-registry-core#vendor-guide) in the central repository for how vendor repos work, how to add approvals, and how validation runs.
