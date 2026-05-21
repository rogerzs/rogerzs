# Gemini Notes → Google Doc resume (automation runbook)

This document describes what a scheduled agent needs in order to summarize Gemini meeting notes into a shared Google Doc and notify you on Slack.

## Target Google Doc pattern

Each entry should follow this structure:

```
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

## Required access (not available in a bare Cursor Cloud agent)

1. **Email** — Read messages from Gemini Notes (Gmail API, Google Workspace routing, or forwarded copies into a system the agent can read).
2. **Google Docs** — OAuth or a service account with edit access to the destination document. Anonymous fetch returns a sign-in page.
3. **Slack** — A way to open a DM (or an agreed channel) when at least one note was successfully summarized.

## Slack notification rule

Send a notification **only** if one or more notes were summarized in that run. If nothing could be processed, send nothing (avoid accidental “test” posts).

## Token usage

Exact token counts for an agent run are not exposed to the model in this environment; use Cursor or your provider’s usage/billing dashboards if you need totals.
