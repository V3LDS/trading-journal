---
tags: [reference, rules]
---

# 📋 My Trading Rules

> Review before every session. Breaking rules costs money and discipline.

---

## Pre-Session Checklist

- [ ] Check economic calendar — avoid trading 5 min before/after major releases
- [ ] Identify key support/resistance levels
- [ ] Define market bias for the day
- [ ] Confirm mental/emotional state is ready to trade
- [ ] Set daily max loss: $___
- [ ] Set max trades for the day: ___

---

## Entry Rules

1. Only take A or B setups — if you're convincing yourself, it's a C or lower
2. Confirm setup on your primary timeframe before entering
3. Know your stop loss price BEFORE entering — no exceptions
4. Size position based on stop distance, not gut feeling
5. No trading in the first 5 minutes of open (unless pre-planned catalyst play)
6. No chasing — missed entry = wait for next one

---

## During-Trade Rules

1. Do not move stop loss against your position
2. Let the trade play to its target or stop — no micro-managing without new information
3. Partials allowed only at pre-defined levels (e.g., 50% at 1:1)
4. Do not add to a losing position
5. If daily loss limit is hit — stop trading immediately, no exceptions

---

## Exit Rules

1. Primary: target reached — take it
2. Secondary: stop hit — accept it, no fighting
3. Time-based: if no movement after ___ minutes, re-evaluate
4. Hard close: all positions closed by ___

---

## Risk Rules

1. Max risk per trade: 1–2% of account
2. Daily loss limit: 3% of account — hard stop, walk away
3. Weekly loss limit: 7% of account — take the rest of the week off
4. Never risk more than defined at entry (no stop widening)

---

## Post-Trade Rules

1. Log every trade immediately after it closes
2. Grade the execution honestly — outcome is not the grade
3. Write one lesson from every losing trade
4. Wait 30+ minutes before taking another trade after 3 consecutive losses

---

## Prohibited Behaviors

- No trading when angry, euphoric, or sleep-deprived
- No doubling down on losing positions
- No "just one more trade" after daily loss limit
- No social media / tips as sole trade basis

---

## Discipline Stats (Last 30 Days)

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

*Last reviewed: — update this date when you revise rules*

*[[00 - Dashboard/🏠 Home|Home]] | [[08 - Reference/⚖️ Risk Management|Risk Management]]*
