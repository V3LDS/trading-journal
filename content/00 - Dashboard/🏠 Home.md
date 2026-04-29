---
tags: [dashboard]
---

# 🏠 Trading Journal

> **Quick Actions**
> - `Cmd+Shift+T` — Log a new trade (QuickAdd)
> - `Cmd+Shift+D` — Open today's daily review
> - `Cmd+Shift+I` — Insert template into current note

---

## Today's Session

```dataview
TABLE ticker, direction, setup_type, session, entry_price, exit_price, pl_dollars, r_multiple, grade, followed_rules
FROM "02 - Trades"
WHERE date = date(today)
SORT time_entry ASC
```

### Today's Summary

```dataview
TABLE
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  sum(rows.pl_dollars > 0 ? 1 : 0) AS "W",
  sum(rows.pl_dollars <= 0 ? 1 : 0) AS "L",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 0) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
WHERE date = date(today)
GROUP BY date
```

---

## This Week

```dataview
TABLE date, ticker, direction, setup_type, pl_dollars, r_multiple, grade
FROM "02 - Trades"
WHERE date >= date(today) - dur(7 days)
SORT date DESC, time_entry DESC
LIMIT 40
```

### Week Summary

```dataview
TABLE
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 0) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
WHERE date >= date(today) - dur(7 days)
GROUP BY true
```

---

## 30-Day Performance

```dataview
TABLE
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 3) AS "Expectancy (R)",
  max(rows.pl_dollars) AS "Best ($)",
  min(rows.pl_dollars) AS "Worst ($)"
FROM "02 - Trades"
WHERE date >= date(today) - dur(30 days)
GROUP BY true
```

---

## 90-Day Expectancy

```dataview
TABLE
  length(rows) AS "Sample",
  round(sum(rows.pl_dollars) / length(rows), 2) AS "Avg P&L ($)",
  round(sum(rows.r_multiple) / length(rows), 3) AS "Expectancy (R)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %"
FROM "02 - Trades"
WHERE date >= date(today) - dur(90 days)
GROUP BY true
```

---

## Recent Trade Log

```dataview
TABLE date, ticker, direction, setup_type, pl_dollars, r_multiple, grade, emotional_state_before
FROM "02 - Trades"
SORT date DESC, time_entry DESC
LIMIT 15
```

---

## Quick Links

| | |
|--|--|
| [[00 - Dashboard/📊 Performance\|📊 Performance Analytics]] | [[00 - Dashboard/🧠 Psychology\|🧠 Psychology Dashboard]] |
| [[05 - Strategies/Strategy Index\|📈 Strategy Index]] | [[06 - Psychology/Emotional Patterns\|💭 Emotional Patterns]] |
| [[06 - Psychology/Mistakes Log\|❌ Mistakes Log]] | [[08 - Reference/📋 Trading Rules\|📋 Trading Rules]] |
| [[08 - Reference/⚖️ Risk Management\|⚖️ Risk Management]] | [[08 - Reference/🔧 Vault Setup Guide\|🔧 Vault Setup Guide]] |
