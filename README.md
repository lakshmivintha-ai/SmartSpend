# SmartSpend

**Know if you can afford it — before you spend, not after.**

A real-time spending decision assistant for students and young earners, built for the **Global Innovation Hackathon 2026 – Build for a Better Future**.

Team: X (Product & Frontend) · Y (Backend & Logic)

---

## The Problem

Students and young earners receive money irregularly — allowance, part-time pay, scholarships — with no fixed schedule. In the moment of buying something, there's no easy way to know if it's actually safe to spend. By the time it's obvious money is running low, the decision that caused it was made days earlier. The result is a recurring cycle of running out of money before the next income arrives.

Existing tools don't solve this:
- **Manual expense trackers** only log what already happened — no warning before overspending.
- **Bank/SMS-linked apps** require risky SMS or bank read permissions, which are blocked by modern Android policy and are fragile to build reliably.

## The Solution

SmartSpend flips the order: instead of reporting what you *already* spent, it tells you — with real math, in plain language — whether a purchase you're *about* to make is safe, based on what you have left and how many days until your next income. It then tracks every decision over time to reveal patterns (like consistently overriding its own warnings) and rewards a streak of safe decisions.

No bank access. No SMS permissions. Fully manual, fully offline, fully auditable — every recommendation is a transparent calculation, not an AI guess.

## How It Works

1. **Log income** — enter your current balance and the date your next income is expected.
2. **Check a want** — before buying something, enter the amount, what it's for, and how necessary it is.
3. **Get the math** — SmartSpend calculates your safe daily spend, projects what happens if you go ahead, and gives a verdict: safe, caution, or risky — with the reasoning shown.
4. **Track patterns** — every decision (and whether you skipped or bought anyway) is logged, building a streak and a running history.

## What's Implemented (this prototype)

- Income logging (balance + next income date), stored in the browser (`localStorage`)
- Days-left and safe-daily-spend calculation
- "Can I afford this?" checker with a rules-based affordability engine:
  - Flags purchases that exceed current balance outright
  - Flags purchases that cut projected daily budget by more than 50%
  - Flags "not necessary" purchases that meaningfully reduce the daily budget
  - Otherwise marks the purchase safe
- Plain-language reasoning and a suggestion for every verdict
- Decision logging: mark a checked want as "skipped" or "bought anyway"
- Automatic balance deduction when a purchase is logged as bought
- Decision history list (most recent 12)
- Safe-decision streak counter (skipped when risky/caution, or bought only when safe)
- "Bought anyway despite risk" counter, to surface override patterns

## What's Planned (future scope)

- Optional bank-statement (CSV) import for automated logging
- Regional language support
- Peer-group anonymized spending comparisons
- College partnerships for financial-literacy programs

## Tech Stack

- **Frontend:** Single-page HTML, CSS, and vanilla JavaScript — no framework dependency, so it runs anywhere with zero build step
- **Affordability Engine:** Rules-based math (remaining balance ÷ days left, percentage-drop thresholds) — deliberately not AI-generated, so every recommendation is auditable and explainable
- **Storage:** Browser `localStorage` — no backend, no database, no server required for this prototype

## Running It

No installation required.

1. Clone or download this repository
2. Open `index.html` in any modern browser

Or deploy it as a static site (GitHub Pages, Netlify, Vercel) for a live demo link — the app has no backend dependency.

## Project Structure

smartspend/
├── index.html   # complete app: markup, styles, and logic in one file
└── README.md    # this file

## Demo Script (suggested)

1. Enter a balance (e.g. ₹500) and a next-income date ~12 days out.
2. Check a want: ₹300, "new shoes," marked "Not necessary" → shows a **risky** verdict with the exact daily-budget drop explained.
3. Click "I'll skip / wait" → streak increases, decision appears in history.
4. Check a smaller want (e.g. ₹50, "essential") → shows a **safe** verdict.
5. Click "I'm buying it anyway" → balance updates, decision logged, streak resets if it was risky.