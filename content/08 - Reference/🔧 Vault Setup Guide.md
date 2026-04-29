---
tags: [reference, setup]
---

# 🔧 Vault Setup Guide

Complete this once when you first open the vault. Takes about 10 minutes.

---

## Step 1: Open This Vault in Obsidian

1. Open Obsidian
2. Click **Open folder as vault**
3. Navigate to and select the `Trading Journal` folder
4. Click **Open**

---

## Step 2: Install Community Plugins

**Settings** (gear icon) → **Community plugins** → Turn off **Restricted Mode** → **Browse**

Search for and install each plugin (click Install, then Enable):

| Plugin Name to Search | Purpose |
|-----------------------|---------|
| `Dataview` | Powers all analytics tables in dashboards |
| `Templater` | Auto-fills dates and times in templates |
| `QuickAdd` | One-keystroke trade logging |
| `Charts View` | Visualize equity curves and P&L charts |
| `Calendar` | Navigate vault by date |

---

## Step 3: Configure Dataview

**Settings → Community Plugins → Dataview → Options:**
- Enable JavaScript Queries: **ON**
- Enable Inline Queries: **ON**
- Date Format: `YYYY-MM-DD`

---

## Step 4: Configure Templater

**Settings → Community Plugins → Templater → Options:**
- Template folder location: `_Templates`
- Trigger Templater on new file creation: **ON**
- Add Folder Templates:
  - Folder: `02 - Trades` → Template: `_Templates/Trade Entry`
  - Folder: `01 - Daily Reviews` → Template: `_Templates/Daily Review`
  - Folder: `03 - Weekly Reviews` → Template: `_Templates/Weekly Review`
  - Folder: `04 - Monthly Reviews` → Template: `_Templates/Monthly Review`
  - Folder: `05 - Strategies` → Template: `_Templates/Strategy Page`

---

## Step 5: Configure QuickAdd

**Settings → Community Plugins → QuickAdd → Manage Macros:**

1. Click **Add Choice** → choose **Template**
2. Name it: `New Trade`
3. Template path: `_Templates/Trade Entry`
4. File name format: `{{DATE:YYYY-MM-DD}} {{VALUE:Ticker}}`
5. Create in folder: `02 - Trades/{{DATE:YYYY}}/{{DATE:MMMM}}`
6. Open file when created: **ON**
7. Click the ⚡ (lightning bolt) to add it to the command palette

Then set the hotkey: **Settings → Hotkeys** → search `QuickAdd: Run QuickAdd` → assign `Cmd+Shift+T`

---

## Step 6: Pin the Home Dashboard

1. Open `00 - Dashboard/🏠 Home`
2. Right-click the tab → **Pin**

---

## Step 7: Test Everything

1. Press `Cmd+Shift+T` → enter a ticker like `AAPL` → a new trade file should open
2. Verify the date and time are auto-filled (Templater working)
3. Open `00 - Dashboard/🏠 Home` → today's trade table should show your test entry
4. If Dataview tables show raw code instead of tables → check Dataview is enabled

---

## Daily Workflow

| When | Action |
|------|--------|
| Pre-market | `Cmd+Shift+D` to open today's daily review, note key levels |
| After each trade | `Cmd+Shift+T`, enter ticker, fill out the trade note |
| End of day | Complete daily review, grade all trades |
| End of week | New note in `03 - Weekly Reviews/` using Weekly Review template |
| End of month | New note in `04 - Monthly Reviews/` using Monthly Review template |

---

## YAML Field Reference

Every trade file must use these exact field names for Dataview queries to work:

```yaml
date: 2026-04-29            # YYYY-MM-DD — do not change format
time_entry: 09:45           # HH:mm
ticker: AAPL                # Uppercase
direction: long             # long or short (lowercase)
setup_type: breakout        # your strategy name — must match strategy_name on strategy pages
session: open               # premarket / open / midday / close / afterhours
entry_price: 185.50         # number, no $ sign
exit_price: 188.00
position_size: 100          # shares or contracts
stop_loss: 184.00
take_profit: 190.00
pl_dollars: 250.00          # positive = win, negative = loss
pl_percent: 1.35            # as a number (1.35 = 1.35%)
r_multiple: 1.67            # calculated: pl_dollars / risk_amount
risk_amount: 150.00
emotional_state_before: neutral
emotional_state_during: calm
emotional_state_after: satisfied
followed_rules: true        # true or false — no quotes
market_condition: trending-up
mistakes: []                # YAML list: [early-entry, oversized] or [] if none
grade: B                    # A / B / C / D / F
week: 2026-W18              # auto-filled by Templater
month: 2026-04              # auto-filled by Templater
```

**Valid emotional states:** calm, neutral, focused, anxious, fearful, frustrated, bored, tired, confident, euphoric, impulsive, greedy

**Valid market conditions:** trending-up, trending-down, range-bound, volatile, choppy, news-driven

**Valid sessions:** premarket, open, midday, close, afterhours

**Grade scale:**
- **A** — Perfect execution, followed all rules, hit target
- **B** — Good trade, minor deviations, solid outcome
- **C** — Okay trade, notable issues but not rule-breaking
- **D** — Poor execution, significant emotional or process errors
- **F** — Rule violation, regardless of whether it was profitable

---

*[[00 - Dashboard/🏠 Home|Home]]*
