# AutoScout — Autonomous Market Intelligence Agent

An autonomous agent that monitors companies for news, extracts key insights using AI, and logs structured intelligence to a live spreadsheet — with zero manual effort after setup.

## What it does

Every day at 8 AM, AutoScout automatically:
1. Reads a watchlist of companies from Google Sheets
2. Searches the web for recent news on each company (Jina AI Search)
3. Reads the full article content (Jina AI Reader)
4. Summarizes it and extracts sentiment using AI
5. Logs the structured result — date, headline, summary, sentiment, source — into a live Intelligence Log spreadsheet

## Architecture

Schedule Trigger (daily 8 AM)
↓
Google Sheets: Find Rows (Watchlist)
↓
Loop on Items (per company)
↓
Router (skip header row)
↓ (Otherwise branch)
Jina Search API → Jina Reader API → AI Summarization → Google Sheets: Add Row


## Tech stack

- **Activepieces** — workflow orchestration and automation
- **Jina AI** — web search (`s.jina.ai`) and content extraction (`r.jina.ai`)
- **Google Sheets API** — data source and structured output storage
- **AI (via Activepieces)** — summarization and sentiment extraction

## Sample output

| Date | Company | Headline | Sentiment | Source |
|------|---------|----------|-----------|--------|
| 2026-09-20 | Anthropic | Anthropic unveils Claude Fable 5.1 and Claude Mythos 5.1 | Positive | [anthropic.com](https://www.anthropic.com) |
| 2026-09-20 | Microsoft | Microsoft launches comprehensive AI platform | Positive | [microsoft.com](https://www.microsoft.com) |
| 2026-09-20 | Google DeepMind | Google DeepMind unveils latest AI models | Positive | [deepmind.google/blog](https://deepmind.google/blog) |
| 2026-09-20 | OpenAI | OpenAI closes $122 billion funding round | Positive | [openai.com](https://openai.com/index) |

*Date field now pulls a live timestamp from the HTTP request headers, so it automatically reflects the real date of each run instead of a fixed value.*

## Why this project

Built to demonstrate automation + AI + structured data extraction skills relevant to data analytics, BI reporting, and AI/ML roles — the same pipeline pattern (trigger → fetch → transform → store) that scales to production-grade intelligence tools.

## Known Limitations

- Some websites with strict anti-bot protection (e.g., Tesla's blog) block Jina's reader from extracting content, returning an "Access Denied" message instead of article text. This is a common real-world challenge in web-scraping pipelines, and companies were selected in the Watchlist partly based on scraper-friendliness.
- Search results occasionally return SEO/marketing pages instead of genuine news articles when a company's keyword overlaps with unrelated popular search terms.
- A future improvement would be adding a content-quality check (e.g., minimum word count, retry with next search result) before passing text to the AI summarization step.

## Files in this repo

- `autoscout-flow.json` — exportable Activepieces flow definition
- `flow-diagram.png` — visual pipeline architecture
- `watchlist-sample.png` — example input sheet
- `intelligence-log-sample.png` — example output with real data
- `demo.gif` / `demo.mp4` — short demo of the flow running live
