---
tags: [psychology]
---

# 💭 Emotional Patterns

This page auto-analyzes how your emotional state correlates with trading outcomes. Update your personal notes section as patterns emerge.

---

## Best States (Highest P&L)

```dataview
TABLE
  emotional_state_before AS "State Before",
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
GROUP BY emotional_state_before
SORT sum(rows.pl_dollars) DESC
```

---

## Dangerous States (Avoid Trading)

```dataview
TABLE
  emotional_state_before AS "State Before",
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 1) AS "Win %"
FROM "02 - Trades"
GROUP BY emotional_state_before
SORT sum(rows.pl_dollars) ASC
LIMIT 5
```

---

## Emotional Drift (State Changed During Trade)

```dataview
TABLE date, ticker, emotional_state_before AS "Before", emotional_state_during AS "During", emotional_state_after AS "After", pl_dollars, grade
FROM "02 - Trades"
WHERE emotional_state_before != emotional_state_during
SORT date DESC
LIMIT 30
```

---

## Emotion on Rule-Breaking Trades

```dataview
TABLE date, ticker, emotional_state_before AS "Before", emotional_state_during AS "During", pl_dollars, mistakes, grade
FROM "02 - Trades"
WHERE followed_rules = false
SORT date DESC
```

---

## My Personal Notes

*(Update this as you identify patterns)*

**I trade best when I feel:**

**States that cause me to break rules:**

**Warning signs I'm about to make a mistake:**

**Pre-session routine to reach optimal state:**
1.
2.
3.

**Cooldown routine after a losing streak:**
1.
2.

---

*[[00 - Dashboard/🧠 Psychology|Psychology Dashboard]] | [[06 - Psychology/Mistakes Log|Mistakes Log]]*
