---
name: schedule-social-posts
description: >
  Schedule, preview, edit, and cancel social media posts with PostWing MCP.
  Use when the user wants to post or schedule to Instagram, TikTok, YouTube,
  LinkedIn, X, Facebook, Pinterest, or Threads from Cursor.
---

# Schedule social posts with PostWing

PostWing is a remote MCP server. Auth is OAuth — the user signs in to PostWing the first time they use a tool. Writes always use **preview → confirm**. Never skip the confirm step.

## Before scheduling

1. Call `list_connected_accounts` to see which accounts are linked in the active workspace.
2. If nothing is connected, call `connect_account` and have the user finish OAuth in the browser, then `sync_accounts`.
3. For Pinterest, call `list_pinterest_boards` and pass `board_ids` in `platform_options`.

## Schedule a post

1. Gather caption, media (if any), target accounts or platforms, and send time (ISO 8601 or clear local time + timezone).
2. Call `preview_schedule_post`. Show the user the returned preview (caption, accounts, time).
3. Only after the user explicitly approves, call `confirm_schedule_post` with the `confirmation_token`.
4. Tell the user the post is scheduled and link them to the PostWing calendar if a URL is returned.

## Edit or cancel

- Edits: `preview_edit_posts` → user approval → `confirm_edit_posts`.
- Cancel: identify the post with `list_scheduled_posts` / `get_scheduled_post`, then `cancel_scheduled_post` with `user_confirmed: true` only after the user agrees.

## Media

- Prefer `request_media_upload` for in-chat uploads when the host supports MCP Apps.
- Or `upload_media` with public HTTPS URLs (videos have a size cap).

## Rules

- Never invent account IDs — use values from PostWing tools.
- Never confirm a schedule or edit without showing the preview and getting a clear yes.
- Do not claim analytics or inbox features; PostWing schedules and publishes only.
- Active PostWing subscription required.
