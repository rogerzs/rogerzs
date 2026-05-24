# Hourly Gemini notes → Google Doc summary (automation)

This document describes what the hourly cron needs in order to verify Gemini notes, summarize calls, append to your master Google Doc, and optionally notify you on Slack.

## Target Google Doc

Master log (append summaries here):

`https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit`

## Entry pattern (each meeting)

Use one block per note, in this order:

1. **Date of the Gemini Note** (meeting / note date)
2. **Title of the Meet** (calendar title or doc title)
3. **Resume** (short summary: decisions, actions, owners)
4. **Link to gemini note complete** (full URL to the Gemini Google Doc)

## Required integrations

Without these, the agent cannot complete the workflow end-to-end:

| Capability | Why it is needed |
|------------|------------------|
| **Gmail** (search + read) | Gemini sends “Take notes for me” messages with links to the transcript Google Doc. |
| **Google Docs** (read transcript + **edit** the master doc) | Read source notes and append formatted blocks to the master document. Private docs are not readable without OAuth/service account with access. |
| **Optional: Google Calendar** | Improves titles, attendees, and time anchoring (see internal *Meeting Fetcher* doc). |

Internal reference (Nubank Confluence): [Meeting Fetcher](https://nubank.atlassian.net/wiki/spaces/~5d571af23f5e050c1717a560/pages/265018803118/Meeting+Fetcher) — describes the Gmail → Doc pipeline and the `meeting-fetcher` plugin pattern.

## Slack (fallback, not a full replacement)

If Gmail is unavailable, Slack search (including DMs) can sometimes surface forwarded links or bot posts, but **Gemini note emails usually never appear in Slack**, so this is unreliable as the primary source.

## Notification rule

- If **at least one** Gemini note was summarized and written to the master doc: send a **Slack DM** to the owner with the **titles** of the documents summarized and **token usage** for the run (when the platform exposes it).
- If **zero** notes were summarized: **do not** send Slack.

## Run log (2026-05-24)

- **Time window checked (UTC):** approximately `2026-05-24T01:02`–`2026-05-24T02:05` (hour before cron at `2026-05-24T02:02:03Z`).
- **Gmail:** not connected in this Cursor automation → could not verify Gemini emails.
- **Google Doc:** not editable/readable without Google auth from this environment.
- **Slack search:** no Gemini meeting transcripts in that window (unrelated hits only, e.g. ops “GEMINI” label, incident postmortem doc links).
- **Result:** no summaries appended; no Slack message (per rule above).
