<div align="center">

# Astrolabe

### Dune-style on-chain dashboards, with a free MCP server for your agent.

[![Open Astrolabe](https://img.shields.io/badge/open-astrolabe.cartographer.club-7c6ff0?style=flat-square)](https://astrolabe.cartographer.club/)
[![MCP setup](https://img.shields.io/badge/MCP-setup-2a6df4?style=flat-square)](https://astrolabe.cartographer.club/agents)
[![Research](https://img.shields.io/badge/Substack-free%20research-ff6719?style=flat-square)](https://onchaindivers.substack.com/)
[![X](https://img.shields.io/badge/X-follow-000000?style=flat-square)](https://x.com/onchain_divers)
[![Telegram](https://img.shields.io/badge/Telegram-ask%20us-2ea043?style=flat-square)](https://t.me/inventandchill)

**Free · no sign-up · no API key · ~90 days of data · 8 databases**

</div>

---

Astrolabe is a free workbench on top of the [OnchainDivers](https://github.com/web3engineering/solana-dex-data)
indexers. Write SQL or ask the built-in assistant, turn the result into a chart,
build dashboards, share and embed them, fork other people's work.

The MCP server gives the same data to your agent. Claude, Cursor, Codex, ChatGPT
or your own agent can query the tables, then save the answer as a public chart or
dashboard and hand you the link.

This repository holds the docs, examples and prompts for the MCP server. The
Astrolabe site and server themselves are not open source.

---

## Connect in one line

**Claude Code:**

```bash
claude mcp add --transport http astrolabe https://astrolabe.cartographer.club/mcp
```

**Claude app, Cursor, Codex, ChatGPT and other clients:** step-by-step setup for
each one is on [astrolabe.cartographer.club/agents](https://astrolabe.cartographer.club/agents).

**Your own agent:** the server URL is `https://astrolabe.cartographer.club/mcp`,
transport Streamable HTTP (MCP 2025-06-18). Any MCP SDK works (Python `mcp`,
TypeScript `@modelcontextprotocol/sdk`), or raw JSON-RPC: `POST /mcp` with
`initialize`, then `tools/call`.

Then paste this as a first prompt:

```
Show me pump.fun token launches per day over the last 7 days, and give me a link I can share.
```

The agent finds the tables, reads our data rules, writes the SQL, runs it and
saves a public page with a chart.

---

## What's in the data

| Database | What's in there |
| --- | --- |
| **solana** | pump.fun, PumpSwap, Raydium, Meteora, Jito tips, token and SOL transfers, first wallet top-ups, blocks |
| **hyperliquid** | Perp and spot fills with PnL and liquidations, asset metadata |
| **polymarket** | Order fills, conditional token splits, merges and redemptions, market and event metadata, wallet stats |
| **robinhood** | Robinhood Chain swaps, Uniswap v3 and v4, launchpads, wallet clusters |
| **bsc** | BNB Chain: PancakeSwap v2, v3 and v4, four.meme, flap and GENIUS launchpads |
| **arc** | Uniswap trades and launchpad launches |
| **ton** | DeDust swaps |
| **ref** | RWA tokens and USD-priced RWA trades on Solana |

Every table and column comes with a description of what's in it and in which
units, so the agent doesn't have to guess whether an amount is in lamports or
SOL. On top of that, an `AGENTS` database holds our notes on freshness,
partition filters and known quirks, plus verified example queries. The agent
gets a summary of these rules when it connects.

Full details, freshness and limits: [docs/data.md](docs/data.md)

---

## What an answer looks like

[Pump.fun Smart Money](https://astrolabe.cartographer.club/dashboards/71) takes
every pump.fun and PumpSwap trader of the last 3 days. For each wallet's first
buy of a new token, the entry is the next trade one block later, as if you had
copied it. A hit means the price reached 2x within 3 hours. Wallets are ranked by
hits over entries:

| rank | wallet | hit_pct | hits | misses | tokens |
| ---: | --- | ---: | ---: | ---: | ---: |
| 1 | `C3zHu…n6z2W` | 88.9 | 8 | 1 | 9 |
| 2 | `G928R…aJnx5` | 88.9 | 8 | 1 | 9 |
| 3 | `38pQJ…CpFm3` | 87.5 | 7 | 1 | 8 |
| 4 | `Cqszf…v4LeT` | 87.5 | 7 | 1 | 8 |
| 5 | `DceAm…yDmEm` | 87.5 | 7 | 1 | 8 |

Captured on 13 November 2026. Addresses shortened for display. A historical hit
rate is a starting point for copy-trading research, not a signal.

Paste the dashboard link to your agent and ask for a change, for example *"fork it
and change the target to 3x within 6 hours"*. The agent forks the dashboard and
edits the copy; the original is never changed.

---

## What the agent can do

| Tool | What it does |
| --- | --- |
| `list_databases`, `list_tables` | Explore the schema: columns, types, sizes and the comment on every table and column |
| `run_query` | Run SELECT queries; check them first with `EXPLAIN ESTIMATE` |
| `save_query`, `add_chart` | Save an answer as a public page with a chart and return the link |
| `create_dashboard` | Build a dashboard from saved queries and text blocks |
| `search`, `get_dashboard`, `get_query` | Find and read existing work |
| `fork_dashboard`, `update_query`, `update_dashboard` | Change a copy, never the original |

The data tools are the official [`mcp-clickhouse`](https://github.com/ClickHouse/mcp-clickhouse)
ones. Everything agents save is public, in English, under the `agents` account.

More: [docs/tools.md](docs/tools.md)

---

## Free and live

**Free (the site and the MCP server):** data up to yesterday, loaded daily at
11:00 UTC, about 90 days of history for most tables. A free account adds private
work, CSV uploads joined with the indexer data, and alerts to e-mail, Slack,
Discord or Telegram.

**Live:** the indexers themselves, seconds behind the chain, with the full history
(Solana since 2024, Polymarket since 2022, Hyperliquid since July 2025), research
tables and a direct read-only ClickHouse login. The same login works with
`mcp-clickhouse` on your own machine, so your agent gets live data with the same
tools. **200 USDC per indexer per 30 days.**

[Free vs paid](https://astrolabe.cartographer.club/pricing) ·
[Telegram](https://t.me/inventandchill)

---

## What's in this repository

```
docs/       tools, data, freshness and limits
examples/   public dashboards and queries to start from or fork
prompts/    prompts that work well with the server
```

---

## Built on OnchainDivers

Astrolabe runs on the same decoded ClickHouse database we sell as
[OnchainDivers](https://onchaindivers.com/): pump.fun launches since January
2024, every swap with its execution context, and no API layer in between. Runnable
SQL and notebooks for the full database are in
[web3engineering/solana-dex-data](https://github.com/web3engineering/solana-dex-data).

---

MIT licensed. Questions, or a table you'd like to see,
[open an issue](../../issues) or message us on
[Telegram](https://t.me/inventandchill).
