[![Add to Cursor](https://fastmcp.me/badges/cursor_dark.svg)](https://fastmcp.me/MCP/Details/1109/reddit-buddy)
[![Add to VS Code](https://fastmcp.me/badges/vscode_dark.svg)](https://fastmcp.me/MCP/Details/1109/reddit-buddy)
[![Add to Claude](https://fastmcp.me/badges/claude_dark.svg)](https://fastmcp.me/MCP/Details/1109/reddit-buddy)
[![Add to ChatGPT](https://fastmcp.me/badges/chatgpt_dark.svg)](https://fastmcp.me/MCP/Details/1109/reddit-buddy)
[![Add to Codex](https://fastmcp.me/badges/codex_dark.svg)](https://fastmcp.me/MCP/Details/1109/reddit-buddy)
[![Add to Gemini](https://fastmcp.me/badges/gemini_dark.svg)](https://fastmcp.me/MCP/Details/1109/reddit-buddy)

# 🤖 Reddit MCP Buddy

### Reddit Browser for Claude Desktop and AI Assistants

A Model Context Protocol (MCP) server that enables Claude Desktop and other AI assistants to browse Reddit, search posts, and analyze user activity. Clean, fast, and actually works - no API keys required.

[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-blue)](https://modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![npm version](https://img.shields.io/npm/v/reddit-mcp-buddy.svg)](https://www.npmjs.com/package/reddit-mcp-buddy)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18.0.0-blue)](https://nodejs.org)

## Table of Contents

- [What makes Reddit MCP Buddy different?](#what-makes-reddit-buddy-different)
- [Quick Start](#quick-start-30-seconds)
- [What can it do?](#what-can-it-do)
- [Available Tools](#available-tools)
- [Authentication](#authentication-optional)
- [Installation Options](#installation-options)
- [Comparison with Other Tools](#comparison-with-other-tools)
- [Troubleshooting](#troubleshooting)
- [Development](#development)
- [Support](#support)

## What makes Reddit MCP Buddy different?

- **🚀 Zero setup** - Works instantly, no Reddit API registration needed
- **⚡ Up to 10x more requests** - Optional authentication increases rate limits
- **🎯 Clean data** - No fake "sentiment analysis" or made-up metrics
- **🧠 LLM-optimized** - Built specifically for AI assistants like Claude
- **📦 TypeScript** - Fully typed, reliable, and maintainable

## Quick Start (30 seconds)

### For Claude Desktop

Add this to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "reddit": {
      "command": "npx",
      "args": ["reddit-mcp-buddy"]
    }
  }
}
```

That's it! Reddit MCP Buddy is now available in Claude.

## What can it do?

Ask your AI assistant to:

- 📊 **"What's trending on Reddit?"** - Browse hot posts from r/all
- 🔍 **"Search for discussions about AI"** - Search across all subreddits
- 💬 **"Get comments from this Reddit post"** - Fetch post with full comment threads
- 👤 **"Analyze user spez"** - Get user history, karma, and activity
- 📚 **"Explain Reddit karma"** - Understand Reddit terminology

## Available Tools

### `browse_subreddit`
Browse posts from any subreddit with sorting options.
```
- Subreddit:
  - "all" - entire Reddit frontpage
  - "popular" - trending across Reddit
  - Any specific subreddit (e.g., "technology", "programming", "science")
- Sort by: hot, new, top, rising, controversial
- Time range: hour, day, week, month, year, all (for top/controversial sort)
- Include subreddit info: Optional flag for subreddit metadata
```

### `search_reddit`
Search across Reddit or specific subreddits.
```
- Query: Your search terms
- Filter by: subreddit, author, time, flair
- Sort by: relevance, hot, top, new, comments
```

### `get_post_details`
Get a post with all its comments.
```
- Input:
  - Reddit URL (full URL including subreddit), OR
  - Post ID alone (will auto-detect subreddit, 2 API calls), OR
  - Post ID + subreddit (most efficient, 1 API call)
- Options: comment sorting, depth, link extraction
```

### `user_analysis`
Analyze a Reddit user's profile.
```
- Username: Any Reddit user
- Returns: karma, posts, comments, active subreddits
```

### `reddit_explain`
Get explanations of Reddit terms.
```
- Terms: karma, cake day, AMA, ELI5, etc.
```

## Authentication (Optional)

Want more requests? Add Reddit credentials to your Claude Desktop config:

### Setup Steps

1. Go to https://www.reddit.com/prefs/apps
2. Create an app (type: **script** - IMPORTANT!)
3. Find your credentials:
   - **Client ID**: Shows under "personal use script"
   - **Client Secret**: The secret string on the app page
4. Update your Claude Desktop config:

```json
{
  "mcpServers": {
    "reddit": {
      "command": "npx",
      "args": ["reddit-mcp-buddy"],
      "env": {
        "REDDIT_CLIENT_ID": "your_client_id",
        "REDDIT_CLIENT_SECRET": "your_client_secret",
        "REDDIT_USERNAME": "your_username",
        "REDDIT_PASSWORD": "your_password"
      }
    }
  }
}
```

### Rate Limits

- **No auth**: 10 requests/minute (default)
- **Client ID + Secret only**: 60 requests/minute
- **With username + password**: 100 requests/minute

**Note**: For maximum rate limits (100 req/min), you need all four credentials including username and password.

## Testing & Development

### Interactive Authentication Setup (for local testing only)

For local development and testing, you can set up authentication interactively:
```bash
npx reddit-buddy --auth
```

This will prompt you for Reddit app credentials and save them locally. **Note: This does NOT work with Claude Desktop** - use environment variables in your Claude config instead.

### Testing with HTTP Mode

To test the server directly in your terminal:
```bash
# Run in HTTP mode on port 3000
npx reddit-mcp-buddy --http

# Or with custom port
REDDIT_BUDDY_PORT=8080 npx reddit-mcp-buddy --http
```

**Note:** The server runs in stdio mode by default (for Claude Desktop). Use `--http` flag for testing with Postman MCP or direct API calls.

### Global Install
```bash
npm install -g reddit-mcp-buddy
reddit-buddy --http  # For testing
```

### From Source
```bash
git clone https://github.com/karanb192/reddit-mcp-buddy.git
cd reddit-mcp-buddy
npm install
npm run build
npm link
```

### Using Docker
```bash
docker run -it karanb192/reddit-mcp-buddy
```

## Comparison with Other Tools

| Feature | Reddit MCP Buddy | Other MCP Tools |
|---------|-------------|----------------|
| **Zero Setup** | ✅ Works instantly | ❌ Requires API keys |
| **Language** | TypeScript/Node.js | Python (most) |
| **Tools Count** | 5 (focused) | 8-10 (redundant) |
| **Fake Metrics** | ✅ Real data only | ❌ "Sentiment scores" |
| **Search** | ✅ Full search | Limited or none |
| **Caching** | ✅ Smart caching | Usually none |
| **LLM Optimized** | ✅ Clear params | Confusing options |

## Rate Limits

| Mode | Requests/Minute | Cache TTL | Setup Required |
|------|----------------|-----------|----------------|
| Anonymous | 10 | 15 min | None |
| App-only | 60 | 5 min | Client ID + Secret |
| Authenticated | 100 | 5 min | All credentials |

## Why Reddit MCP Buddy?

### What others do wrong:
- ❌ **Fake metrics** - "sentiment scores" that are just keyword counting
- ❌ **Complex setup** - Requiring API keys just to start
- ❌ **Bloated responses** - Returning 100+ fields of Reddit's raw API
- ❌ **Poor LLM integration** - Confusing parameters and unclear descriptions

### What we do right:
- ✅ **Real data only** - If it's not from Reddit's API, we don't make it up
- ✅ **Clean responses** - Only the fields that matter
- ✅ **Clear parameters** - LLMs understand exactly what to send
- ✅ **Fast & cached** - Responses are instant when possible

## Examples

### Your AI can now answer:

**"What are the top posts about GPT-4 today?"**
```
→ search_reddit with query="GPT-4", time="day", sort="top"
```

**"Show me what's trending in technology"**
```
→ browse_subreddit with subreddit="technology", sort="hot"
```

**"What do people think about this article?"**
```
→ search_reddit with the article URL to find discussions
```

**"Analyze the user DeepFuckingValue"**
```
→ user_analysis with username="DeepFuckingValue"
```

**"Get the comments from this Reddit post"**
```
→ get_post_details with url="https://reddit.com/r/..."
```

**"What's trending across all of Reddit?"**
```
→ browse_subreddit with subreddit="all", sort="hot"
```

## Troubleshooting

### Common Issues

**"Command not found" error**
```bash
# Ensure npm is installed
node --version
npm --version

# Try with full npx path
$(npm bin -g)/reddit-mcp-buddy
```

**Rate limit errors**
- Without auth: Limited to 10 requests/minute
- With app credentials only: 60 requests/minute
- With full authentication: 100 requests/minute
- Solution: Add Reddit credentials (see [Authentication](#authentication-optional))

**"Subreddit not found"**
- Check spelling (case-insensitive)
- Some subreddits may be private or quarantined
- Try "all" or "popular" instead

**Connection issues**
- Reddit may be down (check https://www.redditstatus.com)
- Firewall blocking requests
- Try restarting the MCP server

### Environment Variables

#### Authentication Variables
| Variable | Description | Required | Rate Limit |
|----------|-------------|----------|------------|
| `REDDIT_CLIENT_ID` | Reddit app client ID | No | 60 req/min (with secret) |
| `REDDIT_CLIENT_SECRET` | Reddit app secret | No | 60 req/min (with ID) |
| `REDDIT_USERNAME` | Reddit account username | No | 100 req/min (with all 4) |
| `REDDIT_PASSWORD` | Reddit account password | No | 100 req/min (with all 4) |
| `REDDIT_USER_AGENT` | User agent string | No | - |

#### Server Configuration
| Variable | Description | Default |
|----------|-------------|---------|
| `REDDIT_BUDDY_HTTP` | Run as HTTP server instead of stdio | `false` |
| `REDDIT_BUDDY_PORT` | HTTP server port (when HTTP=true) | `3000` |
| `REDDIT_BUDDY_NO_CACHE` | Disable caching (always fetch fresh) | `false` |

## Technical Details

### Smart Caching System

Reddit MCP Buddy includes intelligent caching to improve performance and reduce API calls:

- **Memory Safe**: Hard limit of 50MB - won't affect your system performance
- **Adaptive TTLs**: Hot posts (5min), New posts (2min), Top posts (30min)
- **LRU Eviction**: Automatically removes least-used data when approaching limits
- **Hit Tracking**: Optimizes cache based on actual usage patterns

This means faster responses and staying well within Reddit's rate limits, all while using minimal system resources.

## Development

```bash
# Install dependencies
npm install

# Run in development
npm run dev

# Build
npm run build

# Test
npm test

# Lint
npm run lint

# Type check
npm run typecheck
```

### Requirements
- Node.js >= 18.0.0
- npm or yarn
- TypeScript 5.5+

## Contributing

PRs welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

We keep things simple:
- No fake analytics
- Clean, typed code
- Clear documentation
- Fast responses

## Support

- 🐛 [Report bugs](https://github.com/karanb192/reddit-mcp-buddy/issues)
- 💡 [Request features](https://github.com/karanb192/reddit-mcp-buddy/issues)
- ⭐ [Star on GitHub](https://github.com/karanb192/reddit-mcp-buddy)

## License

MIT - Use it however you want!

---

Made with ❤️ for the MCP community. No venture capital, no tracking, just a good MCP server.