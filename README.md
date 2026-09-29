# PostWing for Cursor

Schedule social media posts from Cursor via [PostWing](https://postwing.io)’s remote MCP server.

Connect Instagram, TikTok, YouTube, LinkedIn, X, Facebook, Pinterest, and Threads. Every write uses a **preview → confirm** flow so nothing publishes until you say yes.

## Install

Add PostWing as a custom MCP server in Cursor (**Customize → MCP**, or edit `~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "postwing": {
      "url": "https://postwing.io/api/mcp"
    }
  }
}
```

Cursor authenticates with OAuth against PostWing. Leave client ID/secret blank — dynamic registration is supported. Sign in to PostWing when prompted, then ask the agent to schedule a post.

### Local plugin test

```bash
mkdir -p ~/.cursor/plugins/local
cp -R . ~/.cursor/plugins/local/postwing
```

Then **Developer: Reload Window**, open Customize, and confirm the PostWing MCP server appears.

## Requirements

- Active [PostWing](https://postwing.io) subscription (7-day free trial available)
- Social accounts connected in the PostWing dashboard (or via MCP `connect_account`)

## What you can do

| Task | How |
| --- | --- |
| List accounts | `list_connected_accounts` |
| Schedule a post | `preview_schedule_post` → approve → `confirm_schedule_post` |
| Edit queued posts | `preview_edit_posts` → approve → `confirm_edit_posts` |
| Cancel a post | `cancel_scheduled_post` (with confirmation) |
| Upload media | `request_media_upload` or `upload_media` |

The bundled skill `schedule-social-posts` teaches the agent this flow.

## MCP endpoint

- **URL:** `https://postwing.io/api/mcp`
- **Transport:** Streamable HTTP
- **Auth:** OAuth 2.0 (preferred) or Bearer API key from [postwing.io/dashboard/ai](https://postwing.io/dashboard/ai)

## Privacy & security

- Access is scoped to your PostWing user.
- OAuth redirects are limited to trusted clients (including Cursor).
- Schedule and edit require a short-lived confirmation token after preview.

See [postwing.io/privacy](https://postwing.io/privacy) and [postwing.io/docs](https://postwing.io/docs).

## Support

- Product: [postwing.io/support](https://postwing.io/support)
- Dashboard AI setup: [postwing.io/dashboard/ai](https://postwing.io/dashboard/ai)
