# Gemini call resume — Google Doc pattern

Use this block for each meeting when appending to the [rolling summary document](https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit).

## Pattern (one entry per note)

```
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

Replace bracketed lines with real values. The resume should be a concise summary of decisions, actions, and open topics from the full Gemini transcript.

## Automation prerequisites

Hourly or agent-based resume workflows need **read access to Gmail** (to detect “Gemini notes” / “Take notes for me” messages) and **read/write access to Google Docs** (to open each transcript and append to the summary doc). At Nubank, the **Meeting Fetcher** plugin documents the same requirement: Google Workspace MCP (Gmail + Docs). See [Meeting Fetcher](https://nubank.atlassian.net/wiki/spaces/~5d571af23f5e050c1717a560/pages/265018803118/Meeting+Fetcher) on Confluence.

Without those integrations, an agent cannot verify the inbox, open transcript links, or update the document.

## Slack notification (optional)

After at least one note is resumed, send yourself a Slack DM with:

- Titles of the Gemini docs (or meetings) summarized  
- Approximate token usage for the run  

In Slack MCP, DMs use your Slack user ID as `channel_id` (see the Slack tool description for the acting user).
