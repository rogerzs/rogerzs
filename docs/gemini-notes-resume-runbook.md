# Gemini Notes → Google Doc resume (automation runbook)

This document describes the intended workflow for summarizing recent Gemini meeting notes into a single Google Doc, and what is required for a cloud agent to complete it end to end.

## Target Google Doc

- Edit URL: `https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit`
- The document is private; unauthenticated HTTP export returns a Google sign-in page, so agents without Google credentials cannot read or append content.

## Entry format (each resumed note)

Use this block pattern for every summarized note:

```text
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

Repeat the block for multiple meetings, separated by blank lines if you prefer readability.

## Intended agent steps

1. **Email (Gmail)** — Confirm receipt of Gemini Notes notification email(s) in the last hour (sender/subject filters depend on your Gemini Notes setup).
2. **Open each note** — Follow links from email (or Meet/Gemini history) to the full note text.
3. **Summarize** — Produce a concise resume of the call from the note body.
4. **Write to Google Doc** — Append (or insert) each block using the pattern above.
5. **Slack** — If at least one note was successfully resumed and written to the Doc, notify the owner (DM or agreed channel) with the **titles** of the documents/meetings summarized and **token usage** if your platform exposes it.

## Why a bare cloud agent often cannot complete this

| Step | Typical blocker |
|------|-----------------|
| Gmail | No Gmail API or OAuth token injected into the agent; Atlassian MCP does not replace personal inbox access. |
| Google Doc | Docs API requires OAuth (user) or a service account with **explicit share** on the Doc; anonymous export is blocked for private docs. |
| Slack DM | Automation may only have a **fixed channel** webhook or bot scope; direct messages need the user’s Slack ID and `im:write` (or equivalent) for the app. |

## What to configure for a working automation

1. **Google Cloud project** — Enable **Gmail API** and **Google Docs API**.
2. **Auth** — OAuth consent for your Google account (read Gmail messages, read/write the target Doc) *or* a service account whose client email is granted Editor on the Doc (Gmail still usually needs user OAuth).
3. **Secrets** — Store refresh tokens or service-account JSON as CI/automation secrets, not in the repo.
4. **Slack** — Ensure the bot can DM you (or post to your chosen channel) and document where notifications should go.

## Run log — 2026-05-22 (automation attempt)

- Gmail: not accessible from this environment (no inbox integration).
- Gemini note URLs/content: not available without email or another feed.
- Google Doc: export URL returned sign-in; no append performed.
- Slack: a mistaken connectivity test message was posted to the configured workspace channel; follow-up in thread clarified that **no** Gemini notes were resumed on this run, so no “titles + tokens” completion message applied.
