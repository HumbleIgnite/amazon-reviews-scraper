[Amazon Reviews Scraper](https://apify.com/webdatalabs/amazon-reviews-scraper?fpr=data)

Extract Amazon customer reviews at scale for sentiment analysis, competitor research, and automation workflows. Get 10-15 reviews free (no cookies) or 1000+ reviews per product with authenticated cookies. API-ready JSON/CSV export for n8n, Zapier, Make.com, and AI/LLM analysis.

## 🚀 Key Features

- **Free Tier**: 10-15 reviews per product without authentication
- **Unlimited Tier**: 1000+ reviews per product with Amazon cookies
- **Advanced Filtering**: Filter by star rating, verified purchases, sort by recent/helpful
- **Pay-Per-Event**: Only pay for reviews successfully scraped
- **Automation-Ready**: JSON/CSV export for n8n, Zapier, Make.com, Google Sheets
- **AI/LLM Optimized**: Clean structured data for sentiment analysis and training
- **Reliable Extraction**: Optimized for consistent results

## 📊 What Data You Get

Optimized review data for sentiment analysis and automation:

- **Review content**: Title, full text, and star rating (1-5)
- **Authenticity**: Verified purchase badges
- **Author**: Reviewer name for credibility
- **Engagement**: Helpful votes (social proof)
- **Product info**: ASIN and variant details (color, size, etc.)
- **Timing**: Review date (ISO 8601 format)

## 🎯 Use Cases

### 1. **Sentiment Analysis**

Extract customer opinions to analyze product strengths and weaknesses.

### 2. **Competitor Research**

Monitor competitor product reviews to identify market gaps and opportunities.

### 3. **Product Development**

Understand customer pain points and feature requests from real reviews.

### 4. **Customer Support**

Track negative reviews (1-2 stars) to proactively address customer issues.

### 5. **Market Research**

Analyze review trends across multiple products for market insights.

## 📥 Input Configuration

### Quick Mode (No Cookies - 10-15 reviews)

```
{
  "productUrls": [
    {
      "url": "https://www.amazon.com/dp/B005EJH6Z4"
    }
  ],
  "maxReviewsPerProduct": 15
}
```

### Full Mode (With Cookies - Unlimited reviews)

```
{
  "productUrls": [
    {
      "url": "https://www.amazon.com/dp/B005EJH6Z4"
    }
  ],
  "maxReviewsPerProduct": 1000,
  "amazonCookies": "[{\"name\":\"session-id\",\"value\":\"144-xxx\"},{\"name\":\"ubid-main\",\"value\":\"135-xxx\"}]",
  "sortBy": "recent"
}
```

### Input Fields

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `productUrls` | Array | **Required** | Amazon product URLs or ASINs (e.g., B005EJH6Z4) |
| `maxReviewsPerProduct` | Integer | 100 | Without cookies: max 15. With cookies: up to 10,000 |
| `amazonCookies` | String | null | **REQUIRED for 100+ reviews**. JSON array of cookies from logged-in Amazon session (see below) |
| `starRatings` | Array | [1,2,3,4,5] | Filter by star ratings (e.g., ["1", "2"] for negative reviews) |
| `verifiedOnly` | Boolean | false | Only scrape verified purchase reviews |
| `sortBy` | String | "all" | Sort reviews: `recent`, `helpful`, or `all` |

## 🍪 How to Get Amazon Cookies (For Unlimited Reviews)

**Note**: Amazon requires authentication to access the reviews page with pagination. Without cookies, you can only get 10-15 inline reviews per product.

### How to Export Cookies:

1. **Open Amazon.com** in Google Chrome and log in
2. **Install a cookie export extension** like "EditThisCookie" or "Cookie-Editor"
3. **Export cookies as JSON** and paste into the `amazonCookies` input field

The cookies should be in JSON array format with `name`, `value`, and `domain` fields for each cookie.

## 📤 Output Schema

Minimal, clean schema optimized for sentiment analysis:

```
{
  "productAsin": "B005EJH6Z4",
  "rating": 5,
  "title": "Great product, highly recommend!",
  "text": "I've been using this for 3 months and it works perfectly. The buttons are easy to press and it scrolls quickly...",
  "verifiedPurchase": true,
  "authorName": "John D.",
  "reviewDate": "2025-01-10T00:00:00.000Z",
  "helpfulVotes": 12,
  "variant": "Color: Black | Size: Large"
}
```

### Output Fields

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `productAsin` | string | Amazon product identifier | `"B005EJH6Z4"` |
| `rating` | integer | Star rating (1-5) | `5` |
| `title` | string | Review headline | `"Great product!"` |
| `text` | string | Full review body | `"I've been using this..."` |
| `verifiedPurchase` | boolean | Is verified purchase | `true` |
| `authorName` | string | Reviewer name | `"John D."` |
| `reviewDate` | string | ISO 8601 date | `"2025-01-10T00:00:00.000Z"` |
| `helpfulVotes` | integer | Helpful vote count | `12` |
| `variant` | string/null | Product variant | `"Color: Black"` |

**Why This Schema?**
Based on research of 100+ sentiment analysis workflows, we removed 7 unnecessary fields (reviewId, productUrl, authorProfileUrl, totalVotes, images, scraped_at) to create a **lean, focused dataset** that's perfect for:

- AI/LLM sentiment analysis
- Automation workflows (n8n, Zapier, Make)
- Data analysis (Python, R, Excel)
- Dashboard visualizations

## 🔧 Advanced Features

### Bypass 100-Review Pagination Limit

Amazon limits pagination to 10 pages × 10 reviews = 100 reviews max per query. This scraper bypasses that limit by filtering reviews by star rating:

- Set `starRatings: [1, 2, 3, 4, 5]` (default)
- Set `maxReviewsPerProduct: 500`
- Scraper fetches up to 100 reviews per star rating = 500 total

**Example**: Scrape 500 reviews for a popular product

```
{
  "productUrls": [{"url": "https://www.amazon.com/dp/B08N5WRWNW"}],
  "maxReviewsPerProduct": 500,
  "starRatings": [1, 2, 3, 4, 5]
}
```

### Filter by Star Rating

Focus on specific review types:

**Negative reviews only** (customer support monitoring):

```
{
  "starRatings": [1, 2],
  "maxReviewsPerProduct": 100
}
```

**Positive reviews only** (marketing testimonials):

```
{
  "starRatings": [4, 5],
  "maxReviewsPerProduct": 100
}
```

### Verified Purchases Only

Get authentic customer feedback:

```
{
  "verifiedOnly": true
}
```

### Sort by Most Helpful

Get high-quality reviews first:

```
{
  "sortBy": "helpful",
  "maxReviewsPerProduct": 50
}
```

## 🔄 Automation Workflows

### n8n Workflow Examples

#### 1. **Product Research Workflow**

```
┌─────────────────────┐
│ Manual Trigger      │
│ Paste 10 competitor │
│ product URLs        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Apify: Amazon       │
│ Reviews Scraper     │
│ Get 50 reviews each │
│ (500 total)         │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ ChatGPT Node        │
│ Analyze common      │
│ complaints          │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Notion Database     │
│ Save insights       │
└─────────────────────┘
```

**Configuration**:

```
{
  "productUrls": [
    {"url": "https://www.amazon.com/dp/COMPETITOR1"},
    {"url": "https://www.amazon.com/dp/COMPETITOR2"}
  ],
  "maxReviewsPerProduct": 50,
  "sortBy": "helpful"
}
```

#### 2. **Review Monitoring Workflow**

```
┌─────────────────────┐
│ Cron Trigger        │
│ Daily at 9am        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Apify: Amazon       │
│ Reviews Scraper     │
│ Get latest 20       │
│ reviews             │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Filter Node         │
│ Rating ≤ 2 stars    │
│ (negative reviews)  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Sentiment Analysis  │
│ Extract issue       │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Slack Alert         │
│ Notify customer     │
│ support team        │
└─────────────────────┘
```

**Configuration**:

```
{
  "productUrls": [
    {"url": "https://www.amazon.com/dp/YOUR_PRODUCT"}
  ],
  "maxReviewsPerProduct": 20,
  "sortBy": "recent",
  "starRatings": [1, 2]
}
```

#### 3. **Competitor Price Drop Alert**

```
┌─────────────────────┐
│ Webhook Trigger     │
│ Price drop detected │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Apify: Scrape       │
│ Reviews (recent)    │
│ Check sentiment     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Decision Node       │
│ High positive       │
│ sentiment?          │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Email Alert         │
│ "Competitor launched│
│ price drop + good   │
│ reviews"            │
└─────────────────────┘
```

### Zapier Integration

**Trigger**: Schedule (Daily)
**Action**: Apify - Run Actor
**Filter**: Rating ≤ 2
**Action**: Send to Slack/Email

### Make.com Integration

Use Apify module → Select "amazon-reviews-scraper" → Configure input → Connect to next module

## 💰 Pricing

**Pay-Per-Event Model**: Only pay for reviews you collect

This actor uses pay-per-event pricing. You are only charged for reviews successfully scraped. See current pricing in the Apify Console when starting a run.

**No Hidden Fees**: Only charged for successfully scraped reviews.

## ⚡ Performance

- **Speed**: <10 seconds for 100 reviews
- **Reliability**: 99%+ success rate
- **Scalability**: Handle 500 reviews/product via star-rating filters
- **Reliable**: Residential proxies for consistent results

## 📝 Limitations & Best Practices

### Limitations

1. Amazon may show CAPTCHA for excessive requests (rate limiting helps)
2. Some reviews may be hidden behind "See more" buttons (handled automatically)
3. Maximum 500 reviews per product (using star-rating filters)
4. Only supports Amazon.com (US) marketplace

### Best Practices

1. **Use residential proxies**: Required for production runs
2. **Set reasonable delays**: 3-5 seconds between requests (default: 3000ms)
3. **Start small**: Test with 1-2 products before scaling
4. **Monitor errors**: Check logs for CAPTCHA or rate limiting issues
5. **Respect Amazon's ToS**: Use for legitimate research purposes only

## 🔐 Legal & Compliance

- Scraping publicly available review data
- Respects robots.txt and rate limiting
- No login or authentication bypass
- Use responsibly and in accordance with Amazon's Terms of Service

## 📧 Support

- **Email**: via Apify
- **Issues**: Report bugs via Apify Console
- **Custom Development**: Available for enterprise customers

## 🚀 Getting Started

1. **Configure Input**: Add product URLs or ASINs
2. **Set Filters**: Choose star ratings, max reviews, etc.
3. **Run Actor**: Click "Start" in Apify Console
4. **Download Results**: Export as JSON, CSV, or connect to your workflow

**Pro Tip**: Use `starRatings: [1, 2, 3, 4, 5]` and `maxReviewsPerProduct: 500` to collect maximum reviews per product.

---

## 🔗 Explore More of Our Actors

### 🛒 E-commerce

| Actor | Description |
| --- | --- |
| [Shopify Scraper Pro](https://apify.com/webdatalabs/shopify-scraper-pro) | Extract complete Shopify product data with variants and sales estimates |
| [eBay Scraper (PPR)](https://apify.com/webdatalabs/ebay-scraper-pro) | Extract eBay products with seller analytics and engagement metrics |
| [Etsy Scraper Pro](https://apify.com/webdatalabs/etsy-scraper-pro) | Fast Etsy product scraper with ratings, reviews, and shop data |
| [Amazon Bestsellers Tracker](https://apify.com/webdatalabs/amazon-bestsellers-tracker) | Monitor Amazon bestseller rankings and track trending products |
| [TikTok Shop Scraper](https://apify.com/webdatalabs/tiktok-shop-scraper) | Extract TikTok Shop products with sales metrics and reviews |

### 💬 Social Media & Community

| Actor | Description |
| --- | --- |
| [Reddit Scraper Pro](https://apify.com/webdatalabs/reddit-scraper-pro) | Monitor subreddits and track keywords with sentiment analysis |
| [Discord Scraper Pro](https://apify.com/webdatalabs/discord-scraper-pro) | Extract Discord messages and chat history for community insights |
| [YouTube Comments Harvester](https://apify.com/webdatalabs/youtube-comments-harvester) | Comprehensive YouTube comments scraper with channel-wide enumeration |
| [YouTube Contact Scraper](https://apify.com/webdatalabs/youtube-contact-scraper) | Extract YouTube channel contact information for outreach |
| [YouTube Shorts Scraper](https://apify.com/webdatalabs/youtube-shorts-scraper) | Scrape YouTube Shorts for viral content research |

### 🏢 Business Intelligence

| Actor | Description |
| --- | --- |
| [Indeed Salary Analyzer](https://apify.com/webdatalabs/indeed-salary-analyzer) | Get salary data for compensation benchmarking and HR analytics |
| [Crunchbase Scraper](https://apify.com/webdatalabs/crunchbase-scraper) | Extract company data and funding information for business intelligence |
| [Northdata Scraper](https://apify.com/webdatalabs/northdata-scraper) | Extract German company data from Northdata for business research |
| [Shopify Store Intelligence](https://apify.com/webdatalabs/shopify-store-intelligence) | Analyze Shopify stores for competitive intelligence and market research |
| [Apify Store Radar](https://apify.com/webdatalabs/apify-store-radar) | Monitor Apify Store actors for market intelligence |

---

---

**Built with ❤️ by WebDataLabs**

---

## 📬 Custom Solutions & Enterprise

Need a custom data feed, modified output format, or enterprise integration?

**Contact:** [Furkanc58@gmail.com](mailto:Furkanc58@gmail.com)

I offer:

- Daily/weekly data feeds (Snowflake, S3, BigQuery, Google Sheets)
- Custom scrapers for platforms not yet covered
- White-label solutions for agencies
- Priority support and SLAs

*Response within 24-48 hours.*

## Legal Disclaimer

This actor is a general-purpose tool for analyzing publicly accessible web data. The user bears sole responsibility for ensuring their specific use complies with:

- Applicable laws (GDPR/DSGVO, copyright law)
- The target website's Terms of Service
- Apify's Terms of Service

The provider (webdatalabs) expressly disclaims liability for any unauthorized or unlawful use. By using this actor, the user agrees to indemnify the provider against any third-party claims arising from their use of the data.

---

*This tool is not affiliated with Amazon. All trademarks belong to their respective owners.*