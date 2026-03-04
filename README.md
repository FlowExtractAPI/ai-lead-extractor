# 🤖 AI Lead Extractor - Dual Mode

Extract any information from websites OR analyze any data using intelligent AI. A powerful Apify actor that combines traditional web scraping with advanced AI capabilities to extract contact information, generate summaries, analyze data, or create custom structured outputs from any website or raw data.

![Version](https://img.shields.io/badge/version-4.0-blue)
[![AI Lead Extractor Status](https://apify.com/actor-badge?actor=dz_omar/ai-lead-extractor)](https://apify.com/dz_omar/ai-lead-extractor)

---

## 🚀 Quick Start

### Run in 3 Simple Steps

**1. Basic Contact Extraction (No Configuration Needed)**

Click "Start" with default settings to extract emails, phone numbers, and social links from any website. No AI knowledge required.

```json
{
  "startUrls": [{"url": "https://example.com/contact"}],
  "useAI": false
}
```

**2. AI-Powered Extraction (Tell It What You Want)**

Enable AI and describe what you need in plain English. The AI understands natural language.

```json
{
  "startUrls": [{"url": "https://apify.com/about"}],
  "useAI": true,
  "aiInstructions": "Extract company name, CEO, and main contact email"
}
```

**3. Data Analysis Mode (No Website Needed)**

Analyze your own data directly without scraping. Perfect for transforming CSV, JSON, or any text data.

```json
{
  "data": "name,email\nAlice,alice@example.com\nBob,bob@example.com",
  "aiInstructions": "Convert to JSON array with name and email fields"
}
```

### First-Time Users

New to web scraping? Start here:

1. **Sign up** for a [free Apify account](https://apify.com?fpr=smcx63)
2. **Find this Actor** by searching "AI Lead Extractor" 
3. **Add a URL** in the `startUrls` field (e.g., "https://example.com")
4. **Click Start** and wait 30-60 seconds
5. **Download results** as JSON, CSV, or Excel

That's it! No coding required.

---

## 📋 Table of Contents

- [Features](#-features)
- [Two Operating Modes](#-two-operating-modes)
- [Input Configuration](#-input-configuration)
- [Output Structure](#-output-structure)
- [Pricing & Billing](#-pricing--billing)
- [Use Cases](#-use-cases)
- [API Usage](#-api-usage)
- [Advanced Configuration](#-advanced-configuration)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Support](#-support)

---

## ✨ Features

### 🎯 Dual Extraction Modes
- **Normal Mode**: Web scraping with full browser automation for JavaScript-heavy sites
- **Standby Mode**: Direct data analysis without browser overhead for faster processing

### 🤖 AI-Powered Intelligence
- **Free Tier**: Basic extraction plus AI via OpenRouter (pay-as-you-go)
- **Paid Tier**: Advanced AI included with superior accuracy and 60% cost savings
- **Natural Language Instructions**: Describe what you want in plain English (max 75 words)
- **Flexible Output**: JSON, CSV, markdown, or any custom format you specify

### ⚡ Performance & Reliability
- **Full Browser Rendering**: Handles dynamic JavaScript websites seamlessly
- **Automatic Screenshots**: Captures page screenshots for visual reference and verification
- **Smart Retry Logic**: Automatically recovers from temporary failures
- **Token Management**: Built-in 30K token limit with automatic overflow protection
- **Graceful Fallback**: Falls back to basic extraction if AI encounters issues

### 💰 Transparent Billing
- **Memory-Based Pricing**: Predictable costs based on allocated memory (Normal Mode only)
- **Word-Based AI Billing**: Pay only for words processed (input + output)
- **Detailed Usage Tracking**: Complete breakdown of all charges in results
- **Tier-Based Discounts**: Up to 75% savings for Bronze, Silver, and Gold subscribers

---

## 🎭 Two Operating Modes

### 1️⃣ Normal Mode - Web Scraping

**When to use**: Extract data from live websites

**How it works**:
- Launches a full browser using Playwright
- Navigates to your specified URLs
- Extracts content using AI or basic regex patterns
- Captures screenshots for reference
- Returns structured data in your preferred format

**Best for**: Company websites, contact pages, product listings, competitor analysis

**Example**:
```json
{
  "startUrls": [
    {"url": "https://apify.com/about"},
    {"url": "https://example.com/contact"}
  ],
  "useAI": true,
  "aiInstructions": "Extract company description, CEO name, and all contact information"
}
```

**Result**: Structured data with company info, contacts, and a screenshot of each page

---

### 2️⃣ Standby Mode - Data Analysis

**When to use**: Analyze existing data without web scraping

**How it works**:
- No browser launched (faster and cheaper)
- Accepts any data format: JSON, CSV, text, XML, HTML
- AI analyzes and transforms your data
- Returns processed results in seconds
- Cost-effective for pure data processing tasks

**Best for**: Data transformation, format conversion, text analysis, report generation

**Example using API**:
```bash
curl -X POST "https://dz-omar--ai-lead-extractor.apify.actor?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "data": "Company A: info@companya.com, +1-555-0100\nCompany B: contact@companyb.com, +1-555-0200",
    "aiInstructions": "Extract as JSON array with company name, email, and phone"
  }'
```

**Result**: Instant JSON transformation without any web scraping overhead

**Key Difference**: 
- **Normal Mode** = Browser required, processes URLs, memory billing applies
- **Standby Mode** = No browser, processes your data, no memory billing for creator

---

## 📥 Input Configuration

### Basic Fields

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `startUrls` | Array | Yes* | `[]` | URLs to scrape (*not needed in Standby Mode for data analysis) |
| `useAI` | Boolean | No | `false` | Enable AI-powered extraction |
| `aiInstructions` | String | No | Auto | Natural language instructions (max 75 words/500 chars) |
| `data` | String | No | `null` | Your data to analyze (Standby Mode only) |

**Default AI Instructions** (when `useAI: true` but no instructions provided):
```
"Extract all useful information: emails, phones, social links, descriptions, etc."
```

---

### Example 1: Basic Contact Extraction (No AI)

Perfect for simple contact scraping without AI costs.

```json
{
  "startUrls": [
    {"url": "https://example.com/contact"},
    {"url": "https://example.com/about"}
  ],
  "useAI": false
}
```

**What you get**: 
- Email addresses
- Phone numbers  
- Social media links
- Page screenshots

**Cost**: Memory only (~$0.01 per page)

---

### Example 2: AI Extraction (Free Tier - Pay Per Use)

AI extraction with usage-based billing for free users.

```json
{
  "startUrls": [{"url": "https://apify.com/about"}],
  "useAI": true,
  "aiInstructions": "Summarize this company in 3 bullet points and extract the CEO's name"
}
```

**What you get**: 
- AI-generated summary
- CEO name
- Basic contacts
- Full cost breakdown

**Cost**: Memory + AI words (~$0.02-$0.05 per page)

---

### Example 3: Premium AI (Paid Subscribers - Included)

Advanced AI with better accuracy and discounted rates.

```json
{
  "startUrls": [{"url": "https://apify.com/about"}],
  "useAI": true,
  "aiInstructions": "Extract: CEO full name, primary support email, company mission statement, year founded, and number of employees if mentioned"
}
```

**What you get**: 
- More accurate extraction
- Better understanding of complex requests
- 60% lower costs than free tier

**Cost**: ~$0.01 per page (GOLD tier example)

---

### Example 4: Standby Mode - Data Analysis

Analyze your own data without any web scraping.

```json
{
  "data": "Product A: $299, 4.5 stars, 128 reviews\nProduct B: $399, 4.8 stars, 256 reviews\nProduct C: $199, 4.2 stars, 89 reviews",
  "aiInstructions": "Convert to JSON array with fields: name, price (as number), rating, reviewCount"
}
```

**What you get**: 
- Structured JSON output
- Fast processing (no browser)
- No memory charges (in Standby)

**Cost**: AI words only

---

### Example 5: Batch Processing Multiple URLs

Process many pages in one run.

```json
{
  "startUrls": [
    {"url": "https://company1.com/about"},
    {"url": "https://company2.com/contact"},
    {"url": "https://company3.com/team"},
    {"url": "https://company4.com/careers"}
  ],
  "useAI": true,
  "aiInstructions": "Extract company name, industry, and all email addresses"
}
```

**What you get**: 
- Consistent data structure across all URLs
- Parallel processing for speed
- One dataset with all results

---

## 📤 Output Structure

### Basic Extraction Output (No AI)

```json
{
  "url": "https://example.com/contact",
  "title": "Contact Us - Example Company",
  "basicExtraction": {
    "emails": ["info@example.com", "support@example.com"],
    "phones": ["+1-555-0100", "+1-800-EXAMPLE"],
    "socialLinks": [
      "https://twitter.com/example",
      "https://linkedin.com/company/example"
    ],
    "extractionMethod": "regex"
  },
  "screenshot": {
    "available": true,
    "url": "https://api.apify.com/v2/key-value-stores/xyz/records/screenshot-123456"
  },
  "extractionTier": "FREE",
  "extractionMethod": "Basic Only",
  "scrapedAt": "2025-01-10T14:30:00.000Z"
}
```

---

### AI-Powered Extraction Output

```json
{
  "url": "https://apify.com/about",
  "title": "About · Apify",
  "aiExtraction": {
    "company_name": "Apify",
    "ceo_name": "Jan Čurn",
    "support_email": "support@apify.com",
    "company_mission": "Make the web more programmable",
    "year_founded": "2015",
    "summary": "Apify is a web scraping and automation platform that helps developers extract data from websites and automate web workflows."
  },
  "basicExtraction": {
    "emails": ["support@apify.com", "hello@apify.com"],
    "phones": ["+420-123-456-789"],
    "socialLinks": [
      "https://linkedin.com/company/apify",
      "https://twitter.com/apify"
    ]
  },
  "aiCost": {
    "inputWords": 2836,
    "outputWords": 2606,
    "totalWords": 5442,
    "cost": "$0.015981",
    "breakdown": "Processed 2,836 input words, generated 2,606 output words"
  },
  "screenshot": {
    "available": true,
    "url": "https://api.apify.com/v2/key-value-stores/xyz/records/screenshot-789012"
  },
  "extractionTier": "PAID",
  "extractionMethod": "AI-Powered + Basic",
  "userTier": "GOLD",
  "scrapedAt": "2025-01-10T14:30:00.000Z"
}
```

---

### Output Field Reference

| Field | Description | Always Present |
|-------|-------------|----------------|
| `url` | The scraped website URL | ✅ Yes |
| `title` | HTML page title | ✅ Yes |
| `aiExtraction` | AI-extracted data (structure varies by instructions) | Only with AI |
| `basicExtraction` | Contact info (emails, phones, social links) | ✅ Yes |
| `aiCost` | Detailed AI usage breakdown (words processed, cost) | Only with AI |
| `screenshot` | Screenshot URL for visual reference | ✅ Yes |
| `extractionMethod` | Method used (Basic, AI-Powered, etc.) | ✅ Yes |
| `extractionTier` | User tier (FREE, PAID) | ✅ Yes |
| `userTier` | Subscription level (FREE, BRONZE, SILVER, GOLD) | ✅ Yes |
| `scrapedAt` | ISO 8601 timestamp | ✅ Yes |

**Note**: The structure of `aiExtraction` varies based on your `aiInstructions`. The AI automatically determines the best format for your requested data.

---

## 💰 Pricing & Billing

### Understanding Costs

This actor has two billing components:

1. **Memory-Based Billing** (Normal Mode only)
2. **AI Word-Based Billing** (when AI is enabled)

---

### 1. Memory-Based Billing (Normal Mode Only)

**Charged every 30 seconds** based on allocated memory. Does NOT apply in Standby Mode.

| Memory | Events per 30s | FREE Tier | GOLD Tier | Savings |
|--------|----------------|-----------|-----------|---------|
| 128 MB | 1 | $0.0008 | $0.0002 | 75% |
| 256 MB | 2 | $0.0016 | $0.0004 | 75% |
| 512 MB | 4 | $0.0032 | $0.0008 | 75% |
| 1024 MB | 8 | $0.0064 | $0.0016 | 75% |

**Formula**: Events = Memory (MB) ÷ 128

**Example**: Running at 256 MB for 2 minutes
- **FREE tier**: 4 intervals × 2 events × $0.0016 = **$0.0128**
- **GOLD tier**: 4 intervals × 2 events × $0.0004 = **$0.0032** (75% savings)

---

### 2. AI Word-Based Billing

**Charged per 1,000 words processed** when AI is enabled.

| Type | FREE | BRONZE | SILVER | GOLD |
|------|------|--------|--------|------|
| Input Words (per 1K) | $0.0015 | $0.0012 | $0.0010 | $0.0008 |
| Output Words (per 1K) | $0.0045 | $0.0036 | $0.0030 | $0.0024 |

**Conversion**: ~1 token = 0.75 words (approximately 4 characters)

**Example AI extraction** (typical page):
- **Input**: 2,836 words (page content)
- **Output**: 2,606 words (extracted data)
- **FREE tier**: $0.00425 + $0.01173 = **$0.01598**
- **GOLD tier**: $0.00227 + $0.00625 = **$0.00852** (47% savings)

---

### Complete Cost Examples

#### Example 1: Basic Extraction (No AI)
**Scenario**: Extract contacts from 5 pages, 2 minutes total, 256 MB memory

- **Memory Cost** (FREE): $0.0128
- **AI Cost**: $0 (AI disabled)
- **Total**: **$0.0128**

---

#### Example 2: AI Extraction - Free Tier
**Scenario**: AI extract from 3 pages, 3 minutes total, 256 MB memory

- **Memory Cost**: 6 intervals × 2 events × $0.0016 = **$0.0192**
- **AI Cost** (3 pages avg): 3 × $0.016 = **$0.048**
- **Total**: **$0.0672**

---

#### Example 3: AI Extraction - GOLD Tier
**Scenario**: Same as Example 2, but with GOLD subscription

- **Memory Cost**: 6 intervals × 2 events × $0.0004 = **$0.0048**
- **AI Cost** (3 pages avg): 3 × $0.0085 = **$0.0255**
- **Total**: **$0.0303** (55% savings vs FREE)

---

#### Example 4: Standby Mode - Data Analysis
**Scenario**: Analyze CSV data with 5,000 words

- **Memory Cost**: $0 (no browser in Standby)
- **AI Cost** (GOLD): ~$0.005
- **Total**: **$0.005**

**Note**: In Standby Mode with PPE (Pay-Per-Event), the user pays execution costs, not the creator.

---

### Upgrade Benefits

| Feature | Free Tier | Paid Tiers (BRONZE/SILVER/GOLD) |
|---------|-----------|----------------------------------|
| Basic Extraction | ✅ Always included | ✅ Always included |
| AI Model | Simple (OpenRouter) | **Advanced (higher accuracy)** |
| AI Billing | Pay-per-use | **20-47% discounts** |
| Memory Rates | Standard | **Up to 75% savings** |
| AI Accuracy | Good | **Superior** |
| Complex Instructions | Limited | **Excellent** |
| Support Priority | Standard | **Priority response** |

---

### Cost-Saving Tips

1. **Use Basic Extraction First**: If you only need emails/phones, disable AI to save costs
2. **Batch Processing**: Process multiple URLs in one run to amortize startup costs
3. **Lower Memory**: Start with 256 MB and increase only if needed
4. **Upgrade for Volume**: If processing 50+ pages/month with AI, paid tiers save money
5. **Use Standby Mode**: For data analysis tasks, Standby Mode avoids memory charges

---

## 🎯 Use Cases

### 🏢 Lead Generation & Sales Intelligence

Extract comprehensive contact information and company data for sales prospecting.

**Example Tasks**:
- Build targeted prospect lists from company websites
- Extract decision-maker names and contact details
- Gather company descriptions for personalized outreach
- Find direct phone numbers and email addresses

**Sample Instructions**:
```
"Extract CEO name, CFO name, main company email, phone number, and LinkedIn profile"
```
```
"Find all team members listed with their job titles and email addresses"
```
```
"Get company size, industry, and all available contact methods"
```

**Real-World Workflow**:
1. Input list of 50 competitor/prospect websites
2. Extract key decision-makers and contacts
3. Export to CSV for CRM import
4. Use data for personalized outreach campaigns

---

### 📊 Market Research & Competitive Analysis

Analyze competitor offerings, pricing, and market positioning.

**Example Tasks**:
- Compare pricing plans across multiple competitors
- Extract product features and specifications
- Monitor changes in competitor messaging
- Analyze value propositions

**Sample Instructions**:
```
"List all pricing tiers with features and monthly costs"
```
```
"Summarize the company's main value proposition in 2 sentences"
```
```
"Extract all product names with their descriptions and target audience"
```
```
"Compare this company's features against industry standard offerings"
```

**Real-World Workflow**:
1. Scrape 20 competitor pricing pages
2. Extract structured pricing data
3. Generate comparison matrix
4. Identify pricing gaps and opportunities

---

### 🤖 Data Processing & Transformation

Transform unstructured data into structured formats.

**Example Tasks**:
- Convert CSV to JSON with custom fields
- Clean and normalize messy datasets
- Extract specific information from documents
- Merge and deduplicate data sources

**Sample Instructions**:
```
"Convert this CSV to JSON array with fields: name, email, company, title"
```
```
"Extract all dates, amounts, and invoice numbers from this text"
```
```
"Normalize phone numbers to E.164 format and remove duplicates"
```
```
"Parse job postings and extract: position, salary range, location, requirements"
```

**Real-World Workflow**:
1. Upload raw CSV/text data via Standby Mode
2. Specify desired output structure
3. Get clean, structured JSON
4. Import directly into your database

---

### 📝 Content Research & Citation Management

Gather information for content creation and fact-checking.

**Example Tasks**:
- Research topics with source attribution
- Extract statistics and data points
- Generate article summaries
- Collect citation information

**Sample Instructions**:
```
"Extract all statistics mentioned with their sources"
```
"Generate a 5-bullet-point summary of the main arguments"
```
```
"List all studies/papers cited with publication dates and authors"
```
```
"Extract key takeaways and actionable insights"
```

**Real-World Workflow**:
1. Input list of research articles/blogs
2. Extract key facts and statistics
3. Generate summary report
4. Use as research base for content creation

---

### 🏪 E-Commerce & Product Intelligence

Monitor product listings, reviews, and market trends.

**Example Tasks**:
- Extract product specifications
- Monitor price changes
- Analyze review sentiment
- Track competitor inventory

**Sample Instructions**:
```
"Extract product name, price, rating, and number of reviews"
```
```
"List all product features and specifications in JSON format"
```
```
"Summarize top 3 positive and negative points from reviews"
```

**Real-World Workflow**:
1. Scrape competitor product pages
2. Extract pricing and features
3. Monitor changes daily
4. Adjust your pricing strategy accordingly

---

### 📧 Email Finder & Contact Enrichment

Discover and verify contact information for outreach.

**Example Tasks**:
- Find verified email addresses
- Extract phone numbers with validation
- Discover social media profiles
- Build contact databases

**Sample Instructions**:
```
"Find all email addresses and categorize as: sales, support, general"
```
```
"Extract contact form URL, main phone, and support email"
```
```
"List team members with their roles and LinkedIn profiles"
```

**Real-World Workflow**:
1. Input list of target company websites
2. Extract all contact methods
3. Verify and categorize contacts
4. Export to your CRM or email tool

---

## 🔌 API Usage

### Method 1: Run Actor via Apify API

Standard actor execution for batch processing.

```bash
curl -X POST "https://api.apify.com/v2/acts/IeZZMR1Uv6J9h7pdS/runs?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "startUrls": [
      {"url": "https://apify.com/about"},
      {"url": "https://example.com/contact"}
    ],
    "useAI": true,
    "aiInstructions": "Extract company info and contact details"
  }'
```

**Response**:
```json
{
  "data": {
    "id": "run_abc123xyz",
    "status": "RUNNING",
    "defaultDatasetId": "dataset_xyz789"
  }
}
```

**Then fetch results**:
```bash
curl "https://api.apify.com/v2/datasets/dataset_xyz789/items?token=$APIFY_TOKEN"
```

---

### Method 2: Standby Mode (Real-Time API)

Fast, synchronous responses for real-time applications.

#### Web Scraping in Standby Mode

```bash
curl -X POST "https://dz-omar--ai-lead-extractor.apify.actor?token=YOUR_STANDBY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com/about",
    "useAI": true,
    "aiInstructions": "Extract company name, description, and contact email"
  }'
```

**Response** (immediate):
```json
{
  "url": "https://example.com/about",
  "aiExtraction": {
    "company_name": "Example Corp",
    "description": "Leading provider of...",
    "contact_email": "info@example.com"
  },
  "basicExtraction": {
    "emails": ["info@example.com"],
    "phones": ["+1-555-0100"]
  }
}
```

---

#### Data Analysis in Standby Mode

```bash
curl -X POST "https://dz-omar--ai-lead-extractor.apify.actor?token=YOUR_STANDBY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "data": "Alice,alice@example.com,CEO\nBob,bob@example.com,CTO\nCarol,carol@example.com,CFO",
    "aiInstructions": "Convert to JSON array with fields: name, email, role"
  }'
```

**Response** (immediate):
```json
[
  {"name": "Alice", "email": "alice@example.com", "role": "CEO"},
  {"name": "Bob", "email": "bob@example.com", "role": "CTO"},
  {"name": "Carol", "email": "carol@example.com", "role": "CFO"}
]
```


## 🔧 Advanced Configuration

### Custom AI Instructions Best Practices

**Be Specific**: 
```
✅ "Extract: CEO full name, primary support email, company mission (max 20 words)"
❌ "Get company info"
```

**Specify Format**:
```
✅ "Return as JSON with fields: name, email, phone. Phone in E.164 format."
❌ "Give me contact details"
```

**Set Boundaries**:
```
✅ "Summarize in exactly 3 bullet points, max 15 words each"
❌ "Summarize the page"
```

**Use Examples**:
```
✅ "Extract pricing like: {tier: 'Pro', price: 29, features: ['A', 'B', 'C']}"
❌ "Extract pricing"
```

---

### Memory Allocation Guide

Choose memory based on your needs:

| Memory | Use Case | Typical Speed | Cost (FREE) |
|--------|----------|---------------|-------------|
| 128 MB | Simple pages, no JS | 15-30 sec | $0.0008/30s |
| 256 MB | **Recommended default** | 10-20 sec | $0.0016/30s |
| 512 MB | Complex JS sites | 5-10 sec | $0.0032/30s |
| 1024 MB | Heavy pages, many images | 3-7 sec | $0.0064/30s |

**Recommendation**: Start with 256 MB. Increase only if you see timeout errors or slow performance.

---

### Handling Large Datasets

**Batch Processing** (Normal Mode):
```json
{
  "startUrls": [
    {"url": "https://site1.com"},
    {"url": "https://site2.com"},
    {"url": "https://site3.com"}
    // ... up to 1000+ URLs
  ],
  "useAI": true,
  "aiInstructions": "Extract contacts"
}
```

**Pagination Support**:
```json
{
  "startUrls": [
    {"url": "https://example.com/page?p=1"},
    {"url": "https://example.com/page?p=2"},
    {"url": "https://example.com/page?p=3"}
  ]
}
```

---

### Error Handling & Retries

The actor automatically handles common errors:

- **Timeouts**: Automatic retry with increased timeout
- **Network errors**: 3 retry attempts with exponential backoff
- **AI failures**: Graceful fallback to basic extraction
- **Invalid URLs**: Skipped with error logged

**Error Output Example**:
```json
{
  "url": "https://invalid-site.com",
  "error": "Page timeout after 60 seconds",
  "errorType": "TIMEOUT",
  "basicExtraction": null,
  "scrapedAt": "2025-01-10T14:30:00.000Z"
}
```
---

## 📞 Support

### Get Help

- 🌐 **Website**: [flowextractapi.com](https://flowextractapi.com)
- 📧 **Email**: [flowextractapi@outlook.com](mailto:flowextractapi@outlook.com)
- 🙋 **Apify Profile**: [FlowExtract API](https://apify.com/dz_omar?fpr=smcx63)
- 💬 **GitHub Issues**: [FlowExtractAPI](https://github.com/FlowExtractAPI)

### Social Media

- 💼 **LinkedIn**: [flowextract-api](https://www.linkedin.com/in/flowextract-api/)
- 🐦 **Twitter**: [@FlowExtractAPI](https://x.com/@FlowExtractAPI)
- 📱 **Facebook**: [flowextractapi](https://www.facebook.com/flowextractapi)

### Documentation

- 📚 **Apify Docs**: [docs.apify.com](https://docs.apify.com)
- 🔧 **API Reference**: [docs.apify.com/api/v2](https://docs.apify.com/api/v2)
- 🎓 **Tutorials**: Check our blog for guides and examples

---

## 🌟 Related Actors by FlowExtract API

### 🎬 Video & Media
- **[YouTube Transcript Extractor](https://apify.com/dz_omar/youtube-transcript-metadata-extractor?fpr=smcx63)** - Extract transcripts with timestamps
- **[YouTube Scraper Pro](https://apify.com/dz_omar/Youtube-Scraper-Pro?fpr=smcx63)** - Complete channel and playlist extraction
- **[Zoom Scraper](https://apify.com/dz_omar/zoom-scraper?fpr=smcx63)** - Download recordings and transcripts
- **[Loom Scraper](https://apify.com/dz_omar/loom-video-scraper?fpr=smcx63)** - Loom video and transcript extraction

### 🏠 Real Estate
- **[Idealista Scraper API](https://apify.com/dz_omar/idealista-scraper-api?fpr=smcx63)** - Spanish property data with API
- **[Idealista Scraper](https://apify.com/dz_omar/idealista-scraper?fpr=smcx63)** - Real estate listings extractor

### 🛠️ Developer Tools
- **[Screenshot](https://apify.com/dz_omar/screenshot?fpr=smcx63)** - Fast webpage screenshots
- **[Ultimate Screenshot](https://apify.com/dz_omar/ultimate-screenshot?fpr=smcx63)** - Advanced screenshot tool
- **[Network Security Scanner](https://apify.com/dz_omar/network-security-scanner?fpr=smcx63)** - Security vulnerability scanner

### 📱 Social Media
- **[Facebook Ads Scraper Pro](https://apify.com/dz_omar/facebook-ads-scraper-pro?fpr=smcx63)** - Extract Facebook ads data

---

## 📄 License

This actor is provided as-is for use on the Apify platform. Use responsibly and in accordance with applicable laws and website terms of service.

---

## ⚖️ Legal & Compliance

This actor extracts **publicly available** information from websites. Ensure your use complies with:

- ✅ Website Terms of Service
- ✅ Copyright laws
- ✅ Data protection regulations (GDPR, CCPA)
- ✅ Robots.txt directives
- ✅ Your jurisdiction's laws

**You are responsible** for how you use extracted data. Use ethically and legally.

---

## 🚀 Ready to Start?

1. **[Sign up for Apify](https://apify.com?fpr=smcx63)** (free tier available)
2. **[Try AI Lead Extractor](https://apify.com/dz_omar/ai-lead-extractor?fpr=smcx63)**
3. **Configure your first extraction**
4. **Get results in seconds**

**Have questions?** Contact us at [flowextractapi@outlook.com](mailto:flowextractapi@outlook.com)

---
