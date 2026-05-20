# Gemini notes → Google Doc resume (automation runbook)

This document describes the workflow for summarizing recent **Gemini meeting notes** into a shared Google Doc and notifying on Slack. It also records what an agent needs in order to run the steps end to end.

## Target Google Doc

- URL: `https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit`

## Entry pattern (append each summarized note)

Use one block per note, in this order:

1. `[Date of the Gemini Note]`
2. `[Title of the Meet]`
3. `[Resume]` — concise summary (decisions, owners, follow-ups).
4. `[Link to gemini note complete]` — full URL to the original Gemini note.

Example:

```text
2026-05-20
Weekly sync — Infra
Discussed rollout timeline; agreed to pause deploy until Monday. Action: Alice to update runbook.
https://notebooklm.google.com/... (full link)
```

## Operational steps (manual or automated)

1. **Email** — In the mailbox that receives Gemini note notifications, filter for messages from Gemini / Google Meet notes (or your configured sender) in the **last hour** (or the window you care about).
2. **Open each note** — Use the link in the email to open the full Gemini note; extract title, date, and substantive content.
3. **Update the Google Doc** — Append a new section following the pattern above.
4. **Slack** — If at least one note was summarized, send a direct message to the owner with:
   - Titles of the documents (or meetings) summarized
   - Approximate token usage for that agent run (if your platform exposes usage; otherwise omit or use “not available”).

If **no** qualifying notes were found or summarized, **do not** send Slack.

## What Cursor Cloud / this agent environment must have

To execute the steps automatically, **all** of the following are required:

| Capability | Why |
|------------|-----|
| **Gmail (or equivalent) API** with OAuth or service account delegated access | To list and read “Gemini notes” emails from the last hour. |
| **Google Docs API** with write access to the target document | To append formatted text. The doc must be shared with the identity used by the automation. |
| **Slack** with `im:write` (or a user token) if you need a **DM**; or a fixed channel if DMs are not required | Native integrations vary; confirm scopes for your workspace. |

Without these, an agent can only document the procedure (this file) and cannot fill the live document or verify the inbox.

## Run log template

| Date (UTC) | Notes summarized | Blockers |
|------------|------------------|----------|
| 2026-05-20 | 0 | No mailbox or Google Docs API in environment; target Doc URL requires sign-in; no Gemini note URLs retrieved. |
