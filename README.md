# Meeting Prep

**Never walk into a meeting cold.** For every upcoming meeting with someone new, Meeting Prep quietly does your homework (who they are, why you're meeting, and a few smart things to ask) and leaves a private prep note right on your calendar, so it's one tap away when you need it. It keeps everything up to date on its own and never touches your real meetings.

**To start:** connect your calendar and say *"set up meeting prep."* After that, run it anytime with *"prep my meetings"*, or set it on a schedule so your prep is always waiting for you.

## Getting started (about 2 minutes)

1. **Install the plugin.**
2. **Connect your calendar.** That's the only thing it truly needs. Connecting email, chat, or a notes app (like Notion) makes the briefings richer, but none of them are required; you can add them later.
3. **Say: "set up meeting prep."** Claude takes it from here. It looks at your own activity (your calendar, and any email/chat/notes you've connected) and shows you a quick "here's what I know about you" draft (your background, what you're focused on, the kinds of meetings you take). You just confirm it or fix a line. No forms to fill out.
4. **Try it: "prep my meetings."** It'll find your upcoming meetings with new people and drop a prep note on your calendar for each. (If you skip step 3, running this the first time will walk you through setup automatically.)
5. **Optional but recommended: put it on autopilot.** Ask Claude to set up a recurring task like *"run my meeting prep every weekday at 7 AM."* Run it once a day, a few times a day, or only when you ask. Your call.

That's it. From then on, your prep is just… there, waiting on your calendar.

## What it does, each time it runs

- **Finds** your new meetings with people you haven't met, including holds you booked yourself (e.g. "Mariya coffee") and interviewers in an active interview loop, the ones most easily missed.
- **Digs up context** from whatever you've connected: the "let's meet about X" email or chat message that's often the real agenda.
- **Researches** each person (background, what they've built, how they think) and writes a short, skimmable brief tailored to you.
- **Drops a private prep note on your calendar**: muted and color-coded, with the highlights and key links right in the event, and a link to the full brief.
- **Keeps up**: re-times prep notes if a meeting moves, and refreshes briefs for meetings in the next 48 hours with any late-breaking news.

It only ever creates and maintains its *own* private prep notes. It never edits, moves, or deletes your real meetings, and it only ever reads your chat.

## Where the full brief lives

Wherever is easiest for you. If you've connected a notes app (Notion, Google Docs), briefs go there in one browsable place. If not, Meeting Prep can save each brief as its own private page (a Claude artifact) and link it, or just put the whole brief right in the calendar event. Either way, the highlights are always in the event itself, so there's nothing extra to open on the run.

## Running unattended (scheduled)

For the scheduled run to work while you're away, the tools it uses need to be allowed to run **without asking**, especially **web search** (for research), plus your calendar and connectors. If those still prompt for approval, a 7 AM run will just sit there waiting and appear to "do nothing." Set them to always-allow / auto-approve for the task when you turn on the schedule. (This is a permission you grant; a plugin can't enable it for you.)

The recurring schedule itself is a Claude Cowork feature (Cowork's scheduled tasks), so turning on autopilot happens in Cowork. Once it's on, the task runs in the cloud on its schedule using your connected accounts; it does not need your computer awake or the desktop app open. Running it on demand ("prep my meetings") works in any Claude interface that has your calendar connected.

## Making it yours

Adapt it freely. Nothing here can break it:

- **How often it runs:** it's just a recurring task you set up; change the time or frequency anytime, or run it only on demand.
- **What it knows about you:** re-run "set up meeting prep," or say "update my meeting prep profile to…". No files to edit.
- **A one-off tweak:** just say it when you run, e.g. "prep today's meetings but skip anything internal."
- **The actual rules:** to change built-in behavior (say, look 30 days out instead of 14), open a Claude session and ask it to customize the plugin; you'll get back an updated file to reinstall.

Each installed copy is independent, so your changes never affect anyone else's. And if a newer version is shared with you, reinstall it to pick up the changes (installs don't auto-update).

## What's in it

- **meeting-prep**: the routine that does the work above.
- **meeting-prep-setup**: the quick, guided setup that builds your profile from your own activity so briefs are about *you*. Run it once; re-run anytime.

## Tools / connectors

Only a calendar is required; everything else is optional and just makes briefs better. See `CONNECTORS.md` for the categories and options; the recommended default stack (Google Calendar + Gmail + Slack + Notion + Google Drive) has exact specifics in `skills/meeting-prep/references/default-stack.md`.
