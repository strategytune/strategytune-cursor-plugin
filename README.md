# StrategyTune

Cursor plugin that connects the agent to [StrategyTune](https://strategytune.com), a backtesting platform for trading strategies, through StrategyTune's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

The agent can write and save chart indicators, reusable market conditions (signals and filters) and full trading strategies, run them tick-by-tick against real historical market data in StrategyTune's sandboxed cloud, run ad-hoc research code over the same data, read full backtest reports with every trade, and control a StrategyTune chart you have open in the browser.

Everything runs on historical data. The server does not connect to a broker, place live orders, or give investment advice.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **StrategyTune**.
3. Click **Install**, then complete the StrategyTune sign-in prompt.

Or run `/add-plugin strategytune` in chat.

## MCP

```json
{
  "mcpServers": {
    "strategytune": {
      "type": "http",
      "url": "https://strategytune.com/mcp"
    }
  }
}
```

Auth is OAuth 2.1 with Dynamic Client Registration. Cursor prompts for StrategyTune sign-in when the plugin connects. There is no client ID or API key to configure. A free StrategyTune account is enough; cloud runs consume a daily compute allowance that depends on your plan.

## Knowledge

The agent does not need to be taught the platform. Through the `get_knowledge` tool it reads StrategyTune's built-in documentation topics itself: what the platform is, what scripts are, how to write indicators, signals and filters, and strategies, how backtests run, which instruments and data exist, and what is on the user's screen.

## What agents can do

| Category | Tools |
| --- | --- |
| Scripts | `list_scripts`, `get_script`, `save_script` (compiled and type-checked on save), `duplicate_script`, `delete_script`, `list_deleted_scripts`, `restore_script` |
| Backtests & research | `run_backtest`, `run_code` (one-off research code over tick data), `get_run_status`, `get_run_result`, `cancel_run`, `find_instruments` |
| Sessions | `list_manual_sessions`, `list_automated_sessions`, `get_session_trades`, `delete_session` |
| Your charts (needs an open, signed-in StrategyTune tab) | `list_tabs`, `get_tab_state`, `switch_instrument`, `switch_timeframe`, `jump_to_date`, `load_session`, `attach_to_run` |
| Indicators & tracks (needs an open tab) | `list_builtin_indicators`, `list_chart_indicators`, `get_chart_data`, `add_indicator`, `get_indicator_inputs`, `update_indicator_inputs`, `remove_indicator`, `list_timeline_tracks`, `add_track`, `update_track`, `remove_track` |
| Docs & feedback | `get_knowledge`, `send_feedback` |

The hosted server is the source of truth for tool names and schemas. The full list with descriptions: [What your AI can do](https://strategytune.com/docs/connected-ai/capabilities).

## Example prompts

- Explain how manual and automated backtesting fit together in StrategyTune.
- Write a strategy that buys when the 20 EMA crosses above the 50 EMA and sells on the opposite cross, then backtest it on EURUSD 15m for the last year.
- How often did EURUSD move more than 50 pips within the first hour of the London session in 2025? Run the code and tell me.
- Show me the trades from my last backtest and summarize what went wrong.

## Support

support@strategytune.com
