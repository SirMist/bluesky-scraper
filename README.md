[Bluesky Scraper](https://apify.com/s0rgcl/bluesky-scraper?fpr=data)

# Bluesky Scraper — All-in-One Posts, Profiles, Followers & Search

The most complete Bluesky scraper on Apify. Search posts, extract profiles, track followers, analyze engagement — all in one Actor. No authentication required for public data. MCP server included for AI agents.

## 🚀 Why This Scraper?

Stop using 5 different scrapers for Bluesky. This single Actor replaces them all:

| Feature | This Actor | Others |
| --- | --- | --- |
| Search posts by keyword | ✅ | ✅ (separate actor) |
| Search users | ✅ | ✅ (separate actor) |
| Get user profiles | ✅ | ❌ |
| Get user posts/feed | ✅ | ✅ (separate actor) |
| Get followers | ✅ | ✅ (separate actor, $17.99/mo) |
| Get following | ✅ | ❌ |
| Get post threads | ✅ | ❌ |
| Get post engagement (likes, reposts, quotes) | ✅ | ❌ |
| Profile analytics | ✅ | ❌ |
| MCP server for AI agents | ✅ | ❌ (or $49/mo) |
| **Price** | **$1/1,000 results** | **$17.99-$49/mo fixed** |

## 💰 Pricing

**Pay only for what you use.** No monthly fees, no subscriptions.

- **$1.00 per 1,000 results** — the cheapest Bluesky scraper on Apify
- 100 results = $0.10
- 10,000 results = $10.00
- Free to try with Apify's free tier

## 📋 Features

### 8 Scraping Modes

1. **Search Posts** — Find posts by keyword, hashtag, or phrase with date/language filters
2. **Search Users** — Find Bluesky users by name or keyword
3. **Get Profile** — Extract complete profile data including bio, stats, and avatar
4. **Get User Posts** — Extract a user's recent posts with engagement metrics
5. **Get Followers** — Get the list of followers for any public account
6. **Get Following** — Get the list of accounts a user follows
7. **Get Post Thread** — Extract full conversation threads with all replies
8. **Get Post Engagement** — Get the users who liked, reposted, or quoted a post

### Key Capabilities

- No authentication required — all public data, no API keys needed
- Automatic pagination — get up to 10,000 results per run
- Rate limiting built-in — respects Bluesky API limits automatically
- Clean, consistent output — every result has the same structure
- Batch support — process multiple handles or post URIs in one run
- MCP server — connect directly to Claude, Cursor, or any MCP-compatible AI

## 📖 Input Examples

### Search Posts

```
{
  "mode": "search-posts",
  "query": "artificial intelligence",
  "sort": "top",
  "limit": 500,
  "language": "en",
  "since": "2025-01-01",
  "until": "2025-12-31"
}
```

### Get User Profile

```
{
  "mode": "get-profile",
  "handles": ["jay.bsky.team", "pfrazee.com"]
}
```

### Get User Posts

```
{
  "mode": "get-user-posts",
  "handles": ["jay.bsky.team"],
  "limit": 200,
  "includeReplies": false
}
```

### Get Followers

```
{
  "mode": "get-followers",
  "handles": ["jay.bsky.team"],
  "limit": 1000
}
```

### Get Following

```
{
  "mode": "get-following",
  "handles": ["jay.bsky.team"],
  "limit": 500
}
```

### Search Users

```
{
  "mode": "search-users",
  "query": "machine learning researcher",
  "limit": 100
}
```

### Get Post Thread

```
{
  "mode": "get-post-thread",
  "postUris": ["at://did:plc:ragtjsm2j2vknwkz3zp4oxrd/app.bsky.feed.post/3l2s5xxv2ze2c"],
  "threadDepth": 20
}
```

### Get Post Engagement

```
{
  "mode": "get-post-engagement",
  "postUris": ["at://did:plc:ragtjsm2j2vknwkz3zp4oxrd/app.bsky.feed.post/3l2s5xxv2ze2c"],
  "limit": 500
}
```

## 📊 Output Examples

### Post Output

```
{
  "uri": "at://did:plc:ragtjsm2j2vknwkz3zp4oxrd/app.bsky.feed.post/3l2s5xxv2ze2c",
  "url": "https://bsky.app/profile/jay.bsky.team/post/3l2s5xxv2ze2c",
  "author": {
    "handle": "jay.bsky.team",
    "displayName": "Jay Graber",
    "did": "did:plc:ragtjsm2j2vknwkz3zp4oxrd",
    "avatar": "https://cdn.bsky.app/img/avatar/...",
    "followersCount": 350000,
    "followsCount": 1200,
    "postsCount": 5400
  },
  "text": "Excited to announce new features for Bluesky...",
  "createdAt": "2025-06-15T10:30:00.000Z",
  "likes": 4200,
  "reposts": 890,
  "replies": 312,
  "quotes": 45,
  "tags": ["bluesky", "atprotocol"],
  "language": "en",
  "hasImages": true,
  "hasVideo": false,
  "images": [
    {
      "url": "https://cdn.bsky.app/img/feed_fullsize/...",
      "alt": "Screenshot of new feature"
    }
  ],
  "embed": null,
  "isReply": false,
  "isRepost": false
}
```

### Profile Output

```
{
  "did": "did:plc:ragtjsm2j2vknwkz3zp4oxrd",
  "handle": "jay.bsky.team",
  "displayName": "Jay Graber",
  "description": "CEO @bluesky. Building decentralized social media.",
  "avatar": "https://cdn.bsky.app/img/avatar/...",
  "banner": "https://cdn.bsky.app/img/banner/...",
  "followersCount": 350000,
  "followsCount": 1200,
  "postsCount": 5400,
  "url": "https://bsky.app/profile/jay.bsky.team",
  "createdAt": "2023-04-01T00:00:00.000Z",
  "indexedAt": "2025-06-15T10:30:00.000Z",
  "labels": []
}
```

### Follower Output

```
{
  "did": "did:plc:xyz123",
  "handle": "user.bsky.social",
  "displayName": "User Name",
  "avatar": "https://cdn.bsky.app/img/avatar/...",
  "followersCount": 1234,
  "followsCount": 567,
  "postsCount": 890,
  "url": "https://bsky.app/profile/user.bsky.social",
  "description": "Tech enthusiast and developer"
}
```

## 🤖 MCP Server Setup

This Actor includes a built-in MCP (Model Context Protocol) server, allowing AI agents like Claude and Cursor to interact with Bluesky data directly.

### For Claude Desktop

Add to your `claude_desktop_config.json`:

```
{
  "mcpServers": {
    "bluesky": {
      "type": "url",
      "url": "https://bluesky-scraper.apify.actor/mcp"
    }
  }
}
```

### For Cursor

Add to your MCP settings:

```
{
  "mcpServers": {
    "bluesky": {
      "type": "url",
      "url": "https://bluesky-scraper.apify.actor/mcp"
    }
  }
}
```

### Available MCP Tools

| Tool | Description |
| --- | --- |
| `search_posts` | Search Bluesky posts by keyword |
| `get_profile` | Get a user's profile data |
| `get_user_posts` | Get recent posts from a user |
| `get_followers` | Get a user's followers |
| `get_following` | Get who a user follows |
| `get_post_thread` | Get a full post thread |
| `get_post_engagement` | Get likes, reposts, quotes |
| `search_users` | Search for users |
| `analyze_profile` | Full profile analysis with metrics |

## 🎯 Use Cases

- **Social Listening** — Monitor brand mentions, hashtags, and trending topics on Bluesky
- **Competitor Analysis** — Track competitor accounts, their engagement, and content strategy
- **Lead Generation** — Find potential customers by searching for relevant keywords and profiles
- **Market Research** — Analyze sentiment and trends in specific industries or topics
- **Influencer Discovery** — Find influential users by follower count and engagement rates
- **Content Research** — Discover top-performing content in your niche
- **Trend Tracking** — Monitor emerging trends on the decentralized social web
- **Academic Research** — Study social dynamics on the AT Protocol ecosystem
- **Journalism** — Monitor news, public figures, and breaking stories on Bluesky

## ⚙️ Technical Details

- Uses the public Bluesky API (AT Protocol) — no authentication required for public data
- Built-in rate limiting (token bucket algorithm) to respect API limits
- Automatic retries with exponential backoff for transient errors
- Cursor-based pagination for complete data extraction
- Clean TypeScript codebase with strict type checking

## 📝 Notes

- This scraper only accesses **publicly available data** on Bluesky
- No authentication credentials are needed or stored
- Rate limits are respected automatically — the scraper throttles requests to avoid hitting API limits
- Handles can be in the format `user.bsky.social` or custom domains like `user.com`
- Post URIs use the AT Protocol format: `at://did:plc:xxx/app.bsky.feed.post/xxx`

## 🔗 Resources

- [Bluesky](https://bsky.app) — The social network
- [AT Protocol Documentation](https://atproto.com/docs) — The underlying protocol
- [Bluesky API Reference](https://docs.bsky.app/docs/category/http-reference) — API documentation
- [Apify Platform](https://apify.com/) — The platform powering this scraper