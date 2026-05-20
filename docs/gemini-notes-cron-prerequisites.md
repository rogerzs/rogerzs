# Gemini notes → Google Doc cron (agent prerequisites)

This automation is intended to: read **Gemini Notes** from email (last hour), append summaries to a **Google Doc** in a fixed format, and notify via **Slack DM** when at least one note was summarized.

## What the agent needs

1. **Gmail (or equivalent)**  
   Read access to the inbox (or a dedicated label) to find messages from Gemini Notes and extract links or bodies. The Cursor cloud agent in this environment does not ship with authenticated Gmail; configure an MCP server or API credentials if email search is required.

2. **Google Docs**  
   Edit access to the target document. Unauthenticated `https://docs.google.com/document/d/.../edit` requests return the public sign-in page only; the agent cannot insert text without the Docs API or an authenticated integration.

3. **Slack**  
   To DM the owner with titles and token usage when summaries succeed, Slack must be usable (bot token or MCP Slack not in `needsAuth` state). The fixed channel/DM id used by the automation tool must remain valid.

## Summary block format (for the doc)

Each entry:

- Date of the Gemini Note  
- Title of the Meet  
- Resume (summary)  
- Link to the full Gemini note  

## Token usage

If the product does not expose per-run token counts to the agent, report that limitation in Slack rather than inventing numbers.
