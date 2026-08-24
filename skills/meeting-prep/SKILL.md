---
name: meeting-prep
description: Prepares briefings for upcoming meetings with people the user hasn't met, and manages a set of private "prep" events on their calendar. Use when the user asks to "prep my meetings", "run meeting prep", "sync my prep events", or has a recurring meeting-prep task. Discovers newly scheduled meetings (including self-created title-only holds that name a person, and interviewer/panelist slots in an active interview loop), gathers context from email and chat DMs, researches each person deeply, writes a scannable brief, and creates a private prep event linking it — then keeps prep events time-synced and refreshes imminent briefs with late-breaking news.
---

# Meeting Prep

Prepare briefings for upcoming meetings with people the user hasn't met, and manage a set of private "prep" events on their calendar. Each run does THREE jobs: (A) discover newly scheduled meetings with new people, gather context from email AND chat DMs, research the person deeply, write the brief, and create a private prep event that links it; (B) keep existing prep events time-synced to their source meetings; and (C) refresh briefs for imminent meetings (within 48h) with late-breaking news.

## What this is for — and guiding the user (read this first)

This may be someone's very first run. Be a guide, not a silent batch job.

- **Say what it does, up front, in plain language:** "I look at your upcoming calendar, find meetings with people you haven't met, research each person, and put a private 'Prep:' event on your calendar — with the key points (who they are, why you're meeting, a few questions) right in the event, plus a link to a longer, detailed brief — so you're ready. I keep those in sync and refresh them as meetings get close." When you mention connectors, be inclusive: it works with **whatever they've connected** — email, chat (Slack, Teams, etc.), meeting notes/transcripts, a CRM, and more all make the briefs richer — and specifically, **connecting a notes app like Notion or Google Docs lets it save a longer, full brief there** (without one, they still get a tight brief right in the calendar event or a linked page). Don't name only one or two products; frame it as "whatever you use."
- **Only a calendar is required.** Email, chat, a notes app, transcripts, a CRM — all optional, and they only make briefs richer. **NEVER block, nag, refuse, or stall because Gmail/email or any non-calendar source isn't connected.** Proceed with whatever is connected, and mention *once, lightly* that connecting more would improve results. Do not repeat the ask.
- **On first run (no saved profile), automatically kick off `meeting-prep-setup`** — don't wait to be asked. It leads with "here's what I know about you" from the owner's own activity and confirms it. That's what makes briefs personal. If the owner declines or it can't run, proceed with sensible defaults derived from their calendar and say so.
- **The deliverable that matters is the private prep EVENT on the calendar.** Creating these events is explicitly allowed and is the entire point of the tool — create one per new meeting (Part A). If a run ends with new meetings found but no prep events created, something went wrong; fix it, don't report success.
- **End every run by telling the owner what you did** — which prep events you created (with links), what you skipped and why — and offer to schedule it to run automatically.
- **The magic is that it's invisible.** Meeting Prep is designed to run on a schedule in the background, so prep is always ready without the owner asking. Getting the recurring schedule turned on (during setup) matters as much as any single run — if the owner isn't on a schedule yet, nudge them toward it.

## Step 0 — Load the owner profile (do this first)

Every brief is tailored to the user ("the owner"). Load their profile before anything else:

1. Read the saved profile, checking these in order and using whichever exists: (a) **memory** — a file such as `/meeting-prep-profile.md`, if memory tools are available; (b) a page titled **"Meeting Prep — Profile"** in the owner's **notes app**; (c) a private all-day **calendar** event titled **"Meeting Prep — Profile"** (find it by searching the calendar for the marker `MEETING_PREP_PROFILE`), reading the profile from its description. The calendar fallback means even a calendar-only user has a saved profile.
2. If no profile exists, run the **meeting-prep-setup** skill first (it interviews the owner and saves the profile), then continue.

