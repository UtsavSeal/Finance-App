# The Ledger — Personal Finance Tracker

A single-file, self-contained personal finance tracker with an editorial newspaper aesthetic. Reads from any public Google Sheet, no backend required. Deploys to GitHub Pages in 2 minutes.

## What's in this folder

```
├── index.html                       ← the entire app (open in browser, done)
├── finance-tracker-template.csv     ← starter CSV with example data
├── .nojekyll                        ← tells GitHub Pages to skip Jekyll
└── README.md                        ← this file
```

## Set up your Google Sheet

### Option A — quick (recommended)

1. Create a new Google Sheet
2. Open `finance-tracker-template.csv` and copy its contents, or upload the CSV via **File → Import**
3. Click **Share** (top-right) → change to "Anyone with the link" → "Viewer"
4. Copy the URL
5. Paste it into the app's "Connect your Google Sheet" field and hit **Load Sheet**

### Option B — Publish to web

1. **File → Share → Publish to web**
2. Choose the sheet, format: **Comma-separated values (.csv)**
3. Click **Publish** and copy the URL
4. Paste into the app

The app handles both URL formats automatically.

## CSV Format

The template has these columns. Only the first 5 are required — the rest are optional metadata:

|Column|Required|Example|Notes|
|-|-|-|-|
|Date|✅|`2026-01-15` or `15/01/2026`|Most common formats work|
|Description|✅|`Petrol - HP Pump`|Free text|
|Category|✅|`Food`, `Housing`, `Transport`|Used for grouping|
|Amount|✅|`4200`|Just the number, no symbols needed|
|Type|✅|`Income` or `Expense`|Case-insensitive|
|Payment Method|❌|`UPI`, `Credit Card`|Future use|
|Account|❌|`HDFC Savings`|Future use|
|Tags|❌|`groceries;essentials`|Semicolon-separated|
|Notes|❌|`Weekly run`|Free text|

### Recognized categories (with custom colors)

Housing, Food, Dining, Transport, Utilities, Shopping, Entertainment, Health, Education, Travel, Investment, Personal, Income, Other

Anything else gets a default color — categories don't have to match this list.

## Features

**Date filtering** — five modes:

* **Quick presets**: Today, last 7/30/90 days, MTD, last month, YTD, this year, last year, all time
* **By Month**: pick any individual month from your data
* **By Quarter**: Q1/Q2/Q3/Q4 across years
* **By Year**: any year present in the data
* **Custom Range**: arbitrary start and end dates

**Period comparison** — toggle "Compare with previous period" to see income/expense/net side-by-side with the prior equivalent period (and % change on the headline stats).

**Reports**:

* *Overview* — category pie + top individual outlays + daily pattern (for ranges ≤ 60 days)
* *Category Report* — bar chart + full breakdown table with averages and shares
* *Trends* — monthly income vs expense area chart, net savings per month
* *Ledger* — full sortable transaction list

The sheet URL is remembered in `localStorage`, so reloads stick.

## Troubleshooting

**"Sheet returned 401/403"** → Sharing isn't set to "Anyone with the link". Open the sheet → Share → change permissions.

**"Sheet appears empty"** → Make sure the first row is the header (Date, Description, etc.) and there's at least one data row below.

**"CORS error" in console** → Use the **File → Share → Publish to web → CSV** route instead of plain sharing. That endpoint allows browser fetches.

**Dates not parsing** → The parser handles `YYYY-MM-DD`, `DD/MM/YYYY`, `DD-MM-YYYY`. If yours uses something exotic, reformat in Sheets first.

**Currency** → Currently hardcoded to INR (₹) with Indian number formatting (lakhs). To change, find the `fmt` and `fmtCompact` functions in `index.html` and swap the locale/currency.

## Privacy

No backend, no analytics, no tracking. The app runs entirely in your browser. The only network requests are:

* Fonts and JS libraries from CDNs (Google Fonts, unpkg)
* Your Google Sheet (only when you click "Load Sheet")

Your sheet URL is saved in your browser's `localStorage`, not sent anywhere.

