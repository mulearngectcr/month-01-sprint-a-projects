# 📡 TrendPulse — Weekly AI News Digest

An **n8n automation workflow** that curates and delivers a personalized weekly newsletter of trending tech articles, powered by AI-driven relevance scoring.

## How It Works

1. **Fetches topics** from a Google Sheet (filtered by active status)
2. **Pulls articles** from NewsAPI and Hacker News based on those topics
3. **Scores & summarizes** each article using Groq (LLaMA 3.3 70B) for relevance, sentiment, and a one-line summary
4. **Builds a styled HTML digest** highlighting the top pick and grouping articles by topic
5. **Sends the digest via email** (SMTP) on a weekly schedule

## Tech Stack

- **n8n** — Workflow automation
- **Google Sheets** — Topic management
- **NewsAPI & Hacker News** — Article sources
- **Groq (LLaMA 3.3 70B)** — AI analysis
- **SMTP** — Email delivery

## Files

| File | Description |
|------|-------------|
| `MuLearn-Project.json` | n8n workflow export (importable) |
| `brave_screenshot_localhost.png` | Workflow screenshot |
| `brave_screenshot_mail.google.com.png` | Email output screenshot |

## Setup

1. Import `MuLearn-Project.json` into your n8n instance
2. Configure credentials: Google Sheets, NewsAPI, Groq, and SMTP
3. Update the Google Sheet URL and email addresses
4. Activate the workflow

---

*Built by Sooraj K R*
