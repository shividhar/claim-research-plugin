# Claim Research for Codex

Read completed research findings, exact source quotes, source links, and saved
conversation context in Codex. Requires an authorized Claim Research account.

Copy this prompt into Codex:

```text
Set up the Claim Research native Codex plugin from https://github.com/shividhar/claim-research-plugin. Install it and help me connect my account.
```

1. Let Codex install the plugin and open the sign-in page.
2. Sign in with your own Claim Research account in the browser and approve read
   access and remembered login.
3. Restart Codex if requested, open a new chat, then paste:

   ```text
   Use Claim Research to read this run: <run URL>.
   Show an exact quote, its source link, and relevant saved parent context.
   ```

No Claim Research CLI installation is needed. Codex manages the connection.
Installing the plugin does not grant access to research data; an administrator
must enable your account first.

## For the setup agent

Use the CLI bundled with the running Codex desktop app when available so the
versions match. This connection was tested with Codex 0.171.0-alpha.13. On macOS,
the bundled CLI is at
`/Applications/ChatGPT.app/Contents/Resources/codex-cli/CodexCLI.app/Contents/MacOS/codex`.
Preserve other plugins and settings. Run these commands with that binary:

```sh
codex plugin marketplace add https://github.com/shividhar/claim-research-plugin.git --json
codex plugin add claim-research@claim-research-internal --json
codex mcp login claim_research
```

The login command resolves the plugin's bundled MCP configuration and opens
browser sign-in. Keep the process running until sign-in completes. Tell the
user when to restart Codex or start a new chat. Do not ask them to edit TOML,
run keychain commands, or handle tokens. Keep sign-in URLs and tokens out of chat.
Do not create a separate manual MCP entry. If a manual `claim_research` entry
already exists, it overrides the plugin. After verifying plugin installation,
back up that entry privately and use `codex mcp remove claim_research` to remove
only that manual entry before login. Preserve all other settings and credentials.

This repository contains only public plugin metadata and connection settings.
The existing hosted MCP server enforces Clerk sign-in and reader authorization.
