# Gemini notes resume automation (cron)

This document records what the hourly cron is expected to do and what is required for it to succeed.

## Intended workflow

1. Check the mailbox for new **Gemini notes** emails (typically within the last hour).
2. Open each linked Gemini note, extract the meeting title, date, and substance.
3. Append to the shared Google Doc using this pattern for each note:

   - `[Date of the Gemini Note]`
   - `[Title of the Meet]`
   - `[Resume]`
   - `[Link to gemini note complete]`

4. If at least one note was summarized, send a **Slack DM** with the titles of the documents resumed and the **token usage** for that summarization run. If none were resumed, send nothing.

Target doc (edit URL):  
`https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit`

## Run log — 2026-05-21 (cron trigger ~21:01 UTC)

**Result:** No Gemini notes were resumed; the Google Doc was not modified.

**Blockers in this environment:**

| Step | Status |
|------|--------|
| Email (Gemini notifications) | No Gmail or generic mail integration available to the agent. |
| Google Doc read/write | Doc URL returns Google sign-in; no Docs API credentials in the workspace. |
| Slack DM + token count | Slack MCP reported `needsAuth` (tools unavailable). Token usage is not exposed as a machine-readable metric in this agent run. |

## What to configure for a successful automated run

- **Mail:** A connector the automation can call (e.g. Gmail API with a service account or OAuth, or a webhook that forwards Gemini note metadata).
- **Google Docs:** OAuth or service account with access to the target document and the [Google Docs API](https://developers.google.com/docs/api) enabled.
- **Slack:** MCP or bot token with `im:write` (or equivalent) to open a DM with the user, plus a way to resolve the user’s Slack member ID.
- **Token reporting:** If the orchestrator runs an LLM step, it should log usage from the provider’s usage API or response metadata and pass that into the Slack message.

Until those pieces are connected, the cron will correctly take the “do nothing” path for Slack when no notes can be processed.
