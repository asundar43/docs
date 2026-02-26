---
summary: "CLI reference for `simpleclaw devices` (device pairing + token rotation/revocation)"
read_when:
  - You are approving device pairing requests
  - You need to rotate or revoke device tokens
title: "devices"
---

# `simpleclaw devices`

Manage device pairing requests and device-scoped tokens.

## Commands

### `simpleclaw devices list`

List pending pairing requests and paired devices.

```
simpleclaw devices list
simpleclaw devices list --json
```

### `simpleclaw devices remove <deviceId>`

Remove one paired device entry.

```
simpleclaw devices remove <deviceId>
simpleclaw devices remove <deviceId> --json
```

### `simpleclaw devices clear --yes [--pending]`

Clear paired devices in bulk.

```
simpleclaw devices clear --yes
simpleclaw devices clear --yes --pending
simpleclaw devices clear --yes --pending --json
```

### `simpleclaw devices approve [requestId] [--latest]`

Approve a pending device pairing request. If `requestId` is omitted, SimpleClaw
automatically approves the most recent pending request.

```
simpleclaw devices approve
simpleclaw devices approve <requestId>
simpleclaw devices approve --latest
```

### `simpleclaw devices reject <requestId>`

Reject a pending device pairing request.

```
simpleclaw devices reject <requestId>
```

### `simpleclaw devices rotate --device <id> --role <role> [--scope <scope...>]`

Rotate a device token for a specific role (optionally updating scopes).

```
simpleclaw devices rotate --device <deviceId> --role operator --scope operator.read --scope operator.write
```

### `simpleclaw devices revoke --device <id> --role <role>`

Revoke a device token for a specific role.

```
simpleclaw devices revoke --device <deviceId> --role node
```

## Common options

- `--url <url>`: Gateway WebSocket URL (defaults to `gateway.remote.url` when configured).
- `--token <token>`: Gateway token (if required).
- `--password <password>`: Gateway password (password auth).
- `--timeout <ms>`: RPC timeout.
- `--json`: JSON output (recommended for scripting).

Note: when you set `--url`, the CLI does not fall back to config or environment credentials.
Pass `--token` or `--password` explicitly. Missing explicit credentials is an error.

## Notes

- Token rotation returns a new token (sensitive). Treat it like a secret.
- These commands require `operator.pairing` (or `operator.admin`) scope.
- `devices clear` is intentionally gated by `--yes`.
- If pairing scope is unavailable on local loopback (and no explicit `--url` is passed), list/approve can use a local pairing fallback.
