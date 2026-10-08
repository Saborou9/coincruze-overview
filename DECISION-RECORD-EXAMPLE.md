# Example of a decision record

> **This is an illustrative, synthetic example of the record format. It is not a real customer, not a real recommendation, and not a performance result.** "Example Corp (EXMP)" is a made-up company.

Every cycle writes a record like this, including cycles where nothing is traded.

```yaml
cycle_id: example-0001
trigger: nightly            # nightly | deposit | new account | emergency news
model: <configured trading model>
customer_profile_rules:
  max_position: 20%
  sector_cap: 30%
  asset_classes: [stocks, ETFs]

inputs:
  portfolio: snapshot attached
  candidates_scored: 3796
  news_signals_used: 4

decision:
  - action: hold
    asset: EXMP
    reason: >
      EXMP's score is unchanged since last week and today's news about a
      supplier delay does not change the company's earnings outlook.
      Holding keeps the position within the customer's 20% limit.
  - action: no_trade
    reason: >
      No candidate improved on current holdings enough to justify a trade
      after the customer's sector limits were applied.

rule_checks:
  pre_ai:  { sector_cap: pass, drawdown_breaker: not_tripped }
  post_ai: { position_cap: pass, order_size: n/a (no order) }

outcome: no orders queued
recorded_at: 2026-10-01T03:14:00Z
```

Why it matters: a customer can read what the system looked at, what it decided and why, and which rules limited it, including on days when it did nothing.
