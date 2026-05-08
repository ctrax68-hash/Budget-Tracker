# 💰 Family Budget App

A mobile-first personal finance dashboard built as a single HTML file. No server, no database, no dependencies to install — open it in a browser and it works.

**Live demo:** `https://<your-username>.github.io/family-budget`

-----

## Features

- **Budget tracking** — Income and expenses organized by category and line item
- **Actual vs Budget** — Import bank CSV exports to compare real spending against your plan
- **Manual entry** — Log purchases on the fly with the + button; CSV import reconciles them automatically
- **Multi-account** — Tag transactions to different bank accounts (checking, credit cards, spouse’s accounts)
- **Year navigation** — Back-load all of 2026 at once, then add months as statements close
- **Inline editing** — Tap any amount, line item name, or category name to edit it directly
- **Excel import/export** — Load your existing budget spreadsheet; export changes back to Excel
- **Mobile-first** — Designed for phone use with bottom nav, swipeable month strip, and thumb-friendly tap targets

-----

## Getting Started

### Option 1 — GitHub Pages (recommended)

1. Fork this repo
1. Go to **Settings → Pages**
1. Set source to `main` branch, `/ (root)` folder
1. Your app is live at `https://<your-username>.github.io/family-budget`

The included GitHub Actions workflow (`.github/workflows/deploy.yml`) also auto-deploys on every push to `main`.

### Option 2 — Run locally

```bash
git clone https://github.com/<your-username>/family-budget.git
cd family-budget
# Open in browser — no build step needed
open index.html
```

Or serve it with any static file server:

```bash
npx serve .
# or
python3 -m http.server 8080
```

-----

## How to Use

### First time setup

1. Open the app and tap **Login as Kevt** or **Login as Kristen** (or sign up with your own credentials)
1. Browse to the **Expenses** tab to review and edit your budget categories and line items
1. Tap any dollar amount to edit it; tap any name to rename it

### Tracking spending

**During the month:**

- Tap the orange **+** button on any screen
- Enter the amount, merchant, date, and which budget line it belongs to
- It shows as “⏳ Pending” until your statement confirms it

**At month end:**

- Download your bank statement as a CSV (most banks call it “Export” or “Download transactions”)
- Go to **Settings → Import Bank Transactions**
- Name the account (Chase Checking, Capital One Visa, etc.)
- The app auto-categorizes transactions and matches any pending manual entries — no duplicates

### Importing your existing Excel budget

1. Go to **Settings → Import Excel Budget**
1. Select your `budget_interactive.xlsx` file
1. All your categories and amounts load automatically
1. Use **Export to Excel** anytime to save changes back to a spreadsheet

### Back-loading historical data

1. Download CSVs from your bank for Jan–May (or however far back you want)
1. Import each one, tagging it to the right account
1. Use the `‹ 2026 ›` year stepper on the Actual tab to navigate between years

-----

## Sample Data

A `sample_bank_transactions.csv` file is included with 33 realistic May transactions. Use it to test the import flow before connecting your real bank data.

-----

## CSV Format Compatibility

The app auto-detects column order and supports all major US bank formats:

|Bank            |Format                                                                       |
|----------------|-----------------------------------------------------------------------------|
|Chase           |Date, Description, Amount                                                    |
|Bank of America |Date, Description, Amount, Running Bal.                                      |
|Wells Fargo     |Date, Amount, *, *, Description                                              |
|Capital One     |Transaction Date, Posted Date, Card No., Description, Category, Debit, Credit|
|Citi            |Status, Date, Description, Debit, Credit                                     |
|American Express|Date, Description, Amount                                                    |

If your bank’s format isn’t auto-detected, open an issue with a sample (sensitive data removed).

-----

## Project Structure

```
family-budget/
├── index.html                    # The entire app — HTML, CSS, and JS in one file
├── sample_bank_transactions.csv  # Test data for the CSV import feature
├── README.md                     # This file
├── .gitignore
└── .github/
    └── workflows/
        └── deploy.yml            # Auto-deploy to GitHub Pages on push
```

Everything lives in `index.html`. There is no build process, no `node_modules`, no compilation step.

-----

## Sharing Between Two People

Since this is a static file app, “sharing” means both people have access to the same URL (GitHub Pages link). Data is stored in browser memory only — it resets on refresh.

**To make data persist and sync between you and your spouse**, see the roadmap below. The next step is adding `localStorage` so data survives a refresh, followed by a lightweight backend for real-time sync.

**Current workaround:** Use the **Export to Excel** feature to save your budget state, then re-import it next session.

-----

## Roadmap

- [ ] `localStorage` persistence (survive page refresh, no backend needed)
- [ ] PWA / Add to Home Screen support (feels like a native app)
- [ ] Plaid or Teller.io live bank connection (replace CSV import)
- [ ] Push notifications for budget alerts (“you’re 85% through dining budget”)
- [ ] Shared backend via Firebase or Supabase (real-time sync between spouses)
- [ ] Recurring transaction detection and auto-categorization improvement

-----

## Tech Stack

|Layer  |Technology                               |
|-------|-----------------------------------------|
|UI     |Vanilla HTML/CSS/JS — no framework       |
|Charts |Chart.js 3.9 (CDN)                       |
|Excel  |SheetJS / xlsx 0.18 (CDN)                |
|Fonts  |DM Sans + DM Serif Display (Google Fonts)|
|Hosting|GitHub Pages                             |
|Build  |None                                     |

-----

## Contributing

This is a personal family finance tool. If you fork it and make improvements — better categorization rules, new bank format support, UI fixes — pull requests are welcome.

-----

## License

MIT — use it however you want.