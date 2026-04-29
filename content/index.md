---
title: Trading Journal
tags: []
---

# Trading Journal

A complete day trader's journal system built in [Obsidian](https://obsidian.md) — free, local-first, and fully automatic. Log a trade in seconds, and your performance dashboards update instantly.

---

## Get Started in 5 Minutes

**1. Download the vault**

Click the button below, extract the zip, and open the folder in Obsidian.

> **[⬇ Download ZIP](https://github.com/V3LDS/trading-journal/archive/refs/heads/main.zip)**

**2. Install Obsidian** (free) from [obsidian.md](https://obsidian.md)

**3. Open folder as vault** → follow the [[08 - Reference/🔧 Vault Setup Guide|Setup Guide]] inside

---

## What You Get

| | |
|--|--|
| **🏠 Home Dashboard** | Today's trades, weekly P&L, 30-day performance, 90-day expectancy — all live |
| **📊 Performance** | P&L by month, setup, session, ticker, direction — every angle covered |
| **🧠 Psychology** | Emotion vs win rate, discipline %, mistake frequency, rule violation log |
| **⚡ One-keystroke logging** | `Cmd+Shift+T` → enter ticker → trade note opens with date/time auto-filled |
| **📝 5 Templates** | Trade Entry, Daily / Weekly / Monthly Review, Strategy Page |
| **📋 Reference docs** | Trading rules checklist, position sizing guide, risk management formulas |

---

## How It Works

Every trade is a markdown file with YAML frontmatter. [Dataview](https://github.com/blacksmithgu/obsidian-dataview) reads those fields and powers every table and stat across the dashboards — no manual updating, no formulas to break.

```yaml
ticker: AAPL
direction: long
setup_type: breakout
pl_dollars: 270
r_multiple: 1.8
emotional_state_before: calm
followed_rules: true
grade: A
```

Add that to a trade note → Home dashboard shows it immediately.

---

## Browse the Vault

- [[_Templates/Trade Entry|Trade Entry Template]] — the YAML schema every dashboard depends on
- [[_Templates/Daily Review|Daily Review Template]]
- [[_Templates/Weekly Review|Weekly Review Template]]
- [[_Templates/Monthly Review|Monthly Review Template]]
- [[_Templates/Strategy Page|Strategy Page Template]]
- [[08 - Reference/📋 Trading Rules|Trading Rules]]
- [[08 - Reference/⚖️ Risk Management|Risk Management Guide]]
- [[08 - Reference/🔧 Vault Setup Guide|Full Setup Guide]]

---

## Built With

- [Obsidian](https://obsidian.md) — the note-taking app
- [Dataview](https://github.com/blacksmithgu/obsidian-dataview) — SQL-like queries over your notes
- [Templater](https://github.com/SilentVoid13/Templater) — auto-fill date/time in templates
- [QuickAdd](https://github.com/chhoumann/quickadd) — one-keystroke trade capture
- [Quartz](https://quartz.jzhao.xyz) — this website

---

*Free and open source. [View on GitHub](https://github.com/V3LDS/trading-journal)*
