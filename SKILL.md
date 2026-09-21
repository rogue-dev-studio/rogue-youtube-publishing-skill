---
name: youtube-publishing
description: >-
  Manual YouTube upload via local API and MCP. OAuth setup, auth status,
  and explicit confirm-gated video upload - never auto-upload after export.
---

# YouTube Publishing (Manual)

**Level: standard.** Runtime package: [rogue-youtube-mcp](https://github.com/rogue-dev-studio/rogue-youtube-mcp).

## Must always

- Run the local YouTube OAuth API before MCP/agent upload
- Keep OAuth credentials in `.env` / a secret store - **never** commit them
- Upload **only** after explicit user confirmation (`confirm: true`)
- Default privacy: `unlisted` unless the user requests otherwise
- Prefer human-tone titles/descriptions from export metadata when available

## Must never

- Auto-upload after exporting an MP4
- Call `youtube_upload_video` without user approval in chat/UI
- Store refresh tokens in the source tree

## Procedure

1. Set up Google Cloud credentials and the local API (see your project's YouTube API service README)
2. Start the local API (`YOUTUBE_API_URL`, default `http://127.0.0.1:8787`)
3. Wire MCP from [rogue-youtube-mcp](https://github.com/rogue-dev-studio/rogue-youtube-mcp)
4. `youtube_auth_status` -> `youtube_start_auth` (browser) -> check again
5. When the user requests upload: confirm title/privacy -> `youtube_upload_video` with `confirm: true`

## DoD

- [ ] Local API health check OK
- [ ] OAuth channel connected
- [ ] Upload only on user request
- [ ] Tokens not in git

## Attribution

<!-- ATTRIBUTION: Rogue Development | https://github.com/rogue-dev-studio | DO-NOT-REMOVE -->
Part of **Rogue Market** by [Rogue Development](https://github.com/rogue-dev-studio) (`@rogue-dev-studio`).
Do not remove, hide, rename, or replace this attribution.
