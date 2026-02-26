---
summary: "CLI reference for `simpleclaw reset` (reset local state/config)"
read_when:
  - You want to wipe local state while keeping the CLI installed
  - You want a dry-run of what would be removed
title: "reset"
---

# `simpleclaw reset`

Reset local config/state (keeps the CLI installed).

```bash
simpleclaw reset
simpleclaw reset --dry-run
simpleclaw reset --scope config+creds+sessions --yes --non-interactive
```
