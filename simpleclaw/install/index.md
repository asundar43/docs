---
summary: "Install SimpleClaw — installer script, npm/pnpm, from source, Docker, and more"
read_when:
  - You need an install method other than the Getting Started quickstart
  - You want to deploy to a cloud platform
  - You need to update, migrate, or uninstall
title: "Install"
---

# Install

Already followed [Getting Started](/start/getting-started)? You're all set — this page is for alternative install methods, platform-specific instructions, and maintenance.

## System requirements

- **[Node 22+](/install/node)**
- macOS, Linux, or Windows
- `pnpm` only if you build from source
- Access to the SimpleClaw private registry (Google Artifact Registry)

<Note>
On Windows, we strongly recommend running SimpleClaw under [WSL2](https://learn.microsoft.com/en-us/windows/wsl/install).
</Note>

## Install methods

<Tip>
SimpleClaw is distributed via a **private npm registry** on Google Artifact Registry. You need GCP access to install.
</Tip>

<AccordionGroup>
  <Accordion title="npm (recommended)" icon="package" defaultOpen>
    ```bash
    npm install -g simpleclaw --registry https://us-central1-npm.pkg.dev/jarvis-486806/simpleclaw-npm
    simpleclaw onboard --install-daemon
    ```

    <Accordion title="sharp build errors?">
      If you have libvips installed globally (common on macOS via Homebrew) and `sharp` fails, force prebuilt binaries:

      ```bash
      SHARP_IGNORE_GLOBAL_LIBVIPS=1 npm install -g simpleclaw --registry https://us-central1-npm.pkg.dev/jarvis-486806/simpleclaw-npm
      ```

      If you see `sharp: Please add node-gyp to your dependencies`, either install build tooling (macOS: Xcode CLT + `npm install -g node-gyp`) or use the env var above.
    </Accordion>
  </Accordion>

  <Accordion title="pnpm" icon="package">
    ```bash
    pnpm add -g simpleclaw --registry https://us-central1-npm.pkg.dev/jarvis-486806/simpleclaw-npm
    pnpm approve-builds -g        # approve simpleclaw, node-llama-cpp, sharp, etc.
    simpleclaw onboard --install-daemon
    ```

    <Note>
    pnpm requires explicit approval for packages with build scripts. After the first install shows the "Ignored build scripts" warning, run `pnpm approve-builds -g` and select the listed packages.
    </Note>
  </Accordion>

  <Accordion title="From source" icon="github">
    For contributors or anyone who wants to run from a local checkout.

    <Steps>
      <Step title="Clone and build">
        Clone the [SimpleClaw repo](https://github.com/simpleclaw/simpleclaw) and build:

        ```bash
        git clone https://github.com/simpleclaw/simpleclaw.git
        cd simpleclaw
        pnpm install
        pnpm ui:build
        pnpm build
        ```
      </Step>
      <Step title="Link the CLI">
        Make the `simpleclaw` command available globally:

        ```bash
        pnpm link --global
        ```

        Alternatively, skip the link and run commands via `pnpm simpleclaw ...` from inside the repo.
      </Step>
      <Step title="Run onboarding">
        ```bash
        simpleclaw onboard --install-daemon
        ```
      </Step>
    </Steps>

    For deeper development workflows, see [Setup](/start/setup).

  </Accordion>
</AccordionGroup>

## Other install methods

<CardGroup cols={2}>
  <Card title="Docker" href="/install/docker" icon="container">
    Containerized or headless deployments.
  </Card>
  <Card title="Podman" href="/install/podman" icon="container">
    Rootless container: run `setup-podman.sh` once, then the launch script.
  </Card>
  <Card title="Nix" href="/install/nix" icon="snowflake">
    Declarative install via Nix.
  </Card>
  <Card title="Ansible" href="/install/ansible" icon="server">
    Automated fleet provisioning.
  </Card>
  <Card title="Bun" href="/install/bun" icon="zap">
    CLI-only usage via the Bun runtime.
  </Card>
</CardGroup>

## After install

Verify everything is working:

```bash
simpleclaw doctor         # check for config issues
simpleclaw status         # gateway status
simpleclaw dashboard      # open the browser UI
```

If you need custom runtime paths, use:

- `SIMPLECLAW_HOME` for home-directory based internal paths
- `SIMPLECLAW_STATE_DIR` for mutable state location
- `SIMPLECLAW_CONFIG_PATH` for config file location

See [Environment vars](/help/environment) for precedence and full details.

## Troubleshooting: `simpleclaw` not found

<Accordion title="PATH diagnosis and fix">
  Quick diagnosis:

```bash
node -v
npm -v
npm prefix -g
echo "$PATH"
```

If `$(npm prefix -g)/bin` (macOS/Linux) or `$(npm prefix -g)` (Windows) is **not** in your `$PATH`, your shell can't find global npm binaries (including `simpleclaw`).

Fix — add it to your shell startup file (`~/.zshrc` or `~/.bashrc`):

```bash
export PATH="$(npm prefix -g)/bin:$PATH"
```

On Windows, add the output of `npm prefix -g` to your PATH.

Then open a new terminal (or `rehash` in zsh / `hash -r` in bash).
</Accordion>

## Update / uninstall

<CardGroup cols={3}>
  <Card title="Updating" href="/install/updating" icon="refresh-cw">
    Keep SimpleClaw up to date.
  </Card>
  <Card title="Migrating" href="/install/migrating" icon="arrow-right">
    Move to a new machine.
  </Card>
  <Card title="Uninstall" href="/install/uninstall" icon="trash-2">
    Remove SimpleClaw completely.
  </Card>
</CardGroup>
