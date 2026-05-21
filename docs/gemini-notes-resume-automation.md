# Gemini Notes → Call resume (automation runbook)

## Target Google Doc

https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit

Append each summarized meeting using this pattern (one block per note):

```
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

## What the agent needs to run end-to-end

1. **Gmail (or equivalent)** — read messages from Gemini Notes (sender/subject filters) for the requested time window. This Cursor Cloud environment does not ship Gmail credentials; connect Gmail via Google Workspace API or forward Gemini emails into a system the agent can read.
2. **Google Docs API** — service account or OAuth client with edit access to the document above (share the doc with the service account email, or use a user OAuth flow outside Cloud Agent).
3. **Slack** — optional notification after at least one note is summarized; include titles and token usage if your platform exposes usage metrics.

## Automation run log

| Run (UTC) | Email check | Doc update | Notes summarized | Slack |
|-----------|-------------|------------|------------------|-------|
| 2026-05-21 16:00 | Not available — no Gmail/IMAP integration in workspace; Atlassian MCP not authenticated | Not available — Google Doc requires account sign-in from unauthenticated fetch | 0 | Skipped (nothing resumed) |
