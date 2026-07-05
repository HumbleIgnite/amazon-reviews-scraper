[Amazon Reviews Scraper](https://apify.com/saswave/amazon-reviews-scraper?fpr=data)

## 🛒 Amazon Reviews Scraper

Extract Verified & Public Customer Reviews from Amazon Products

The Amazon Reviews Scraper allows you to collect customer reviews directly from Amazon product pages using the ASIN.

It extracts review content, ratings, reviewer profiles, purchase status, and timestamps in a clean, structured JSON format.

Perfect for product research, sentiment analysis, brand monitoring, and competitive intelligence.

## How to extract cookies from your browser

![Screenshot cookies extraction](https://images.apifyusercontent.com/6V1S8wRVI1tOTLRBo-464gj-cL3a8rq5fLxKnMCgxiM/w:1800/cb:1/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL2RldnNhc3dhdmUvYXNzZXRzLXNhc3dhdmUvcmVmcy9oZWFkcy9tYWluL0Fwb2xsb19jb3B5X2Nvb2tpZXMucG5n.webp)

- install EditThisCookie chrome extension
- login to your account and go to your amazon home page
- Use the extension and click "export"
- Paste the cookies in the input "cookies" from the actor

The apify documentation has a tutorial on how to do it with screenshots, [https://docs.apify.com/tutorials/log-in-by-transferring-cookies#export-your-cookies](https://docs.apify.com/tutorials/log-in-by-transferring-cookies#export-your-cookies) go to the export your cookies section

## ⭐ Key Features

🔍 Scrape public Amazon customer reviews by ASIN

⭐ Extract ratings, titles, and full review text

🧾 Identify verified vs non-verified purchases

👤 Collect reviewer name, profile link & avatar

🌍 Supports multiple Amazon marketplaces (FR, US, DE, UK, etc.)

🕒 Capture localized review dates

🔗 Direct review & reviewer profile URLs

📦 Clean JSON output, ready for databases or AI pipelines

⚡ Designed for automation & large-scale scraping

## 📦 Output example

```
{
  "asin": "B0FMYPQQVX",
  "id": "RBWPQE0D6DUOB",
  "link": "https://www.amazon.fr/gp/customer-reviews/RBWPQE0D6DUOB/ref=cm_cr_getr_d_rvw_ttl",
  "title": "Très bonne protection",
  "rating": "5,0",
  "date": "Commenté en France le 22 décembre 2025",
  "content": [
    "Parfait, protège très bien l'écran et s'adapte parfaitement."
  ],
  "verified_purchase": false,
  "reviewer_link": "https://www.amazon.fr/gp/profile/amzn1.account.AF5IJFUJA43RT2JHTZQ6QTSO2H6A/ref=cm_cr_getr_d_gw_btm",
  "reviewer_avatar": "https://images-na.ssl-images-amazon.com/images/G/01/x-locale/common/grey-pixel.gif",
  "reviewer_name": "Isabelle"
}
```

## 📌 Use Cases

🧠 Sentiment analysis & NLP training

📊 Product quality & satisfaction monitoring

🛍️ E-commerce competitor research

⭐ Rating & reputation tracking

📉 Detect negative review spikes

🧪 Market validation before product launch

🤖 AI review summarization & insights

🧾 Build review databases for BI tools

## Notes

Only publicly available reviews are collected

Amazon limits reviews results to 10 page or 100 reviews

Verified purchase flag depends on Amazon availability

Review language & date format follow local marketplace

## 🛟 SUPPORT

Share your runs with the developer team and create issues on error to help us improve actor quality.

You might discover edge case we didn't test yet

We stay available anytime