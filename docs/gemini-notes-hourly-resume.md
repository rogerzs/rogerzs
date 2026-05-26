# Hourly Gemini notes — call resume (runbook)

This document describes the **resume call** workflow: turn Gemini “Take notes for me” notifications into structured entries in your consolidated Google Doc.

## Target log document

- **Google Doc (append summaries here):** https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit?tab=t.0

## Entry pattern (each meeting)

Paste one block per meeting, in this order:

1. **[Date of the Gemini Note]** — date the note was created or emailed (use the date in the Gemini email or doc, in a consistent format you prefer, e.g. `2026-05-26`).
2. **[Title of the Meet]** — meeting title from Calendar / Gemini / the doc title.
3. **[Resume]** — short summary: decisions, action items (owner + deadline if present), risks, and follow-ups.
4. **[Link to gemini note complete]** — full URL to the Gemini-generated Google Doc (from the email).

Example:

```text
2026-05-26
Weekly sync — Data platform
Resume: Agreed to postpone the cutover to the next sprint; @alice to confirm the migration window by Friday; open question on rollback testing ownership.
Link: https://docs.google.com/document/d/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/edit
```

## Operational steps (manual or automated)

1. **Inbox — Gemini notes email**  
   Confirm you received mail from Gemini / Google Meet notes (subject usually references the meeting or “Notes”).

2. **Open each note**  
   Use the link in the email to open the full Gemini Google Doc. Skim transcript + summary sections.

3. **Append to the log doc**  
   Add a new block following the pattern above. Prefer appending at the end (or a dated section) so history stays chronological.

4. **Notify yourself (optional)**  
   If you use Slack, send yourself a DM listing which meeting titles were resumed and any usage metrics your tooling exposes (e.g. model token usage), if required by your personal automation.

## Why Cursor hourly automation may no-op here

Nubank’s **Meeting Fetcher** pipeline explicitly requires **Google Workspace MCP (Gmail + Google Docs)** to search mail and read/write doc content, plus Meet **“Take notes for me”** enabled. See internal doc: [Meeting Fetcher](https://nubank.atlassian.net/wiki/spaces/~5d571af23f5e050c1717a560/pages/265018803118/Meeting+Fetcher).

A Cursor Cloud Agent that only has **Slack** and **Atlassian** MCP cannot:

- Read your Gmail for Gemini notifications  
- Open or edit the destination Google Doc via API  

In that configuration, the correct behavior for **“otherwise, do nothing”** (no Slack summary) is: **no Gemini notes were resumed in this run**.

## Recommended fix for hands-off runs

- Install/configure **Google Workspace MCP** (Gmail + Docs, and Calendar if you want anchoring), **or** use the internal **Meeting Fetcher** plugin (`meeting-fetcher@nubank-ai-agents-plugins`) with `/fetch-meetings` as described in Meeting Fetcher, then copy or sync summaries into this doc if you still want a single rolling log.

---

*Branch: documentation for Gemini notes resume workflow (`gemini-notes-hourly-resume`).*
