---
summary: "CLI reference for `simpleclaw pairing` (approve/list pairing requests)"
read_when:
  - You’re using pairing-mode DMs and need to approve senders
title: "pairing"
---

# `simpleclaw pairing`

Approve or inspect DM pairing requests (for channels that support pairing).

Related:

- Pairing flow: [Pairing](/channels/pairing)

## Commands

```bash
simpleclaw pairing list telegram
simpleclaw pairing list --channel telegram --account work
simpleclaw pairing list telegram --json

simpleclaw pairing approve telegram <code>
simpleclaw pairing approve --channel telegram --account work <code> --notify
```

## Notes

- Channel input: pass it positionally (`pairing list telegram`) or with `--channel <channel>`.
- `pairing list` supports `--account <accountId>` for multi-account channels.
- `pairing approve` supports `--account <accountId>` and `--notify`.
- If only one pairing-capable channel is configured, `pairing approve <code>` is allowed.
