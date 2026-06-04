[Bluesky Scraper](https://apify.com/adrianreinag/bluesky-scraper?fpr=data)

# 🦋 Bluesky Scraper — Posts, Profiles, Threads & Followers

[![Apify Store](https://img.shields.io/badge/Apify-Store-blue)](https://apify.com/)
[![Node.js](https://img.shields.io/badge/Node.js-20+-green)](https://nodejs.org)
[![AT Protocol](https://img.shields.io/badge/AT%20Protocol-Public%20API-purple)](https://atproto.com)

The most complete Bluesky scraper on Apify Store. Extract posts, user profiles, full conversation threads, and follower/following lists from [Bluesky](https://bsky.app) — the decentralized social network with 30M+ users.

⚡ **No browser needed.** Pure API calls via the open AT Protocol.

🔓 **No auth required** for profiles and feeds.

💰 **From $0.002/result** — the best price on the store.

---

## 🚀 Quick Start

1. Choose a **mode** (profiles/feeds need NO auth)
2. Add Bluesky **handles** or a **search query**
3. Click **Run** — get clean JSON in seconds

**Default config works out of the box** — try it with the pre-filled handle.

---

## 🎯 Six Powerful Modes

| Mode | Auth | What You Get |
| --- | --- | --- |
| 🔍 **Search Posts** | Required | Find posts by keyword, hashtag, or advanced query (`from:user`) |
| 👤 **Get Profiles** | None | Display name, bio, avatar, followers/following/post counts |
| 📝 **Get User Feed** | None | All posts from any public user with engagement metrics |
| 👥 **Get Followers** | Required | Complete follower list with profile data |
| 🚶 **Get Following** | Required | Complete following list with profile data |
| 🧵 **Get Thread** | Required | Full conversation tree — reconstructs entire threads |

---

## 📊 Output — Clean, Flat JSON

Every post comes normalized and ready for CSV export:

```
{
  "uri": "at://did:plc:z72i.../app.bsky.feed.post/3mk6i...",
  "cid": "bafyreig...",
  "authorHandle": "bsky.app",
  "authorDid": "did:plc:z72i...",
  "authorDisplayName": "Bluesky",
  "authorAvatar": "https://cdn.bsky.app/img/avatar/...",
  "text": "We hear and appreciate your feedback...",
  "createdAt": "2026-04-23T17:06:32.796Z",
  "indexedAt": "2026-04-23T17:06:33.123Z",
  "likeCount": 4102,
  "replyCount": 426,
  "repostCount": 493,
  "quoteCount": 0,
  "langs": ["en"],
  "isReply": false,
  "hasMedia": false,
  "mediaCount": 0,
  "hashtags": [],
  "mentions": [],
  "links": [],
  "postUrl": "https://bsky.app/profile/bsky.app/post/3mk6ipt5iv22y",
  "type": "post"
}
```

**Thread mode** adds `threadDepth` (0 = root post, 1 = direct reply, etc.) so you can reconstruct the conversation tree.

---

## 📥 Input Parameters

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `mode` | string | ✅ | `getUserFeed` | Scrape mode |
| `searchQuery` | string | For search | — | Keyword/hashtag/query |
| `handles` | string[] | For profiles/feed/follows | `["bsky.app"]` | Bluesky handles |
| `threadUri` | string | For thread | — | AT URI of any post in thread |
| `maxItems` | integer | No | 100 | Max results (1–10,000) |
| `sort` | string | No | `latest` | `latest` or `top` |
| `language` | string | No | — | ISO code filter (e.g. `en`, `es`) |
| `includeReplies` | boolean | No | `true` | Include reply posts |
| `blueskyHandle` | string | For auth modes | — | Your handle |
| `blueskyAppPassword` | string | For auth modes | — | App password (not main!) |

---

## 💰 Pricing

| Plan | Price |
| --- | --- |
| Free tier | $5 free credit (try it!) |
| Pay-per-result | **$0.002/item** |

**Cost examples:**

- 100 posts: $0.20
- 1,000 posts: $2.00
- 10,000 posts: $20.00

> 💡 **33% cheaper** than competitors ($0.003/item). Platform usage included — no hidden compute fees.

---

## 🆚 Why This Scraper?

| Feature | Us | tugelbay | george | cryptosignals |
| --- | --- | --- | --- | --- |
| Search posts | ✅ | ✅ | ✅ | ✅ |
| Get profiles | ✅ | ✅ | ✅ | ✅ |
| Get user feed | ✅ | ✅ | ✅ | ✅ |
| **Thread reconstruction** | ✅ | ❌ | ❌ | ❌ |
| **Followers export** | ✅ | ❌ | ❌ | ✅ |
| **Following export** | ✅ | ❌ | ❌ | ✅ |
| Auth optional | ✅ | ✅ | ❌ | ❌ |
| Language filter | ✅ | ✅ | ❌ | ❌ |
| **Price per item** | **$0.002** | $0.003 | $0.003 | ~$0.0012 |

---

## 🔧 Technical

- **Runtime:** Node.js 20+ (fast, lightweight)
- **API:** AT Protocol public endpoints (`public.api.bsky.app`)
- **Authentication:** App Password (Bluesky Settings → App Passwords)
- **Rate limiting:** Automatic 429 handling with retry-after
- **Memory:** 256 MB recommended
- **Timeout:** 1 hour default (adjustable)

---

## 📝 Use Cases

- **Brand Monitoring** — Track mentions across Bluesky
- **Competitive Intelligence** — Analyze competitor content and engagement
- **Influencer Discovery** — Find top voices with follower data
- **AI Training Data** — Build clean datasets for LLMs
- **Academic Research** — Study social media discourse
- **Lead Generation** — Find users by interest, extract profiles

---

Built with ❤️ using [Apify SDK for JavaScript](https://docs.apify.com/sdk/js) and the [AT Protocol](https://atproto.com).