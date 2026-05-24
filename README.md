# music-sentiment-stock-returns
Reproduced the research framework from a Journal of Financial Economics paper, building an automated GCP pipeline to analyze the correlation between music sentiment and next-day stock returns across 15 countries.

# music-sentiment-stock-returns

Reproduced the research framework from a Journal of Financial Economics paper, building an automated GCP pipeline to analyze the correlation between music sentiment and next-day stock returns across 15 countries.

> Inspired by Edmans et al. (2022) — [Music Sentiment and Stock Returns Around the World](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3776071)

---

## What this project does

1. Downloads Spotify Charts data (15 countries, 2017–2021) via Kaggle API
2. Computes Stream-Weighted Average Valence (SWAV) per country per day
3. Pulls historical stock market data via Yahoo Finance API
4. Stores everything in BigQuery and builds analysis views using SQL window functions
5. Visualizes the relationship between music sentiment and next-day stock returns in Looker Studio

---

## Architecture

```
Kaggle API → Cloud Storage → Cloud Function → BigQuery → Looker Studio
                                    ↑
                            Cloud Scheduler
                           (weekly trigger)
```

---

## Tools & Stack

| Category | Tools |
|----------|-------|
| Cloud | GCP Cloud Functions (Gen2), Cloud Scheduler, Cloud Storage |
| Data Warehouse | BigQuery |
| SQL | CTE, LEAD(), PARTITION BY |
| Python | pandas, yfinance, google-cloud-bigquery, kagglehub |
| APIs | Kaggle API, Yahoo Finance API |
| Visualization | Looker Studio |

---

## Repository structure

```
├── cloud_function/
│   ├── main.py              # Cloud Function entry point
│   └── requirements.txt     # Dependencies
│
├── pipeline/
│   ├── 01_compute_swav.py   # Compute stream-weighted average valence
│   ├── 02_stock_returns.py  # Fetch stock market data
│   └── 03_views.sql         # BigQuery analysis views
│
└── screenshots/             # GCP console & dashboard screenshots
```

---

## Key limitation

Full reproduction of the paper's findings requires access to Spotify's official Charts API (not publicly available). This project uses the Kaggle Spotify Charts dataset as a proxy, which may dilute the sentiment signal due to incomplete valence coverage.

---

## Dashboard

🔗 [[View Looker Studio Dashboard](#)](https://datastudio.google.com/reporting/9e55ec82-21a8-430a-ba05-9b5109e0ac16) ← 之後換成真實連結
