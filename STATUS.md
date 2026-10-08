# Status: built, designed, not proven

Updated 8 Oct 2026. Only what is true as of that date.

## Built and running (paper mode)

| Capability | State |
|---|---|
| Four services running together | Running in paper mode |
| Daily chain: scoring, news, decision cycle, order queue | Runs unattended; orders reach Interactive Brokers paper accounts |
| Decision audit log with prompt, model, reasoning and rejection reasons | Built |
| Scoring engine with 0-1 scores across seven dimensions | Built |
| News pipeline: FinBERT first pass, LLM for hard cases | Built |
| Pre-trade and post-trade rule checks (position caps, sector caps, drawdown breaker, confidence floors) | Built |

## Designed, not built

| Capability | State |
|---|---|
| "Brain" of specialised agents that wake up depending on the news | Next milestone, in development |
| Per-position stop loss | Decided, not built (today only a portfolio-level breaker exists) |
| Crypto trading, education content | Not built |
| Finding assets outside the customer's watchlist | Requirement set, not built |
| Tax-aware trading | Designed, not built |
| Pause and approve-before-trade controls | Not in the first release; on the roadmap |

## Not proven

- No evidence yet that the strategy beats a simple portfolio. Nothing has traded with real money.
- No real customers, no revenue.
- Not a registered investment adviser. Registration, an Interactive Brokers partner agreement and commercial data licences are open.

## Evidence rules I hold myself to

- No performance advertising; no claim of "first", "only" or "registered".
- The AI decision layer is tested forward, against a scores-only baseline, before any change reaches real money.
