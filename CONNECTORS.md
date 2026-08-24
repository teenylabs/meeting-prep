# Connectors

## How tool references work

This plugin describes its workflow in terms of tool **categories** (marked `~~category`) so anyone can use it with whatever tools they've connected. Connect one tool per category you want. The recommended default stack is called out below and has exact, ready-to-run specifics in `skills/meeting-prep/references/default-stack.md`.

## Connectors for this plugin

| Category | Placeholder | Recommended | Other options |
| --- | --- | --- | --- |
| Calendar | `~~calendar` | Google Calendar | Outlook Calendar |
| Email | `~~email` | Gmail | Outlook Mail |
| Chat (read-only) | `~~chat` | Slack | Microsoft Teams |
| Notes (brief output) | `~~notes` | Notion | Google Docs, Obsidian |
| Files (fallback output) | `~~files` | Google Drive | OneDrive |
| Web search | — | built in | — |
| Any other source (read context) | `~~other` | — | Granola (transcripts), a CRM, Confluence, task/project trackers, etc. |

**Calendar** is the only hard requirement — it's how meetings are discovered and where prep events are created. **Email** and **chat** make the briefs much richer (chat especially: many meetings are arranged entirely over chat DMs with no email trail, and that DM is often the single most useful piece of context). **Notes** is where briefs are written; without it, briefs fall back to the **files** app.

The routine is **not limited to these categories**: it reads context from *any* source the owner has connected that might hold history on a person or meeting — meeting transcripts, a CRM, extra doc stores, task trackers, and so on. More connected sources means richer briefs, automatically.
