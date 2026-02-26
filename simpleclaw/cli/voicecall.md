---
summary: "CLI reference for `simpleclaw voicecall` (voice-call plugin command surface)"
read_when:
  - You use the voice-call plugin and want the CLI entry points
  - You want quick examples for `voicecall call|continue|status|tail|expose`
title: "voicecall"
---

# `simpleclaw voicecall`

`voicecall` is a plugin-provided command. It only appears if the voice-call plugin is installed and enabled.

Primary doc:

- Voice-call plugin: [Voice Call](/plugins/voice-call)

## Common commands

```bash
simpleclaw voicecall status --call-id <id>
simpleclaw voicecall call --to "+15555550123" --message "Hello" --mode notify
simpleclaw voicecall continue --call-id <id> --message "Any questions?"
simpleclaw voicecall end --call-id <id>
```

## Exposing webhooks (Tailscale)

```bash
simpleclaw voicecall expose --mode serve
simpleclaw voicecall expose --mode funnel
simpleclaw voicecall expose --mode off
```

Security note: only expose the webhook endpoint to networks you trust. Prefer Tailscale Serve over Funnel when possible.
