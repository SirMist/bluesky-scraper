[Bluesky Scraper](https://apify.com/diverse_venture/bluesky-scraper?fpr=data)

The most comprehensive Bluesky scraper on Apify. Extract profiles, posts, engagement data, and search for users — all via the open AT Protocol API.

**No login or API key required.** Bluesky's AT Protocol is designed for open data access.

## Features

- **Profile scraping**: Followers, following, post count, bio, avatar, labels
- **Post scraping**: Full text, likes, reposts, replies, quotes, images, links
- **User search**: Find accounts by keyword with full profile data
- **Engagement analytics**: Total engagement scores per post
- **Pagination**: Automatically pages through results up to your limit
- **Export**: JSON, CSV, XML, or Excel

## Use cases

- **Social listening**: Monitor what people say about your brand on Bluesky
- **Influencer research**: Find and analyze Bluesky influencers by topic
- **Competitor analysis**: Track competitor accounts and their engagement
- **Academic research**: Study social network dynamics on decentralized platforms
- **Journalism**: Find sources and track public discourse
- **Marketing**: Identify trending topics and influential voices

## Modes

### 1. Profiles

Get detailed profile data for specific Bluesky handles.

```
{
  "mode": "profiles",
  "handles": ["jay.bsky.team", "nytimes.com", "bsky.app"]
}
```

### 2. Posts

Get recent posts with full engagement data.

```
{
  "mode": "posts",
  "handles": ["jay.bsky.team"],
  "maxPostsPerUser": 50
}
```

### 3. Search

Find users by keyword.

```
{
  "mode": "search",
  "searchQuery": "artificial intelligence",
  "maxSearchResults": 50
}
```

## Output example

```
{
  "type": "profile",
  "handle": "jay.bsky.team",
  "displayName": "Jay",
  "followersCount": 596185,
  "followsCount": 3964,
  "postsCount": 4076,
  "description": "Founder & Chief Innovation Officer @ Bluesky"
}
```

## Cost

Uses only lightweight API calls — no browser automation. A typical run completes in seconds and costs less than $0.005 in Apify credits.