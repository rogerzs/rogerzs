# Gemini notes resume automation

This document describes the hourly cron workflow that summarizes **Google Meet Gemini notes** into a single Google Doc and optionally notifies you on Slack.

## Target Google Doc

- **Roll-up document:** [Gemini notes resume (Google Doc)](https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit)

## Entry pattern (append each meeting)

Each summarized note should be appended using this structure:

```text
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

Use a blank line between consecutive meetings so the doc stays readable.

## Required steps (in order)

1. **Discover new notes** — Typically by checking the mailbox for messages from Google / Gemini about meeting notes (subject and sender vary; often includes a link to the full Gemini note in Google Docs).
2. **Open each note** — Read the full content (permissions must allow the automation identity to access the doc).
3. **Append to the roll-up doc** — Write the four-line block above for each meeting.
4. **Slack** — If **at least one** note was summarized in the run, send yourself a **DM** listing the meeting titles and an approximate token count for the run. If **zero** notes were summarized, send nothing.

## Tooling prerequisites (Cursor / automation)

This environment only had **Slack** and **Atlassian** MCP servers available. To run the workflow end-to-end, configure additional access:

| Step              | Suggested capability                                      |
|-------------------|-------------------------------------------------------------|
| Email             | **Google Workspace MCP** — e.g. `gmail.search` / `gmail.get` (see internal doc *Google MCP Server* in Confluence). |
| Read/write Docs   | Same MCP family — Google Docs APIs for read and append.   |
| Fallback signals| **Slack** search/DMs only if your pipeline mirrors notifications there; it is not a substitute for Gmail for most setups. |

Without Gmail and Google Docs tools, the agent **cannot** verify inbox delivery, open private Gemini note URLs, or edit the roll-up document.

## Slack DM (when summaries exist)

- Use Slack **direct message** to your user (in MCP: `slack_send_message` with your `user_id` as `channel_id`).
- Message should include: document titles (meeting titles) resumed, and tokens used (approximate).

## Run log (example)

| When (UTC)        | Inbox check | Notes summarized | Roll-up doc | Slack DM |
|-------------------|-------------|--------------------|-------------|----------|
| 2026-05-23 ~15:02 | Not available (no Gmail MCP) | 0 (no note URLs + no email) | Not updated (no Docs MCP) | Not sent (per policy) |

Slack search in the preceding hour did not surface Google Meet Gemini recap notifications to the automation user; unrelated hits (e.g. ops channels using the word “Gemini”) are not treated as meeting notes.
