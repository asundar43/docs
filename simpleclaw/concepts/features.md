---
summary: "SimpleClaw capabilities across channels, routing, media, marketplace, and UX."
read_when:
  - You want a full list of what SimpleClaw supports
title: "Features"
---

## Highlights

<Columns>
  <Card title="Channels" icon="message-square">
    WhatsApp, Telegram, Discord, and iMessage with a single Gateway.
  </Card>
  <Card title="Plugins" icon="plug">
    Add Mattermost and more with extensions.
  </Card>
  <Card title="Routing" icon="route">
    Multi-agent routing with isolated sessions.
  </Card>
  <Card title="Media" icon="image">
    Images, audio, and documents in and out.
  </Card>
  <Card title="Web Control UI" icon="monitor">
    Browser dashboard for chat, config, and sessions.
  </Card>
  <Card title="Skill marketplace" icon="store">
    Private catalog of curated skills and plugins via GAR and GCS.
  </Card>
</Columns>

## Full list

- WhatsApp integration via WhatsApp Web (Baileys)
- Telegram bot support (grammY)
- Discord bot support (channels.discord.js)
- Mattermost bot support (plugin)
- iMessage integration via local imsg CLI (macOS)
- Agent bridge for Pi in RPC mode with tool streaming
- Streaming and chunking for long responses
- Multi-agent routing for isolated sessions per workspace or sender
- Subscription auth for Anthropic and OpenAI via OAuth
- Sessions: direct chats collapse into shared `main`; groups are isolated
- Group chat support with mention based activation
- Media support for images, audio, and documents
- Optional voice note transcription hook
- WebChat browser interface
- Private skill marketplace backed by Google Artifact Registry and Google Cloud Storage
- Marketplace CLI: `simpleclaw marketplace list`, `search`, `install`, `sync`, `publish`

<Note>
Legacy Claude, Codex, Gemini, and Opencode paths have been removed. Pi is the only
coding agent path.
</Note>
