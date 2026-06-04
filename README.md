[Bluesky Scraper](https://apify.com/janbruinier/bluesky-scraper?fpr=data)

Scrapes posts, profiles, and feeds from Bluesky social network. Extracts post text, likes, reposts, replies, author info, timestamps, and media links.

## Features

- Extract posts, profiles, engagement metrics, and media from Bluesky Social
- Export to JSON, CSV, Excel, and other formats
- Configurable result limits and pagination
- Proxy support for reliable scraping
- Pay-per-result pricing with free tier (50 results free per run)

## Input Parameters

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `search_queries` | array | No | `["python"]` | List of search queries to find posts on Bluesky (e.g. 'artificial intelligence', 'python programming'). |
| `profile_handles` | array | No | - | List of Bluesky handles to scrape profiles and feeds from (e.g. 'jay.bsky.team', 'bsky.app'). |
| `max_posts` | integer | No | `100` | Maximum number of posts to scrape per query or profile feed. |
| `include_replies` | boolean | No | `false` | Whether to include reply posts in search results and feeds. |

## Output Example

```
{
  "author": "username",
  "text": "Post content...",
  "likes": 42,
  "reposts": 7,
  "replies": 3,
  "timestamp": "2025-01-15T10:30:00Z",
  "url": "https://example.com/post/123"
}
```

## Cost Calculator

| Results | Cost |
| --- | --- |
| 50 | Free |
| 1,000 | $0.75 |
| 10,000 | $7.50 |
| 100,000 | $75.00 |

*Plus $0.005 per actor run. First 50 results per run are free.*

## Use Cases

- Social listening and brand monitoring
- Influencer research and audience analysis
- Trend detection and hashtag tracking
- Content performance benchmarking
- Community sentiment analysis

## Limitations

- Results depend on Bluesky Social's availability and structure
- Some pages may require residential proxies for reliable access
- Rate limiting may apply for very large scrapes
- Website layout changes may temporarily affect data extraction

## Changelog

- **v0.1** - Initial release