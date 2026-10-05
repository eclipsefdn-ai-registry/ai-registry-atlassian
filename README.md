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

- **Atlassian Teamwork Graph CLI** (`io.github.atlassian-labs/twg-plugins`) — an [agent-plugins.org](https://agent-plugins.org)-conformant plugin at the root of [atlassian-labs/twg-plugins](https://github.com/atlassian-labs/twg-plugins): `plugin.json` declares `$schema: https://agent-plugins.org/schemas/1.0.0/plugin.schema.json`, name `atlassian-twg-cli`, author "Atlassian" (`https://www.atlassian.com`), homepage `https://developer.atlassian.com/cloud/twg-cli/`. It bundles the `twg-setup` skill (`skills/twg-setup/SKILL.md`) that connects the Teamwork Graph CLI to a coding agent, surfaced as `containedSkills`. This repo was previously excluded (see below) because it only carried host-specific manifests; it has since added a repo-root `plugin.json`, so it now qualifies. `atlassian-labs` is a GitHub-verified organisation with `atlassian.com` as its listed blog domain.

  This is the first approval here sourced from `atlassian-labs` rather than `atlassian`, so the basis is worth stating: it was admitted because the org is **independently** GitHub-verified *and* the artifact is documented on Atlassian's own developer-docs domain (`developer.atlassian.com`) — not because the org carries the vendor's name or because `plugin.json` names Atlassian as author. A manifest's self-declared author is not evidence on its own. Repos under other Atlassian-adjacent orgs still have to clear those same two signals individually; nothing is inherited from this entry.
- **Forge Skills** (`io.github.atlassian/forge-skills`) — an [agent-plugins.org](https://agent-plugins.org)-conformant plugin at the root of [atlassian/forge-skills](https://github.com/atlassian/forge-skills) (`plugin.json`, author "Atlassian Developer"), bundling six Forge-focused skills (app builder, review, cost optimizer, debugger, connector, security review) plus two MCP servers (Forge docs/tooling, Atlassian Design System lookup) declared in `.mcp.json`. Consolidation surfaces the bundled skills and MCP servers as read-only `containedSkills`/`containedMcpServers` on this single plugin entry, not as separate standalone approvals.

### Considered and excluded

- **`atlassian-labs/twg-plugins` — host-specific manifests and marketplace files.** The repo-root `plugin.json` is now approved as an Agent Plugin above; its sibling `.claude-plugin/`, `.codex-plugin/`, `.cursor-plugin/`, `.devin-plugin/`, `.grok-plugin/` and `.qoder-plugin/` manifests are host-specific repackagings of that same plugin and are not approved separately. Its `.agents/plugins/marketplace.json` is a single-entry self-wrapper pointing back at `twg-plugins` itself, not a curated index, so no marketplace approval was added. Its one skill (`skills/twg-setup`) is surfaced through the plugin's `containedSkills` and is not approved as a standalone Agent Skill.
- **`atlassian-labs/copilot-marketplace`** — carries only `.claude-plugin/marketplace.json`, a Claude-Code-specific format this registry's marketplace schema doesn't cover (it accepts only Codex `.agents/plugins/marketplace.json`), and that file is itself a single-entry self-wrapper (`"source": "./"`) for one canvas listing with no repo-root `plugin.json` underneath. Not approvable as either a marketplace or an Agent Plugin.
- **`atlassian-labs/roving-office`** — a Codex session visualiser authored by an individual ("Mike Cannon-Brookes") with only `.codex-plugin/`, `.claude-plugin/` and `openclaw-plugin/` manifests, no repo-root agent-plugins.org `plugin.json`.
- **`atlassian-labs/mcp-compressor`** — an MCP proxy/library that shrinks another server's tool surface. It has no fixed connectable endpoint of its own (the configuration depends entirely on which backend server it wraps), so it's a framework building block rather than a standalone MCP server artifact.
- **A2A agents** — no Atlassian-published `agent_card.json` or equivalent A2A Agent Card was found. Atlassian is a listed A2A protocol launch partner, and a third-party MCP-to-A2A bridge exists for the Rovo Dev CLI, but neither is a first-party Atlassian Agent Card. No agent approval is included.
- **Rovo MCP Server (IDE/product-bundled variants)** — Atlassian's Rovo MCP server is already covered by the registry-listed `com.atlassian/atlassian-mcp-server` approval above; no separate approval was added for product-specific bundling.

## Documentation

See the [Vendor Guide](https://github.com/eclipsefdn-ai-registry/ai-registry-core#vendor-guide) in the central repository for how vendor repos work, how to add approvals, and how validation runs.
