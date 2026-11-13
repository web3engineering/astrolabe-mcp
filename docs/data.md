# Data

The MCP server and the site query the same tables, with the same column comments.

## Databases

| Database | What's inside |
|---|---|
| `solana` | pump.fun, PumpSwap, Raydium, Meteora, Jito tips, token and SOL transfers, first top-ups of wallets, blocks |
| `hyperliquid` | Perp and spot fills with PnL and liquidations, asset metadata |
| `polymarket` | Order fills, conditional token splits, merges and redemptions, market and event metadata, wallet stats |
| `robinhood` | Robinhood Chain: swaps, Uniswap v3/v4, launchpads, wallet clusters |
| `bsc` | BNB Chain: PancakeSwap v2, v3 and v4, four.meme, flap and GENIUS launchpads |
| `arc` | Uniswap trades and launchpad launches on Arc |
| `ton` | DeDust swaps |
| `ref` | RWA tokens and USD-priced RWA trades |

Every table and column of `solana` carries a comment with units and quirks. Read them with `list_tables` before writing SQL.

## Freshness and history

- Data is loaded **once a day at 11:00 UTC** for the previous UTC day. The newest rows are from yesterday; there is no "now".
- Most tables keep **about 90 days**. Exceptions: `jito_tips` and `tx_timestamps` keep 14 days; `token_transfers` and `sol_top_ups` keep 31 days.
- "Last 24 hours" means the latest 24 hours of loaded data, counted back from the newest block, not from the clock.

## Limits

- Per query: 300 seconds and 63 GB of memory.
- 32 queries at a time for all MCP users together.
- Big scans (for example `pumpswap_all_swaps` or `tx_timestamps` without a date or slot filter) will hit these limits. Filter first, aggregate in SQL, and always add a `LIMIT` to row listings.

## Live data

Live indexers (seconds behind the chain), the full history (Solana since 2024, Polymarket since 2022, Hyperliquid since July 2025) and the team's research tables are a paid subscription: 200 USDC per indexer per 30 days. See [Free vs paid](https://astrolabe.cartographer.club/pricing).

With a subscription you get a read-only ClickHouse login on the Account page. The same login works with `mcp-clickhouse` on your own machine, so your agent gets live data with the same three data tools:

```bash
CLICKHOUSE_HOST=<host from Account> CLICKHOUSE_PORT=<port> CLICKHOUSE_SECURE=true \
CLICKHOUSE_USER=<login> CLICKHOUSE_PASSWORD=<password> \
uvx mcp-clickhouse
```

Never commit your login or password to a repository. Keep them in environment variables or a local `.env` file.
