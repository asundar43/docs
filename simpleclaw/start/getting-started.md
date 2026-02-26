---
summary: "Get SimpleClaw installed and run your first chat in minutes."
read_when:
  - First time setup from zero
  - You want the fastest path to a working chat
title: "Getting Started"
---

# Getting Started

Goal: go from zero to a first working chat with minimal setup.

<Info>
Fastest chat: open the Control UI (no channel setup needed). Run `simpleclaw dashboard`
and chat in the browser, or open `http://127.0.0.1:18789/` on the
<Tooltip headline="Gateway host" tip="The machine running the SimpleClaw gateway service.">gateway host</Tooltip>.
Docs: [Dashboard](/web/dashboard) and [Control UI](/web/control-ui).
</Info>

## Prereqs

- Node 22 or newer

<Tip>
Check your Node version with `node --version` if you are unsure.
</Tip>

## Quick setup (CLI)

<Steps>
  <Step title="Install SimpleClaw">
    ```bash
    npm install -g simpleclaw --registry https://us-central1-npm.pkg.dev/jarvis-486806/simpleclaw-npm
    ```

    <Note>
    Other install methods and requirements: [Install](/install).
    </Note>

  </Step>
  <Step title="Run the onboarding wizard">
    ```bash
    simpleclaw onboard --install-daemon
    ```

    The wizard configures auth, gateway settings, and optional channels.
    See [Onboarding Wizard](/start/wizard) for details.

  </Step>
  <Step title="Check the Gateway">
    If you installed the service, it should already be running:

    ```bash
    simpleclaw gateway status
    ```

  </Step>
  <Step title="Open the Control UI">
    ```bash
    simpleclaw dashboard
    ```
  </Step>
</Steps>

<Check>
If the Control UI loads, your Gateway is ready for use.
</Check>

## Optional checks and extras

<AccordionGroup>
  <Accordion title="Run the Gateway in the foreground">
    Useful for quick tests or troubleshooting.

    ```bash
    simpleclaw gateway --port 18789
    ```

  </Accordion>
  <Accordion title="Send a test message">
    Requires a configured channel.

    ```bash
    simpleclaw message send --target +15555550123 --message "Hello from SimpleClaw"
    ```

  </Accordion>
</AccordionGroup>

## Useful environment variables

If you run SimpleClaw as a service account or want custom config/state locations:

- `SIMPLECLAW_HOME` sets the home directory used for internal path resolution.
- `SIMPLECLAW_STATE_DIR` overrides the state directory.
- `SIMPLECLAW_CONFIG_PATH` overrides the config file path.

Full environment variable reference: [Environment vars](/help/environment).

## Go deeper

<Columns>
  <Card title="Onboarding Wizard (details)" href="/start/wizard">
    Full CLI wizard reference and advanced options.
  </Card>
  <Card title="Marketplace" href="/tools/marketplace">
    Browse and install skills from the private catalog.
  </Card>
</Columns>

## What you will have

- A running Gateway
- Auth configured
- Control UI access or a connected channel

## Next steps

- DM safety and approvals: [Pairing](/channels/pairing)
- Connect more channels: [Channels](/channels)
- Advanced workflows and from source: [Setup](/start/setup)
