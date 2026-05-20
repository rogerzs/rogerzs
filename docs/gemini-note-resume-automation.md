# Gemini note resume automation

## Output pattern (Google Doc)

Each resumed meeting should be appended using this structure:

```
[Date of the Gemini Note]
[Title of the Meet]
[Resume]
[Link to gemini note complete]
```

## What this environment needs to complete the workflow

1. **Email** — Incoming Gemini Notes notifications must be readable (for example Gmail API with a service account or OAuth, or a forwarding webhook). This Cursor automation has no configured mailbox integration.

2. **Google Docs** — The target document must be updatable via the [Google Docs API](https://developers.google.com/docs/api) (or Apps Script) using credentials that can edit  
   `https://docs.google.com/document/d/1fY7UTQHJ4q8e5nezqH9_41tE9poreAywjZsFmIXzl1U/edit`. Unauthenticated HTTP access only returns the sign-in page.

3. **Slack** — After at least one note is resumed, send a direct message with each document title resumed and token usage. That requires a Slack app with `chat.postMessage` (and `im.open` or user mapping for DMs), or an authenticated Slack MCP connection.

## Cron run log (agent)

When the above integrations are missing, the agent cannot read the last hour’s Gemini emails, cannot open private note links without credentials, and cannot write to the Doc. Per instructions, **no Slack message** is sent in that case.
