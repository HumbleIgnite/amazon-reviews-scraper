[Amazon Reviews Scraper](https://apify.com/dltik/amazon-reviews-scraper?fpr=data)

# Amazon Reviews Scraper — Sentiment + Pros/Cons Auto-Extraction

> Extract **Amazon product reviews** with built-in **sentiment scoring** and **automatic pros/cons extraction**. The only Amazon reviews scraper that breaks down each review into positive and negative aspects automatically. Get rating, full text, author, verified flag, helpful votes, date. Supports `amazon.com`, `.fr`, `.de`, `.co.uk`, `.it`, `.es`, `.ca`, `.co.jp`. **$0.002 per review** ($2 per 1,000).

⭐ **Bookmark this Amazon Reviews Scraper** — Apify ranks actors by bookmarks, so it directly helps the visibility of this scraper on the Apify Store.

## What is the Amazon Reviews Scraper?

The **Amazon Reviews Scraper** is an Apify actor that pulls every review from any Amazon product page (across 8 marketplaces) and ships back a clean JSON dataset with sentiment scores and pros/cons baked in. Drop in an ASIN or a product URL, choose how many reviews to fetch, and the actor returns each review with: full text, star rating, author name, verified-purchase flag, helpful votes, posting date — plus a sentiment score (positive/neutral/negative + confidence) and a list of pros and cons distilled from the text.

Built on AFINN-165 lexicon for sentiment, with negation handling. No external sentiment API call, no extra cost.

## Use cases

- **Product research before launch** — analyze 1,000 reviews of competitor products to find unmet needs.
- **Brand monitoring** — daily scrape of your own product reviews; alert on dropping sentiment.
- **Comparative analysis** — pros/cons of product A vs product B at a glance.
- **AI training data** — labeled review datasets for fine-tuning sentiment models.
- **Refund / quality issue detection** — surface negative reviews mentioning "broken", "defective", "doesn't work" early.
- **Affiliate content generation** — auto-generate "Pros and Cons" sections for affiliate review articles.

## Input

```
{
  "productUrl": "https://www.amazon.com/dp/B0EXAMPLE12",
  "maxReviews": 200,
  "sortBy": "recent"
}
```

## Output

```
{
  "asin": "B0EXAMPLE12",
  "review_id": "R3EXAMPLE",
  "rating": 4,
  "title": "Great battery life, mediocre packaging",
  "text": "The battery lasts all day, way better than my old one...",
  "author": "Verified Buyer",
  "verified_purchase": true,
  "helpful_votes": 12,
  "review_date": "2026-04-15",
  "sentiment": "positive",
  "sentiment_score": 0.62,
  "pros": ["battery life", "build quality"],
  "cons": ["packaging", "instructions"]
}
```

## Pricing

**PAY_PER_EVENT — $0.002 per review** (= $2 per 1,000). No charge on errors.

## FAQ — Amazon Reviews API

**How is sentiment computed?** AFINN-165 lexicon with negation handling, in pure Python. No external API. Score from -1 (very negative) to +1 (very positive).

**Where do pros/cons come from?** Heuristic NLP extraction — adjective + noun pairs, negation reversal, frequency-weighted across the review.

**Does it handle multi-language reviews?** Yes — supports English, French, German, Spanish, Italian, Japanese (via per-locale lexicons).

**Can I scrape closed/restricted listings?** No — only public Amazon product pages.

---

⭐ **Found this useful? Bookmark this Amazon Reviews Scraper** — it's the strongest signal for Apify Store ranking.

### Related actors

- [Amazon Bestsellers Scraper](https://apify.com/dltik/amazon-bestsellers) — top 100 per category, 8 marketplaces
- [Trustpilot Scraper — Reviews + Sentiment](https://apify.com/dltik/trustpilot-scraper) — same sentiment engine for Trustpilot
- [Reddit Scraper — Posts + Sentiment](https://apify.com/dltik/reddit-scraper) — same sentiment engine for Reddit

License: MIT · Author: [dltik](https://apify.com/dltik)