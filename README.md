[Amazon Reviews Scraper](https://apify.com/rastriq/amazon-reviews-scraper?fpr=data)

# Amazon Products & Reviews Scraper

Collect customer reviews and product data from Amazon across all major marketplaces — ES, US, DE, FR, UK, IT, BR, MX, CA, AU, JP, and more.

## What you can do with it

- Monitor how customer sentiment evolves for your products or your competitors' over time
- Analyse reviews before entering a new market or launching a new product category
- Track rating drops that signal supply issues, quality problems, or negative PR
- Build datasets for sentiment analysis, voice-of-customer research, or AI training
- Compare product availability and pricing across multiple European or global marketplaces
- Identify weak spots in competing products by mining low-rated reviews at scale

## Filters

| Filter | What it does |
| --- | --- |
| Products (ASINs or URLs) | The list of Amazon products you want to collect data for |
| Mode | Choose what to collect: reviews only, product data only, or both together |
| Marketplace | Select the Amazon country store to query (e.g. amazon.es, amazon.de) |
| Max Reviews per Product | Cap how many reviews to collect per product |
| Cookies | Your Amazon session cookies — required once to unlock review access (see setup below) |

## What you get

**Review records include:**

| Field | What it contains |
| --- | --- |
| review_id | Unique identifier for the review |
| author | Reviewer display name |
| country | Country where the review was posted |
| rating | Star rating (1 to 5) |
| date | Date the review was published |
| title | Review headline |
| body | Full review text |
| verified_purchase | Whether Amazon confirmed the reviewer bought the product |
| helpful_votes | Number of people who marked the review as helpful |
| variant | Product variant the reviewer purchased (colour, size, etc.) |

**Product records include:**

| Field | What it contains |
| --- | --- |
| title | Product name |
| brand | Brand name |
| price | Current price including currency |
| rating | Average star rating |
| review_count | Total number of ratings on the product |
| availability | Stock status |
| category | Product category breadcrumb |
| bullets | Key feature bullet points from the product page |
| description | Full product description |
| specs | Detailed technical attributes (e.g. dimensions, materials) |
| main_image | Link to the main product photo |
| variants | Available colour or size options |
| url | Direct link to the product on Amazon |

## Cookie setup (one-time, 2 minutes)

Amazon requires an active login session to access reviews. You only need to do this once — after the first successful run, your session is saved automatically for all future runs.

1. Log into your Amazon account in Chrome on the marketplace you want to use (e.g. amazon.es)
2. Install the free Cookie-Editor browser extension
3. While on the Amazon page, open Cookie-Editor and click Export
4. Copy the exported cookies and paste them into the Cookies field in the actor input
5. Run the actor — your session is now saved and you will not need to repeat this

If reviews stop loading after a few weeks, your session has expired. Simply export fresh cookies and paste them in again.

## Pricing

**$5.00 per 1,000 results. First 500 results free.**

## Legal

This actor collects publicly available information from Amazon's website. Use responsibly and in accordance with Amazon's Terms of Service and applicable data protection laws.