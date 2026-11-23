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
3. Wait for Codex to confirm sign-in succeeded, restart if requested, and open a
   new chat. Copy the full run URL from the research website, then paste:

   ```text
   Use Claim Research to read this run: <full research run URL>.
   Show an exact quote, its source link, and relevant saved parent context.
   ```

No Claim Research CLI installation is needed. Codex manages the connection.
Installing the plugin does not grant access to research data; an administrator
must enable your account first.

If Codex reports **Auth required**, paste this recovery prompt:

```text
Read https://github.com/shividhar/claim-research-plugin and repair my Claim Research connection. Complete browser sign-in and verify schema access before saying it is connected. Preserve my other settings and credentials.
```

## For the setup agent

Use the CLI bundled with the running Codex desktop app when available so the
versions match. This connection was tested with Codex 0.171.0-alpha.13. On macOS,
the bundled CLI is at
`/Applications/ChatGPT.app/Contents/Resources/codex-cli/CodexCLI.app/Contents/MacOS/codex`.
Preserve other plugins and settings. Confirm the CLI uses the desktop app's
effective Codex home (`CODEX_HOME`) and OAuth credential store; inspect only the
needed settings and paths, not credentials or full process environments. Run these commands with that binary and
the same environment:

```sh
codex plugin marketplace add https://github.com/shividhar/claim-research-plugin.git --json
codex plugin add claim-research@claim-research-internal --json
codex mcp login claim_research
```

The login command resolves the plugin's bundled MCP configuration and opens
browser sign-in. Keep it running until it exits successfully (exit code 0);
opening the browser or clicking consent does not establish that login completed.
Refresh the desktop MCP connection after login; if it still has cached
unauthenticated state, help the user restart Codex and open a new chat.

Verify that the desktop can read `urn:claim-research:findings:4`. If the user
provides a run URL, call `get_findings` with that full website URL, not a bare
run ID. An **Auth required** initialization error happens before run lookup;
repair the connection before diagnosing the URL or interpreting findings. Do
not report success from CLI login alone. Do not ask users to edit TOML, run
keychain commands, or handle tokens. Keep sign-in URLs and tokens out of chat.
Do not treat an empty `codex mcp list` as proof the plugin is missing: the
tested client can omit plugin-provided servers from that command. Use the
desktop schema read as the connection check.
Do not log out, delete credentials, or terminate unrelated processes to repair
the connection.

Do not create a separate manual MCP entry. If a manual `claim_research` entry
already exists, it overrides the plugin. Confirm it points to this plugin's
Claim Research API before migrating it. After verifying plugin installation,
back up that entry privately and remove only the confirmed manual duplicate
with `codex mcp remove claim_research` before login. Preserve all other settings
and credentials.

The current deployment intentionally pairs the website
`https://claim-research-production-web.onrender.com` with the API
`https://claim-research-demo-api.onrender.com/mcp`. The different hostnames do
not imply a wrong endpoint. Use the plugin's bundled API URL.

This repository contains only public plugin metadata and connection settings.
The existing hosted MCP server enforces Clerk sign-in and reader authorization.
