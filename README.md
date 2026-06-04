[Bluesky Scraper](https://apify.com/junipr/bluesky-scraper?fpr=data)

# Bluesky Scraper

## What does Bluesky Scraper do?

Bluesky Scraper extracts posts, profiles, search results, and full threads from the Bluesky social network using the public AT Protocol API. It collects structured data including post text, engagement metrics (likes, reposts, replies, quotes), embedded media, author information, and direct web URLs. No login or authentication is required since the actor uses Bluesky's public API endpoints.

Whether you need to monitor brand mentions, analyze trending topics, research competitor activity, or build a dataset of public Bluesky content, this actor handles pagination automatically and delivers clean, structured JSON output ready for analysis or integration.

## Features

- **Four scrape modes** — Fetch user posts, profiles, search results, or entire post threads
- **Batch handle support** — Scrape multiple Bluesky accounts in a single run
- **Full engagement metrics** — Likes, reposts, replies, and quote counts for every post
- **Embedded content detection** — Identifies images, links, videos, and quoted records with URLs
- **Profile data** — Follower/following counts, post counts, bios, avatar and banner URLs
- **Content labels** — Captures moderation labels applied to posts
- **Language detection** — Returns the primary language tag for each post
- **Direct web URLs** — Every post includes a clickable bsky.app link
- **Configurable pagination** — Set max results from 1 to 10,000 per handle or query
- **Rate limit protection** — Adjustable request delay to avoid API throttling
- **Pay-per-event pricing** — Only pay for the items you actually scrape

## Input Configuration

```
{
  "scrapeType": "posts",
  "handles": ["bsky.app", "jay.bsky.team"],
  "searchQuery": "",
  "threadUri": "",
  "maxResults": 100,
  "includeReplies": true,
  "includeReposts": true,
  "maxConcurrency": 5,
  "requestDelay": 500
}
```

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `scrapeType` | string | `"posts"` | What to scrape: `posts`, `profile`, `search`, or `thread` |
| `handles` | string[] | `["bsky.app"]` | Bluesky handles to scrape (for `posts` and `profile` modes) |
| `searchQuery` | string | `""` | Search query (for `search` mode only) |
| `threadUri` | string | `""` | AT Protocol URI of the thread (for `thread` mode only) |
| `maxResults` | integer | `100` | Maximum items to scrape per handle/query (1-10,000) |
| `includeReplies` | boolean | `true` | Include replies in the user feed (`posts` mode) |
| `includeReposts` | boolean | `true` | Include reposts in the user feed (`posts` mode) |
| `maxConcurrency` | integer | `5` | Maximum concurrent API requests (1-10) |
| `requestDelay` | integer | `500` | Delay between requests in milliseconds (minimum 100) |

## Output Format

Each post item in the dataset looks like this:

```
{
  "type": "post",
  "uri": "at://did:plc:abc123/app.bsky.feed.post/xyz789",
  "cid": "bafyreiabc123",
  "author": {
    "handle": "bsky.app",
    "displayName": "Bluesky",
    "avatar": "https://cdn.bsky.app/img/avatar/plain/..."
  },
  "text": "Hello, Bluesky!",
  "createdAt": "2025-01-15T12:00:00.000Z",
  "likeCount": 42,
  "repostCount": 10,
  "replyCount": 5,
  "quoteCount": 3,
  "embedType": "image",
  "embedUrl": "https://cdn.bsky.app/img/feed_fullsize/...",
  "labels": [],
  "language": "en",
  "url": "https://bsky.app/profile/bsky.app/post/xyz789"
}
```

Profile items return:

```
{
  "type": "profile",
  "handle": "bsky.app",
  "did": "did:plc:abc123",
  "displayName": "Bluesky",
  "description": "The official Bluesky account.",
  "avatar": "https://cdn.bsky.app/img/avatar/plain/...",
  "banner": "https://cdn.bsky.app/img/banner/plain/...",
  "followersCount": 100000,
  "followsCount": 500,
  "postsCount": 1200,
  "createdAt": "2023-04-01T00:00:00.000Z"
}
```

## Usage Examples / Use Cases

- **Brand monitoring** — Track mentions of your brand or product by searching for keywords across all public Bluesky posts
- **Influencer research** — Pull profile data and post history for multiple accounts to compare follower counts, engagement rates, and posting frequency
- **Content analysis** — Collect posts about a trending topic to analyze sentiment, language distribution, and media usage patterns
- **Thread archiving** — Save complete threads with all replies for research, compliance, or record-keeping
- **Competitive intelligence** — Monitor competitor accounts to track their messaging, engagement, and posting cadence
- **Academic research** — Build structured datasets of public social media content for linguistic, sociological, or network analysis

## FAQ

### Does this actor require a Bluesky account or login?

No. Bluesky Scraper uses the public AT Protocol API (`public.api.bsky.app`), which does not require authentication. All data accessed is publicly available content.

### What is the thread URI format?

Thread URIs follow the AT Protocol format: `at://did:plc:XXXXXXX/app.bsky.feed.post/XXXXXXX`. You can find this by looking at a post's URL on bsky.app and converting it, or by using the `posts` scrape mode to collect URIs first.

### How many posts can I scrape?

You can scrape up to 10,000 items per handle or search query in a single run. For larger datasets, run the actor multiple times with different handles or queries. The actor handles pagination automatically.

### Will I get rate limited?

The actor includes a configurable `requestDelay` (default 500ms) to stay within Bluesky's API rate limits. If you experience rate limiting, increase the delay to 1000ms or higher. The public API is generous but does enforce limits on rapid requests.

### Can I filter out replies and reposts?

Yes. Set `includeReplies` to `false` to exclude replies and `includeReposts` to `false` to exclude reposts. This only applies to `posts` mode when scraping a user's feed.

## Related Actors

- [Reddit Scraper](https://apify.com/junipr/reddit-scraper) — Scrape posts and comments from Reddit subreddits and threads
- [Hacker News Scraper](https://apify.com/junipr/hacker-news-scraper) — Extract stories and comments from Hacker News
- [Google News Scraper](https://apify.com/junipr/google-news-scraper) — Collect news articles from Google News by topic or query
- [Product Hunt Scraper](https://apify.com/junipr/product-hunt-scraper) — Scrape product launches, upvotes, and reviews from Product Hunt
- [Contact Info Scraper](https://apify.com/junipr/contact-info-scraper) — Extract emails, phones, and social media links from any website