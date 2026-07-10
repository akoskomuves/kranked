# Kranked

App Store keyword research for your AI coding assistant. Ask Claude, Cursor, or any
MCP client how hard a keyword is, how popular it is, and where your app ranks — without
leaving the editor.

Kranked is an [MCP](https://modelcontextprotocol.io) server. The free tools run locally
and use Apple's own public data. No dashboard, no API keys.

## Install

```bash
# any MCP client
uvx kranked-mcp

# Claude Code
claude mcp add kranked -- uvx kranked-mcp
```

Then just ask:

> "Use kranked to check the keyword *habit tracker* — how hard is it, how popular, and where does my app rank?"

## Tools

| Tool | What it answers |
|---|---|
| `search_apps` | Find apps (and their App Store id) matching a term |
| `check_keyword` | One-shot: difficulty + popularity + competitors, and your app's rank |
| `keyword_difficulty` | How hard a keyword is to rank for (0–100), with the top-10 competitors |
| `keyword_popularity` | How searched a keyword is (Apple suggest signal) |
| `keyword_suggestions` | Apple's autocomplete hints for a seed term |

All tools take a two-letter `country` (default `us`).

### How the scores work

- **Difficulty (0–100)** looks at the top-10 ranking apps' review volume and rating quality.
  More established competitors means a harder keyword. Labeled Very Easy through Very Hard.
- **Popularity** is a free, Apple-derived proxy based on whether Apple auto-suggests the term.

## Hosted version

A hosted version adds **real Apple Search Ads keyword popularity** (a 0–100 index) and a few
extras, and needs zero local setup. It's in early access — reach out if you'd like in.

## About

Built by [Akos Komuves](https://tallpoppy.xyz) (Tall Poppy). Kranked started as a native
macOS/iOS ASO app; this is the same keyword engine, exposed to your agent.

MIT licensed.
