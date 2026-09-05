# Kranked

App Store keyword research for your AI coding assistant. Ask Claude, Cursor, or any
MCP client how hard a keyword is, how popular it is, and where your app ranks — without
leaving the editor.

Kranked is an [MCP](https://modelcontextprotocol.io) server. It runs locally on your own
machine, uses Apple's own public endpoints, and needs no account, no dashboard and no API
key.

## Install

Needs Python 3.10+ and [uv](https://docs.astral.sh/uv/) (`brew install uv`).

```bash
# Claude Code
claude mcp add kranked -- uvx kranked-mcp
```

Claude Desktop or Cursor — add this to your MCP config:

```json
{
  "mcpServers": {
    "kranked": {
      "command": "uvx",
      "args": ["kranked-mcp"]
    }
  }
}
```

Restart the client, then just ask:

> "Use kranked to check the keyword *habit tracker* — how hard is it, how popular, and where does my app rank?"

## Tools

| Tool | What it answers |
|---|---|
| `search_apps` | Find apps (and their App Store id) matching a term |
| `check_keyword` | One-shot: difficulty + popularity + KEI + competitors, and your app's rank |
| `keyword_difficulty` | How hard a keyword is to rank for (0–100), with the top-10 competitors |
| `keyword_popularity` | How searched a keyword is (0–100) |
| `popular_keywords` | The most-searched keywords in a category, ranked |
| `keyword_suggestions` | Apple's autocomplete hints for a seed term |

All tools take a two-letter `country` (default `us`).

### How the scores work

- **Difficulty (0–100)** looks at the top-10 ranking apps' review volume and rating quality.
  More established competitors means a harder keyword. Labeled Very Easy through Very Hard.
- **Popularity (0–100)** has two sources, and every answer tells you which one it used.
  Out of the box it's a free proxy derived from whether Apple auto-suggests the term. Add
  your own Apple Search Ads credentials and it becomes Apple's real `searchPopularity`
  index instead — see below.
- **KEI** is popularity ÷ difficulty. Higher is a better bet.
- **Rank** is read from the App Store's own search ordering rather than the public iTunes
  Search API, because the documented Search API doesn't return the store's real ordering.

### Real popularity numbers (optional, bring your own key)

Apple's `searchPopularity` is scoped to an Apple Search Ads account, so it needs **your**
account — free to create, no ad spend required. The keys stay on your machine.

```bash
uvx --with 'kranked-mcp[appleads]' kranked-mcp
```

Then set `KRANKED_APPLEADS_CLIENT_ID`, `_TEAM_ID`, `_KEY_ID`, `_ORG_ID` and
`_PRIVATE_KEY` (or `_PRIVATE_KEY_PATH`). Without them nothing breaks — popularity just
falls back to the free proxy.

## About

Built by [Akos Komuves](https://tallpoppystudio.com) (Tall Poppy). Kranked started as a
native macOS/iOS ASO app; this is the same keyword engine, exposed to your agent.

Questions or bugs: [open an issue](https://github.com/akoskomuves/kranked/issues).

MIT licensed.
