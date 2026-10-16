# Curio MCP

Connect your AI to [Curio](https://designbycurio.com) — a design-style library
built for AI agents. Hundreds of tokenized design styles (real design
movements, brands, cultural traditions), each with a machine-readable spec
your agent can apply directly to slides, websites, and products.

- **Endpoint**: `https://mcp.designbycurio.com/mcp` (streamable HTTP)
- **Auth**: OAuth sign-in for most clients. A client that can't open a browser to sign in uses a personal [API key](#api-key) instead. Searching and browsing are free; 1 credit unlocks a style for good ([credit packs](https://designbycurio.com/pricing), never expire).
- **Protocol**: MCP 2026-07-28 and the 2025 revisions
- **Docs**: [designbycurio.com/docs](https://designbycurio.com/docs)

## Tools

| Tool | What it does | Cost |
|---|---|---|
| `search_styles` | Keyword + facet search over the library | free |
| `list_styles` | Browse / paginate, filtered by facets | free |
| `get_style` | Metadata + preview image for one style | free |
| `get_style_spec` | Full design spec (DESIGN.md) for a style you've unlocked; for a locked style it returns the cost and your balance instead | free |
| `unlock_style` | Unlock a style for good and return its spec — your AI asks you first | 1 credit, once per style |
| `get_balance` | Your credit balance and how many styles you've unlocked | free |

Your AI never spends a credit on its own: `get_style_spec` only reads, and `unlock_style` is meant to be called after you agree. Unlocking a style you already own costs nothing.

## Install

### Gemini CLI

```bash
gemini extensions install https://github.com/designbycurio/curio-mcp-extension
```

### Claude Code

```bash
claude mcp add --transport http curio https://mcp.designbycurio.com/mcp
```

### Claude.ai / Claude Desktop

Settings → Connectors → **Add custom connector** → `https://mcp.designbycurio.com/mcp`

### Cursor

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=curio&config=eyJ1cmwiOiJodHRwczovL21jcC5kZXNpZ25ieWN1cmlvLmNvbS9tY3AifQ==)

The button opens Cursor and adds Curio for you. Or add it to `~/.cursor/mcp.json` yourself — Cursor opens a browser to sign in on first use:

```json
{
  "mcpServers": {
    "curio": { "url": "https://mcp.designbycurio.com/mcp" }
  }
}
```

### VS Code (Copilot)

[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Curio-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=curio&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.designbycurio.com%2Fmcp%22%7D) [![Install in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_Curio-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=curio&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.designbycurio.com%2Fmcp%22%7D&quality=insiders)

The button opens VS Code and installs Curio in your user MCP config. Or add it to `.vscode/mcp.json` yourself — VS Code opens a browser to authorize on first connect:

```json
{
  "servers": {
    "curio": { "type": "http", "url": "https://mcp.designbycurio.com/mcp" }
  }
}
```

### Codex (CLI / IDE extension)

```bash
codex mcp add curio --url https://mcp.designbycurio.com/mcp
```

### Kimi Code CLI

```bash
kimi mcp add --transport http --auth oauth curio https://mcp.designbycurio.com/mcp
```

### ChatGPT

Settings → Apps & Connectors → **Developer mode** → add `https://mcp.designbycurio.com/mcp`.

## API key

Some clients can't open a browser to sign in — they only have a field for a token (ZCode, WorkBuddy, Qoder, Trae, Cherry Studio, Antigravity, Manus…). For those, create a personal API key and send it as a request header. Clients that can sign in with OAuth don't need one.

1. Sign in at designbycurio.com and open [Account → Connected apps → API keys](https://designbycurio.com/account/connected#api-keys). Name the key after the client and create it.
2. Copy the key straight away — it starts with `curio_sk_` and is shown only once.
3. In the client's MCP settings, add the server URL with this header:

```
Authorization: Bearer curio_sk_…
```

Most clients take a JSON block like this. Some name the address field `serverUrl` or `httpUrl`, or ask for a transport type — pick **streamable HTTP**.

```json
{
  "mcpServers": {
    "curio": {
      "url": "https://mcp.designbycurio.com/mcp",
      "headers": { "Authorization": "Bearer curio_sk_…" }
    }
  }
}
```

**Claude Code** takes the header on the command line:

```bash
claude mcp add --transport http curio https://mcp.designbycurio.com/mcp --header "Authorization: Bearer curio_sk_…"
```

**Codex** reads the key from an environment variable, so it never sits in a config file:

```bash
export CURIO_API_KEY=curio_sk_…
codex mcp add curio --url https://mcp.designbycurio.com/mcp --bearer-token-env-var CURIO_API_KEY
```

**VS Code** can prompt for the key and store it securely instead of writing it into `mcp.json`:

```json
{
  "inputs": [
    { "type": "promptString", "id": "curio-key", "description": "Curio API key", "password": true }
  ],
  "servers": {
    "curio": {
      "type": "http",
      "url": "https://mcp.designbycurio.com/mcp",
      "headers": { "Authorization": "Bearer ${input:curio-key}" }
    }
  }
}
```

**Two kinds of key.** A read-only key (the default) can search, browse and fetch styles you've already unlocked, and never spends credits. Tick **Allow it to spend credits to unlock styles** when you create a key and your AI may also call `unlock_style` — after asking you, same as over OAuth. Treat a key like a password: don't paste it into a chat or commit it to a repo. Revoke it any time on the same page; clients using it stop working within 30 seconds.

## Example prompts

- *"Find a Japanese minimal style and restyle my landing page with it."*
- *"Browse Curio for an 80s retro style that works for a dashboard."*
- *"Fetch the bauhaus-weimar spec and apply it to my slides."*
- *"How many Curio credits do I have left?"*

## Links

[Website](https://designbycurio.com) · [Gallery](https://designbycurio.com/gallery) · [Pricing](https://designbycurio.com/pricing) · [Docs](https://designbycurio.com/docs) · [Privacy](https://designbycurio.com/privacy) · [Terms](https://designbycurio.com/terms) · support@designbycurio.com
