# Iran News Tracker

Automated news aggregation system that monitors global media coverage of Iran across 36+ trusted sources spanning 8 regions.

## Overview

This repository stores daily CSV files of Iran-related headlines running every 31-37 minutes. Data is sourced from Google News RSS feeds, filtered for relevance, deduplicated, and committed automatically.

## Sources

| Region | Sources |
|--------|---------|
| Global | Reuters, AP, BBC, Financial Times, Bloomberg, AFP |
| Europe | DW, France 24, Euronews, Le Monde |
| US | NYT, Washington Post, WSJ, CNN, Fox News, Axios, NY Post, Politico |
| UK | The Guardian, The Telegraph, The Independent |
| Arab | Al Jazeera, Arab News, Al Arabiya, The National, Asharq Al-Awsat |
| Israel | Times of Israel, Haaretz, Jerusalem Post |
| China | CGTN, Xinhua, Caixin Global |
| Pakistan | Dawn, Express Tribune |
| Russia | RT |
| Iran | Press TV |

## Data Structure

Each CSV file (`news/YYYY-MM-DD.csv`) contains:

| Column | Description |
|--------|-------------|
| `headline` | Article headline (source name stripped) |
| `link` | Direct URL to the article |
| `source` | Trusted source name (matched via regex) |
| `region` | Geographic region of the source |
| `published_at` | Publication timestamp (ISO 8601) |

## Filtering Pipeline

1. RSS feeds fetched from Google News for each source (last 1 hour window)
2. Headlines matched against trusted source patterns
3. Iran relevance check (primary: Iran, Tehran, IRGC, etc.)
4. Context check (Middle East, sanctions, oil, diplomacy, etc.)
5. Deduplication by URL and headline across historical and current runs
6. Sorted by publish time, limited to top 50 per cycle
7. Stored in Google Sheets, sent to Telegram channel, and committed here

## Distribution

- **Telegram**: [@iranfocused](https://t.me/iranfocused)
- **GitHub**: This repository (long-term archival)
