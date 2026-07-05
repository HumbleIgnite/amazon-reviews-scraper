[Amazon Reviews Scraper](https://apify.com/junipr/amazon-reviews-scraper?fpr=data)

# Amazon Reviews Scraper

Extract Amazon product reviews at scale with full review data including ratings, review text, verified purchase status, helpful votes, reviewer info, and review images. Ideal for sentiment analysis, competitive research, brand monitoring, and market intelligence. Supports 12 Amazon marketplaces worldwide.

## What can it do?

Amazon Reviews Scraper lets you extract structured review data from any Amazon product listing. Key capabilities:

- **Complete review data** — Reviewer name, star rating, title, full review text, date, verified purchase status, helpful votes, and review images
- **Advanced filtering** — Filter by star rating (1-5, positive, critical), date range, verified purchases only, or keyword search within reviews
- **Batch ASIN input** — Scrape reviews for hundreds of products in a single run by providing a list of ASINs or product URLs
- **Review image extraction** — Download URLs for all customer-uploaded images attached to reviews
- **Multi-marketplace support** — amazon.com, .co.uk, .de, .fr, .it, .es, .ca, .com.au, .co.jp, .in, .com.br, .com.mx
- **Sorted output** — Sort by most recent, most helpful, or top reviews
- **Robust anti-bot handling** — Automatic session rotation, CAPTCHA detection, and residential proxy support
- **Product context** — Each review row includes product name, price, overall rating, and total review count

## What data can you extract from Amazon reviews?

| Field | Description |
| --- | --- |
| `asin` | Amazon Standard Identification Number |
| `productName` | Product title |
| `productUrl` | Direct link to the product page |
| `productPrice` | Current listed price |
| `productOverallRating` | Average star rating across all reviews |
| `productTotalReviews` | Total number of ratings for the product |
| `reviewId` | Unique Amazon review identifier |
| `reviewUrl` | Direct link to the individual review |
| `reviewerName` | Display name of the reviewer |
| `reviewerProfileUrl` | Link to the reviewer's Amazon profile |
| `rating` | Star rating given by the reviewer (1-5) |
| `title` | Review headline |
| `body` | Full review text |
| `date` | Review date (YYYY-MM-DD) |
| `dateIso` | Review date in ISO 8601 format |
| `isVerifiedPurchase` | Whether the review is from a verified purchase |
| `helpfulVotes` | Number of people who found the review helpful |
| `images` | URLs of images uploaded by the reviewer |
| `variant` | Product variant details (color, size, etc.) |
| `countryReviewed` | Country the review was posted from |
| `marketplace` | Amazon marketplace code (US, UK, DE, etc.) |

## How to use

1. **Scrape reviews by ASIN** — Provide one or more product ASINs:

```
{
  "asins": ["B0D5CRCWXC", "B09V3KXJPB"],
  "maxReviews": 200,
  "sortBy": "recent"
}
```

1. **Filter negative reviews** — Get only critical reviews for competitive analysis:

```
{
  "asins": ["B0D5CRCWXC"],
  "filterRating": "critical",
  "filterVerified": true,
  "maxReviews": 500
}
```

1. **Search within reviews** — Find reviews mentioning specific topics:

```
{
  "asins": ["B0D5CRCWXC"],
  "searchKeyword": "battery life",
  "maxReviews": 100
}
```

1. **International marketplace** — Scrape reviews from Amazon UK:

```
{
  "asins": ["B0D5CRCWXC"],
  "marketplace": "UK",
  "maxReviews": 50
}
```

## Pricing

This actor uses pay-per-event pricing at **$3.90 per 1,000 reviews** ($0.0039 per review). You only pay for successfully extracted reviews — blocked requests, empty products, failed pages, and duplicate reviews are never charged.

Pricing includes all platform compute costs — no hidden fees.

**Cost examples:**

- 100 reviews for one product: $0.25
- 1,000 reviews across 10 products: $2.50
- 5,000 reviews for market research: $12.50

This is 10x cheaper than enterprise alternatives like Bright Data or Oxylabs, which start at $500+/month for Amazon data.

## Proxy Requirements

This actor requires residential proxies because Amazon aggressively blocks datacenter IP addresses on review pages.

- **Paid Apify plan users**: Works automatically with the default residential proxy configuration.
- **Free plan users**: Provide your own residential proxy URL in the Proxy Configuration input field.
- Without a residential proxy, the actor will exit with a clear error message.

## Input and Output examples

**Input:**

```
{
  "asins": ["B0D5CRCWXC"],
  "maxReviews": 50,
  "filterRating": "all",
  "sortBy": "recent",
  "includeImages": true,
  "includeProductInfo": true
}
```

**Output (single review):**

```
{
  "asin": "B0D5CRCWXC",
  "productName": "Apple AirPods Pro (2nd Generation)",
  "productUrl": "https://www.amazon.com/dp/B0D5CRCWXC",
  "productPrice": "$249.00",
  "productOverallRating": 4.7,
  "productTotalReviews": 85432,
  "reviewId": "R3ABC123DEF456",
  "reviewUrl": "https://www.amazon.com/gp/customer-reviews/R3ABC123DEF456",
  "reviewerName": "John D.",
  "reviewerProfileUrl": "https://www.amazon.com/gp/profile/amzn1.account.ABC123",
  "rating": 5,
  "title": "Best noise cancelling earbuds I've owned",
  "body": "I've been using these for two months now and the noise cancellation is incredible...",
  "date": "2026-02-15",
  "dateIso": "2026-02-15T00:00:00.000Z",
  "isVerifiedPurchase": true,
  "helpfulVotes": 42,
  "images": [
    "https://images-na.ssl-images-amazon.com/images/I/abc123.jpg"
  ],
  "variant": "Color: White, Size: One Size",
  "countryReviewed": "Reviewed in the United States",
  "marketplace": "US",
  "scrapedAt": "2026-03-11T12:00:00.000Z"
}
```

## Related scrapers by Junipr

- [Yelp Business Scraper](https://apify.com/junipr/yelp-scraper) — Extract business data, reviews, hours, menus, and photos from Yelp
- [Google News Scraper](https://apify.com/junipr/google-news-scraper) — Scrape Google News articles by topic or keyword
- [Contact Info Scraper](https://apify.com/junipr/contact-info-scraper) — Extract emails, phones, and social links from any website
- [Trustpilot Reviews Scraper](https://apify.com/junipr/trustpilot-reviews-scraper) — Scrape Trustpilot business reviews

## FAQ

### How much does it cost to scrape Amazon reviews?

The actor charges $3.90 per 1,000 reviews extracted. You only pay for successful extractions — blocked requests, empty products, and duplicate reviews are free. A typical run of 100 reviews for one product costs about $0.39.

### Can I scrape reviews from international Amazon sites?

Yes. The actor supports 12 Amazon marketplaces: US, UK, Germany, France, Italy, Spain, Canada, Australia, Japan, India, Brazil, and Mexico. Set the `marketplace` input parameter to the desired country code (e.g., "UK", "DE", "JP").

### How do I filter only negative reviews?

Set `filterRating` to `"critical"` to get only 1-3 star reviews, or use a specific star number like `"1"` or `"2"`. Combine with `filterVerified: true` to focus on verified purchase complaints for competitive intelligence.

### Does it extract review images?

Yes. When `includeImages` is set to `true` (the default), the actor extracts URLs for all customer-uploaded photos attached to reviews. Image URLs point to high-resolution versions on Amazon's CDN.

### Can I scrape reviews for multiple products at once?

Yes. Provide multiple ASINs in the `asins` array or multiple product URLs in the `productUrls` array. The actor processes them sequentially with delays between products to avoid detection. You can scrape up to 500 products in a single run.

### Is the data structured for sentiment analysis?

Yes. Each review is output as a structured JSON object with separate fields for rating, title, body text, date, and verified purchase status. This format is ready for direct import into NLP pipelines, pandas DataFrames, or sentiment analysis tools without additional parsing.

### Why do I need a residential proxy?

Amazon uses aggressive anti-bot protection on review pages including IP reputation scoring, browser fingerprint validation, and CAPTCHA challenges. Datacenter IPs are blocked immediately. Residential proxies route traffic through real ISP addresses, which Amazon treats as legitimate browser traffic. Paid Apify plans include residential proxy access automatically.