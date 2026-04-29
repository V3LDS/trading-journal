---
tags: [dashboard]
---

# 📊 Performance Analytics

---

## All-Time P&L by Month

```dataview
TABLE
  month,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY month
SORT month DESC
```

---

## Cumulative P&L by Day

```dataview
TABLE
  date,
  sum(rows.pl_dollars) AS "Daily P&L ($)"
FROM "02 - Trades"
GROUP BY date
SORT date ASC
```

---

## Best Performing Setups (All Time)

```dataview
TABLE
  setup_type,
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

## Performance by Session

```dataview
TABLE
  session,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY session
SORT sum(rows.pl_dollars) DESC
```

---

## Performance by Direction

```dataview
TABLE
  direction,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY direction
```

---

## Market Condition Analysis

```dataview
TABLE
  market_condition,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY market_condition
SORT sum(rows.pl_dollars) DESC
```

---

## Grade Distribution

```dataview
TABLE
  grade,
  length(rows) AS "Count",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY grade
SORT grade ASC
```

---

## Top Tickers by P&L

```dataview
TABLE
  ticker,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY ticker
SORT sum(rows.pl_dollars) DESC
LIMIT 25
```

---

## R-Multiple Distribution

```dataview
TABLE date, ticker, setup_type, r_multiple, pl_dollars, grade
FROM "02 - Trades"
SORT r_multiple DESC
```

---

## Top 10 Wins

```dataview
TABLE date, ticker, setup_type, session, pl_dollars, r_multiple, grade
FROM "02 - Trades"
WHERE pl_dollars > 0
SORT pl_dollars DESC
LIMIT 10
```

## Top 10 Losses

```dataview
TABLE date, ticker, setup_type, session, pl_dollars, r_multiple, grade, followed_rules, mistakes
FROM "02 - Trades"
WHERE pl_dollars < 0
SORT pl_dollars ASC
LIMIT 10
```

---

*[[00 - Dashboard/🏠 Home|Home]] | [[00 - Dashboard/🧠 Psychology|🧠 Psychology]]*
