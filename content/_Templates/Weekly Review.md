---
date: <% tp.date.now("YYYY-MM-DD") %>
week: <% tp.date.now("YYYY-[W]WW") %>
month: <% tp.date.now("YYYY-MM") %>
tags: [weekly-review]
---

# Weekly Review — Week <% tp.date.now("WW, YYYY") %>

## All Trades This Week

```dataview
TABLE date, ticker, direction, setup_type, session, pl_dollars, r_multiple, grade, followed_rules
FROM "02 - Trades"
WHERE week = "<% tp.date.now("YYYY-[W]WW") %>"
SORT date ASC, time_entry ASC
```

## Weekly Stats

```dataview
TABLE
  length(rows) AS "Total Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R",
  max(rows.pl_dollars) AS "Best Trade ($)",
  min(rows.pl_dollars) AS "Worst Trade ($)"
FROM "02 - Trades"
WHERE week = "<% tp.date.now("YYYY-[W]WW") %>"
GROUP BY week
```

## By Setup Type

```dataview
TABLE
  setup_type,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
WHERE week = "<% tp.date.now("YYYY-[W]WW") %>"
GROUP BY setup_type
SORT sum(rows.pl_dollars) DESC
```

## By Session

```dataview
TABLE
  session,
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %"
FROM "02 - Trades"
WHERE week = "<% tp.date.now("YYYY-[W]WW") %>"
GROUP BY session
SORT sum(rows.pl_dollars) DESC
```

## Rule Violations This Week

```dataview
TABLE date, ticker, emotional_state_before, pl_dollars, grade, mistakes
FROM "02 - Trades"
WHERE week = "<% tp.date.now("YYYY-[W]WW") %>" AND followed_rules = false
SORT date ASC
```

---

## Weekly Narrative

**Best Trade of the Week:**

**Worst Trade of the Week:**

**Recurring Mistakes:**

**What I Did Well:**

**Adjustments for Next Week:**

---
*[[00 - Dashboard/🏠 Home|Home]] | [[04 - Monthly Reviews/|Monthly Reviews]]*
