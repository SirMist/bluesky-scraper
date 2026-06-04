[Bluesky Scraper](https://apify.com/knotless_cadence/bluesky-scraper?fpr=data)

# Bluesky Scraper — AT Protocol API, No Login Required

Production-grade Bluesky scraper using the **official AT Protocol** (`public.api.bsky.app`). Profile + author-feed scraping needs zero authentication; keyword search uses Bluesky App Password.

## Why Bluesky data?

Bluesky has grown from ~10M to ~32M users since the open-public launch. Built on the open AT Protocol, it's one of the few major social networks where public posts and profile data are exposed via a free, official API — no anti-bot, no rate limit on public endpoints for moderate workloads, no HTML drift.

## Why this scraper

- ✅ **Official AT Protocol** — `com.atproto.identity.resolveHandle` → `app.bsky.actor.getProfile` → `app.bsky.feed.getAuthorFeed`. No HTML parsing.
- ✅ **No login for profile + author-feed scraping** — public endpoints work without credentials.
- ✅ **Search support** with Bluesky App Password (App Passwords are revocable, not your main password).
- ✅ **Cursor-based pagination** — automatic, walks the entire timeline up to `maxPostsPerSource`.
- ✅ **Tested in production** — 23+ runs on Apify Cloud, no anti-bot incidents.

## Output Data — Profile (12 fields)

```
{
  "_type": "PROFILE",
  "did": "did:plc:z72i7hdynmk6r22z27h6tvur",
  "handle": "bsky.app",
  "displayName": "Bluesky",
  "description": "see what's next",
  "avatar": "https://cdn.bsky.app/img/avatar/...",
  "banner": "https://cdn.bsky.app/img/banner/...",
  "followersCount": 3242017,
  "followsCount": 4,
  "postsCount": 725,
  "createdAt": "2023-04-12T04:53:57.057Z",
  "scrapedAt": "2026-04-29T12:30:00.000Z"
}
```

## Output Data — Post (24 fields)

```
{
  "_type": "POST",
  "source": "profile:bsky.app",
  "scrapedAt": "2026-04-29T12:30:00.000Z",
  "uri": "at://did:plc:.../app.bsky.feed.post/3kqxxxxxxx",
  "cid": "bafyrei...",
  "author": {
    "did": "did:plc:z72i7hdynmk6r22z27h6tvur",
    "handle": "bsky.app",
    "displayName": "Bluesky"
  },
  "text": "Welcome to Bluesky!",
  "createdAt": "2026-03-14T01:56:08.229Z",
  "indexedAt": "2026-03-14T01:56:09.123Z",
  "likeCount": 843,
  "repostCount": 77,
  "replyCount": 77,
  "quoteCount": 59,
  "hasImages": false,
  "hasVideo": false,
  "hasLink": true,
  "externalLink": "https://bsky.social",
  "externalTitle": "Bluesky Social",
  "labels": [],
  "languages": ["en"],
  "hashtags": ["#bluesky"],
  "mentions": ["did:plc:..."],
  "isReply": false,
  "parentUri": null
}
```

Field reference (full): `_type, source, scrapedAt, uri, cid, author{did, handle, displayName}, text, createdAt, indexedAt, likeCount, repostCount, replyCount, quoteCount, hasImages, hasVideo, hasLink, externalLink, externalTitle, labels, languages, hashtags, mentions, isReply, parentUri`.

## Use Cases

- **Brand monitoring** — track mentions of your brand on Bluesky
- **Sentiment analysis** — analyze public opinion on trending topics
- **Influencer research** — find Bluesky accounts by follower count + engagement
- **AI training data** — build NLP datasets from public Bluesky conversations
- **Competitive intelligence** — monitor competitor handles + their posting cadence
- **Migration analysis** — track Twitter/X-to-Bluesky cross-posting patterns
- **Academic research** — study decentralized social networks

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `handles` | Array | `[]` | Bluesky handles to scrape (e.g., `bsky.app`, `jay.bsky.team`) |
| `searchQueries` | Array | `[]` | Keyword search across all of Bluesky (requires credentials) |
| `maxPostsPerSource` | Number | `100` | Max posts collected per handle or per query |
| `includeLikes` | Boolean | `false` | (reserved) — placeholder for future like-feed support |
| `includeReposts` | Boolean | `false` | (reserved) — placeholder for future repost-feed support |
| `blueskyHandle` | String | — | Your Bluesky handle (required only for search) |
| `blueskyPassword` | String | — | App Password from `bsky.app/settings/app-passwords` (required only for search) |

## How It Works

1. **Profile + author-feed** (no auth): resolve handle → DID → fetch profile → walk author feed via cursor pagination.
2. **Keyword search** (auth required): `com.atproto.server.createSession` → bearer token → `app.bsky.feed.searchPosts` with cursor pagination.

## Step-by-Step

### 1. Open the actor

[apify.com/knotless_cadence/bluesky-scraper](https://apify.com/knotless_cadence/bluesky-scraper) → "Try for free."

### 2. Provide handles (no auth)

```
{
  "handles": ["bsky.app", "jay.bsky.team"],
  "maxPostsPerSource": 50
}
```

### 3. Or run a search (App Password)

```
{
  "searchQueries": ["llm", "rag"],
  "maxPostsPerSource": 100,
  "blueskyHandle": "you.bsky.social",
  "blueskyPassword": "abcd-1234-..."
}
```

### 4. Results

Profile JSON (1 record per handle, `_type: PROFILE`) plus post JSON (`_type: POST`, full 24-field schema above) emitted to the Apify dataset.

## Pricing

- Standard Apify per-run compute pricing — no per-post or per-profile fee.
- **No proxy required** — public AT Protocol endpoints are not currently anti-bot gated for moderate volume. AT Protocol response sizes are small (~1-3 KB per post), so compute consumption is low.
- Heavier search jobs (auth-required) trade compute for credential rate-limits — see Bluesky's App Password rate guidance if running >1000 search posts per day.

## Honest Limitations

- **`hashtags` extraction is ASCII-word regex (`/#\w+/g`)** — `\w` only matches `[A-Za-z0-9_]`, so non-ASCII hashtags (`#искусственныйинтеллект`, `#人工知能`, `#café`) are NOT captured. If Unicode hashtags matter for your dataset, post-process the `text` field with a Unicode-aware tokenizer.
- **`hasImages` / `hasVideo` / `hasLink` are exclusive** (`===` on `record.embed.$type`). A post using `app.bsky.embed.recordWithMedia` (quote-post with attached media) will have all three flags FALSE — the embed type is `recordWithMedia`, not `images`/`video`/`external`. Same for `app.bsky.embed.record` (pure quote posts).
- **`mentions` extracts only `f.features[0]?.did`** — the FIRST feature in each facet, not all features. Mentions inside a single facet beyond the first are silently lost. In practice, Bluesky places one mention per facet, so impact is minimal — but it is not a complete extraction.
- **Cursor pagination is best-effort.** If `feed.cursor` is missing or null, iteration stops — even if `collected < maxPostsPerSource`. The actor returns whatever it managed to collect; it does not retry the cursor request.
- **Author-feed endpoint** (`app.bsky.feed.getAuthorFeed`) returns posts AND reposts in chronological order. The actor does NOT filter reposts out by default — `isReply` is set, but there is no `isRepost` field in the schema. If you need only original posts, filter on `record.text !== ''` and absence of repost markers downstream.
- **Search requires App Password.** The `bsky.social` auth endpoint is rate-limited per account. Heavy search workloads from a single App Password may receive HTTP 429.
- **No retry logic.** A transient 5xx during cursor pagination ends the loop early for that handle/query.

**Proof of delivery**: This Bluesky scraper has **25 lifetime production runs** as of May 2026. Author maintains 31 published actors (78 total) and shipped a paid 3-article series in March 2026 ($150, proxy industry). Pilot pricing locked through **May 2026**.

**Sample request?** Reply `sample` to [spinov001@gmail.com](mailto:spinov001@gmail.com) and we'll send 2 published case-study articles within 24 hours.

## Custom scraping — pricing

Need data from a different network or in a custom schema? **One-shot pilot tiers:**

- **Pilot — $97**: 1 actor, basic config, 7-day support. Perfect for proof-of-concept.
- **Standard — $297**: custom actor + Slack/email alerts on results, 30-day support. Most clients.
- **Premium — $797**: custom actor + dashboard + 90-day support + 1 modification round.

Email **[spinov001@gmail.com](mailto:spinov001@gmail.com)** with the source URL + the fields you need. Typical turnaround: 48 hours.

## Related actors (verified live)

- [Walmart Reviews Scraper](https://apify.com/knotless_cadence/walmart-reviews-scraper) — Product reviews to CSV/JSON/Excel, 17 fields per review, bypasses Walmart's 100-review UI cap
- [Reddit Discussion Scraper](https://apify.com/knotless_cadence/reddit-discussion-scraper) — 82 runs, 20-field post schema
- [YouTube Comments Scraper](https://apify.com/knotless_cadence/youtube-comments-scraper) — comment threads + replies
- [Trustpilot Review Scraper](https://apify.com/knotless_cadence/trustpilot-review-scraper) — 951 production runs
- [Google News Scraper](https://apify.com/knotless_cadence/google-news-scraper) — RSS + HTML fallback

---

**Proof of work:** [31 public actors on Apify Store](https://apify.com/knotless_cadence) (78 total in portfolio). Production-tested: Trustpilot 951 / Reddit 82 / Google News 45 / Glassdoor 39 / Email Extractor 107 / Hacker News 27 / Bluesky 25.

**More tips:** [t.me/scraping_ai](https://t.me/scraping_ai)

---

### Honest disclosure

- This actor uses the **public Bluesky AT Protocol API** — not HTML scraping. Profile + author-feed endpoints are documented as public; search requires user authentication.
- Output fields reflect what `extractPostData()` and `getProfile()` actually push. No fabricated fields.
- Bluesky-related actors mentioned in earlier README versions (`bluesky-feed-monitor`, `bluesky-hashtag-tracker`, `bluesky-profile-batch`) are **not currently public** — only this scraper is live in the Apify Store. Removed dead links.
- Provided App Passwords are sent only to Bluesky's own auth endpoint (`bsky.social`); the actor does not log or persist them.
- Not affiliated with Bluesky Social PBC or the AT Protocol team.