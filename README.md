# FeedHorizon MCP server

Let Cursor, Claude, ChatGPT and other AI assistants schedule and publish social media posts on **X (Twitter), LinkedIn, Instagram, Bluesky, Pinterest and TikTok** (TikTok in beta: private posts until TikTok's review).

FeedHorizon is a social media API and hosted MCP server. EU hosted (Frankfurt), the first 2 connected accounts are free.

- **URL:** `https://feedhorizon.com/mcp` (streamable HTTP)
- **Sign-in:** OAuth. Your assistant opens a FeedHorizon sign-in page the first time. An API key as `Authorization: Bearer fh_…` works too.
- **Docs:** https://feedhorizon.com/docs/guides/mcp
- **Official MCP Registry:** `com.feedhorizon/mcp`

## What the assistant can do

- See your profiles and connected accounts
- Check a post against each network's rules (length, media, schedule) before it is saved
- Create drafts, schedule posts at a time, add them to your queue, publish now
- Read and set queue slots, duplicate, cancel and retry posts
- Import media from a URL or create an upload link
- Create a connect link so a client can connect their own account
- Search the FeedHorizon docs

The assistant can do nothing your account could not do through the REST API: same checks, limits and permissions.

## Tools

| Tool | What it does |
| --- | --- |
| `get_context` | Organization, permissions, profiles with time zone and local time, queue state and connected accounts. Called first. |
| `get_platform_rules` | Text length, media count and file types per platform |
| `search_docs` | Searches the FeedHorizon docs |
| `list_posts` | Lists posts, or a calendar range, with filters |
| `get_post` | The full post with per-account status, links and errors |
| `validate_post` | Checks a post against every platform without saving it |
| `get_queue` | A profile's queue slots and which posts hold them |
| `list_pinterest_boards` | The boards of a Pinterest account |
| `get_tiktok_creator` | Creator name and allowed privacy and interaction settings of a TikTok account |
| `create_post` | Saves a draft, schedules a post or adds it to the queue |
| `update_post` | Changes text, accounts, media or time of a post |
| `publish_post_now` | Publishes a post immediately (asks for confirmation) |
| `cancel_post` | Takes a post off the schedule, keeping it as a draft |
| `retry_post` | Publishes the failed accounts of a post again (asks for confirmation) |
| `duplicate_post` | Copies a post as a new draft |
| `delete_post` | Deletes a post in FeedHorizon (asks for confirmation) |
| `set_queue_slots` | Replaces a profile's weekly queue slots |
| `import_media_from_url` | Stores an image, video or PDF from a public URL |
| `create_upload_link` | A link to upload a local file |
| `create_connect_link` | A link to connect a social account to a profile |

## Cursor

Add this to `.cursor/mcp.json` (project) or `~/.cursor/mcp.json` (global):

```json
{
  "mcpServers": {
    "feedhorizon": {
      "url": "https://feedhorizon.com/mcp"
    }
  }
}
```

Cursor opens the FeedHorizon sign-in when you first use a tool. To use an API key instead, add `"headers": { "Authorization": "Bearer fh_your_api_key" }`.

## Claude, ChatGPT and other clients

Add a custom connector / remote MCP server with the URL `https://feedhorizon.com/mcp` and sign in. Step-by-step guides for each client: https://feedhorizon.com/docs/guides/mcp

## Example prompts

- "Schedule a LinkedIn post for tomorrow 9:00 announcing our new pricing page."
- "Fill next week's queue on X with five tips from our blog post <url>."
- "Check this Instagram caption and image against Instagram's limits before scheduling."

## Links

- Website: https://feedhorizon.com
- Pricing: https://feedhorizon.com/pricing
- API reference: https://feedhorizon.com/docs
- llms.txt: https://feedhorizon.com/llms.txt
