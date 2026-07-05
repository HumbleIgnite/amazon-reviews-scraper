[Amazon Reviews Scraper](https://apify.com/khadinakbar/amazon-reviews-scraper?fpr=data)

# 🛒 Amazon Reviews Scraper — Extract Ratings, Sentiment & Verified Purchases

## What does Amazon Reviews Scraper do?

Amazon Reviews Scraper extracts structured review data from any Amazon product page — no Amazon API key required. Give it a product URL or ASIN, and it returns clean JSON with every review's star rating, full text, verified purchase status, helpful vote count, reviewer info, images, and product variant — ready for sentiment analysis, brand monitoring, competitive research, or AI pipelines.

## Why use Amazon Reviews Scraper?

- **Beats the market leader on rating** — built from scratch with production-grade selectors, session pools, and residential proxies that actually work
- **Flexible input** — accepts Amazon URLs, raw ASINs, or both at the same time
- **Powerful filters** — filter by star rating (1★–5★), keywords (e.g. "battery"), and date cutoffs
- **Full pagination** — automatically follows all review pages up to your `maxReviews` limit
- **MCP-ready output** — semantic field names, consistent schema, and a rich dataset view so Claude and other AI agents can use it directly
- **33% cheaper** than the leading competitor at $0.004 per review (FREE tier)

## What data can Amazon Reviews Scraper extract?

| Field | Type | Description |
| --- | --- | --- |
| `asin` | string | Amazon product ID (e.g. B0CWXNS552) |
| `product_title` | string | Product name |
| `product_url` | string | Direct Amazon product URL |
| `review_id` | string | Amazon's unique review ID |
| `reviewer_name` | string | Reviewer display name |
| `reviewer_profile_url` | string | Link to reviewer's Amazon profile |
| `is_verified_purchase` | boolean | Was this a confirmed Amazon purchase? |
| `rating` | number | Star rating 1.0–5.0 |
| `review_title` | string | Short review headline |
| `review_body` | string | Full review text (great for NLP/sentiment) |
| `review_date` | string | Raw date string from Amazon |
| `review_date_iso` | string | ISO 8601 parsed date for filtering |
| `helpful_votes` | number | Upvote count from other Amazon users |
| `images` | array | Full-size review image URLs |
| `variant` | string | Product variant reviewed (color, size, etc.) |
| `country` | string | Country where review was written |
| `is_top_review` | boolean | Amazon-labeled top review flag |
| `scraped_at` | string | ISO timestamp of when scraped |
| `source_url` | string | Exact reviews page URL scraped |

## How to scrape Amazon reviews — tutorial

### Option 1: Quick start in the Apify Console

1. Go to your actor page on Apify Store
2. Click **Try for free**
3. Paste one or more Amazon product URLs into **Amazon Product URLs**
4. Click **Start** — reviews appear in the **Output** tab within seconds

### Option 2: Via API (for developers)

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('USERNAME/amazon-reviews-scraper').call({
    productUrls: [
        { url: 'https://www.amazon.com/dp/B0CWXNS552' }
    ],
    maxReviews: 200,
    sort: 'recent',
    filterByRatings: ['oneStar', 'twoStar'],  // scrape only negative reviews
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(`Scraped ${items.length} reviews`);
console.log(items[0]);
// {
//   asin: 'B0CWXNS552',
//   product_title: 'Apple iPhone 15 Pro...',
//   rating: 2,
//   review_title: 'Disappointing battery life',
//   review_body: 'Expected better from Apple...',
//   is_verified_purchase: true,
//   helpful_votes: 18,
//   review_date_iso: '2024-03-12T00:00:00.000Z',
//   ...
// }
```

### Option 3: Input by raw ASIN

You can skip the URL and use the ASIN directly:

```
{
    "asins": ["B0CWXNS552", "B09G9FPHY6"],
    "maxReviews": 100,
    "sort": "helpful"
}
```

### Option 4: Keyword + star filter combination

Scrape only 1-star reviews mentioning "broken":

```
{
    "productUrls": [{ "url": "https://www.amazon.com/dp/B0CWXNS552" }],
    "filterByRatings": ["oneStar"],
    "filterByKeywords": ["broken", "defective"],
    "maxReviews": 500,
    "sort": "recent"
}
```

### Option 5: Date-filtered monitoring

Track reviews from the last 30 days:

```
{
    "productUrls": [{ "url": "https://www.amazon.com/dp/B0CWXNS552" }],
    "reviewsCutoffDate": "2026-03-09",
    "sort": "recent",
    "maxReviews": 1000
}
```

## Input parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `productUrls` | array | `[{url: "https://..."}]` | Amazon product page URLs |
| `asins` | array | `[]` | Raw 10-char ASINs (e.g. B0CWXNS552) |
| `maxReviews` | integer | `100` | Max reviews per product per filter |
| `sort` | string | `helpful` | Sort order: `helpful` or `recent` |
| `filterByRatings` | array | `["allStars"]` | Star rating filter(s) |
| `filterByKeywords` | array | `[]` | Keyword filter(s) |
| `reviewsCutoffDate` | string | `null` | Skip reviews older than this date |
| `scrapeProductDetails` | boolean | `true` | Include product title in output |
| `proxyConfiguration` | object | Residential | Proxy settings (residential required) |

## Pricing

This actor uses **pay-per-event pricing** at **$0.004 per review** (FREE tier).

| Reviews | Cost (FREE tier) | Cost (GOLD tier) |
| --- | --- | --- |
| 100 | $0.40 | $0.30 |
| 500 | $2.00 | $1.50 |
| 1,000 | $4.00 | $3.00 |
| 10,000 | $40.00 | $30.00 |

You are only charged for reviews successfully extracted and written to the dataset. Failed pages and skipped duplicates are free.

## Use cases

**Brand monitoring** — Track what customers say about your products over time. Set up a scheduled run with `reviewsCutoffDate` to get only new reviews weekly.

**Competitive research** — Scrape reviews of competitor products to identify their weaknesses. Filter by 1★ and 2★ to find common complaints.

**Sentiment analysis / NLP** — Feed `review_body` into your AI pipeline. The `is_verified_purchase` field lets you weight genuine buyers more heavily.

**Product improvement** — Filter by keyword (e.g. "battery", "quality", "shipping") to quickly surface the most common issues.

**AI training data** — Collect thousands of rated review texts for fine-tuning or evaluation datasets.

**Price intelligence** — Monitor variant-specific reviews to understand how different configurations are received.

## Technical details

- **Crawler:** CheerioCrawler (fast HTTP-based HTML parsing — no browser overhead)
- **Proxy:** Apify Residential proxies (required for Amazon — datacenter IPs are blocked)
- **Deduplication:** Reviews are deduplicated by review ID across all filter combinations
- **Pagination:** Automatic — follows all Next Page links up to `maxReviews`
- **Rate limiting:** Max 3 concurrent requests with session rotation (5 uses per session)
- **Retries:** Up to 3 retries per page with fresh sessions

## FAQ

**Why do I need residential proxies?** Amazon aggressively blocks datacenter IPs. Residential proxies (included in Apify's proxy offering) route requests through real user connections, making scraping reliably work. Without them you'll get bot-detection pages.

**Why am I getting fewer reviews than `maxReviews`?** Amazon limits how many reviews are visible per filter combination. For example, a product may have 5,000 total reviews but only 100 reviews showing for the "2 star" filter. This is an Amazon limitation, not a scraper bug.

**Can I scrape reviews for products on Amazon.co.uk, .de, etc.?** The actor currently targets Amazon.com. To scrape other marketplaces, change the domain in the product URL (e.g. `amazon.co.uk/dp/...`) — the selectors are the same across most Amazon domains.

**How do I get reviews in a specific language?** Pass the URL with a language parameter or use a proxy location matching the target marketplace.

**Will this break if Amazon updates their site?** The actor uses multiple CSS selector fallbacks per element to survive minor redesigns. If Amazon does a major redesign, open an issue and we'll update within 48 hours.

**Is it legal to scrape Amazon reviews?** Amazon reviews are publicly available data. This actor is built for lawful use cases — market research, academic study, brand monitoring. Users are responsible for compliance with Amazon's Terms of Service, applicable laws, and data protection regulations (GDPR, CCPA, etc.).

## Other actors you might like

- [Amazon Product Scraper](https://apify.com/USERNAME/amazon-product-scraper) — Scrape product titles, prices, ratings, and BSR rankings
- [Google Shopping Scraper](https://apify.com/USERNAME/google-shopping-scraper) — Compare prices across retailers

---

*This actor is intended for lawful data collection from publicly available sources. Users are responsible for compliance with applicable laws, terms of service, and data protection regulations (GDPR, CCPA, etc.). Review data may contain personal information — handle in accordance with your privacy policy.*