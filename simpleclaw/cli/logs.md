---
summary: "CLI reference for `simpleclaw logs` (tail gateway logs via RPC)"
read_when:
  - You need to tail Gateway logs remotely (without SSH)
  - You want JSON log lines for tooling
title: "logs"
---

# `simpleclaw logs`

Tail Gateway file logs over RPC (works in remote mode).

Related:

- Logging overview: [Logging](/logging)

## Examples

```bash
simpleclaw logs
simpleclaw logs --follow
simpleclaw logs --json
simpleclaw logs --limit 500
simpleclaw logs --local-time
simpleclaw logs --follow --local-time
```

Use `--local-time` to render timestamps in your local timezone.
