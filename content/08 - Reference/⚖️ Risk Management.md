---
tags: [reference, risk]
---

# ⚖️ Risk Management

---

## Position Sizing Formula

```
Position Size = Risk Amount ($) ÷ (Entry Price − Stop Loss Price)
```

**Example:**
- Account: $25,000 | Risk: 1% = $250
- Entry: $50.00 | Stop: $49.00 → Risk per share: $1.00
- Position Size: 250 ÷ 1.00 = **250 shares**

---

## Account Risk Tiers

| Account | 1% Risk | 2% Risk | Daily Stop (3%) | Weekly Stop (7%) |
|---------|---------|---------|-----------------|-----------------|
| $5,000 | $50 | $100 | $150 | $350 |
| $10,000 | $100 | $200 | $300 | $700 |
| $25,000 | $250 | $500 | $750 | $1,750 |
| $50,000 | $500 | $1,000 | $1,500 | $3,500 |
| $100,000 | $1,000 | $2,000 | $3,000 | $7,000 |

---

## R-Multiple System

```
R-Multiple = P&L ($) ÷ Initial Risk Amount ($)
```

| R | Meaning |
|---|---------|
| +3R | Won 3× your risk |
| +1R | Won exactly your risk |
| 0R | Break even |
| −1R | Full stop loss hit |
| −2R | Should never happen (stop moved or no stop) |

**Expectancy:**
```
Expectancy = (Win Rate × Avg Win R) − (Loss Rate × Avg Loss R)
```
Positive expectancy = profitable system over a large sample.

---

## Loss Limits

| Limit | Action |
|-------|--------|
| Daily loss limit (3%) | Stop trading for the rest of the day |
| Weekly loss limit (7%) | Stop trading for the rest of the week. Review what went wrong |
| Monthly drawdown (15%) | Reduce position size by 50% for the rest of the month |

---

## My Risk Settings

| Parameter | Value |
|-----------|-------|
| Account Balance | $ |
| Risk per Trade (%) | % |
| Risk per Trade ($) | $ |
| Daily Loss Limit ($) | $ |
| Weekly Loss Limit ($) | $ |

---

## Risk Stats from Journal (Last 30 Days)

```dataview
TABLE date, ticker, risk_amount, position_size, pl_dollars, r_multiple
FROM "02 - Trades"
WHERE date >= date(today) - dur(30 days)
SORT date DESC
```

## Average Risk vs Results (Last 30 Days)

```dataview
TABLE
  round(sum(rows.risk_amount) / length(rows), 2) AS "Avg Risk ($)",
  round(sum(rows.pl_dollars) / length(rows), 2) AS "Avg P&L ($)",
  round(sum(rows.r_multiple) / length(rows), 3) AS "Avg R"
FROM "02 - Trades"
WHERE date >= date(today) - dur(30 days)
GROUP BY true
```

---

*[[08 - Reference/📋 Trading Rules|Trading Rules]] | [[00 - Dashboard/🏠 Home|Home]]*
