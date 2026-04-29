---
date: <% tp.date.now("YYYY-MM-DD") %>
month: <% tp.date.now("YYYY-MM") %>
month_label: <% tp.date.now("MMMM YYYY") %>
tags: [monthly-review]
---

# Monthly Review — <% tp.date.now("MMMM YYYY") %>

## Monthly Summary

```dataview
TABLE
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R",
  max(rows.pl_dollars) AS "Best ($)",
  min(rows.pl_dollars) AS "Worst ($)"
FROM "02 - Trades"
WHERE month = "<% tp.date.now("YYYY-MM") %>"
GROUP BY month
```

## Performance by Week

```dataview
TABLE
  week,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
WHERE month = "<% tp.date.now("YYYY-MM") %>"
GROUP BY week
SORT week ASC
```

## Best Setups This Month

```dataview
TABLE
  setup_type,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
WHERE month = "<% tp.date.now("YYYY-MM") %>"
GROUP BY setup_type
SORT sum(rows.pl_dollars) DESC
```

## Emotion vs Performance

```dataview
TABLE
  emotional_state_before AS "Emotion Before",
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %"
FROM "02 - Trades"
WHERE month = "<% tp.date.now("YYYY-MM") %>"
GROUP BY emotional_state_before
SORT sum(rows.pl_dollars) DESC
```

## Grade Distribution

```dataview
TABLE
  grade,
  length(rows) AS "Count",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %"
FROM "02 - Trades"
WHERE month = "<% tp.date.now("YYYY-MM") %>"
GROUP BY grade
SORT grade ASC
```

## Rule Violations This Month

```dataview
TABLE date, ticker, pl_dollars, grade, mistakes, emotional_state_before
FROM "02 - Trades"
WHERE month = "<% tp.date.now("YYYY-MM") %>" AND followed_rules = false
SORT date ASC
```

---

## Monthly Narrative

**This Month's Theme:**

**Greatest Strength:**

**Most Costly Weakness:**

**P&L Attribution** *(which setups/sessions/tickers drove results)*:

**Strategy or Rule Changes:**

**Goals for Next Month:**
1.
2.
3.

---
*[[00 - Dashboard/🏠 Home|Home]]*
