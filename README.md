# Claim Research for Codex

Read completed research findings, exact source quotes, source links, and saved
conversation context in Codex. Requires an authorized Claim Research account.

Copy this prompt into Codex:

```text
Set up the Claim Research native Codex plugin from https://github.com/shividhar/claim-research-plugin. Install it and help me connect my account.
```

1. Select **Connect** when prompted.
2. Sign in with your own Claim Research account in the browser and approve read
   access.
3. Open a new chat, then paste:

   ```text
   Use Claim Research to read this run: <run URL>.
   Show an exact quote, its source link, and relevant saved parent context.
   ```

No Claim Research CLI installation is needed. Codex manages the connection.
Installing the plugin does not grant access to research data; an administrator
must enable your account first.

## For the setup agent

Use a current Codex version with plugin commands. Preserve other plugins and
settings:

```sh
codex plugin marketplace add https://github.com/shividhar/claim-research-plugin.git --json
codex plugin add claim-research@claim-research-internal --json
```

If `codex` is unavailable or too old on macOS, check the desktop app's bundled
CLI at `/Applications/ChatGPT.app/Contents/Resources/codex-cli/CodexCLI.app/Contents/MacOS/codex`.
Use the supported plugin connection flow and tell the user when to restart
Codex or start a new chat. Do not ask them to edit TOML, run keychain commands,
or handle tokens. Do not create a separate manual MCP entry. If a manual
`claim_research` connection already exists, explain the duplicate and preserve
it until the plugin connection has been verified; do not blindly delete it.

This repository contains only public plugin metadata and connection settings.
The existing hosted MCP server enforces Clerk sign-in and reader authorization.