The profile provides: `name`, `account` (the single email/calendar account to manage), `timezone`, `about` (background + current focus + meeting types + what they want from meetings — this tailors all research and talking points), `focus` (the owner's current priorities and any active multi-step processes to watch for — e.g. a job search, a sales pipeline, a fundraise, a hiring loop; this decides which meeting-type playbooks get emphasized), `brief_home` (where briefs are saved), `fallback_home`, and `connectors` (which tool the owner uses per category). Wherever this skill says "the owner", use this profile. Skip any context source whose connector the owner doesn't have.

## Connectors

Uses these tool categories (details in CONNECTORS.md; load tools via ToolSearch if not already present). If the owner is on the default stack (Google Calendar + Gmail + Slack + Notion + Google Drive), the exact tool names, fields, and markers are in `references/default-stack.md`. For other common connectors — Outlook Calendar/Mail, Microsoft Teams, Google Docs, Obsidian, OneDrive/SharePoint, Granola, a CRM (Salesforce/HubSpot), Jira/Linear/Confluence — see `references/other-connectors.md`, which maps each to what its category needs.

**`~~calendar` is the ONLY required connector** — it's how meetings are discovered and where prep events are created. **Everything else is optional.** Connect more for richer briefs, but never require, block on, or nag about any non-calendar source. If a source isn't connected, silently skip that context and continue.

- `~~calendar` — **required.** Read events; create/update the private prep events.
- `~~email` — *optional, recommended.* Search threads to test prior contact and pull meeting context.
- `~~chat` — *optional, recommended.* READ-ONLY. Resolve the person and read DMs for meeting context — valuable because many meetings are set up entirely over chat DMs with no email trail, but not required.
- `~~notes` — *optional.* Preferred home for the full brief. **If not connected, put the full brief directly in the prep event description instead** (see Output) — never skip a meeting for lack of a notes app.
- Web search — *optional.* Research people and late-breaking news.
- `~~files` — *optional.* Another fallback home for the brief if there's no notes app.
- `~~other` — ANY other source the owner has connected that may hold history on a person or meeting (meeting-transcript tools, a CRM, doc stores, task/project trackers, etc.). Read-only. More connected sources = richer briefs; use whatever is available.
- **Any other connected source** — READ context from whatever else the owner has connected that could hold history on a person or meeting: meeting-notes/transcript tools (e.g. Granola), a CRM (prior relationship/deal history), document stores (Drive, Notion, Confluence), task/project trackers, etc. Don't limit context-gathering to the categories above — more connected sources means richer briefs. Check what's available and use everything relevant.

## Output format — one brief per meeting

Every new meeting produces a private **prep event on the calendar** (always — the core deliverable) plus a **brief**. Decide where the full brief lives, in this order: (1) `~~notes` under `brief_home` if a notes app is connected — best, since all briefs live in one browsable place; (2) else a **private Claude artifact** — a hosted page with its own shareable link that reflows on mobile and can be updated in place, available without the owner connecting any notes tool — when artifact publishing is available this run; (3) else put the full brief directly in the prep event's own description. The at-a-glance summary always goes in the event description regardless, so it's never blank. Never skip a meeting because there's nowhere to write a separate brief.

- Title: `Prep — <Person> (<Company>) — <Mon D, YYYY>`.
- Rich text, ALWAYS in this opinionated house style (it is fixed, not a per-person setting — write every brief this way): scannable and front-loaded, H2 section headers, short bullets that lead with the key point, inline `[text](URL)` links, bold on only the few things that matter, callouts where useful. No walls of prose — assume the reader skims on a phone, so keep it tight and reflowable. This format is deliberately built to read well for everyone, including large-text/accessibility reading, without asking anyone to configure it.
- Keep the returned page URL — it is the brief link.
- FALLBACK when there's no `~~notes` app, in order: (1) publish the brief as a **private Claude artifact** and link it from the event, if artifact publishing is available; (2) else put the full brief right in the prep event description (always works, needs no other tool); (3) else write it to `~~files` under `fallback_home` if the owner set one. Either way, ALWAYS still create the prep event.
- ALWAYS also put the 2–4 most important links as clickable links in the prep event description, so they're one tap away on a phone.

## Critical safety rules

- You may ONLY: create new briefs and new prep events; change the TIME of prep events you manage; and update the DESCRIPTION/CONTENT of briefs + prep events you manage. A prep event = summary starts with `Prep:` AND description contains `AUTOPREP|source=`.
- NEVER edit, move, reschedule, change attendees on, or delete ANY real meeting or anything with other attendees. Treat every real meeting as read-only — INCLUDING the owner's own self-created holds. You may create a SEPARATE prep event pointing at a hold via `AUTOPREP|source=<hold id>`, but never modify the hold itself.
- `~~chat` is READ-ONLY. Never send, schedule, react, post, or create anything there.
- Prep events: NO attendees, private visibility, notifications off, and a distinct color so they're easy to spot.

## Part A — discover, gather context, research, create brief + prep event

1. List calendar events on the owner's account (now → 14 days ahead). Also find events already handled by searching for the `AUTOPREP` marker; parse `AUTOPREP|source=<ID>|v=1` and skip those sources.
2. CANDIDATE meetings = 2–5 total attendees, ≥1 EXTERNAL attendee (not the owner's own domain, not a room/resource), not declined, not all-day, not already handled, summary not starting `Prep:` (and never the private "Meeting Prep — Profile" storage event / any event carrying the `MEETING_PREP_PROFILE` marker), and NOT a recurring community/group/personal event (skip forums, lunches, squads, all-hands, demo nights, birthdays, generic "Hold for <x>", personal recurring like workouts/PT). Use judgment.

   ALSO treat as candidates — do NOT require the 2–5-attendee test for these; they were the #1 and #2 reasons preps got missed:
   - **Self-created, title-only HOLDS that name a specific person or company** — e.g. "Sandhya Databricks", "Mariya Coffee", "<Name> 1:1 / chat / sync / intro". The owner routinely books these with zero invitees. Resolve the named person from `~~email` / `~~chat` / the itinerary; do NOT skip merely because there's no attendee email. (A bare "Hold" naming no person/company is still a skip.)
   - **Meetings tied to an active, multi-step process the owner is in** (per their `focus` profile — e.g. a job-search interview loop, a sales cycle, a fundraise, a hiring loop where the owner is the interviewer, a partnership/BD deal). This includes coordinator/recruiter/scheduler syncs, logistics or prep calls, and additional-participant slots — EVEN IF the company/deal is already covered. These still get a prep, shaped person/logistics-only (step 4). Only apply this to processes the owner's profile actually says they're in — don't assume a job search or invent a process.

3. PRIOR-CONTACT + CONTEXT TEST (two jobs at once — gates NEW vs. known, AND collects the meeting topic):
   - **(a) `~~email`:** search for prior threads with the person (by address and name). Real prior back-and-forth on SUBSTANTIVE topics → already known, skip. BUT routine logistics/scheduling chatter does NOT count as substantive and does NOT suppress a prep: recruiter/coordinator time-wrangling, calendar invites, "looking forward", NDA or pre-work doc shares, intros. A recruiter/scheduler you've only traded logistics with is still NEW for prep purposes — and that trail is exactly the context the brief should use.
     - **RECENCY / reconnects:** weight how recent the contact is. If the substantive back-and-forth is months stale (the relationship has gone quiet), the person is still "known" — do NOT write a stranger's identity brief — but instead of skipping entirely, produce a light **reconnect refresh**: what's changed with them or their company since you last talked, why you might be meeting now, and 2–3 questions. Never describe a months-cold relationship as if it's current.
   - **(b) `~~chat`:** resolve the person's handle/ID by name and/or email (especially members of shared workspaces), then read DMs with that user. CLASSIFY what you find:
     - Pure meeting-setup chatter ("let's meet", "how about Tue", "see you then", or "let's meet about <TOPIC>") → still NEW for prep purposes — but EXTRACT the topic/agenda and quote/paraphrase it into the brief's "Why this meeting" section (the single highest-leverage piece of context).
     - Substantive prior back-and-forth on real topics → already known, skip prep.
   - **(c) Any other connected source:** also search whatever else the owner has connected for prior context and meeting topic — a meeting-notes/transcript tool (e.g. Granola) for past conversations with or about the person, a CRM for prior relationship/deal history, document stores for shared files or briefs, task trackers for related work. Fold anything relevant into both the prior-contact judgment and the brief. Substantive history in ANY source (not just email/chat) can mark a person "already known"; topic/agenda clues in ANY source feed "Why this meeting."
   - **(d)** If every connected source is quiet → high-signal NEW.
   - **(e) Multi-participant processes (e.g. interview loops) — only if the owner is in one:** read the relevant itinerary AND coordinator/recruiter emails for the NAMES of every participant — every interviewer/panelist in a loop, or every named person on a deal/partnership team — including names mentioned in passing ("the panel will be…") even when a slot is combined, virtual, or later changed. Prep each named person not already covered (person-only if the company/deal is covered). Don't let a single combined block (e.g. "Virtual Interview(s)") hide multiple people.
   - Note any `~~chat` context you used — the report should mention it.

4. For each candidate with ≥1 NEW external person, do DEEP, profile-grade research on the person: identity (with confidence), full career arc and what they personally built/owned, published work/talks, philosophy / what they care about, recent activity, "how to make a strong impression," connection points with the owner (per the profile's `about`), and tailored questions. Include a **"What they've written / how they think"** section: their articles, podcasts, interviews, talks, with short synopses and real links. NEVER fabricate URLs — only include links surfaced by real search results. RECENCY: weight recent signals over old ones — describe what the person is doing NOW; render stale facts in the past tense and date them; never assert a months-old status (a role, a project, a collaboration) as if it's current.

   Then shape the rest to the meeting, applying whichever of these playbooks fit the meeting AND the owner's active contexts (from `about`/`focus` — don't run a job-search or fundraising playbook for someone who isn't doing that):
   - **Customer / sales discovery:** buyer/user profile, pains/workflows, discovery question bank, hypotheses.
   - **Networking / catch-up:** connection points, talking points, asks/offers.
   - **Peer / founder chat:** skip company deep-dive — focus on what they're building now, their prior arc, and what a useful exchange looks like.
   - **Group / dinner:** who's-who roster + must-meet + hooks.
   - **Investor / fundraising** (owner raising): the fund/angel's thesis and check size, portfolio and relevant bets, what they tend to push on, and the narrative + questions to land.
   - **Hiring (owner is the interviewer):** the candidate's background and claims worth probing, role fit, and a tailored question set.
   - **Job interview** (owner job searching): company deep-dive, interviewer focus, likely questions + STAR answers, comp, questions to ask.
   - **Process logistics — recruiter / coordinator / deal-team sync** (person + logistics only; company/deal already covered — skip the deep-dive): who they are and their role in the process; the full sequence (who's involved when + what each step tests or covers); what to ALIGN on — for a job search that's leveling & comp (route to the recruiter), pre-work, format, timeline, accommodations; for other processes, the equivalent next steps and owners; and questions to ask them.

   Add or adapt playbooks as the owner's contexts require — the point is to match the meeting, not to force a fixed list.

   STRUCTURE: if `~~chat` gave you a topic, the brief MUST open with `## Why this meeting` quoting/paraphrasing the DM context — the highest-leverage section. If this is a 2nd+ meeting at a company already covered (check existing briefs, or `~~email`/`~~chat` for an earlier meeting), make it PERSON-ONLY — skip the company deep-dive.

5. Write the brief — to the notes app under `brief_home` if one is connected; else publish it as a private Claude artifact and keep its link (if artifact publishing is available); else the full brief goes in the prep event description in the next step. If any of these fails, do NOT abort — fall back to the event description and carry on.
6. **Create the prep event — this is the REQUIRED deliverable. Always create it, even if research was thin or no notes app was available.** Call the calendar's create-event tool with: summary `Prep: <source meeting title>`; start/end/timezone EXACTLY matching the source; private; notifications off; distinct color; no attendees. Description:
   - Line 1: if the brief has its own home (a notes-app page or a Claude artifact), a bold "Full brief" label with a clickable link to it; if it has no home of its own, put the full brief text here in the description.
   - Tight at-a-glance block: who they are; "Why this meeting" if `~~chat` gave a topic; 1–2 connection points; 3–5 questions to ask.
   - A bold "Key links:" line with 2–4 clickable source links.
   - Literal marker line: `AUTOPREP|source=<SOURCE_MEETING_ID>|v=1`
   After the create call, verify it succeeded (the event should be returned / now on the calendar). If it errored, tell the owner what failed — never report a prep as done when the event wasn't actually created.
7. Avoid duplicates — never create a second brief/prep event for a source already handled.

## Part B — sync prep events to source times

For each prep event (found via the `AUTOPREP` marker, including any just created): parse the source id and fetch the source. If the source is missing/cancelled, leave the prep unchanged and note it. Else if start/end differ, update ONLY the prep event to match exactly (notifications off). Never touch the source.

## Part C — refresh imminent briefs

For each prep event whose SOURCE meeting starts within the next 48 hours: do a quick recency check on the person/company (web search, last ~2 weeks: funding, product launches, role changes, notable posts/press). ALSO re-check `~~chat` DMs — and any other connected source (transcripts, CRM, docs) — for new activity since the brief was written that changes the topic or adds agenda. If anything material is new: prepend a `## What's new (as of <date>)` section to the brief, and refresh the Key links in the prep event description if relevant — keep the `AUTOPREP` marker, event summary, and event time unchanged. (For `~~files` fallback briefs: create a fresh file with "WHAT'S NEW" on top and repoint the prep event link.) If nothing material is new, note "no change." Only ever modify prep briefs/events — never the source.

## Report

Start by naming which connected sources you actually drew on this run (calendar, email, chat, transcripts, CRM, web) and flag any that were connected but empty/unavailable — never conclude a source is empty from a failed natural-language query alone; confirm with a direct listing. Then summarize: new briefs + events created (person, company, meeting time, brief link, AND whether `~~chat` DMs informed the "Why this meeting" section); candidates skipped (why — distinguish email-substantive vs. chat-substantive vs. recurring/group vs. bare placeholder hold); prep events re-synced (old→new); briefs refreshed under Part C (what was new — web news, fresh chat DMs, or both); any cancelled/missing sources. If nothing happened: "No new meetings to prep; all prep events in sync; no imminent briefs needed refreshing."

**Schedule check (manual runs only).** If this run was triggered by the owner by hand — not by a recurring task — check whether they already have a recurring meeting-prep schedule (list their scheduled tasks and look for one whose prompt runs meeting prep). If they DON'T, close by gently pointing out that the best part of Meeting Prep is that it runs on its own, and offer to make it automatic — name a concrete default out loud (twice each weekday, around **7:00 AM and 4:00 PM** their time — morning preps the day, late-afternoon catches meetings booked during the day and preps tomorrow) and give them the chance to pick different times or frequency, then create the recurring task (prompt "Run my meeting prep") and confirm exactly what you scheduled. The times are in the owner's LOCAL timezone — convert to UTC correctly so it fires at the intended local time, and verify that after creating. Offer this ONCE and respect a "no" — never nag on every manual run. (Skip this entirely when the run was itself fired by the recurring task.)

## Notes

- Lean toward over-preparing small external 1:1s when unsure, but never prep recurring community/group events or people with clear substantive prior correspondence.
- Self-created, title-only HOLDS that name a person (coffees, 1:1s, intros, and — if the owner is job searching — recruiter/coordinator syncs) ARE candidates — resolve the person via `~~email`/`~~chat`/itinerary even when the event has no attendee email. This was a top reason real preps got missed.
- "Company/deal already covered" means skip the deep-dive — it does NOT mean skip the meeting. Follow-up syncs, logistics/prep calls, and additional-participant slots tied to an active process the owner is in still get a light person/logistics-only prep.
- For multi-participant processes the owner is in (e.g. an interview loop or a deal team), enumerate every participant named in the itinerary OR coordinator emails (even combined slots or later-changed lineups) and prep each uncovered person.
- Chat DMs that are just meeting-setup chatter ("let's meet about X") count as NEW — and the DM topic is gold for the brief.
