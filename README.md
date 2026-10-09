# Leva-Companion

## Copilot development environment

The `.github/workflows/copilot-setup-steps.yml` workflow installs Flutter
3.35.7 (stable) and preloads Android artifacts before Copilot starts working.
It also supports manual runs and runs when the workflow changes.
There is no Flutter application in this repository yet.

To enable the environment:

1. Merge the setup workflow into the repository's **default branch**. Copilot
   does not use setup workflows that exist only on a task branch.
2. In **Settings → Copilot → Coding agent**, add `storage.googleapis.com` to
   the firewall's custom allowlist and save. Flutter uses this host for SDK
   and engine downloads. Package downloads also require access to `pub.dev`.
   A chat message cannot update these settings.
3. Run **Copilot Setup Steps** from the repository's **Actions** tab to verify
   installation. If it fails, inspect the failed step's logs.
4. Start a new Copilot task asking it to resume the authorized Android/iOS
   Flutter port.

Setup steps run before the agent firewall is enabled, so preloading avoids
the initial SDK download being blocked during an agent session. The allowlist
is still needed for additional downloads while the agent works. This workflow
does not change firewall settings or start a new Copilot task.

The Linux runner supports Android development. Building and signing iOS apps
requires a separate macOS environment with Xcode.

See [GitHub's environment customization guide](https://docs.github.com/en/copilot/customizing-copilot/customizing-the-development-environment-for-copilot-coding-agent)
and [firewall configuration guide](https://docs.github.com/en/copilot/customizing-copilot/customizing-or-disabling-the-firewall-for-copilot-coding-agent).