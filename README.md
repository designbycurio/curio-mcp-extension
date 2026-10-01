# Curio MCP

Connect your AI to [Curio](https://designbycurio.com) — a design-style library
built for AI agents. Hundreds of tokenized design styles (real design
movements, brands, cultural traditions), each with a machine-readable spec
your agent can apply directly to slides, websites, and products.

- **Endpoint**: `https://mcp.designbycurio.com/mcp` (streamable HTTP)
- **Auth**: OAuth sign-in — no API key. Searching and browsing are free; 1 credit unlocks a style for good ([credit packs](https://designbycurio.com/pricing), never expire).
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

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](cursor://anysphere.cursor-deeplink/mcp/install?name=curio&config=eyJ1cmwiOiJodHRwczovL21jcC5kZXNpZ25ieWN1cmlvLmNvbS9tY3AifQ==)

Or add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "curio": { "url": "https://mcp.designbycurio.com/mcp" }
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

## Example prompts

- *"Find a Japanese minimal style and restyle my landing page with it."*
- *"Browse Curio for an 80s retro style that works for a dashboard."*
- *"Fetch the bauhaus-weimar spec and apply it to my slides."*
- *"How many Curio credits do I have left?"*

## Links

[Website](https://designbycurio.com) · [Gallery](https://designbycurio.com/gallery) · [Pricing](https://designbycurio.com/pricing) · [Docs](https://designbycurio.com/docs) · [Privacy](https://designbycurio.com/privacy) · [Terms](https://designbycurio.com/terms) · support@designbycurio.com
