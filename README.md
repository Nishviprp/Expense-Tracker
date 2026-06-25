# Ledger — Daily Expense Tracker

A private, local-first expense tracker that runs entirely in your browser. Log expenses, attach receipt photos, and see your spending broken down by category — all without an account, a server, or any data leaving your device.

![No backend](https://img.shields.io/badge/backend-none-brightgreen) ![Storage](https://img.shields.io/badge/storage-IndexedDB%20(local)-blue) ![License](https://img.shields.io/badge/license-MIT-lightgrey)

## Why this exists

Most expense trackers ask you to create an account and send your spending data to someone's server. Ledger doesn't. It's a single HTML file — open it in a browser and it works. Everything you enter is stored locally on that device using IndexedDB. Nobody, including the developer, has access to it.

## Features

- **Manual entry** with amount, category, date, and description
- **Automatic categorization** — keyword matching guesses the category from what you type (e.g. "Uber to airport" → Transportation, "Big Bazaar groceries" → Groceries) and you can override it
- **Receipt photos** — attach a photo to any entry, stored locally alongside it
- **Monthly summary** — total spent, entry count, and a category-by-category breakdown with percentages
- **Month navigation** — browse past months
- **Category filter** — view entries from one category at a time
- **Backup & restore** — export your data as a JSON file, import it back later or on another device
- **No sign-up, no server, no tracking**

## Getting started

### Option 1: Just open it
Download `expense-tracker.html` and open it in any modern browser (Chrome, Firefox, Edge, Safari). That's it.

### Option 2: Host it yourself
Works with any static hosting — GitHub Pages, Netlify, Vercel, or a plain web server.

```bash
git clone https://github.com/<your-username>/ledger-expense-tracker.git
cd ledger-expense-tracker
# open expense-tracker.html directly, or serve it:
python3 -m http.server 8000
# then visit http://localhost:8000/expense-tracker.html
```

### Option 3: GitHub Pages
1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Set the source branch and root folder
4. Your tracker will be live at `https://<your-username>.github.io/<repo-name>/expense-tracker.html`

## How your data is stored

All entries — amounts, categories, dates, descriptions, and receipt photos — are saved in your browser's **IndexedDB**, scoped to that browser on that device.

- Nothing is sent over the network. There's no server in this project at all.
- Data does **not** sync across devices or browsers automatically.
- Clearing your browser's site data (or using a different browser/device) will not show your old entries.
- Use the **Export** button regularly to download a JSON backup, and **Import** to restore it on the same or a different device.

## Categorization rules

Categorization uses simple keyword matching against the description you type — entirely offline, no AI calls. Current categories:

| Category | Example keywords |
|---|---|
| Food & Dining | restaurant, zomato, swiggy, cafe, coffee |
| Groceries | supermarket, grocery, milk, vegetables |
| Transportation | uber, ola, taxi, fuel, parking, metro |
| Bills & Utilities | electricity, internet, subscription, netflix |
| Shopping | amazon, flipkart, mall, clothing |
| Health | pharmacy, doctor, hospital, clinic |
| Entertainment | movie, concert, cinema, gaming |
| Housing & Rent | rent, mortgage, maintenance fee |
| Travel | hotel, airbnb, flight, vacation |
| Education | tuition, course, book, school fee |
| Other | anything that doesn't match a rule above |

You can edit the `KEYWORD_RULES` array in `expense-tracker.html` to add your own keywords or categories.

## Project structure

```
.
├── expense-tracker.html   # the entire app — HTML, CSS, and JS in one file
└── README.md
```

There's no build step, no dependencies, no `package.json`. It's one file by design, so anyone can download it and run it without setup.

## Customizing

Everything lives in `expense-tracker.html`:
- **Categories & colors** — edit the `CATEGORIES` object
- **Auto-categorization rules** — edit the `KEYWORD_RULES` array
- **Currency symbol** — change the `$` in the `fmtMoney` function and the amount field
- **Styling** — all CSS is in the `<style>` block at the top, using CSS variables for the color palette

## Limitations

- Single-device only (by design — no server means no built-in sync)
- No multi-user support; one ledger per browser profile
- Receipt photos are stored as base64 inside IndexedDB, so very large images will use more local storage
- Categorization is rule-based, not AI — it won't catch everything and is meant to be a fast starting guess, not a final answer

## License

MIT — use it, modify it, ship it.
