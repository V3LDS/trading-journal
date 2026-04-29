---
strategy_name: 
asset_class: stocks
timeframe: 
market_condition: 
tags: [strategy]
date_created: <% tp.date.now("YYYY-MM-DD") %>
status: active
---

# <% tp.file.title %>

## Overview

**Description:**

**Core Concept:**

**Edge:**

---

## Entry Criteria

**All must be true:**
- [ ]
- [ ]
- [ ]

**Nice to have:**
-
-

---

## Exit Criteria

**Profit Target:**

**Stop Loss:**

**Time-Based Exit:**

**Early Exit Conditions:**
-

---

## Risk Parameters

| Parameter | Value |
|-----------|-------|
| Max Risk per Trade | % of account |
| Max Trades per Day | |
| Best Sessions | |
| Avoid When | |

---

## Strategy Statistics

```dataview
TABLE
  length(rows) AS "Total Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R",
  max(rows.pl_dollars) AS "Best ($)",
  min(rows.pl_dollars) AS "Worst ($)"
FROM "02 - Trades"
WHERE setup_type = this.strategy_name
GROUP BY setup_type
```

## Trade Examples

```dataview
TABLE date, ticker, direction, entry_price, exit_price, pl_dollars, r_multiple, grade
FROM "02 - Trades"
WHERE setup_type = this.strategy_name
SORT date DESC
LIMIT 20
```

---

## Notes & Refinements

**Version History:**
- <% tp.date.now("YYYY-MM-DD") %> — Initial documentation

**Known Weaknesses:**

**Conditions to Avoid:**

**Refinements to Test:**
