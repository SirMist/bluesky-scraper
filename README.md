[Bluesky Scraper](https://apify.com/sovereigntaylor/bluesky-scraper?fpr=data)

# Bluesky Social Scraper

Scrape posts, profiles, and engagement data from Bluesky Social (bsky.app). Built on the AT Protocol public API — no login required, no authentication tokens, no scraping workarounds.

## Why Bluesky?

Bluesky is the fastest-growing decentralized social network, built on the AT Protocol. Unlike Twitter/X, Bluesky exposes a **fully public API** that anyone can query without authentication. This makes it the most accessible social network for data collection, brand monitoring, and social intelligence.

## What It Does

This actor extracts structured data from Bluesky via two methods:

**Primary: AT Protocol Public API** (fast, reliable, structured)

- Profile data: display name, handle, DID, bio, follower/following counts, avatar
- Author feed: all posts from a user's timeline with full engagement metrics
- Search: find posts matching keywords, hashtags, or phrases

**Fallback: Web Scraping** (for edge cases when API is unavailable)

- CheerioCrawler-based extraction from bsky.app web pages
- DOM parsing with React hydration data extraction

### Post Data (per post)

| Field | Type | Description |
| --- | --- | --- |
| `author` | string | Display name of the post author |
| `handle` | string | Bluesky handle (e.g., jay.bsky.social) |
| `text` | string | Full post text content |
| `likes` | number | Like count |
| `reposts` | number | Repost count |
| `replies` | number | Reply count |
| `postedAt` | string | ISO 8601 timestamp |
| `images` | array | URLs of attached images |
| `url` | string | Direct web link to the post |
| `isReply` | boolean | Whether the post is a reply |
| `hashtags` | array | Hashtags extracted from rich text facets |
| `mentions` | array | Mentioned user DIDs |
| `links` | array | URLs mentioned in the post |
| `languages` | array | Language codes (e.g., ["en"]) |
| `externalLink` | object | Attached link card data (uri, title, description) |
| `quotedPost` | object | Quoted post summary (text, author, handle) |
| `isRepost` | boolean | Whether this is a repost by someone else |
| `authorFollowers` | number | Author's follower count at time of scraping |

### Profile Data (per handle)

| Field | Type | Description |
| --- | --- | --- |
| `handle` | string | Bluesky handle |
| `displayName` | string | Display name |
| `did` | string | Decentralized Identifier (DID) |
| `description` | string | Bio/description text |
| `followersCount` | number | Number of followers |
| `followsCount` | number | Number of accounts followed |
| `postsCount` | number | Total posts authored |
| `avatar` | string | Avatar image URL |
| `createdAt` | string | Account creation date |

## Features

- **No authentication needed** — Bluesky's AT Protocol API is public
- **Fast API-first approach** — direct XRPC calls, no browser rendering
- **Web fallback** — CheerioCrawler backup if API is unavailable
- **Automatic pagination** — follows cursors through all feed pages
- **Post deduplication** — tracks URIs to prevent duplicate entries
- **Rate limiting** — polite crawling with jitter and burst protection
- **Exponential backoff** — automatic retry with increasing delays
- **Reply filtering** — optionally exclude replies for cleaner data
- **Rich text parsing** — extracts hashtags, mentions, and links from facets
- **Image extraction** — collects all attached image URLs
- **Quote post detection** — identifies and extracts quoted post content
- **Repost detection** — identifies reposts with original author attribution
- **Proxy support** — configurable proxy for high-volume runs
- **Progress tracking** — periodic progress logs with stats
- **Run summary** — final summary record in the dataset

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `profileHandles` | array | `[]` | Bluesky @handles to scrape (e.g., jay.bsky.social) |
| `searchTerms` | array | `[]` | Keywords to search for in posts |
| `maxPosts` | integer | `200` | Maximum total posts to scrape (0 = unlimited) |
| `includeReplies` | boolean | `false` | Include reply posts in results |
| `proxy` | object | - | Proxy configuration for rate limit avoidance |

### Example: Scrape Profiles

```
{
  "profileHandles": [
    "jay.bsky.social",
    "pfrazee.com",
    "bsky.app"
  ],
  "maxPosts": 500,
  "includeReplies": false
}
```

### Example: Search Posts

```
{
  "searchTerms": [
    "artificial intelligence",
    "#buildinpublic",
    "startup funding"
  ],
  "maxPosts": 1000
}
```

### Example: Combined (Profiles + Search)

```
{
  "profileHandles": ["jay.bsky.social"],
  "searchTerms": ["bluesky api", "AT Protocol"],
  "maxPosts": 300,
  "includeReplies": true
}
```

## Output

### Post Record

```
{
  "type": "post",
  "author": "Jay Graber",
  "handle": "jay.bsky.social",
  "text": "Excited to share our latest protocol update! The AT Protocol now supports...",
  "likes": 1523,
  "reposts": 412,
  "replies": 89,
  "postedAt": "2026-02-28T18:30:00.000Z",
  "images": [
    "https://cdn.bsky.app/img/feed_fullsize/plain/did:plc:xxx/bafkrei..."
  ],
  "url": "https://bsky.app/profile/jay.bsky.social/post/3kmxxxxxx",
  "isReply": false,
  "hashtags": ["ATProtocol", "decentralized"],
  "mentions": [],
  "links": ["https://atproto.com/blog/update"],
  "languages": ["en"],
  "externalLink": {
    "uri": "https://atproto.com/blog/update",
    "title": "AT Protocol Update",
    "description": "Latest changes to the AT Protocol specification."
  },
  "quotedPost": null,
  "isRepost": false,
  "authorFollowers": 125000,
  "scrapedAt": "2026-03-01T10:00:00.000Z"
}
```

### Profile Record

```
{
  "type": "profile",
  "handle": "jay.bsky.social",
  "displayName": "Jay Graber",
  "did": "did:plc:oky5czdrnfjpqslsw2a5iclo",
  "description": "CEO @bluesky. Building the AT Protocol.",
  "avatar": "https://cdn.bsky.app/img/avatar/plain/did:plc:xxx/bafkrei...",
  "followersCount": 125000,
  "followsCount": 1200,
  "postsCount": 3400,
  "createdAt": "2023-04-01T00:00:00.000Z",
  "url": "https://bsky.app/profile/jay.bsky.social",
  "scrapedAt": "2026-03-01T10:00:00.000Z"
}
```

### Run Summary Record

```
{
  "type": "runSummary",
  "totalPostsSaved": 500,
  "profilesScraped": 3,
  "searchResultsScraped": 200,
  "handlesCompleted": ["jay.bsky.social", "pfrazee.com"],
  "searchesCompleted": ["AT Protocol"],
  "duplicatesSkipped": 12,
  "errors": 0,
  "elapsedSeconds": 45.3,
  "apiRequests": 28
}
```

## Use Cases

- **Social Monitoring** — Track mentions of your brand, product, or competitors on Bluesky
- **Brand Tracking** — Monitor what key influencers and thought leaders are posting
- **Trend Analysis** — Identify trending topics, hashtags, and conversations
- **Sentiment Analysis** — Feed post text into NLP models for sentiment classification
- **Market Research** — Understand what your target audience discusses and shares
- **Competitive Intelligence** — Track competitor activity and engagement metrics
- **Content Strategy** — Discover what content gets the most engagement
- **Influencer Discovery** — Find high-engagement accounts in your niche
- **Academic Research** — Collect social data for studies on decentralized networks
- **Crisis Monitoring** — Real-time tracking of conversations around events or issues

## Technical Details

- **Runtime**: Node.js 18 on Apify platform
- **Primary method**: AT Protocol XRPC public API (no auth required)
- **Fallback method**: CheerioCrawler for bsky.app web pages
- **Rate limiting**: 200-1500ms between API calls, burst cooldowns every 10 requests
- **Retries**: 5 automatic retries with exponential backoff
- **Deduplication**: URI-based tracking prevents duplicate posts
- **Memory**: ~256 MB recommended for typical runs

### AT Protocol API Endpoints Used

| Endpoint | Purpose |
| --- | --- |
| `app.bsky.actor.getProfile` | Fetch user profile data |
| `app.bsky.feed.getAuthorFeed` | Fetch posts from a user's feed |
| `app.bsky.feed.searchPosts` | Search posts by keyword |
| `com.atproto.identity.resolveHandle` | Resolve handle to DID |

All endpoints are on the public relay at `https://public.api.bsky.app/xrpc/` and require no authentication.

## Pricing (Pay-Per-Event)

This actor uses Apify's pay-per-event model:

- **post-scraped**: $0.003 per post extracted

You set a maximum budget per run, and the actor will never exceed it. Profile records and the run summary are included free.

## How to Run

### On Apify Platform

1. Go to the actor page on Apify Store
2. Click "Start" or "Try for free"
3. Enter profile handles or search terms
4. Set max posts and reply preference
5. Click "Run"
6. Download results as JSON, CSV, or Excel

### Locally

```
# Clone the repository
git clone <repo-url>
cd bluesky-scraper

# Install dependencies
npm install

# Create input file
mkdir -p ./storage/key_value_stores/default
echo '{"profileHandles": ["jay.bsky.social"], "maxPosts": 20}' > ./storage/key_value_stores/default/INPUT.json

# Run
npm start
```

### Via Apify API

```
curl -X POST "https://api.apify.com/v2/acts/<ACTOR_ID>/runs" \
  -H "Authorization: Bearer <YOUR_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
    "profileHandles": ["jay.bsky.social"],
    "searchTerms": ["AT Protocol"],
    "maxPosts": 100,
    "includeReplies": false
  }'
```

## Limitations

- The AT Protocol public API may rate-limit high-volume requests. Use Apify proxies and reasonable `maxPosts` values.
- Search results are limited by the Bluesky search index. Very recent posts may not appear immediately.
- Web fallback extraction is less reliable than the API method and may miss engagement metrics.
- Bluesky's web app uses React SSR, so DOM structure may change over time.
- Private/blocked accounts may return limited or no data.

## Comparison with Twitter/X Scraping

| Feature | Bluesky Scraper | Twitter/X Scraper |
| --- | --- | --- |
| Authentication | None required | API keys or login |
| Rate limits | Generous public API | Strict, paid tiers |
| Data access | Full post + profile | Limited by API tier |
| Cost | PPE only | API subscription + PPE |
| Reliability | High (open protocol) | Varies (frequent changes) |

## Support

Built by Sovereign AI. For issues, feature requests, or custom scraping needs:

- Email: [ricardo.yudi@gmail.com](mailto:ricardo.yudi@gmail.com)
- GitHub: [https://github.com/ryudi84](https://github.com/ryudi84)

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/bluesky-scraper").call(run_input={
    "searchTerm": "bluesky",
    "maxResults": 50
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item.get('title', item.get('name', 'N/A'))}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/bluesky-scraper').call({
    searchTerm: 'bluesky',
    maxResults: 50
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(item.title || item.name || 'N/A'));
```