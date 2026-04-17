# Mysaathi Client Dashboard

A live, client-facing dashboard for the Mysaathi Program — tracking patient engagement and logistics performance. Data is fetched directly from a published Google Sheet and auto-refreshes every 5 minutes.

---

## 📁 File Structure

```
mysaathi-dashboard/
├── index.html       ← Main dashboard (single file, no dependencies)
├── vercel.json      ← Vercel deployment config
└── README.md        ← This file
```

---

## 🚀 Deploying to Vercel

### Option A — Connect GitHub repo (recommended)
1. Push this folder to a GitHub repository
2. Go to [vercel.com](https://vercel.com) → **New Project**
3. Import your GitHub repository
4. Vercel auto-detects the config — click **Deploy**
5. Every time you push to GitHub, Vercel redeploys automatically

### Option B — Vercel CLI
```bash
npm i -g vercel
cd mysaathi-dashboard
vercel --prod
```

---

## 📊 Data Source

| Sheet Tab | GID | Used For |
|---|---|---|
| Client Dashboard | `1310523268` | Patient Overview |
| Client Logistics | `1879543153` | Logistics Overview |

**Published URL base:**
```
https://docs.google.com/spreadsheets/d/e/2PACX-1vQscA-.../pub?gid=<GID>&single=true&output=csv
```

> The sheet must remain **Published to the web** (File → Share → Publish to web) for the dashboard to fetch data.

---

## 🔄 How Live Data Works

- On page load, both sheet tabs are fetched as CSV
- Data auto-refreshes every **5 minutes** in the background
- Clicking the sync pill (top right) triggers a manual refresh
- No backend, no server — pure static HTML

---

## 🗂️ Column Mapping

**Patient Sheet (`Purchase Month`, `Drug Name`, `Current Status`, `QR Type`)**

| Column | Used As |
|---|---|
| `Purchase Month` | Month filter |
| `Drug Name` | Drug type filter |
| `Current Status` | Active / Inactive classification |
| `QR Type` | QR distribution chart |

**Logistics Sheet (`Order Delivered Month`, `Product Name`, `Status`)**

| Column | Used As |
|---|---|
| `Order Delivered Month` | Month of dispatch filter |
| `Product Name` | Product filter |
| `Status` | Delivered / Pending / RTO classification |

> Freight-related data is intentionally not shown on this client-facing dashboard.

---

## 🛠️ Updating the Dashboard

| What changed | What to do |
|---|---|
| Sheet data updated | Nothing — dashboard auto-fetches latest |
| Published URL changed (re-published) | Update `URL_PATIENTS` / `URL_LOGISTICS` in `index.html` |
| New columns added | Update column mapping constants `PC` / `LC` in `index.html` |
| Design changes | Edit `index.html` and push to GitHub |

---

## ⚠️ If Data Stops Loading

1. Open the Google Sheet
2. Go to **File → Share → Publish to web**
3. Confirm status shows **"Published"**
4. If you stopped and republished, the `2PACX-...` ID changes — update the URLs in `index.html`
