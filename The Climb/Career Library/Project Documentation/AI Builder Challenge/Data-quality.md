---
kind: "project-document"
title: "Data-quality"
collection: "AI Builder Challenge"
topic: "Project Documentation"
imported: "2026-10-13"
source_files: ["AI Builder/AI Builder Challenge/docs/data-quality.md"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Data-quality

[[The Climb/Career Library/Career Library]]

# Public Data Source Quality Notes

This project treats public APIs as the evidence layer. The agent should not hide source limitations; it should use them as part of the intelligence read.

## GDELT DOC 2.0

**Role:** Real-time public news and web narrative signal.

**What it is good for:** Detecting whether a category, brand, or behavior is appearing in public coverage and extracting narrative direction from article/source context.

**Observed behavior during local testing:** GDELT explicitly rate-limits rapid public requests. Live probes returned a public message asking clients to limit requests to one every 5 seconds. The MCP server now serializes GDELT calls, waits at least 6 seconds between them, and caches repeated requests for 15 minutes.

**Quality read:** Strong strategic fit, but fragile for rapid-fire demos unless throttled and cached. Best used as a media/narrative layer, not as a purchase measurement source.

## YouTube Data API

**Role:** Public video/comment discussion layer.

**What it is good for:** Consumer language, creator framing, product reviews, objections, comparison language, public comments, and engagement proxies. The wrapper also attempts to pull public timedtext captions where YouTube exposes them.

**Observed behavior during local testing:** The MCP server requires `YOUTUBE_API_KEY`. When the key is missing, the app clearly discloses that YouTube comment intelligence is not configured.

**Quality read:** Strong behavior-like public signal for categories with active review or creator culture. It still does not prove purchases or demographics.

## NewsAPI

**Role:** Media narrative layer.

**What it is good for:** Fresh article framing, competitor news, category narratives, regulation/health concerns, and market conversation context. NewsAPI returns article metadata/snippets; the wrapper follows article URLs and extracts paragraph text where publisher pages allow it.

**Observed behavior during local testing:** The MCP server requires `NEWS_API_KEY`. Without it, the app discloses that NewsAPI is not configured.

**Quality read:** Useful for narrative freshness. It can overrepresent editorial attention, so it should not be treated as consumer demand by itself.

## Yelp Fusion API

**Role:** Local consumer trend layer.

**What it is good for:** Local business categories, review counts, ratings, and review excerpts where available.

**Observed behavior during local testing:** The MCP server requires `YELP_API_KEY`. Without it, the app discloses that Yelp is not configured.

**Quality read:** Useful for place-based consumer behavior and local demand texture. It is not transaction data.

## Product Hunt API

**Role:** Emerging product momentum layer.

**What it is good for:** Launches, tags, maker-market positioning, votes, comments, and early adopter language.

**Observed behavior during local testing:** The MCP server accepts either `PRODUCT_HUNT_TOKEN` or client-only OAuth credentials through `PRODUCT_HUNT_CLIENT_ID` and `PRODUCT_HUNT_CLIENT_SECRET`. Without them, the app discloses that Product Hunt is not configured.

**Quality read:** Strong for early product-market signals, especially software/AI/startup categories. Weak for mainstream CPG or local retail unless the category has startup products.

## Wikipedia / Wikimedia API

**Role:** Public category context and competitor/entity grounding.

**What it is good for:** Quickly grounding a query in known category pages, competitor brands, category lists, regulation topics, and public-interest pages.

**Observed behavior during local testing:** The endpoint responded reliably through `requests` and `curl`; `httpx` received a 403 from this Windows environment, so the connector uses `requests` in a worker thread.

**Quality read:** Useful for grounding and entity discovery. It is not trend volume by itself, but it improves source quality when GDELT is narrow or cooling down.

## Open Food Facts

**Role:** Public product/package/category signal for CPG-style questions.

**What it is good for:** Seeing real products and competitor brands in food, beverage, grocery, and packaged goods categories.

**Observed behavior during local testing:** The database is broad and global, which can create noisy product matches. The MCP server now broadens query terms but filters product records for category relevance.

**Quality read:** Useful as purchase-adjacent product context, not actual purchase behavior. Best paired with GDELT/Wikipedia rather than used alone.

## U.S. Census API

**Role:** Market and geography context.

**What it is good for:** Stable market sizing and demographic context for U.S. states.

**Observed behavior during local testing:** Reliable for state-level context.

**Quality read:** High-quality official public data, but not real-time and not behavioral.

## Product Implication

The public source portfolio can support directional consumer intelligence:

- What public narratives exist?
- Which category entities and competitors show up?
- What product/category signals support the hypothesis?
- What market context changes activation priorities?

It cannot prove:

- Actual purchases.
- Foot traffic.
- Household-level audience membership.
- Campaign lift.

In a production inMarket-style environment, this same agent pattern should connect to proprietary audience, purchase, location, and measurement datasets while keeping public APIs as context.


## Source provenance

- [Original MD](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/AI%20Builder/AI%20Builder%20Challenge/docs/data-quality.md) · AI Builder/AI Builder Challenge/docs/data-quality.md

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
