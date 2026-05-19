# Gemini meeting notes — resume workflow

This document describes how to summarize Google **Gemini** meeting notes and append them to the master log. It matches the automation that runs on a schedule and the format expected in the Google Doc below.

## Target document (append-only log)

**URL:** https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit?tab=t.0

The automation agent must be able to edit this file via the **Google Docs API** (OAuth or a service account with share access to the document). Opening the link in a browser without an authenticated session only shows the Google sign-in page.

## Entry pattern (each Gemini note)

Use one block per meeting note, in this order:

```text
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

- **Date:** Use the date shown in the Gemini note or the email delivery time (timezone should be explicit if relevant).
- **Title:** Meeting title from Gemini (or subject line if the title is only in email).
- **Resume:** Concise summary: purpose of the call, decisions, action items, owners, and follow-ups.
- **Link:** Full URL to the Gemini note (the “open note” link from the email or Meet).

Separate multiple entries with a clear divider (for example a horizontal rule or blank lines) so the log stays readable.

## Step 1 — Verify email (Gemini notes)

1. In the mailbox that receives Meet / Gemini summaries, search for messages from Gemini or Google Meet (typical subjects contain the meeting title and “notes” or “Gemini”).
2. Filter to the **last hour** (or the window defined by the cron schedule).
3. For each matching message, extract the link to the full Gemini note and the meeting metadata.

**Agent requirement:** Gmail (or Google Workspace) API access with read scope for the user’s inbox, or a pre-forwarded webhook / pub-sub integration. The Cursor Cloud Agent in this repository does not include Gmail MCP tools; that access must be configured in the environment that runs the automation.

## Step 2 — Open each note and summarize

1. Open each Gemini note URL (authenticated browser or API).
2. Read the transcript / structured sections.
3. Write the **Resume** in the pattern above: decisions, action items, and names where available.

## Step 3 — Write to Google Docs

Append new blocks to the end of the target document using the Docs API (`documents.batchUpdate` with `insertText` at the document end, or equivalent). Do not overwrite existing log content.

## Step 4 — Notify in Slack (only if work was done)

If **at least one** Gemini note was summarized and appended:

- Send a **direct message** to the document owner with:
  - Titles of the meetings that were resumed.
  - **Token usage** (or API cost) from the model run that produced the summaries — this must come from the inference provider’s usage metadata (for example `usage` in the API response), not an estimate.

If **no** notes were found or resumed in the window, **do not** send a Slack message.

## Why a scheduled run might no-op

| Blocker | Mitigation |
|--------|------------|
| No Gmail / inbox integration | Add Gmail API or forward Gemini emails to a parser the agent can read. |
| Google Doc not shared with the service account / user | Share the Doc with the identity used for Docs API. |
| Gemini links require user session | Use a logged-in session or export notes to a shared Drive file the API can read. |
| Slack MCP not authenticated | Complete Slack MCP auth in Cursor, or use a Slack app with `chat.postMessage` and DM scope for the owner’s user ID. |

## Related repository context

This repo’s Cloud Agent currently exposes a **Slack webhook** secret for notifications; it does not include Google OAuth credentials. Full end-to-end automation requires additional secrets and API projects as described above.
