# MCP tools

The server exposes two groups of tools.

## Data tools

These are the official [`mcp-clickhouse`](https://github.com/ClickHouse/mcp-clickhouse) tools.

| Tool | What it does |
|---|---|
| `list_databases` | Lists the databases. |
| `list_tables` | Lists the tables of a database: columns, types, sorting keys, sizes, and the comment on every table and column. |
| `run_query` | Runs a query. SELECT only. `DESCRIBE` and `EXPLAIN ESTIMATE` are allowed, so the agent can check a query without running it. |

## Astrolabe tools

These turn answers into pages on [astrolabe.cartographer.club](https://astrolabe.cartographer.club).

| Tool | What it does |
|---|---|
| `save_query` | Saves a query as a public page with a chart and returns its link. |
| `add_chart` | Adds a chart to a saved query. |
| `create_dashboard` | Builds a dashboard from saved queries and text blocks. |
| `search` | Finds existing public dashboards and queries. |
| `get_dashboard` / `get_query` | Read a dashboard or a query by its link. |
| `fork_dashboard` | Makes your own copy of a dashboard. |
| `update_query` / `update_dashboard` | Change a copy. The original is never changed. |

## How an answer becomes a page

- Ask for a single number and you get a number.
- Ask for a series, a table, a breakdown or a comparison and the agent answers, saves the query with a chart and gives you a link like `astrolabe.cartographer.club/queries/393`.
- Ask for several things on one topic, or for a dashboard, and it builds one.
- Paste a link to any dashboard and ask for changes: the agent reads it, forks it and changes the copy.

Pages open without an account. Anyone can change the parameters, share, embed and fork them.

Everything agents save is public, in English, under the [agents](https://astrolabe.cartographer.club) account.

## Rules for agents

The `AGENTS` database holds the team's notes on units (lamports, raw token amounts), freshness, partition filters and known quirks, plus verified example queries. The server hands the agent a summary when it connects. The full rules are in `AGENTS.ROOT`.
