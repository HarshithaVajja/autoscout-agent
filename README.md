# AutoScout — Autonomous Market Intelligence Agent

An autonomous agent that monitors companies for news, extracts key insights using AI, and logs structured intelligence to a live spreadsheet — with zero manual effort after setup.

## What it does

Every day at 8 AM, AutoScout automatically:
1. Reads a watchlist of companies from Google Sheets
2. Searches the web for recent news on each company (Jina AI Search)
3. Reads the full article content (Jina AI Reader)
4. Summarizes it and extracts sentiment using AI
5. Logs the structured result — headline, summary, sentiment, source — into a live Intelligence Log spreadsheet

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
| 2026-09-20 | OpenAI | OpenAI considers pre-IPO funding round at $1-2T valuation | Positive | [WSJ](https://www.wsj.com/tech/ai/openai-considers-pre-ipo-funding-round-at-more-than-1-2-trillion-valuation-54555295) |
| 2026-09-20 | Tesla | [Tesla blog update] | Negative | [tesla.com/blog](https://www.tesla.com/blog) |

## Why this project

Built to demonstrate automation + AI + structured data extraction skills relevant to data analytics, BI reporting, and AI/ML roles — the same pipeline pattern (trigger → fetch → transform → store) that scales to production-grade intelligence tools.

## Files in this repo

- `autoscout-flow.json` — exportable Activepieces flow definition
- `flow-diagram.png` — visual pipeline architecture
- `watchlist-sample.png` — example input sheet
- `intelligence-log-sample.png` — example output with real data
- `demo.gif` / `demo.mp4` — short demo of the flow running live


