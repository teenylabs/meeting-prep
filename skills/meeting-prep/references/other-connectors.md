# Other common connectors (beyond the default Google + Slack + Notion stack)

The routine is tool-agnostic: it discovers whatever tools each connected app exposes (via ToolSearch) and uses them. **Exact tool names differ per connector — find them at runtime, don't assume them.** This file maps the common alternatives to what each category needs. For the Google Calendar + Gmail + Slack + Notion + Google Drive stack in exact detail, see `default-stack.md`.

Golden rule: whatever the owner has connected, use it for **read** context; the ONLY thing ever written is the calendar (the private prep events, and — if used — the calendar profile store).

## Calendar (the one required category)
- **Google Calendar** → see `default-stack.md`.
- **Outlook / Microsoft 365 Calendar** → discover its list-events and create-event tools. Create the prep event as: **private**, reminders/notifications **off**, a distinct **category or color** so it stands out, **no attendees**, with start/end/timezone matching the source exactly. Put the same literal marker `AUTOPREP|source=<SOURCE_ID>|v=1` in the body, and find existing prep events by searching for that marker.

## Email (optional)
- **Gmail** → `search_threads` (see `default-stack.md`).
- **Outlook Mail** → use its message/thread search to test prior contact and pull meeting context. Same rule everywhere: routine scheduling/logistics chatter is NOT substantive prior contact.

## Chat — read-only (optional)
- **Slack** → see `default-stack.md`.
- **Microsoft Teams** → resolve the person and read your 1:1 chat with them, READ-ONLY. Many meetings are arranged entirely in Teams chat with no email trail, so mine it for the "Why this meeting" topic. Never post, react, or send.

## Notes — where the full brief lives (optional)
- **Notion** → see `default-stack.md`.
- **Google Docs** → create the brief as a doc under the owner's chosen `brief_home` (a Drive folder); keep headings and clickable links.
- **Obsidian / other note apps** → create a note in the owner's chosen location.
- **No notes app connected** → the full brief goes in a Claude artifact or directly in the calendar event (see the main skill's Output section). Never skip a meeting for lack of a notes app.

## Files — fallback brief home (optional)
- **Google Drive** → see `default-stack.md`.
- **OneDrive / SharePoint** → same fallback role: write the brief as a doc there when there's no notes app and the owner set a files fallback.

## Any other context source (optional, but richer briefs)
- **Meeting transcripts (Granola, etc.)** → LIST recent meetings/notes and read the summaries for prior context and what the owner has discussed. Do NOT trust a natural-language "no meetings" as proof of empty — confirm with a direct listing.
- **A CRM (Salesforce, HubSpot, Attio, etc.)** → look up the person and their company for prior relationship and deal/activity history; use whatever account/contact/activity records the CRM exposes.
- **Docs & wikis (Confluence, SharePoint, Drive)** and **task/project trackers (Jira, Linear, Asana)** → search for anything about the person, their company, or the meeting topic, and fold it into the brief.

When a category has multiple connected options, use them all for context. When a needed tool isn't obvious, discover it with ToolSearch before assuming it isn't there.
