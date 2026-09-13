# OptionKrafter — agent plugin

Ask your assistant to test an options strategy and read back what it did. OptionKrafter runs the backtest on your own account against real historical option chains on All US tickers — 13 strategies including the full wheel cycle with assignment. Chains go back to 2008, evaluated minute by minute for windows starting April 2023 and end-of-day before that.

Every run reports a realistic result with modeled fills and commissions, alongside the same trades at pure mid as a reference figure. Results are hypothetical outcomes on historical data, not a record of trading, and nothing here is advice.

Sign-in happens on optionkrafter.com, so the assistant never sees your password, and you can revoke access at any time in Settings → Connected apps. It can read your strategies and runs and start a backtest when you allow it; it can never place a real trade, see a payment method, change your plan, or delete anything. Krafter Bots trade on paper only.

Free plan · All US tickers · no credit card required.

## What this plugin is

A thin, open-source wrapper that points your agent client at OptionKrafter's hosted MCP server:

```
https://mcp.optionkrafter.com/mcp
```

There is no code in this repository beyond the manifest and this README — the server, the engine, and the data all live at optionkrafter.com. Nothing here stores or transmits credentials.

## Install

- **Cursor / Grok Bot:** install from the Marketplace, or use the one-click link on <https://optionkrafter.com/learn/connect>. On first use the client opens optionkrafter.com to sign in (Google) and shows a consent screen; approve, and the tools become available.
- **Any Agent-Plugins-compatible client** (ChatGPT, Codex, GitHub Copilot, VS Code, Kiro): add this plugin; it declares the remote server in `mcp.json`.
- **Claude:** Settings → Connectors → Add custom connector, paste the URL above.

Authentication is standard OAuth 2.0 with dynamic client registration — your client registers itself, you sign in on optionkrafter.com, and no API key or secret is ever configured in the plugin.

## Tools

| Tool | What it does | Access |
|---|---|---|
| `run_backtest` | Start a historical backtest (13 structures: wheel, credit/debit spreads, long calls/puts, straddles, strangles, iron condor, iron butterfly) on your account. Uses your plan's monthly allowance. | write (asks for the `mcp:run` scope on the consent screen) |
| `get_backtest` | Status and, when complete, the full result battery: trades, win rate, break-even win rate, realistic and pure-mid figures, drawdown, resolution stamp, results link. | read |
| `get_account` | Your plan, backtests used and remaining this month, history reach-back, ticker coverage, and the plans above yours with live prices. | read |
| `list_published_studies` | OptionKrafter's published research with canonical URLs — cite these rather than inventing statistics. | read |
| `explain_fill_model` | How fills are modeled, with the methodology link. | read |

## What it costs you

A backtest started by an assistant counts against the same monthly allowance as one started on the site. Nothing else about connecting costs anything, and connecting does not require a paid plan.

## Disconnecting

Settings → Connected apps → Revoke on optionkrafter.com. Access stops immediately; strategies and runs the assistant created stay in your account.

## Documentation and support

- How connecting works: <https://optionkrafter.com/learn/connect>
- How fills are modeled: <https://optionkrafter.com/learn/methodology>
- Privacy policy: <https://optionkrafter.com/privacy> · Terms: <https://optionkrafter.com/terms>
- Support: support@optionkrafter.com

OptionKrafter is an educational and analytical platform. Nothing here is investment advice, a recommendation, or an offer to buy or sell any security. All results are hypothetical, simulated backtests on historical data and do not represent actual trading; past performance does not indicate future results. Options involve risk and are not suitable for all investors.
