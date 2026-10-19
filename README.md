# Lever Job Scraper [💰$0.13]

Extract structured data from [jobs.lever.co](https://jobs.lever.co) — any company's Lever job board by name or jobs.lever.co URL, on global and EU boards. Every posting returns title, team/department and location with commitment and workplace type, salary when posted and the full description with its lists.

**[Lever Job Scraper [💰$0.13] on Apify →](https://apify.com/blackfalcondata/lever-co-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by 📝 description format, and more.

**Incremental mode** — Only get new or changed jobs since your last run. Content hash per job — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how jobs evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per ${NOUN} to control output size and cost.

**Result cap** — Stop after N jobs (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every job returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured jobs from jobs.lever.co on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor jobs, track trends, and analyze market dynamics with structured, deduplicated data from jobs.lever.co.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on jobs.lever.co to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per job is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "spotify",
  "maxResults": 100,
  "descriptionMaxLength": 0,
  "compact": false,
  "descriptionFormat": "all",
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "emitUnchanged": false,
  "emitExpired": false,
  "skipReposts": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | The company whose Lever board you want — its board name (e.g. "spotify") or the full board URL (e.g. "https://jobs.lever.co/spotify"). Use a JSON array to scrape several boards in one run, e.g. ["spotify","netflix"]. Required if no Start URLs are provided. |
| `location` | string | — | Only return postings in this location, filtered by Lever itself (e.g. "London", "Remote"). Leave empty for every location on the board. |
| `maxResults` | integer | `100` | Maximum total results (0 = unlimited). |
| `startUrls` | array | `[]` | Paste Lever board URLs (e.g. https://jobs.lever.co/spotify). Each URL becomes its own task; results are merged and deduped by job ID across all URLs. When provided, Start URLs REPLACE the company field (unsupported URLs are skipped, and if none is supported the run stops with an input error). |
| `descriptionMaxLength` | integer | `0` | Truncate description to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `descriptionFormat` | enum | `"all"` | Which description representations to emit. `all` keeps every variant (plain text, HTML and Markdown) — the default. `text` / `html` / `markdown` drop the variants you don't need and typically halve output size. |
| `excludeEmptyFields` | boolean | `false` | Drop null / empty-string / empty-array fields (and fully-null nested objects like socialProfiles) from each output record. Off by default to preserve dataset schema compatibility; turn on to slim output for LLM / agent consumption. |
| `extractEmails` | boolean | `true` | Collect email addresses written in each posting's description into extractedEmails (recruiter or application contacts). On by default; turn off to leave extractedEmails empty. |
| `includeRawJson` | boolean | `false` | Add the complete, unmodified Lever posting object to each result as rawJson — every field Lever returns, including ones not mapped to their own column. Off by default; it roughly doubles the record size. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from the boards being scraped, so different board sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `emitUnchanged` | boolean | `false` | Also emit jobs that have not changed since the last run (incrementalMode only). |
| `emitExpired` | boolean | `false` | Also emit jobs that have disappeared since the last run (incrementalMode only). |
| `skipReposts` | boolean | `false` | When incremental, skip jobs whose content matches an expired job from a prior run (cross-run repost detection). |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED jobs. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of jobs included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |

---

## Output fields

Every job returns the same 60-field schema. Missing values are `null` — never omitted.

- `platform`
- `company`
- `companySlug`
- `leverRegion`
- `id`
- `jobId`
- `title`
- `url`
- `hostedUrl`
- `applyUrl`
- `department`
- `team`
- `level`
- `location`
- `locations`
- `allLocations`
- `normalizedLocation`
- `country`
- `workplaceType`
- `isRemote`
- `commitment`
- `workType`
- `employmentTypes`
- `createdAt`
- `createdAtTimestamp`
- `postedAt`
- `ageDays`
- `description`
- `descriptionPlain`
- `descriptionHtml`
- `openingPlain`
- `descriptionBodyPlain`
- `lists`
- `requirementsPlain`
- `benefitsPlain`
- `additionalPlain`
- `salaryRange`
- `salary`
- `salaryDescriptionPlain`
- `source`
- `scrapedAt`
- `listingId`
- `portalUrl`
- `descriptionMarkdown`
- `extractedEmails`
- `extractedPhones`
- `extractedUrls`
- `socialProfiles`
- `salaryMin`
- `salaryMax`
- `salaryCurrency`
- `salaryType`
- `searchQuery`
- `contentQuality`
- `detailFetched`
- `contentHash`
- `changeType`
- `isRepost`
- `repostOfId`
- `repostDetectedAt`

---

## Sample output

One object per job. Here is a real example from a production run:

```json
{
  "platform": "lever",
  "company": "spotify",
  "companySlug": "spotify",
  "leverRegion": "global",
  "id": "223f9722-3579-4ff2-b123-e4cc7b0c1a64",
  "jobId": "223f9722-3579-4ff2-b123-e4cc7b0c1a64",
  "title": "Art Director - Mexico",
  "url": "https://jobs.lever.co/spotify/223f9722-3579-4ff2-b123-e4cc7b0c1a64",
  "hostedUrl": "https://jobs.lever.co/spotify/223f9722-3579-4ff2-b123-e4cc7b0c1a64",
  "applyUrl": "https://jobs.lever.co/spotify/223f9722-3579-4ff2-b123-e4cc7b0c1a64/apply",
  "department": "Markets and Subscriber Growth",
  "team": "Marketing"
}
```

*Truncated — full records contain 60 fields. See Output fields for the complete schema.*

**[Try Lever Job Scraper [💰$0.13] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/lever-co-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.0045 |
| Result | $0.000126 |

See the [actor on Apify](https://apify.com/blackfalcondata/lever-co-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape jobs.lever.co?**
Use this actor on Apify to extract structured data from jobs.lever.co. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get jobs.lever.co data as JSON, CSV, or Excel?**
The actor writes each job to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape jobs.lever.co?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check jobs.lever.co's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each job gets a content hash. On subsequent runs, only new or changed jobs are emitted — saving time, compute, and storage. Expired jobs can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

- [Djinni Scraper](https://apify.com/blackfalcondata/djinni-scraper?fpr=1h3gvi) — Ukraine & CEE tech jobs with salary and English level
- [Work.ua Scraper](https://apify.com/blackfalcondata/work-ua-scraper?fpr=1h3gvi) — Ukraine's work.ua job listings
- [NoFluffJobs Scraper](https://apify.com/blackfalcondata/nofluffjobs-scraper?fpr=1h3gvi) — Poland & CEE IT jobs with transparent salary ranges
- [OLX Jobs Scraper](https://apify.com/blackfalcondata/olx-jobs-scraper?fpr=1h3gvi) — OLX job listings across 7 CEE countries
- [Prace.cz Scraper](https://apify.com/blackfalcondata/prace-scraper?fpr=1h3gvi) — Czech Republic's prace.cz job board
- [Profession.hu Scraper](https://apify.com/blackfalcondata/profession-scraper?fpr=1h3gvi) — Hungary's profession.hu job board

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Lever Job Scraper [💰$0.13]](https://apify.com/blackfalcondata/lever-co-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
