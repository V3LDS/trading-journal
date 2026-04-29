---
tags: [dashboard]
---

# 🧠 Psychology Dashboard

---

## Pre-Trade Emotion vs Performance

```dataview
TABLE
  emotional_state_before AS "Emotion Before",
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY emotional_state_before
SORT sum(rows.pl_dollars) DESC
```

---

## During-Trade Emotion vs Performance

```dataview
TABLE
  emotional_state_during AS "Emotion During",
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY emotional_state_during
SORT sum(rows.pl_dollars) DESC
```

---

## Rule Adherence Over Time

```dataview
TABLE
  month,
  length(rows) AS "Trades",
  sum(rows.followed_rules = true ? 1 : 0) AS "Followed",
  sum(rows.followed_rules = false ? 1 : 0) AS "Broke",
  round(sum(rows.followed_rules = true ? 1 : 0) / length(rows) * 100, 1) AS "Discipline %"
FROM "02 - Trades"
GROUP BY month
SORT month DESC
```

---

## Discipline Score (Last 30 Days)

```dataview
TABLE
  length(rows) AS "Total Trades",
  sum(rows.followed_rules = true ? 1 : 0) AS "Rules Followed",
  sum(rows.followed_rules = false ? 1 : 0) AS "Rules Broken",
  round(sum(rows.followed_rules = true ? 1 : 0) / length(rows) * 100, 1) AS "Discipline %"
FROM "02 - Trades"
WHERE date >= date(today) - dur(30 days)
GROUP BY true
```

---

## Rules Followed vs Broken — P&L Comparison

```dataview
TABLE
  followed_rules AS "Rules Followed?",
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY followed_rules
```

---

## Rule Violations — Detail

```dataview
TABLE date, ticker, emotional_state_before, emotional_state_during, pl_dollars, grade, mistakes
FROM "02 - Trades"
WHERE followed_rules = false
SORT date DESC
```

---

## Mistake Frequency

```dataview
TABLE mistakes AS "Mistake", length(rows) AS "Times", sum(rows.pl_dollars) AS "P&L Cost ($)"
FROM "02 - Trades"
WHERE mistakes != null AND mistakes != []
FLATTEN mistakes
GROUP BY mistakes
SORT length(rows) DESC
```

---

## Grade vs Pre-Trade Emotion

```dataview
TABLE
  emotional_state_before AS "Emotion",
  grade,
  length(rows) AS "Count",
  sum(rows.pl_dollars) AS "P&L ($)"
FROM "02 - Trades"
GROUP BY emotional_state_before, grade
SORT emotional_state_before ASC, grade ASC
```

---

## Emotional Drift (State Changed Mid-Trade)

```dataview
TABLE date, ticker, emotional_state_before AS "Before", emotional_state_during AS "During", emotional_state_after AS "After", pl_dollars, grade
FROM "02 - Trades"
WHERE emotional_state_before != emotional_state_during
SORT date DESC
LIMIT 20
```

---

*[[00 - Dashboard/🏠 Home|Home]] | [[06 - Psychology/Emotional Patterns|Emotional Patterns]] | [[06 - Psychology/Mistakes Log|Mistakes Log]]*
