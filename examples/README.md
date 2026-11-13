# Examples

Public dashboards and queries on Astrolabe. Open them without an account, change the parameters, or fork them to make your own version. You can also paste any of these links to your agent and ask it to change something: it will fork the page and edit the copy.

## Dashboards

### [Pump.fun Smart Money](https://astrolabe.cartographer.club/dashboards/71)

Wallets whose first buys of new pump.fun tokens are followed by a 2x within 3 hours.

It takes every token created on pump.fun in the last `days` days and joins its bonding-curve and PumpSwap trades into one price series. For each wallet's first buy of a token, the entry is the next trade one block later, as if you had copied it. A hit means the price reached `x` times the entry within `hours` hours. Wallets are ranked by hits over entries.

Parameters: `days`, `hours`, `x`, `min_tokens`, `max_tokens`, `wallet`, `token`.

A starting point for copy-trading research, not a signal.

### [RWA Overview](https://astrolabe.cartographer.club/dashboards/17)

Real-world assets on Solana: tokenized stocks, pre-IPO assets and commodities.

### [Hyperliquid Overview](https://astrolabe.cartographer.club/dashboards/38)

Volume, traders, coins and liquidations on Hyperliquid perps.

### [Polymarket Overview](https://astrolabe.cartographer.club/dashboards/33)

Volume, trades, traders and market activity on Polymarket.

## Queries built by an agent

### [Pump.fun / PumpSwap: best wallets for copy-trading, last 10 days](https://astrolabe.cartographer.club/queries/573)

Ranks traders by reconstructed realized PnL per token (SOL spent on buys minus SOL received on sells, closed positions only) over the last 10 days, filtered for organic win rates, minimum holding time and profit factor. Built entirely by an agent over MCP.

## More

Browse all public dashboards at [astrolabe.cartographer.club/dashboards](https://astrolabe.cartographer.club/dashboards) and queries at [astrolabe.cartographer.club/queries](https://astrolabe.cartographer.club/queries).
