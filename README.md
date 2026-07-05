[Amazon Reviews Scraper](https://apify.com/neatrat/amazon-reviews-scraper?fpr=data)

Effortlessly collect thousands of reviews for any Amazon product (ASIN) with powerful, customizable filters! This Apify actor is designed for professionals, researchers, and brands who need high-quality, targeted review data for market analysis, sentiment research, and product feedback. **No login required!**

---

## 🏆 Key Features

- **No Login Required**: No need to log in to Amazon.
- **No Proxy Required**: We handle proxies for you.
- **No CAPTCHA Solving Required**: All CAPTCHAs are solved for you.
- **Massive Review Collection**: Capture 10,000+ reviews per ASIN by leveraging robust pagination and filtering.
- **Flexible Filtering**:

- **Sort by**: Most recent, most helpful, or top-rated reviews.
- **Verified Purchase**: Focus on reviews from verified buyers only.
- **Star Ratings**: Select specific ratings (e.g., only 5-star or 1-star reviews).
- **Media Type**: Filter for reviews with images or videos.
- **Keyword Search**: Extract reviews containing specific keywords (case-insensitive).
- **Unique Only**: Remove duplicates for a clean dataset.
- **ASIN Array Support**:

- Pass multiple ASINs as a comma-separated list (e.g., `B00NGV4506,B08N5WRWNW,B07XJ8C8F5`).
- Region-specific ASINs supported using the format `region:ASIN` (e.g., `de:B00NGV4506,com:B08N5WRWNW`).
- **Comprehensive Review Data**: Get detailed fields including:

- Review URL, Product URL, ASIN, Brand, Product Title
- Review Date, Images, Review Score, Reviewer Name & Profile
- Review Title & Content, Verified status, Variant details, Helpful counts
- **Efficient & Scalable**: Built on Apify's infrastructure for fast, reliable, and large-scale data extraction.
- **Multiple Output Formats**: Download your results as JSON, CSV, or integrate directly into your data pipelines.

---

## 💡 How It Works

1. **Input ASIN**: Enter the Amazon product ASIN you want to analyze.
2. **Configure Filters**: Set your desired filters (ratings, verified, keywords, etc.).
3. **Run the Actor**: Start the scraper and let it collect reviews.
4. **Download Results**: Export your data in your preferred format.

---

## ❓ FAQ

- **Why am I stuck at 100 reviews?**
Amazon now limits general searches to 10 pages, with 10 reviews each. To fetch more reviews, consider adding general keywords to your search to bypass this limitation.

### Here's What's Happening on Page 10

![Amazon Review Limit](https://images.apifyusercontent.com/wwOBjItyoM8o-dR1OUUkeghMIdT38D7Oxk2n0Ipqsmw/w:1800/cb:1/aHR0cHM6Ly9pLmltZ3VyLmNvbS9OeTNUcjFYLnBuZw.webp)
- **So how to scrape more than 100 reviews?**
Run the scraper multiple times with different keywords each time, setting `pagesToScrape` to 10. For example, use general keywords like "great", "value", "quality", "recommend", "satisfied". Gather 100 such words and run 100 times to get 1000 reviews. A feature to automate this process is coming soon!

---

## 🧩 Input Configuration

Customize your scraping with these parameters:

- **asin** (required): The Amazon Standard Identification Number of the product. You can pass:

- A single ASIN (e.g., `B00NGV4506`)
- Multiple ASINs separated by commas (e.g., `B00NGV4506,B08N5WRWNW,B07XJ8C8F5`)
- Multiple Region-specific ASINs using the format `region:ASIN` (e.g., `de:B00NGV4506,com:B08N5WRWNW`)
- **startPage**: Which review page to start from (default: 1).
- **pagesToScrape**: How many pages to scrape (default: 10, up to 10,000+ reviews possible).
- **keywords**: Use this as a search query to include reviews containing these keywords. This can help you get more than 100 general results by expanding the search scope.
- **sortBy**: Sort reviews by 'top' (helpful) or 'recent'.
- **verifiedPurchase**: 'all' or 'verified' only.
- **ratings**: Select star ratings to include (e.g., [5], [1,2,3,4,5]).
- **mediaType**: 'all' or 'with_media_only'.
- **maxReviews**: Maximum number of reviews to return (default: 100).
- **endDate**: Only include reviews up to this date (YYYY-MM-DD).
- **recentDays**: Only include reviews from the last N days.
- **uniqueOnly**: Only include unique reviews (by reviewId).

---

## 📦 Example Output

```
{
  "reviewId": "R1CV8NB96UZ4BP",
  "reviewUrl": "https://www.amazon.com/gp/customer-reviews/R1CV8NB96UZ4BP",
  "rating": 5.0,
  "reviewer": "Andres Polanco",
  "title": "Good phone",
  "date": "2025-03-28",
  "reviewedIn": "United States",
  "body": "The iPhone 11 is excellent. The camera takes high-quality photos, even in low light...",
  "verifiedPurchase": true,
  "userImage": "https://m.media-amazon.com/images/I/51HbwvWaFIL.jpg",
  "reviewImages": [
    "https://m.media-amazon.com/images/I/51HbwvWaFIL.jpg",
    "https://m.media-amazon.com/images/I/51kU1WbmjOL.jpg"
  ],
  "position": 1,
  "variantDetails": ["Size: 128GB", "Color: Black"],
  "variantASIN": "B07ZPKN6YR",
  "helpfulCounts": 1,
  "videoUrl": "https://www.amazon.com/video/review/R1CV8NB96UZ4BP"
}
```

---

## 🏁 Getting Started

1. **Create an Apify Account**: [Sign up here](https://apify.com/sign-up).
2. **Deploy the Actor**: Add this actor to your Apify account.
3. **Input ASIN & Filters**: Enter the ASIN and set your filters.
4. **Run the Actor**: Start scraping reviews.
5. **Download Results**: Export your data in JSON, CSV, or Excel.

---

## 🤝 Support & Feedback

Need help or have suggestions? Reach out via Apify support or leave feedback on the actor's page.

---

## 🏷️ Tags

AmazonScraper, ReviewScraper, MarketResearch, SentimentAnalysis, ProductFeedback, AmazonReviews, DataCollection, Ecommerce, Apify