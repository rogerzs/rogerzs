# Gemini Notes call resume workflow

This document describes how call resumes from **Google Gemini in Meet** (Gemini notes) are supposed to be consolidated into the master Google Doc, and why an automated run may not be able to complete every step without connected accounts.

## Target Google Doc

- **URL:** https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit

## Entry pattern (each meeting block)

Use this structure for every summarized note, in order:

1. **[Date of the Gemini Note]** — Date shown on the note (or from the email notification).
2. **[Title of the Meet]** — Meeting title from Gemini / calendar context.
3. **[Resume]** — Concise summary: decisions, action items, owners, and open questions.
4. **[Link to gemini note complete]** — Full URL to the Gemini note (from the email or Meet).

Repeat the block for each meeting processed in the same session.

## Intended procedure

1. **Inbox** — Look for recent messages from Gemini / Google Meet related to new notes (typically within the last hour for a scheduled automation).
2. **Open each note** — Follow the link in the email, read the full Gemini note, and extract title, date, and substantive content for the resume.
3. **Update the Google Doc** — Append a new block using the pattern above (preserve existing content).
4. **Slack** — If at least one note was summarized, notify the owner in Slack with the **titles** of those meetings and **token usage** for the summarization pass. If nothing was summarized, skip Slack.

## Prerequisites for automation

For a machine agent to run this end-to-end, the environment needs:

| Step | Requirement |
|------|-------------|
| Email | Gmail API (OAuth or service account with domain-wide delegation), or another ingestion path (e.g. forwarded webhook). |
| Read/write Doc | Google Docs API with OAuth and scopes such as `https://www.googleapis.com/auth/documents`. The document must be accessible to that identity. |
| Slack DM | Slack API with a bot token and `chat.postMessage` to the user’s DM channel (`user_id` → `conversations.open`), or an approved app install in the workspace. |

This repository does not store Google credentials; they must be supplied by the host environment (e.g. Cursor Cloud secrets or a secure runner).

## Run log (automation transparency)

- **Environment check:** No Gmail or Google Docs credentials were available in the agent workspace. The target Doc URL returns a Google sign-in page when fetched without an authenticated session.
- **Outcome:** No Gemini note could be read from email, and the master document could not be edited. Per the procedure above, **no Slack notification** was sent (zero resumes completed).

Token usage for summarization is reported by the hosting product (e.g. Cursor usage); it is not exposed to this agent as a numeric value in the run environment.
