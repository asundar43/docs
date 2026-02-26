---
summary: "CLI reference for `simpleclaw agents` (list/add/delete/set identity)"
read_when:
  - You want multiple isolated agents (workspaces + routing + auth)
title: "agents"
---

# `simpleclaw agents`

Manage isolated agents (workspaces + auth + routing).

Related:

- Multi-agent routing: [Multi-Agent Routing](/concepts/multi-agent)
- Agent workspace: [Agent workspace](/concepts/agent-workspace)

## Examples

```bash
simpleclaw agents list
simpleclaw agents add work --workspace ~/.simpleclaw/workspace-work
simpleclaw agents set-identity --workspace ~/.simpleclaw/workspace --from-identity
simpleclaw agents set-identity --agent main --avatar avatars/simpleclaw.png
simpleclaw agents delete work
```

## Identity files

Each agent workspace can include an `IDENTITY.md` at the workspace root:

- Example path: `~/.simpleclaw/workspace/IDENTITY.md`
- `set-identity --from-identity` reads from the workspace root (or an explicit `--identity-file`)

Avatar paths resolve relative to the workspace root.

## Set identity

`set-identity` writes fields into `agents.list[].identity`:

- `name`
- `theme`
- `emoji`
- `avatar` (workspace-relative path, http(s) URL, or data URI)

Load from `IDENTITY.md`:

```bash
simpleclaw agents set-identity --workspace ~/.simpleclaw/workspace --from-identity
```

Override fields explicitly:

```bash
simpleclaw agents set-identity --agent main --name "SimpleClaw" --emoji "🦞" --avatar avatars/simpleclaw.png
```

Config sample:

```json5
{
  agents: {
    list: [
      {
        id: "main",
        identity: {
          name: "SimpleClaw",
          theme: "space lobster",
          emoji: "🦞",
          avatar: "avatars/simpleclaw.png",
        },
      },
    ],
  },
}
```
