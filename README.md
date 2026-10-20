# WA Smart Sender for Claude, ChatGPT and other AI apps

Run your WhatsApp Business account from your AI assistant. Read and answer customer conversations, manage contacts and tags, send approved templates, launch and track campaigns, tune your AI agents and check results in your [WA Smart Sender](https://wsmartsender.com) workspace, all from chat.

Everything connects to one address, and you sign in with your WA Smart Sender account. You don't need an API key:

```
https://public-api.wsmartsender.com/mcp
```

## Claude (claude.ai, Claude Desktop, mobile)

Add **WA Smart Sender** from the Connectors directory. Or go to **Settings → Connectors → Add custom connector**, paste the address above, and press **Connect**. Sign in, check the workspace and role, and approve.

## Claude Code

```
/plugin marketplace add unobuno/wasmartsender-ai
/plugin install wasmartsender@wasmartsender
```

Then run `/mcp` and choose **wasmartsender → Authenticate** to sign in. The plugin also adds a WhatsApp skill and two commands, `/whatsapp-inbox` and `/whatsapp-report`.

If you'd rather not use the plugin:

```
claude mcp add --transport http wasmartsender https://public-api.wsmartsender.com/mcp
```

## Codex

```
codex mcp add wasmartsender --url https://public-api.wsmartsender.com/mcp
codex mcp login wasmartsender
```

## ChatGPT

Find **WA Smart Sender** in the Apps directory. Or, with developer mode on, go to **Settings → Apps → Create**, paste the address, choose OAuth, and connect.

## Cursor, VS Code and other MCP clients

Add a remote (HTTP) MCP server with the address above. The client opens your browser so you can sign in. When you connect, choose **Read only** or **Read and change**.

## What it can do

When you connect from an app directory, your assistant gets the everyday tools: inbox, contacts, templates, campaigns, analytics, AI agents, knowledge base and orders. It can reach the full set of about 250 tools through `search_tools` and `run_tool`. See the [full tool reference](https://wsmartsender.com/developers).

## Safety

- The app acts with **your own role** (owner, admin or agent) and can only do what you can.
- Anything that messages customers or deletes data is marked so your assistant asks you first. Deletes and other risky actions also need an explicit confirmation.
- Every action is recorded in your workspace's audit log.
- You can disconnect at any time in **Settings → API keys**, and access stops immediately.

Privacy policy: https://wsmartsender.com/privacy · Terms: https://wsmartsender.com/terms · Support: hello@wsmartsender.com
