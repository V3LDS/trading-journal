---
tags: [strategy-index]
---

# 📈 Strategy Index

Create a new strategy page: open the `_Templates/Strategy Page` template and save it to this folder.

---

## All Strategies

```dataview
TABLE
  strategy_name AS "Strategy",
  timeframe AS "Timeframe",
  market_condition AS "Best Condition",
  status AS "Status",
  date_created AS "Created"
FROM "05 - Strategies"
WHERE contains(tags, "strategy")
SORT status ASC, strategy_name ASC
```

---

## Strategy Performance Comparison (All Trades)

```dataview
TABLE
  setup_type AS "Setup",
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R",
  max(rows.pl_dollars) AS "Best ($)",
  min(rows.pl_dollars) AS "Worst ($)"
FROM "02 - Trades"
GROUP BY setup_type
SORT sum(rows.pl_dollars) DESC
```

---

*[[00 - Dashboard/🏠 Home|Home]]*
