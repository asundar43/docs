---
summary: "Uninstall SimpleClaw completely (CLI, service, state, workspace)"
read_when:
  - You want to remove SimpleClaw from a machine
  - The gateway service is still running after uninstall
title: "Uninstall"
---

# Uninstall

Two paths:

- **Easy path** if `simpleclaw` is still installed.
- **Manual service removal** if the CLI is gone but the service is still running.

## Easy path (CLI still installed)

Recommended: use the built-in uninstaller:

```bash
simpleclaw uninstall
```

Non-interactive (automation / npx):

```bash
simpleclaw uninstall --all --yes --non-interactive
npx -y simpleclaw uninstall --all --yes --non-interactive
```

Manual steps (same result):

1. Stop the gateway service:

```bash
simpleclaw gateway stop
```

2. Uninstall the gateway service (launchd/systemd/schtasks):

```bash
simpleclaw gateway uninstall
```

3. Delete state + config:

```bash
rm -rf "${SIMPLECLAW_STATE_DIR:-$HOME/.simpleclaw}"
```

If you set `SIMPLECLAW_CONFIG_PATH` to a custom location outside the state dir, delete that file too.

4. Delete your workspace (optional, removes agent files):

```bash
rm -rf ~/.simpleclaw/workspace
```

5. Remove the CLI install (pick the one you used):

```bash
npm rm -g simpleclaw
pnpm remove -g simpleclaw
bun remove -g simpleclaw
```

6. If you installed the macOS app:

```bash
rm -rf /Applications/SimpleClaw.app
```

Notes:

- If you used profiles (`--profile` / `SIMPLECLAW_PROFILE`), repeat step 3 for each state dir (defaults are `~/.simpleclaw-<profile>`).
- In remote mode, the state dir lives on the **gateway host**, so run steps 1-4 there too.

## Manual service removal (CLI not installed)

Use this if the gateway service keeps running but `simpleclaw` is missing.

### macOS (launchd)

Default label is `ai.simpleclaw.gateway` (or `ai.simpleclaw.<profile>`; legacy `com.simpleclaw.*` may still exist):

```bash
launchctl bootout gui/$UID/ai.simpleclaw.gateway
rm -f ~/Library/LaunchAgents/ai.simpleclaw.gateway.plist
```

If you used a profile, replace the label and plist name with `ai.simpleclaw.<profile>`. Remove any legacy `com.simpleclaw.*` plists if present.

### Linux (systemd user unit)

Default unit name is `simpleclaw-gateway.service` (or `simpleclaw-gateway-<profile>.service`):

```bash
systemctl --user disable --now simpleclaw-gateway.service
rm -f ~/.config/systemd/user/simpleclaw-gateway.service
systemctl --user daemon-reload
```

### Windows (Scheduled Task)

Default task name is `SimpleClaw Gateway` (or `SimpleClaw Gateway (<profile>)`).
The task script lives under your state dir.

```powershell
schtasks /Delete /F /TN "SimpleClaw Gateway"
Remove-Item -Force "$env:USERPROFILE\.simpleclaw\gateway.cmd"
```

If you used a profile, delete the matching task name and `~\.simpleclaw-<profile>\gateway.cmd`.

## Normal install vs source checkout

### Normal install (install.sh / npm / pnpm / bun)

If you used `the private npm registry` or `install.ps1`, the CLI was installed with `npm install -g simpleclaw@latest`.
Remove it with `npm rm -g simpleclaw` (or `pnpm remove -g` / `bun remove -g` if you installed that way).

### Source checkout (git clone)

If you run from a repo checkout (`git clone` + `simpleclaw ...` / `bun run simpleclaw ...`):

1. Uninstall the gateway service **before** deleting the repo (use the easy path above or manual service removal).
2. Delete the repo directory.
3. Remove state + workspace as shown above.
