# Hourly Gemini notes resume (Cursor Cloud Agent)

This runbook describes how to resume Google Meet **Gemini (“Take notes for me”)** transcripts into your master Google Doc, and what this repository documents for automation.

## Target Google Doc pattern

Append each meeting block using this structure (repeat per note):

```text
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

**Master document (edit in browser):**  
https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit

## Prerequisites (required for full automation)

Internal **Meeting Fetcher** documentation states that the reliable pipeline is:

`Gmail (Gemini notification emails) → Google Doc transcript → summarization → destination`

That flow needs **Google Workspace MCP (Gmail + Google Docs)** on the agent (and optionally **Google Calendar MCP** for anchoring attendees). Without those integrations, an agent cannot read your inbox or private Doc contents.

Reference: Confluence page **Meeting Fetcher** (`/wiki/spaces/~5d571af23f5e050c1717a560/pages/265018803118/Meeting+Fetcher` on the Nubank Atlassian site).

## What the hourly Cloud Agent can do today

Configured MCP servers in this environment: **Slack** and **Atlassian** only. There is **no Gmail** or **Google Docs** API access, and unauthenticated HTTP fetch of the target Doc returns a Google sign-in page.

Operational checks performed on the **2026-05-25 09:00 UTC** cron run (window **08:00:33–09:00:33 UTC**, matching “the last hour” before trigger `2026-05-25T09:00:33.338Z`):

1. **Email** — Not accessible from this agent (no Google Workspace MCP).  
2. **Slack** — Searched private and public Slack (including DMs) for Gemini / Meet notes / transcript-style phrases in that window; **no Gemini meeting-note notifications** were found (one unrelated message contained the word “GEMINI” in an ops roster sense).  
3. **Google Doc** — Could not be read or updated programmatically without Google auth.

**Slack DM rule:** If at least one note is successfully resumed, DM yourself with resumed **titles** and **token usage**. If **zero** notes are resumed, **send nothing** (no DM).

## Recommended setup for a working hourly job

1. Enable **Gemini note-taking** in Google Meet (“Take notes for me”).  
2. Attach **Google Workspace MCP** (Gmail + Docs) to the automation that runs this task.  
3. Optionally add **Calendar MCP** for better name anchoring.  
4. Re-run the workflow: list Gemini emails in the lookback window, open each linked Doc, summarize, append to the master Doc, then notify in Slack with titles + token count from your platform metrics.

## Related internal tooling

Nubank engineers can use the **meeting-fetcher** plugin (`meeting-fetcher@nubank-ai-agents-plugins`) with `/fetch-meetings` for a fuller fetch-and-archive pipeline; the hourly “resume into one Google Doc” flow is a lighter variant but still needs Gmail + Docs access for source material.
