---
date: <% tp.date.now("YYYY-MM-DD") %>
week: <% tp.date.now("YYYY-[W]WW") %>
month: <% tp.date.now("YYYY-MM") %>
market_bias: 
overall_mood: 
discipline_score: 
tags: [daily-review]
---

# Daily Review — <% tp.date.now("dddd, MMMM D YYYY") %>

## Today's Trades

```dataview
TABLE ticker, direction, setup_type, session, entry_price, exit_price, pl_dollars, r_multiple, grade, followed_rules
FROM "02 - Trades"
WHERE date = date("<% tp.date.now("YYYY-MM-DD") %>")
SORT time_entry ASC
```

## Today's Summary

```dataview
TABLE
  length(rows) AS "Trades",
  sum(rows.pl_dollars) AS "P&L ($)",
  sum(rows.pl_dollars > 0 ? 1 : 0) AS "W",
  sum(rows.pl_dollars <= 0 ? 1 : 0) AS "L",
  round(sum(rows.pl_dollars > 0 ? 1 : 0) / length(rows) * 100, 0) AS "Win %",
  round(sum(rows.r_multiple) / length(rows), 2) AS "Avg R"
FROM "02 - Trades"
WHERE date = date("<% tp.date.now("YYYY-MM-DD") %>")
GROUP BY date
```

---

## Market Overview

**Pre-Market Notes:**

**Key Levels:**
- Resistance:
- Support:
- News/Catalyst:

**Market Condition:** *(trending-up / trending-down / range-bound / volatile / choppy)*

---

## Psychology Check-In

**Overall Mood:** *(calm / neutral / anxious / frustrated / euphoric / tired)*

**Discipline Score (1–10):**

**Emotional Patterns Observed:**

---

## Lessons

**Best Decision Today:**

**Biggest Mistake Today:**

**Key Takeaway:**

**Focus for Tomorrow:**

---

## Consistency Checklist

- [ ] Followed position sizing rules
- [ ] Did not revenge trade
- [ ] Only took A/B setups
- [ ] Stopped at daily loss limit (or didn't hit it)
- [ ] Reviewed all trades post-market

---
*[[03 - Weekly Reviews/|Weekly Reviews]] | [[00 - Dashboard/🏠 Home|Home]]*
