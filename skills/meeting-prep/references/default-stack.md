# Default-stack specifics

Exact values for the recommended stack: **Google Calendar + Gmail + Slack + Notion + Google Drive**. If the owner uses other tools in a category, translate the intent (a private, muted, distinctly-colored calendar event; a rich-text notes page; read-only DM search; etc.).

## Tools to load (via ToolSearch)

- Google Calendar: `list_events`, `get_event`, `create_event`, `update_event`
- Gmail: `search_threads`
- Slack: `slack_search_users`, `slack_search_public_and_private`, `slack_read_thread`, `slack_read_user_profile` (READ-ONLY)
- Notion: `notion-search`, `notion-fetch`, `notion-create-pages`, `notion-update-page`
- Google Drive (fallback): `create_file`, `get_file_metadata`, `list_recent_files`
- Web search

## Calendar (Google Calendar)

- Discover: `list_events` on the primary calendar, now → 14 days, `orderBy` startTime, `pageSize` 100. Find already-handled sources with `list_events` `fullText="AUTOPREP"`.
- Prep event fields: `colorId` "8" (graphite), `visibility` "private", **`overrideReminders` set to an EMPTY array `[]`**, `notificationLevel` NONE, no attendees, `summary` "Prep: <source title>". `startTime`/`endTime`/`timeZone` exactly match the source.
- **`overrideReminders: []` is what actually silences the event, and it is required on every create AND every update.** These are two different settings and only one of them stops a popup: `notificationLevel` controls *emails to attendees* about the event (irrelevant here, since prep events have no attendees), while `overrideReminders` controls the *reminder alert that fires before the event*. Omitting `overrideReminders` does NOT mean "no reminder"; it means the event inherits the calendar's DEFAULT reminders, which for most people is a popup 10 minutes before. That popup is exactly what makes the routine feel intrusive instead of invisible. Pass the empty array explicitly every time.
- Part B: `get_event(source)`; if start/end differ, `update_event` on the PREP event only.

## Notes output (Notion)

- Parent for every brief: `{"type":"page_id","page_id":"<NOTES_HOME_PAGE_ID>"}`, from the profile's `brief_home`. (The original author's page was under a "Meeting Notes" page; each owner sets their own.)
- Title `Prep: <Person> (<Company>), <Mon D, YYYY>`, icon 📝.
- Content = Notion-flavored Markdown; if unsure of syntax, fetch `notion://docs/enhanced-markdown-spec` first. H2 headers, short bullets, inline `[text](URL)` links, callouts.
- Returned brief URL form: `https://www.notion.so/<id>`.
- Part C refresh: `notion-update-page` with `command="insert_content"` at `position {"type":"start"}` adding the `## What's new (as of <date>)` section.

## Email (Gmail)

- `search_threads(from:EMAIL OR to:EMAIL, plus the person's name)` to test prior contact and pull context.

## Chat (Slack)

- `slack_search_users` by name/email to resolve handle/ID (especially members of shared workspaces). Then `slack_search_public_and_private` restricted to DMs with that user. READ-ONLY: never post, react, schedule, or create canvases.

## Files fallback (Google Drive)

- `create_file` with `contentMimeType="text/plain"` (Drive auto-converts to a native Google Doc) in folder `parentId="<FALLBACK_FOLDER_ID>"` (from the profile's `fallback_home`), title `Prep: <Person> (<Company>), <date>`. ALL-CAPS headers, blank lines, "• " bullets, plain URLs in a LINKS section.

## Prep event description (HTML)

- Line 1: `<b>📝 Full brief (Notion, rich text, reflows):</b> <a href="<notion url>">Open the brief</a>` (or `📄 Full brief (Google Doc…)` for the fallback).
- Tight at-a-glance block: who they are; `<b>Why this meeting</b>` if Slack gave a topic; 1–2 connection points; 3–5 questions to ask.
- `<b>Key links:</b>` with 2–4 clickable `<a>` source links.
- Literal marker line: `AUTOPREP|source=<SOURCE_MEETING_ID>|v=1`
