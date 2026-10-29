# Sndz Data: web scrapers and data tools

16 ready-to-use data tools that run in the cloud on [Apify](https://apify.com/sndzcc): no servers, no proxies, no code needed.
Open any of them, press **Try for free**, and download the results as Excel, CSV or JSON, or call them from your code with the examples in this repo.

| Tool | What you get | Price |
|---|---|---|
| [BORME Scraper API](https://apify.com/sndzcc/borme-spain-companies) | Every new company registered in Spain, daily | $0.003 per company record |
| [App Store & Google Play Reviews Scraper API](https://apify.com/sndzcc/app-reviews-scraper) | App Store and Google Play reviews in one run | $0.00025 per review |
| [Job Scraper API](https://apify.com/sndzcc/ats-jobs-scraper) | All open jobs from Greenhouse, Lever, Ashby and more | $0.001 per job |
| [Google News Scraper API](https://apify.com/sndzcc/google-news-scraper) | News by keyword or topic, with real article URLs | $0.0015 per article |
| [Email & Contact Scraper API](https://apify.com/sndzcc/contact-details-scraper) | Emails, phones and social profiles from any website | $0.0015 per website with contacts |
| [Telegram Scraper API](https://apify.com/sndzcc/telegram-channel-scraper) | Posts, views and media from public Telegram channels | $0.0007 per post |
| [Brand Monitoring API](https://apify.com/sndzcc/brand-mentions-radar) | Brand mentions across 9 sources, with sentiment | $0.003 per mention |
| [AI Image Upscaler API](https://apify.com/sndzcc/ai-image-upscaler) | Upscale and enhance photos 4x with AI | $0.01 per upscaled image |
| [Keyword Research API](https://apify.com/sndzcc/keyword-ideas-machine) | Hundreds of keyword ideas from 5 search engines | $0.001 per keyword idea |
| [Tech Stack Detector API](https://apify.com/sndzcc/tech-stack-detector) | The technologies behind any website, in bulk | $0.0015 per website analyzed |
| [Polymarket & Kalshi API](https://apify.com/sndzcc/prediction-markets-scraper) | Live odds from Polymarket and Kalshi in one dataset | $0.002 per market |
| [WHOIS & Domain Lookup API](https://apify.com/sndzcc/domain-intel) | WHOIS, availability, DNS and SSL for any list of domains | $0.0015 per domain |
| [Bluesky Scraper API](https://apify.com/sndzcc/bluesky-scraper) | Posts, profiles and followers from Bluesky, no login | $0.001 per result |
| [SEO Audit API](https://apify.com/sndzcc/seo-audit) | SEO audit and broken link checker for any website | $0.002 per page audited |
| [OCR API](https://apify.com/sndzcc/image-pdf-to-text) | Text from images and scanned PDFs, 100+ languages | $0.004 per page |
| [Speech to Text API](https://apify.com/sndzcc/speech-to-text) | Audio, video and podcasts to text and subtitles with Whisper AI | $0.005 per audio minute |

## How to use them

1. Open a tool's page and press **Try for free** (Apify's free plan includes monthly credit).
2. Fill in the input, or keep the example, and press **Start**.
3. Download the results, schedule the tool, or connect it to Google Sheets, Make, Zapier, n8n or your API.

From code: get your token in Apify Console (Settings > API & Integrations) and use the Python snippet under each tool (JavaScript works the same way with the `apify-client` npm package).

## Tools

### BORME Scraper API - Spain New Company Leads Daily

Scrape BORME, Spain's official company registry gazette: every new company registered in Spain each day with name, address, activity, capital and directors. Fresh Spanish B2B leads.

- Run it in the browser: **[https://apify.com/sndzcc/borme-spain-companies](https://apify.com/sndzcc/borme-spain-companies)** (free Apify plan available, no credit card)
- Price: **$0.003 per company record**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/borme-spain-companies").call(run_input={"lastEditions": 1, "actTypes": ["Constitución"], "provinces": ["MADRID"], "maxItems": 20})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **What is BORME?** The Boletín Oficial del Registro Mercantil, Spain's official gazette where every new company, director change, capital change and dissolution is published, Monday to Friday.
- **Can I get only new companies in my province or sector?** Yes. Filter by act type (Constitución = new company), province and keywords in the company name or business purpose.
- **Can I get it every day automatically?** Yes. Create an Apify Schedule with "Last N editions" = 1 and send the results to Google Sheets, Slack or your CRM.

### App Store & Google Play Reviews Scraper API

Scrape app reviews from the Apple App Store and Google Play in one run, for any app and country: rating, review text, version, date and developer replies. Export to CSV, Excel or JSON.

- Run it in the browser: **[https://apify.com/sndzcc/app-reviews-scraper](https://apify.com/sndzcc/app-reviews-scraper)** (free Apify plan available, no credit card)
- Price: **$0.00025 per review**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/app-reviews-scraper").call(run_input={"apps": ["https://play.google.com/store/apps/details?id=com.spotify.music", "https://apps.apple.com/us/app/spotify-music-and-podcasts/id324684580"], "countries": ["us"], "maxReviewsPerApp": 50})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Can I scrape iPhone and Android reviews together?** Yes. Paste App Store and Google Play links in the same run: both come out in the same format.
- **How many App Store reviews can I get?** Apple's public feed gives the latest 500 reviews per country. Add more countries to get more. Google Play has no fixed limit.
- **Can I get only negative reviews?** Yes. Select star ratings 1 and 2, and you only pay for those.

### Job Scraper API - Greenhouse, Lever, Ashby & Workable

Scrape every open job of any company from Greenhouse, Lever, Ashby, Workable, SmartRecruiters and Recruitee job boards. Just type company names: title, location, salary, remote, description and URL.

- Run it in the browser: **[https://apify.com/sndzcc/ats-jobs-scraper](https://apify.com/sndzcc/ats-jobs-scraper)** (free Apify plan available, no credit card)
- Price: **$0.001 per job**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/ats-jobs-scraper").call(run_input={"companies": ["stripe", "https://jobs.lever.co/palantir", "https://jobs.ashbyhq.com/ramp"], "maxJobsPerCompany": 20})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Which job boards are supported?** Greenhouse, Lever, Ashby, Workable, SmartRecruiters and Recruitee, the ATS used by most tech companies and startups.
- **Do I need to know which ATS a company uses?** No. Type the company name (for example stripe) and every supported ATS is checked.
- **Does it include salaries?** Yes, when the company publishes them (common on Ashby, Lever and Recruitee).

### Google News Scraper API - Articles with Real URLs

Scrape Google News by keyword, topic or site, in any country and language: headline, source, date and the real article URL, not the news.google.com redirect. For news monitoring and AI.

- Run it in the browser: **[https://apify.com/sndzcc/google-news-scraper](https://apify.com/sndzcc/google-news-scraper)** (free Apify plan available, no credit card)
- Price: **$0.0015 per article**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/google-news-scraper").call(run_input={"queries": ["artificial intelligence"], "timeRange": "1d", "maxArticlesPerFeed": 30})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Do I get the real article link?** Yes. Google News redirect links are converted into the publisher's own URL.
- **Can I use search operators?** Yes: "exact phrase", site:reuters.com, -exclude and OR work like on Google News.
- **How many articles per search?** Google News returns up to 100 per search or topic. Split broad searches by site or time range to get more.

### Email & Contact Scraper API - Emails, Phones & Socials

Email scraper and contact finder: extract emails, phone numbers, WhatsApp, LinkedIn, Instagram and other social links from any list of company websites, in bulk. Pay only for sites with contacts.

- Run it in the browser: **[https://apify.com/sndzcc/contact-details-scraper](https://apify.com/sndzcc/contact-details-scraper)** (free Apify plan available, no credit card)
- Price: **$0.0015 per website with contacts**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/contact-details-scraper").call(run_input={"websites": ["https://apify.com", "https://www.python.org", "https://www.mozilla.org"], "maxPagesPerSite": 6})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **What contact details does it find?** Emails, phone numbers, WhatsApp and social profiles (LinkedIn, Instagram, Facebook, X, TikTok, YouTube, Telegram, Pinterest), from the homepage and the contact, about and legal pages.
- **Do I pay for websites without contacts?** No. Only websites where contacts are found are saved and billed.
- **Where do I get the list of websites?** From Google Maps, directories, trade fairs or your CRM. Our BORME Scraper gives you new Spanish companies every day.

### Telegram Scraper API - Channel Posts, Views & Media

Telegram channel scraper with no login, phone or API key: scrape messages from any public Telegram channel with text, date, views, reactions, links, photos and videos, plus channel stats.

- Run it in the browser: **[https://apify.com/sndzcc/telegram-channel-scraper](https://apify.com/sndzcc/telegram-channel-scraper)** (free Apify plan available, no credit card)
- Price: **$0.0007 per post**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/telegram-channel-scraper").call(run_input={"channels": ["https://t.me/durov", "@telegram"], "maxPostsPerChannel": 30})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Do I need a Telegram account or API key?** No. No account, phone number or API ID, so there is no risk for your own account.
- **Can I scrape private channels or groups?** No. Only public channels with a web preview (t.me/s/name) can be read.
- **Can I get only recent posts or posts with a keyword?** Yes. Use "Posted since" and "Keywords", and you only pay for the posts you keep.

### Brand Monitoring API - Mentions Radar for News & Reddit

Brand monitoring and social listening tool: track every mention of your brand, product or competitor across Google News, Reddit, Hacker News, Bluesky, Mastodon, YouTube, Stack Overflow, GitHub and Lemmy. With sentiment.

- Run it in the browser: **[https://apify.com/sndzcc/brand-mentions-radar](https://apify.com/sndzcc/brand-mentions-radar)** (free Apify plan available, no credit card)
- Price: **$0.003 per mention**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/brand-mentions-radar").call(run_input={"brands": ["Notion"], "timeRange": "7d", "maxPerSource": 10})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Which sources does it monitor?** Google News, Reddit, Hacker News, Bluesky, Mastodon, YouTube, Stack Overflow, GitHub and Lemmy, in one run.
- **Can I get alerts only for new mentions?** Yes. Turn on "Only new mentions" and schedule it daily: mentions you already have are skipped and free.
- **Is it a cheaper alternative to Mention, Brand24 or Awario?** Yes for most small brands: there is no monthly subscription, you pay only per mention found.

### AI Image Upscaler API - Upscale & Enhance Photos 4x

Upscale and enhance any image 2x or 4x with Real-ESRGAN AI, in bulk. Increase resolution and sharpen small, blurry or compressed photos. A pay-per-image Topaz, Upscayl and Let's Enhance alternative.

- Run it in the browser: **[https://apify.com/sndzcc/ai-image-upscaler](https://apify.com/sndzcc/ai-image-upscaler)** (free Apify plan available, no credit card)
- Price: **$0.01 per upscaled image**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/ai-image-upscaler").call(run_input={"images": ["https://raw.githubusercontent.com/xinntao/Real-ESRGAN/master/inputs/0014.jpg"], "scale": "4", "outputFormat": "jpg"})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **How much bigger can images get?** 2x or 4x per side. A 700x700 image becomes 2800x2800 at 4x.
- **Is it real AI upscaling?** Yes. It uses Real-ESRGAN, the open-source model behind popular desktop upscalers, which rebuilds edges and textures.
- **Which formats are supported?** Input: JPG, PNG, WebP, GIF, BMP and TIFF. Output: PNG (keeps transparency), JPG or WebP.

### Keyword Research API - Google, YouTube & Amazon Ideas

Keyword research tool: turn one keyword into hundreds of long-tail keyword ideas from Google, YouTube, Amazon, Bing and DuckDuckGo autocomplete, in any country and language. With intent and score.

- Run it in the browser: **[https://apify.com/sndzcc/keyword-ideas-machine](https://apify.com/sndzcc/keyword-ideas-machine)** (free Apify plan available, no credit card)
- Price: **$0.001 per keyword idea**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/keyword-ideas-machine").call(run_input={"keywords": ["running shoes"], "depth": "quick"})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Where do the keyword ideas come from?** From the autocomplete of Google, YouTube, Amazon, Bing and DuckDuckGo: what people really type.
- **Does it give search volume?** It gives a popularity score based on how often and how high each engine suggests the idea, not exact monthly volumes.
- **Does it work for Amazon and YouTube keywords?** Yes. Amazon uses each country's own store, and YouTube shows video searches.

### Tech Stack Detector API - Wappalyzer & BuiltWith Alternative

Find the technologies behind any website in bulk: CMS, ecommerce platform, analytics, ad pixels, marketing tools, live chat, payments, hosting and email provider. A Wappalyzer and BuiltWith alternative.

- Run it in the browser: **[https://apify.com/sndzcc/tech-stack-detector](https://apify.com/sndzcc/tech-stack-detector)** (free Apify plan available, no credit card)
- Price: **$0.0015 per website analyzed**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/tech-stack-detector").call(run_input={"websites": ["https://www.allbirds.com", "https://www.python.org", "https://vercel.com"]})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Is it a Wappalyzer or BuiltWith alternative?** Yes. It detects 300+ technologies from the code each website loads, in bulk, without a browser extension or subscription.
- **Can I find only websites that use a specific technology?** Yes. Fill in "Only websites using" (for example Shopify or Klaviyo) and you only pay for the websites that match.
- **How does it find the email provider?** From the domain's public MX and SPF records: Google Workspace, Microsoft 365, Zoho, SendGrid, Mailchimp, Salesforce and more.

### Polymarket & Kalshi API - Prediction Market Odds

Live odds, probabilities, 24h moves and volume of every Polymarket and Kalshi prediction market in one dataset. Search by keyword or category, or get only the biggest moves of the day.

- Run it in the browser: **[https://apify.com/sndzcc/prediction-markets-scraper](https://apify.com/sndzcc/prediction-markets-scraper)** (free Apify plan available, no credit card)
- Price: **$0.002 per market**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/prediction-markets-scraper").call(run_input={"keywords": ["bitcoin", "fed"], "maxMarketsPerPlatform": 10})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Do I need a Polymarket or Kalshi account?** No. It reads both platforms' public APIs, with no login or API key.
- **Can I compare the same event on both platforms?** Yes. Search a keyword (for example fed or bitcoin) and both platforms come out in the same format, side by side.
- **Can I get alerts when odds move a lot?** Yes. Set "Min 24h move" (for example 10 points) and schedule it hourly or daily.

### WHOIS & Domain Lookup API - DNS, SSL & Availability

Bulk WHOIS and domain lookup: availability, registrar, creation and expiry dates, nameservers, DNS records, email provider, SPF, DMARC and SSL certificate of any list of domains.

- Run it in the browser: **[https://apify.com/sndzcc/domain-intel](https://apify.com/sndzcc/domain-intel)** (free Apify plan available, no credit card)
- Price: **$0.0015 per domain**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/domain-intel").call(run_input={"domains": ["python.org", "vercel.app", "this-domain-is-surely-free-4821.com"]})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Is it a bulk WHOIS lookup?** Yes. It reads RDAP, the modern WHOIS run by the registries, and port-43 WHOIS where needed, for thousands of domains per run.
- **Can I check if domains are available?** Yes. Each row says whether the domain is available, and "Only available domains" keeps (and bills) just the free ones.
- **Does it show the owner of a domain?** Only when the registry publishes it. Since GDPR most registries hide owner names and emails; registrar, dates and nameservers are always public.

### Bluesky Scraper API - Posts, Profiles & Followers

Scrape Bluesky without login: posts by keyword or hashtag, profiles with follower counts, every post of a profile, followers and following, and account search to find influencers.

- Run it in the browser: **[https://apify.com/sndzcc/bluesky-scraper](https://apify.com/sndzcc/bluesky-scraper)** (free Apify plan available, no credit card)
- Price: **$0.001 per result**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/bluesky-scraper").call(run_input={"searchTerms": ["#opensource"], "profiles": ["bsky.app"], "maxItems": 20})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Do I need a Bluesky account?** No. It uses Bluesky's public API, with no login, app password or API key.
- **How many posts does a search return?** Up to 100 per term and run, which is what Bluesky serves without login. Profiles, timelines and followers have no limit.
- **Can I find influencers in my niche?** Yes. Use "Search accounts" with a topic and you get matching accounts with follower counts, bios and websites.

### SEO Audit API - Broken Links, Meta Tags & Site Crawler

Crawl any website and audit every page: SEO score, issues to fix, broken links, redirects, titles, meta descriptions, headings, images without alt, structured data, sitemap and robots.txt.

- Run it in the browser: **[https://apify.com/sndzcc/seo-audit](https://apify.com/sndzcc/seo-audit)** (free Apify plan available, no credit card)
- Price: **$0.002 per page audited**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/seo-audit").call(run_input={"startUrls": ["https://www.python.org"], "maxPagesPerSite": 10, "maxLinksToCheck": 100})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **What does the SEO audit check?** Status and redirects, titles, meta descriptions, headings, canonical, noindex, broken links, images without alt, Open Graph, structured data, mixed content, speed, robots.txt and sitemap.
- **Is it a broken link checker too?** Yes. It tests internal and external links and lists the broken ones on each page, ignoring links that only block bots.
- **How is the score calculated?** Each page starts at 100 and loses 15 points per error, 5 per warning and 1 per notice.

### OCR API - Image & PDF to Text Extractor, 100+ Languages

OCR tool to extract text from images, screenshots, photos and scanned or digital PDFs in 100+ languages, in bulk. Image to text and PDF to text with clean output per page. No API key.

- Run it in the browser: **[https://apify.com/sndzcc/image-pdf-to-text](https://apify.com/sndzcc/image-pdf-to-text)** (free Apify plan available, no credit card)
- Price: **$0.004 per page**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/image-pdf-to-text").call(run_input={"files": ["https://raw.githubusercontent.com/tesseract-ocr/tessdoc/main/images/eurotext.png", "https://raw.githubusercontent.com/ocrmypdf/OCRmyPDF/main/tests/resources/skew.pdf"], "languages": ["en"]})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Which files can it read?** JPG, PNG, WebP, TIFF, BMP and GIF images, and PDFs, both digital and scanned.
- **Which languages are supported?** More than 100, including English, Spanish, German, French, Chinese, Japanese, Arabic, Hindi and Russian. Several at once are fine.
- **Does it read scanned PDFs?** Yes. Pages with text are read directly; scanned pages go through OCR, and upside-down pages are turned automatically.

### Speech to Text API - Audio, Video & Podcast Transcription

Transcribe audio, video and podcast episodes to text with Whisper AI, in 99 languages. Get clean text, timestamps and SRT/VTT subtitles, or translate to English. Pay per audio minute.

- Run it in the browser: **[https://apify.com/sndzcc/speech-to-text](https://apify.com/sndzcc/speech-to-text)** (free Apify plan available, no credit card)
- Price: **$0.005 per audio minute**, no monthly fee
```python
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient("YOUR_APIFY_TOKEN")
run = client.actor("sndzcc/speech-to-text").call(run_input={"urls": ["https://github.com/openai/whisper/raw/main/tests/jfk.flac", "https://feeds.npr.org/510289/podcast.xml"], "maxMinutesPerFile": 2})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

- **Which files and links work?** MP3, M4A, WAV, FLAC, OGG, Opus, MP4, MOV, WebM, MKV and more, by direct link, plus podcast RSS feeds, Apple Podcasts links, Dropbox and Google Drive share links and web pages with an audio player.
- **Does it work with YouTube, TikTok or Spotify?** No. Those sites block automated downloads. Use a direct link to the file, the podcast RSS feed or its Apple Podcasts page instead.
- **Which languages are supported?** The 99 languages of Whisper, detected automatically, including English, Spanish, French, German, Portuguese, Italian, Chinese, Japanese, Arabic and Hindi. It can also translate any of them to English.

## Support

Found a bug or need a feature? Open an issue on the tool's **Issues** tab in Apify, or here on GitHub.

The examples in this repository are MIT licensed.
