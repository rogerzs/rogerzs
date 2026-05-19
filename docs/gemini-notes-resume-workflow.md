# Gemini Notes → Google Doc resume (automation runbook)

This document describes how meeting summaries from **Gemini notes** should be copied into the shared Google Doc when the hourly automation runs, and what is required for a future run to succeed end-to-end.

## Target Google Doc

Full URL (do not shorten when sharing or pasting):

`https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit?tab=t.0`

## Pattern to append in the document

Each resumed note should be added using this structure (replace bracketed placeholders):

```text
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

- **Date of the Gemini Note**: Use the date/time shown in the Gemini note or notification email (include timezone if available).
- **Title of the Meet**: Meeting title from Gemini (or email subject line if that is the canonical title).
- **Resume**: Concise bullet or short-paragraph summary of decisions, action items, and key discussion points. Do not invent content; only summarize what appears in the note.
- **Link to gemini note complete**: Full URL to the Gemini note (same standard: paste the complete link).

## Intended automation steps (for a fully wired environment)

1. **Email**: In the mailbox that receives Gemini notifications, search for messages from the last hour (relative to the cron execution time) that correspond to new Gemini notes.
2. **Open each note**: Follow the link from the email (or from Gmail search), read the transcript/summary.
3. **Update the Google Doc**: Append one block per note using the pattern above.
4. **Slack**: If at least one note was successfully resumed, send the user a **direct message** listing:
   - Titles of the documents/notes summarized, and  
   - Token usage for that agent run (from the platform that executed the model, e.g. Cursor/automation metrics).  
   If zero notes were resumed, send nothing.

## Run log — 2026-05-19 (cron ~19:01 UTC)

**Result:** No Gemini note was resumed in this environment.

**Reasons:**

- **Slack MCP** was in `needsAuth` state, so no DM could be sent.
- **Atlassian MCP** was in `needsAuth` state (no alternative path to mail).
- There is **no configured MCP or API** in this workspace for **Gmail** or **Google Docs** read/write, so incoming Gemini mail could not be verified and the Google Doc could not be edited programmatically.
- Fetching the Google Doc URL from this runner **timed out** (typical for private docs without Google credentials).
- The repository workspace contains **no cached Gemini note files** for the last hour.

**Next steps for the operator:** Authenticate Slack (and any Google Workspace connectors) in the Cursor/automation project, and/or provide a service account or OAuth client with Gmail read + Google Docs append scopes so the cron job can perform the steps above without manual intervention.
