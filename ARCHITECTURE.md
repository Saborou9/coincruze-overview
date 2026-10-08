# Architecture

Four services share one PostgreSQL database and run on one production host.

| Service | Technology | Job |
|---|---|---|
| Web app | Ruby on Rails 8 | Accounts, strategy profile, dashboard, decision log |
| Portfolio selection service | Python (FastAPI) | Scores the eligible asset universe from prices and company fundamentals (momentum, sentiment, fundamentals, volatility, value, growth, analyst consensus) |
| News sentiment service | Python (FastAPI) | Reads financial news each market day. A finance-specific language model (FinBERT) does a first pass; a large language model handles hard cases |
| Trading AI service | Python (FastAPI) | Runs the daily decision cycle and places orders through the Interactive Brokers API |

Supporting pieces: PostgreSQL, Redis, nightly database backups with a rehearsed restore, alerts when a scheduler stops or data goes stale, automatic restarts.

## Models

- **Trading decisions:** Claude Opus 5.
- **News sentiment and event classification:** Claude Haiku 4.5, after the FinBERT first pass.
- Model names are configuration, not hard-coded.

## Safety engineering

- A single path to the broker, with duplicate-send protection and per-customer isolation.
- A paper-versus-live gate that blocks a live order from a paper configuration.
- Stale and price-drifted orders are refused and the reason recorded.
- Alerts for stopped schedulers, a dropped broker session, and stale prices, scores, fundamentals or news.

## Testing

Automated test suites across the services. As of 16 Sep 2026: 310 tests (scoring service), 626 (trading service) and 205 (news service), plus the Rails app's own suite.

## Data

The system keeps daily snapshots of scores and the asset universe, and every decision matched to its later outcome, so results can be measured forward over time rather than claimed.

## What is deliberately not in this repository

Source code, prompts, strategy parameters, credentials and any customer or account data.
