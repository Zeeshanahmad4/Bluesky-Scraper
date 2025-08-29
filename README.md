# 🟦 Bluesky Scraper

<p align="center">
A BitBash product for structured Bluesky data (posts & profiles)
</p>

<p align="center">
  <a href="https://www.bitbash.dev/">
    <img alt="BitBash × Bluesky Scraper" src="https://img.shields.io/badge/Built%20by-BitBash-000000.svg?style=for-the-badge">
  </a>
  <a href="https://discord.gg/zX7frTbx">
    <img alt="Discord contact" src="https://img.shields.io/badge/Discord-Appilot-5865F2?logo=discord&logoColor=white&style=for-the-badge">
  </a>
  <a href="https://t.me/devpilot1">
    <img alt="Telegram contact" src="https://img.shields.io/badge/Telegram-@devpilot1-2CA5E0?logo=telegram&logoColor=white&style=for-the-badge">
  </a>
</p>

---

## Introduction
**Bluesky Scraper** extracts public Bluesky data (posts & profiles) into clean **CSV/JSON** for research, social listening, and growth analytics.  
White-hat by design — no CAPTCHA/anti-bot bypass.

---

## Table of Contents
1. [Overview](#overview)
2. [Features](#features)
3. [Why This Matters](#why-this-matters)
4. [Architecture](#architecture)
5. [Workflow](#workflow)
6. [Data Schema](#data-schema)
7. [Quick Start](#quick-start)
8. [Examples](#examples)
9. [FAQ](#faq)
10. [Security & Responsible Use](#security--responsible-use)
11. [Maintainers & Contact](#maintainers--contact)
12. [License](#license)
13. [Footer](#footer)

---

## Overview
Bluesky is growing fast, but its data is fragmented across profiles, threads, and feeds.  
This scraper normalizes public data into a consistent schema you can plug into your analytics stack.

---

## Features

| # | Feature | What It Does | Why It Matters |
|---|---|---|---|
| 1 | **Handle/Feed Input** | Scrape by `@handle`, DID, or feed URLs | Flexible targeting |
| 2 | **Rich Post Fields** | id, text, created_at, reply/repost/like counts, media URLs, external links | Complete analytics picture |
| 3 | **Profile Fields** | handle, display_name, followers_count, following_count, description | Audience insights |
| 4 | **CSV/JSON Export** | Save to CSV/JSON | Easy BI/ML integration |
| 5 | **Pagination** | Traverse timelines/feeds | Scales beyond first page |
| 6 | **Dedupe Helper** | Remove by `post_id` | Clean datasets |
| 7 | **Keyword Filter** | Include/exclude terms | Focused datasets |
| 8 | **White-Hat** | No CAPTCHA bypass | Safer & professional |

---

## Why This Matters
- Rising creator & community activity → **social listening** and **competitor tracking** opportunities.  
- Researchers need **structured public data** without manual copy/paste.  
- Brands & agencies want **trend discovery** and **influencer mapping**.

---

## Architecture
![architecture](./assets/bluesky-architecture.png)

**High-Level Flow**
1. Input (handle / feed URL)  
2. Fetch public pages/feeds  
3. Extract & normalize to schema  
4. Validate fields  
5. Export (CSV/JSON)  
6. Optional enrichment (keywords/sentiment)

---

## Workflow
![workflow](./assets/bluesky-workflow.png)

**Steps**
1. Provide target handle or feed URL  
2. Start collection (pagination enabled)  
3. Extract posts + author metadata  
4. Normalize to schema  
5. Export CSV/JSON  
6. Run `scripts/dedupe.js` if needed

---

## Data Schema

### Fields (Posts)
| Field | Type | Description | Example |
|---|---|---|---|
| post_id | string | Unique post id | `3kxy…` |
| text | string | Post text | `Launching…` |
| created_at | string (ISO) | Post timestamp | `2025-08-01T09:15:00Z` |
| like_count | int | Likes | 42 |
| repost_count | int | Reposts | 7 |
| reply_count | int | Replies | 5 |
| media_urls | string[] | Image/video URLs | `["https://..."]` |
| external_urls | string[] | Links in post | `["https://..."]` |
| language | string | Detected language | `en` |
| author_handle | string | `@handle` | `@bitbash.dev` |
| author_did | string | Bluesky DID | `did:plc:...` |
| author_display_name | string | Profile name | `BitBash` |
| author_followers | int | Followers count | 1204 |
| post_url | string | Canonical URL | `https://bsky.app/profile/.../post/...` |

**JSON Schema:** `./schema/bluesky_post.schema.json`

---

## Quick Start

```bash
# 1) Install
pnpm i   # or npm i / yarn

# 2) Run (example)
node scripts/run_bluesky.js --handle @bitbash.dev --limit 200 --out out/bluesky_posts.csv

# Options
--handle            @handle to scrape
--feed              feed URL to scrape
--limit             max posts (default 200)
--include-media     include media URLs
--include-links     include external links
--json              output JSON (default CSV)

```
---
## Examples

examples/bluesky_sample.csv <br>
examples/bluesky_sample.json

---

## FAQ

Q: Does this bypass protections? <br>
A: No, strictly white-hat.

Q: What about private data?<br> 
A: Only public pages/feeds are targeted.

Q: Rate limits?<br>
A: Throughput depends on your infra/proxies and pacing.

---

## Security & Responsible Use

Respect platform policies and local laws.
Add delays; avoid abusive traffic.
Don’t collect sensitive or private data.

--- 

## Maintainers & Contact

BitBash / Appilot
Website · Discord · Telegram → see badges above.
---

## License

MIT © BitBash

