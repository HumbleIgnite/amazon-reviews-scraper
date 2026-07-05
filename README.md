[Amazon Reviews Scraper](https://apify.com/sovereigntaylor/amazon-reviews-scraper?fpr=data)

# Amazon Product Reviews Scraper

Extract Amazon product reviews at scale. Scrape full review text, star ratings, verified purchase status, helpful vote counts, reviewer profiles, review images, and rating breakdowns for any product by URL or ASIN.

## Features

- Scrape reviews by product URL or ASIN
- Extract full review text, title, rating, date
- Verified purchase identification
- Helpful vote counts
- Review images extraction
- Reviewer name and profile link
- Product-level rating breakdown (5-star to 1-star percentages)
- Overall product rating and total review count
- Filter by star rating (all, positive, critical, or specific stars)
- Sort by most recent or most helpful
- Support for 11 Amazon marketplaces worldwide
- Automatic pagination — scrape hundreds or thousands of reviews
- CAPTCHA and bot detection with retry logic
- Clean, structured JSON output

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| productUrls | array | [] | Amazon product URLs to scrape reviews from |
| asins | array | [] | ASINs to scrape reviews for (uses default marketplace) |
| maxReviews | number | 500 | Max reviews per product (0 = unlimited) |
| sortBy | string | "recent" | Sort: "recent" or "helpful" |
| filterByRating | string | "all" | Filter: all, positive, critical, five_star, four_star, three_star, two_star, one_star |
| verifiedOnly | boolean | false | Only scrape verified purchase reviews |
| marketplace | string | "amazon.com" | Default marketplace for ASIN lookups |
| includeProductInfo | boolean | true | Include product-level rating breakdown |
| includeReviewerProfile | boolean | true | Include reviewer name and profile link |
| proxyConfiguration | object | Apify Residential | Proxy settings (residential strongly recommended) |

## Output — Individual Review

```
{
  "productTitle": "Sony WH-1000XM5 Wireless Noise Canceling Headphones",
  "asin": "B0BX2L8PBS",
  "reviewId": "R3EXAMPLE123",
  "reviewTitle": "Best noise canceling headphones I've ever owned",
  "reviewText": "I've tried Bose, Apple, and Sennheiser — nothing comes close to the XM5. The noise canceling is incredible on flights, and the sound quality is warm and detailed...",
  "rating": 5,
  "author": "AudioEnthusiast",
  "authorProfileUrl": "https://www.amazon.com/gp/profile/amzn1.account.EXAMPLE",
  "date": "2025-12-15",
  "dateRaw": "Reviewed in the United States on December 15, 2025",
  "verified": true,
  "helpful": 42,
  "images": [
    "https://m.media-amazon.com/images/I/review-image-1.jpg"
  ],
  "variant": "Color: Black",
  "marketplace": "amazon.com",
  "overallRating": 4.7,
  "totalReviews": 15234,
  "ratingBreakdown": {
    "5": "72%",
    "4": "14%",
    "3": "6%",
    "2": "4%",
    "1": "4%"
  },
  "scrapedAt": "2026-03-02T12:00:00.000Z"
}
```

## Use Cases

- **Sentiment Analysis**: Analyze customer sentiment at scale across products
- **Product Research**: Understand what customers love and hate before sourcing
- **Competitor Intelligence**: Monitor competitor product feedback trends
- **Brand Monitoring**: Track reviews for your own products over time
- **Quality Control**: Detect emerging quality issues from negative review spikes
- **Market Research**: Identify unmet customer needs and feature gaps
- **Review Aggregation**: Build review databases for analytics platforms
- **Content Analysis**: Extract real customer language for marketing copy

## Pricing

Pay per review scraped — you only pay for what you extract. See the Pricing tab for details.

$0.003 per review scraped.

## Example — Scrape by URLs

```
{
  "productUrls": [
    "https://www.amazon.com/dp/B0BX2L8PBS",
    "https://www.amazon.com/dp/B09V3KXJPB"
  ],
  "maxReviews": 200,
  "sortBy": "recent",
  "filterByRating": "all"
}
```

## Example — Scrape by ASINs (Critical Reviews Only)

```
{
  "asins": ["B0BX2L8PBS", "B09V3KXJPB"],
  "maxReviews": 100,
  "sortBy": "helpful",
  "filterByRating": "critical",
  "marketplace": "amazon.com"
}
```

## Example — Verified 5-Star Reviews Only

```
{
  "productUrls": ["https://www.amazon.com/dp/B0BX2L8PBS"],
  "maxReviews": 500,
  "filterByRating": "five_star",
  "verifiedOnly": true
}
```

## Tips

- **Always use residential proxies** — Amazon aggressively blocks datacenter IPs
- **Start small** — Test with 50-100 reviews before running large jobs
- **Sort by "recent"** for the latest reviews, "helpful" for the most impactful ones
- **Combine with Amazon Product Scraper** — search for products first, then deep-dive into reviews
- Products with 50K+ reviews may take significant time — use maxReviews to limit

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/amazon-reviews-scraper").call(run_input={
    "productUrl": "https://www.amazon.com/dp/B0EXAMPLE",
    "maxResults": 100
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item.get('rating', 0)} stars: {item.get('title', '')}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/amazon-reviews-scraper').call({
    productUrl: 'https://www.amazon.com/dp/B0EXAMPLE',
    maxResults: 100
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(item.title || item.name || 'N/A'));
```

## Related Actors

- [Amazon Product Scraper](https://apify.com/sovereigntaylor/amazon-product-scraper) — Scrape Amazon product listings and prices
- [Amazon BSR Tracker](https://apify.com/sovereigntaylor/amazon-bsr-tracker) — Track Best Seller Rank over time
- [Amazon Keyword Tracker](https://apify.com/sovereigntaylor/amazon-keyword-tracker) — Monitor keyword rankings on Amazon
- [eBay Scraper](https://apify.com/sovereigntaylor/ebay-scraper) — Compare with eBay marketplace data
- [Walmart Scraper](https://apify.com/sovereigntaylor/walmart-scraper) — Cross-marketplace price comparison