[Bluesky Scraper](https://apify.com/aurumworks/bluesky-scraper?fpr=data)

**Scrape Bluesky social network.** Search posts by keyword, get user profiles with follower counts, fetch user feeds, and extract post threads with replies. No login or API key needed.

## How to use

1. Click **Try for free**
2. Select a **Mode** — search posts, get a profile, fetch a user's feed, or get a post thread
3. Enter your search query or Bluesky handle
4. Click **Start** and download results as JSON, CSV, or Excel

## Modes

| Mode | What you get |
| --- | --- |
| **search_posts** | Search posts by keyword — text, likes, reposts, replies, images |
| **user_profile** | Profile details — bio, follower/following counts, post count, avatar |
| **user_feed** | A user's recent posts with engagement metrics |
| **post_thread** | A post and all its replies (up to 10 levels deep) |

## Input

| Field | Description | Default |
| --- | --- | --- |
| Mode | What to scrape | search_posts |
| Search Query | Keywords for post search | artificial intelligence |
| Handle | Bluesky handle for profile/feed | bsky.app |
| Post URI | AT URI for thread mode | — |
| Max Results | Maximum posts to fetch (1–500) | 50 |

## Output Examples

### Post

```
{
  "dataType": "search_result",
  "handle": "alice.bsky.social",
  "displayName": "Alice",
  "text": "Just tried the new Claude model and it's incredible...",
  "likeCount": 42,
  "repostCount": 12,
  "replyCount": 8,
  "createdAt": "2026-04-30T10:15:00.000Z",
  "images": [],
  "externalUrl": "https://example.com/article"
}
```

### Profile

```
{
  "dataType": "profile",
  "handle": "bsky.app",
  "displayName": "Bluesky",
  "description": "Social media as it should be.",
  "followersCount": 1500000,
  "followsCount": 50,
  "postsCount": 2500
}
```

## Cost

A typical run costs **$0.01–$0.03**. Lightweight API calls, no browser needed.

## Tips

- **Search operators**: Try specific phrases in quotes for exact matches
- **User feeds**: Great for monitoring competitors or influencers
- **Post threads**: Extract full conversations including nested replies
- **Schedule it**: Run daily to track trending topics or monitor brand mentions

## FAQ

**Is this legal?**

Yes. Bluesky is built on the AT Protocol, an open and decentralized protocol. All public posts are accessible through their official public API.

**Do I need a Bluesky account?**

No. This actor uses Bluesky's public API which doesn't require authentication.

**Can I scrape private/blocked content?**

No. Only public posts and profiles are accessible.