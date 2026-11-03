# PennyWise — Frontend prototype v0.1

A local-first personal expense analytics prototype using HTML, CSS and vanilla JavaScript.

## Run locally

**Quickest:** extract the ZIP and double-click `index.html` to open it in Chrome, Edge or Firefox.

**Recommended for editing:** open this folder in Visual Studio Code, install the Live Server extension, right-click `index.html`, then choose **Open with Live Server**.

No Python, Flask, SQLite, npm or build step is required yet. Chart.js is loaded from jsDelivr, so charts need an internet connection.

## Files

- `index.html` — structure of the app: sidebar, dashboard, transactions, analytics, budgets, settings and expense modal.
- `css/style.css` — dark fintech visual design, responsive layout, colors, spacing and mobile navigation.
- `js/app.js` — sample data, calculations, charts, form validation, add/edit/delete, filters, CSV export and browser localStorage persistence.

## Features

- INR reporting currency and monthly budget.
- Add, edit and delete expenses.
- Multi-currency entry with a **manual exchange rate** saved on each transaction.
- Search, category/currency filters and sorting.
- Spending trend and category charts.
- CSV export and sample-data reset.

For foreign currency, enter how many INR equal **one unit** of that currency. Example: USD amount `10`, rate `83.20` gives INR equivalent `₹832.00`. INR expenses use rate `1`.

## Prototype limitations

This is the frontend-only learning phase, not yet the Flask + SQLite application. Data is stored in this browser's localStorage; it is not encrypted, synced or backed up, and clearing browser data can remove it. Use sample data only for now. Currency calculations are prototype-grade; the production backend should use decimal-safe money handling and validation. The starter transactions are fictional sample data. Use Settings → Restore sample data to reset.

## Suggested learning order

1. Inspect the page sections in `index.html`.
2. Change a color or spacing value in `css/style.css` and refresh.
3. In `js/app.js`, inspect `sample`, `save()`, `renderDash()` and `open()`.
4. Add a category and trace how it appears in the expense form and filters.
5. Next phase: connect the interface to a Python Flask API and SQLite database.


## v0.2.0 — First-time setup and home screen

- First-time visitors see a setup screen to enter their name, optional email, and monthly budget.
- The account start date is automatically filled using the device's local date.
- Profile details are saved in `localStorage` under `pw_profile`.
- On later visits in the same browser on the same device, the setup screen is skipped and the user lands on the Home page.
- Home provides shortcuts to Add Expense, Analytics, Transactions, Budgets, Dashboard and Settings.
- CSV export now includes a UTF-8 BOM and a compact `DD MMM YYYY` date format to improve compatibility when opening in Excel.

### Important hosting/storage clarification

This is still a static HTML/CSS/JavaScript frontend. GitHub Pages can host it publicly, but it cannot run a private SQLite database for each visitor. This version saves each visitor's data in that visitor's browser `localStorage`, isolated by browser and website origin. It stays on that device/browser and is not shared with other users. Clearing browser data or changing browsers/devices can remove or make the data unavailable.

When we build the Python + Flask + SQLite version, SQLite will run on a server or on a user's own local machine. A public GitHub Pages website cannot directly create and manage a separate SQLite database file on every visitor's device. For a public, multi-user hosted app, we will need a backend and a proper per-user data-isolation design. Do not describe this frontend prototype as using SQLite yet.

### Resetting first-time setup during testing

To test the first-time setup again, open the browser developer tools → Application/Storage → Local Storage for your PennyWise site and remove the `pw_profile` key. Removing all site storage will also remove locally saved expenses and budgets, so export data first.
