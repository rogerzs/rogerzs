# Gemini meeting notes — hourly automation

This document describes what the Cursor cron workflow is supposed to do when summarizing **Google Meet Gemini notes**, and why a fully automated run may produce no output.

## Target deliverable

Append entries to the master Google Doc using this pattern (one block per meeting):

```text
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

Doc: `https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit`

## Intended steps

1. **Inbox** — Confirm new mail from Gemini / Google Meet notes for the last hour (typically Gmail).
2. **Open each note** — Follow the link in the email to the full Gemini note (Google-hosted; requires an authenticated Google session or API credentials).
3. **Update the Doc** — Append the four-line block per meeting to the Google Doc (requires Docs API OAuth or an authenticated editor session).
4. **Slack** — If at least one note was summarized, send a **DM** with the meeting titles processed and the **token usage** for that run. If nothing was summarized, send nothing.

## Current automation limits (Cloud Agent)

| Step | Status |
|------|--------|
| Gmail / inbox | Not available in the default MCP tool set (no Gmail connector). |
| Read Gemini note URL | Requires Google sign-in; unauthenticated HTTP fetch only returns the login page. |
| Edit Google Doc | Same: requires OAuth or an authorized Google Docs integration. |
| Slack DM | Available (`slack_send_message` with the recipient’s user ID as `channel_id`). |

To make this reliable end-to-end, configure one or more of:

- **Gmail API** (or forwarding Gemini emails into a system the agent can read), and
- **Google Docs API** (service account or OAuth) with edit access to the target document, or
- A **manual step** where you paste note text or links into Slack / the repo for the agent to process.

## Historical runs

| When (UTC) | Outcome |
|------------|---------|
| 2026-05-26 ~17:01 | No Gemini note emails or note content reachable from this environment; no Doc updates; no Slack notification (per “otherwise do nothing”). |
