---
tags: [psychology]
---

# ❌ Mistakes Log

Mistakes are logged via the `mistakes` YAML list in each trade file. This page auto-aggregates them.

---

## Mistake Frequency (All Time)

```dataview
TABLE mistakes AS "Mistake", length(rows) AS "Times Made", sum(rows.pl_dollars) AS "P&L Cost ($)"
FROM "02 - Trades"
WHERE mistakes != null AND mistakes != []
FLATTEN mistakes
GROUP BY mistakes
SORT length(rows) DESC
```

---

## Recent Mistakes (Last 30 Days)

```dataview
TABLE date, ticker, mistakes, pl_dollars, grade, followed_rules, emotional_state_before
FROM "02 - Trades"
WHERE date >= date(today) - dur(30 days) AND mistakes != null AND mistakes != []
SORT date DESC
```

---

## Mistakes by Emotional State

```dataview
TABLE emotional_state_before AS "Emotion", mistakes AS "Mistake", length(rows) AS "Count", sum(rows.pl_dollars) AS "P&L Cost ($)"
FROM "02 - Trades"
WHERE mistakes != null AND mistakes != []
FLATTEN mistakes
GROUP BY emotional_state_before, mistakes
SORT length(rows) DESC
LIMIT 20
```

---

## Standard Mistake Tags

Use these exact values in the `mistakes` YAML list field on trade notes:

| Tag | Description |
|-----|-------------|
| `early-entry` | Entered before setup fully confirmed |
| `late-entry` | Chased the move past ideal entry |
| `oversized` | Position too large for the risk |
| `no-stop` | Entered without a defined stop loss |
| `moved-stop` | Moved stop against the position |
| `early-exit` | Exited before target was reached |
| `revenge-trade` | Traded to recover a loss |
| `fomo` | Fear of missing out drove entry |
| `no-plan` | No pre-defined trade plan |
| `overtrading` | Too many trades in one session |
| `ignored-rules` | Consciously broke a trading rule |
| `bad-market` | Traded in unfavorable conditions |
| `added-to-loser` | Added to a losing position |

**Example in YAML:**
```yaml
mistakes: [early-entry, oversized]
```

---

## Current Focus Areas

*(Update monthly)*

**Top 3 Mistakes to Fix:**
1.
2.
3.

**Actions I'm Taking:**

---

*[[00 - Dashboard/🧠 Psychology|Psychology Dashboard]] | [[06 - Psychology/Emotional Patterns|Emotional Patterns]]*
