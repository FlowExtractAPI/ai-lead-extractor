# 🤖 AI Lead Extractor

Extract structured lead intelligence — emails, phone numbers, people, company details, and any custom fields you describe — from any website. Every page is run through a fast deterministic contact extractor, and, when you enable AI, an additional structured‑data pass that follows your plain‑English instructions.

[![AI Lead Extractor](https://apify.com/actor-badge?actor=dz_omar/ai-lead-extractor)](https://apify.com/dz_omar/ai-lead-extractor)

---

## ✨ What it does

- **Contact extraction on every page** — emails, phone numbers, and social profiles (LinkedIn, X/Twitter, Facebook, Instagram, YouTube, TikTok, GitHub, Discord, Telegram, WhatsApp), plus links, images, and headings. This always runs, with or without AI.
- **AI extraction (optional)** — describe what you want in plain English and get back structured JSON: company profile, people and roles, or any custom shape you ask for.
- **Screenshots (optional)** — a JPEG of each page, stored and linked from the result.
- **Predictable per‑result pricing** — you pay per page that returns data, not per minute of runtime. Pages that fail to load are never charged.
- **Proxy support** — route requests through Apify Proxy or your own proxy URLs.

---

## 🚀 Quick start

**1. Basic contact extraction (no AI)**

```json
{
  "startUrls": [{ "url": "https://example.com/contact" }],
  "useAI": false
}
```

Returns emails, phones, social links, and page structure.

**2. AI extraction with the default lead prompt**

```json
{
  "startUrls": [{ "url": "https://apify.com/about" }],
  "useAI": true
}
```

Returns a structured company/people/contacts object in addition to the basic contacts.

**3. AI extraction with your own instructions**

```json
{
  "startUrls": [{ "url": "https://apify.com/about" }],
  "useAI": true,
  "aiInstructions": "Extract the company name, the CEO, and the main support email"
}
```

The AI shapes the output around your request.

---

## 📥 Input

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `startUrls` | Array | **Yes** | — | Pages to process. Each entry is `{ "url": "https://…" }`. |
| `useAI` | Boolean | No | `true` | Run the AI extraction pass. When `false`, only the contact extractor runs. |
| `aiInstructions` | String | No | Full lead extraction | Plain‑English description of what to extract. Max 500 characters / 75 words. |
| `includeScreenshot` | Boolean | No | `true` | Capture a JPEG of each page. Turn off if you only need data. |
| `proxyConfig` | Object | No | No proxy | Proxy settings (see [Proxy](#-proxy)). |

**Default AI instructions** (used when `useAI: true` and `aiInstructions` is left blank):

> Extract all the useful information — email, phone number, description, and any relevant structured data from the page.

---

## 📤 Output

One dataset item per URL. `basicExtraction` is **always** present; `aiExtraction` appears when AI runs successfully.

```json
{
  "url": "https://apify.com/about",
  "title": "About · Apify",
  "scrapedAt": "2026-07-20T14:30:00.000Z",
  "ok": true,
  "error": null,
  "extractedBy": ["regex", "ai"],
  "basicExtraction": {
    "emails": ["hello@apify.com"],
    "phones": ["+420123456789"],
    "socialLinks": {
      "linkedin": "https://linkedin.com/company/apify",
      "twitter": "https://twitter.com/apify",
      "facebook": null,
      "instagram": null,
      "youtube": null,
      "tiktok": null,
      "github": "https://github.com/apify",
      "discord": null,
      "telegram": null,
      "whatsapp": null
    },
    "links": [{ "text": "Careers", "url": "https://apify.com/jobs", "external": false }],
    "images": [{ "alt": "logo", "url": "https://…/logo.png" }],
    "headings": [{ "level": 1, "text": "About Apify" }],
    "wordCount": 1240,
    "linkCount": 37
  },
  "aiExtraction": {
    "company": { "name": "Apify", "description": "…", "industry": "Software", "address": null, "website": "https://apify.com" },
    "people": [{ "name": "…", "title": "CEO", "email": null, "linkedin": null }],
    "emails": ["hello@apify.com"],
    "phones": ["+420123456789"],
    "socialLinks": { "linkedin": "…", "twitter": "…", "other": [] }
  },
  "content": {
    "markdown": "# About Apify …",
    "screenshot": {
      "available": true,
      "key": "screenshot-1779998222295-ab12cd",
      "url": "https://api.apify.com/v2/key-value-stores/…/records/screenshot-1779998222295-ab12cd",
      "sizeKb": 18
    }
  },
  "metadata": {
    "aiUsage": { "attempted": true, "inputTokens": 2600, "outputTokens": 220, "totalTokens": 2820 }
  }
}
```

### Field reference

| Field | Description | Always present |
|-------|-------------|----------------|
| `url`, `title`, `scrapedAt` | Source URL, page title, timestamp | ✅ |
| `ok` | `true` if the page loaded | ✅ |
| `error` | `null`, or `{ code, message, id }` when the page failed | ✅ |
| `extractedBy` | `["regex"]`, or `["regex","ai"]` when AI succeeded | ✅ |
| `basicExtraction` | Contacts, social links, links, images, headings, counts | ✅ |
| `aiExtraction` | AI structured data (shape follows your instructions); `null` when AI is off, or an `{ error }` object if the AI pass failed | Only with AI |
| `content.markdown` | Cleaned page text | ✅ |
| `content.screenshot` | `{ available, key, url, sizeKb }`, or `{ available: false }` | ✅ |
| `metadata.aiUsage` | Token accounting for the AI pass | ✅ |

When AI is enabled but the AI pass fails, the page still returns full `basicExtraction`, `aiExtraction` carries a sanitized error, and the page is billed at the **basic** rate — never the AI rate.

---

## 💰 Pricing & billing

This Actor uses **pay‑per‑event** pricing: you are charged **per page that returns data**, at a flat rate per result. Runtime and memory are not billed separately, so cost is predictable regardless of how long a page takes.

Two events:

| Event | When | FREE | BRONZE | SILVER | GOLD |
|-------|------|------|--------|--------|------|
| **AI Extraction** | `useAI: true` and the AI pass succeeds | $0.045 | $0.018 | $0.015 | $0.012 |
| **Basic Extraction** | `useAI: false`, or AI enabled but its pass failed | $0.030 | $0.010 | $0.009 | $0.008 |

*Prices are per page. Paid Apify plans (Bronze → Gold) receive progressively lower rates.*

**What you are not charged for:**
- Pages that fail to load — no result, no charge.
- The AI pass failing — that page drops to the Basic rate.

**AI model usage is separate and billed to your own Apify account**, at cost, when AI is enabled. On the **free** Apify plan, AI responses are shorter (capped around 2,048 tokens) and cost more per token; **paid** Apify plans get full‑length responses at lower cost. This model usage is typically a fraction of a cent per page.

**Spending cap:** set a maximum charge per run (`ACTOR_MAX_TOTAL_CHARGE_USD`) and the Actor stops once it's reached, finishing the page in progress first.

---

## 🌍 Proxy

Requests can be routed through a proxy to reduce rate‑limiting and reach region‑specific content. Configure it under `proxyConfig`:

```json
{
  "startUrls": [{ "url": "https://example.com" }],
  "proxyConfig": { "useApifyProxy": true }
}
```

- **Apify Proxy** — enable `useApifyProxy`. A fresh IP is drawn per page.
- **Your own proxies** — supply `proxyUrls` with your proxy endpoints; requests route through them as‑is.
- **Residential exit IPs** — if you need residential IPs, provide them through your own `proxyUrls`.

If a proxy can't be applied, the run continues on a direct connection rather than failing.

---

## 🧠 Memory

The Actor runs a real browser, so it needs **1 GB** (the default). You can raise it to **2 GB** for heavier pages; because billing is per result, extra memory changes speed, not the per‑page price.

---

## 🎯 Use cases

- **Lead generation** — pull contacts and decision‑makers from company, team, and about pages.
- **Contact enrichment** — turn a list of company URLs into emails, phones, and social profiles.
- **Competitive research** — capture structured company profiles and screenshots at scale.
- **Custom extraction** — describe any structured output ("list job openings with title and location", "extract pricing tiers and features") and get it as JSON.

---

## ❓ FAQ

**Do I have to use AI?**
No. With `useAI: false` you get the full contact extractor (emails, phones, socials, links, headings) at the Basic rate.

**What happens if a page blocks me?**
That page returns `ok: false` with a sanitized error and is not charged. The run continues to the next URL.

**Can I control the output shape?**
Yes — `aiInstructions` drives the structure of `aiExtraction`. Leave it blank for the full lead‑extraction schema.

**Why did a page get the Basic rate when I enabled AI?**
The AI pass didn't complete for that page (for example, a model limit on the free plan). You still get full contact data, so the page is billed at the lower Basic rate.

**How do I keep costs bounded?**
Set a max charge per run, disable screenshots if you don't need them, and start at 1 GB memory.

---

## 🆘 Support

Open an issue on the Actor's Apify page, or contact the developer through Apify Store.
