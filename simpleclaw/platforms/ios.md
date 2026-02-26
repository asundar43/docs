---
summary: "iOS node app: connect to the Gateway, pairing, canvas, and troubleshooting"
read_when:
  - Pairing or reconnecting the iOS node
  - Running the iOS app from source
  - Debugging gateway discovery or canvas commands
title: "iOS App"
---

# iOS App (Node)

<Warning>
The iOS app is **coming soon**. This page describes planned functionality.
</Warning>

Availability: internal preview. The iOS app is not publicly distributed yet.

## What it does

- Connects to a Gateway over WebSocket (LAN or tailnet).
- Exposes node capabilities: Canvas, Screen snapshot, Camera capture, Location, Talk mode, Voice wake.
- Receives `node.invoke` commands and reports node status events.

## Requirements

- Gateway running on another device (macOS, Linux, or Windows via WSL2).
- Network path:
  - Same LAN via Bonjour, **or**
  - Tailnet via unicast DNS-SD (example domain: `simpleclaw.internal.`), **or**
  - Manual host/port (fallback).

## Quick start (pair + connect)

1. Start the Gateway:

```bash
simpleclaw gateway --port 18789
```

2. In the iOS app, open Settings and pick a discovered gateway (or enable Manual Host and enter host/port).

3. Approve the pairing request on the gateway host:

```bash
simpleclaw nodes pending
simpleclaw nodes approve <requestId>
```

4. Verify connection:

```bash
simpleclaw nodes status
simpleclaw gateway call node.list --params "{}"
```

## Discovery paths

### Bonjour (LAN)

The Gateway advertises `_simpleclaw-gw._tcp` on `local.`. The iOS app lists these automatically.

### Tailnet (cross-network)

If mDNS is blocked, use a unicast DNS-SD zone (choose a domain; example: `simpleclaw.internal.`) and Tailscale split DNS.
See [Bonjour](/gateway/bonjour) for the CoreDNS example.

### Manual host/port

In Settings, enable **Manual Host** and enter the gateway host + port (default `18789`).

## Canvas + A2UI

The iOS node renders a WKWebView canvas. Use `node.invoke` to drive it:

```bash
simpleclaw nodes invoke --node "iOS Node" --command canvas.navigate --params '{"url":"http://<gateway-host>:18789/__simpleclaw__/canvas/"}'
```

Notes:

- The Gateway canvas host serves `/__simpleclaw__/canvas/` and `/__simpleclaw__/a2ui/`.
- It is served from the Gateway HTTP server (same port as `gateway.port`, default `18789`).
- The iOS node auto-navigates to A2UI on connect when a canvas host URL is advertised.
- Return to the built-in scaffold with `canvas.navigate` and `{"url":""}`.

### Canvas eval / snapshot

```bash
simpleclaw nodes invoke --node "iOS Node" --command canvas.eval --params '{"javaScript":"(() => { const {ctx} = window.__simpleclaw; ctx.clearRect(0,0,innerWidth,innerHeight); ctx.lineWidth=6; ctx.strokeStyle=\"#ff2d55\"; ctx.beginPath(); ctx.moveTo(40,40); ctx.lineTo(innerWidth-40, innerHeight-40); ctx.stroke(); return \"ok\"; })()"}'
```

```bash
simpleclaw nodes invoke --node "iOS Node" --command canvas.snapshot --params '{"maxWidth":900,"format":"jpeg"}'
```

## Voice wake + talk mode

- Voice wake and talk mode are available in Settings.
- iOS may suspend background audio; treat voice features as best-effort when the app is not active.

## Common errors

- `NODE_BACKGROUND_UNAVAILABLE`: bring the iOS app to the foreground (canvas/camera/screen commands require it).
- `A2UI_HOST_NOT_CONFIGURED`: the Gateway did not advertise a canvas host URL; check `canvasHost` in [Gateway configuration](/gateway/configuration).
- Pairing prompt never appears: run `simpleclaw nodes pending` and approve manually.
- Reconnect fails after reinstall: the Keychain pairing token was cleared; re-pair the node.

## Related docs

- [Pairing](/gateway/pairing)
- [Discovery](/gateway/discovery)
- [Bonjour](/gateway/bonjour)
