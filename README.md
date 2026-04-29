# Trading Journal — Obsidian Vault

A complete day trader's journal built in Obsidian. Log trades fast, track your psychology, and watch your analytics update automatically — no spreadsheets required.

![Obsidian](https://img.shields.io/badge/Obsidian-7C3AED?style=flat&logo=obsidian&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green)

---

## What's Inside

| Section | What it does |
|---------|-------------|
| 🏠 **Home Dashboard** | Today's trades, week summary, 30-day performance, 90-day expectancy — all live |
| 📊 **Performance** | P&L by month/setup/session/ticker, grade distribution, top wins & losses |
| 🧠 **Psychology** | Emotion vs performance, discipline %, mistake frequency, rule violation log |
| 📝 **Templates** | Trade Entry, Daily/Weekly/Monthly Review, Strategy Page |
| 📋 **Trading Rules** | Your rules checklist with live discipline stats |
| ⚖️ **Risk Management** | Position sizing guide and formulas |

All dashboards update automatically as you log trades — powered by [Dataview](https://github.com/blacksmithgu/obsidian-dataview).

---

## Quick Install (5 minutes)

### 1. Download
Click **Code → Download ZIP**, extract it, and rename the folder if you like.

Or clone:
```bash
git clone https://github.com/YOUR_USERNAME/trading-journal.git
```

### 2. Open in Obsidian
- Download [Obsidian](https://obsidian.md) (free)
- Open Obsidian → **Open folder as vault** → select the `Trading Journal` folder

### 3. Install Plugins
**Settings → Community plugins → turn off Restricted Mode → Browse**

Search and install each of these:

| Plugin | Purpose |
|--------|---------|
| `Dataview` | Powers all analytics tables |
| `Templater` | Auto-fills date/time in templates |
| `QuickAdd` | One-keystroke trade logging |
| `Charts View` | Equity curve and chart visualizations |
| `Calendar` | Navigate vault by date |

### 4. Configure Templater
**Settings → Templater:**
- Template folder: `_Templates`
- Enable "Trigger Templater on new file creation": **ON**
- Add folder templates:
  - `02 - Trades` → `_Templates/Trade Entry`
  - `01 - Daily Reviews` → `_Templates/Daily Review`

### 5. Configure QuickAdd
**Settings → QuickAdd → Add Choice → Template:**
- Name: `New Trade`
- Template: `_Templates/Trade Entry`
- File name: `{{DATE:YYYY-MM-DD}} {{VALUE:Ticker}}`
- Folder: `02 - Trades/{{DATE:YYYY}}/{{DATE:MMMM}}`
- Open on creation: ON

Set the hotkey: **Settings → Hotkeys** → search `QuickAdd` → assign `Cmd+Shift+T`

> Full setup instructions with screenshots are in `08 - Reference/🔧 Vault Setup Guide.md` inside the vault.

---

## Daily Workflow

```
Pre-market  →  Cmd+Shift+D  (open today's daily review, note key levels)
After trade →  Cmd+Shift+T  (log the trade — enter ticker, fill YAML, grade it)
End of day  →  Complete daily review, check Home dashboard
End of week →  New note in 03 - Weekly Reviews/ from template
```

---

## Trade YAML Schema

Every trade file uses this frontmatter. Dataview reads it to power all dashboards:

```yaml
date: 2026-04-29
ticker: AAPL
direction: long           # long / short
setup_type: breakout      # must match strategy_name on strategy pages
session: open             # premarket / open / midday / close
entry_price: 185.50
exit_price: 188.00
position_size: 100
stop_loss: 184.00
pl_dollars: 250.00        # positive = win, negative = loss
r_multiple: 1.67          # pl_dollars / risk_amount
risk_amount: 150.00
emotional_state_before: neutral
followed_rules: true      # boolean
mistakes: []              # list: [early-entry, oversized]
grade: B                  # A / B / C / D / F
week: 2026-W18            # auto-filled by Templater
month: 2026-04            # auto-filled by Templater
```

**Grade scale:** A = perfect execution · B = good · C = okay · D = poor · F = rule violation

**Emotional states:** calm · neutral · focused · anxious · fearful · frustrated · euphoric · tired · impulsive

**Mistake tags:** `early-entry` · `late-entry` · `oversized` · `moved-stop` · `revenge-trade` · `fomo` · `no-plan` · `overtrading`

---

## Folder Structure

```
Trading Journal/
├── 00 - Dashboard/       ← Home, Performance, Psychology dashboards
├── 01 - Daily Reviews/   ← One note per trading day
├── 02 - Trades/          ← One note per trade (auto-organized by year/month)
├── 03 - Weekly Reviews/
├── 04 - Monthly Reviews/
├── 05 - Strategies/      ← Strategy docs with auto-populated trade history
├── 06 - Psychology/      ← Emotional patterns + mistakes analysis
├── 07 - Market Analysis/ ← Free-form market notes
├── 08 - Reference/       ← Trading rules, risk management, this setup guide
└── _Templates/           ← All templates (don't edit directly)
```

---

## License

MIT — use it, modify it, share it freely.
