---
summary: "CLI reference for `simpleclaw daemon` (legacy alias for gateway service management)"
read_when:
  - You still use `simpleclaw daemon ...` in scripts
  - You need service lifecycle commands (install/start/stop/restart/status)
title: "daemon"
---

# `simpleclaw daemon`

Legacy alias for Gateway service management commands.

`simpleclaw daemon ...` maps to the same service control surface as `simpleclaw gateway ...` service commands.

## Usage

```bash
simpleclaw daemon status
simpleclaw daemon install
simpleclaw daemon start
simpleclaw daemon stop
simpleclaw daemon restart
simpleclaw daemon uninstall
```

## Subcommands

- `status`: show service install state and probe Gateway health
- `install`: install service (`launchd`/`systemd`/`schtasks`)
- `uninstall`: remove service
- `start`: start service
- `stop`: stop service
- `restart`: restart service

## Common options

- `status`: `--url`, `--token`, `--password`, `--timeout`, `--no-probe`, `--deep`, `--json`
- `install`: `--port`, `--runtime <node|bun>`, `--token`, `--force`, `--json`
- lifecycle (`uninstall|start|stop|restart`): `--json`

## Prefer

Use [`simpleclaw gateway`](/cli/gateway) for current docs and examples.
