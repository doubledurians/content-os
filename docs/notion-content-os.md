# Notion Content OS

The production system lives in Notion. This repo is context, not a replacement.

## Access
- Workspace: **ucla** (not Bruin Ventures).
- In claude.ai it's reached via **Composio**, account `ucla-notion` (tools like `NOTION_QUERY_DATABASE_WITH_FILTER`, `NOTION_INSERT_ROW_DATABASE` with properties as a list of `{name, type, value}`, `NOTION_UPDATE_ROW_DATABASE`, `NOTION_GET_PAGE_MARKDOWN`). The native Notion connector stays on the BV workspace for a BV scheduled run.
- Claude Code does not inherit these. To work with Notion from here, set up a Notion MCP server pointed at the ucla workspace, or have her paste content.
- Rule: only add or update rows. Never delete.

## Structure (page "content OS" `41227be0-e133-8058-aa15-e5d3a677474a`)

One connected system: every reel is one row in the Reels DB; dashboard, reel pages and analytics are views of it.

| Piece | ID | Notes |
|---|---|---|
| Reels DB | `41227be0-e133-81e9-816a-eba6de073058` | Title prop `Reel`. Status: Idea → Scripting → Ready to Film → Filmed → Editing → Scheduled → Posted. Fields include Theme, Format (relation), Hook, Hypothesis, film/edit/post dates, metrics. Each page: theme, format, hook, re-hooks, her script, engagement strategy, fact-check to-dos, "what worked / what I'd change." |
| Brain Dump Inbox DB | `41227be0-e133-814c-a1bb-f5d34dd518a1` | Idea (title), Theme (relation), Raw note, Hook angles, Source (Google Doc / Notebook / Chat), Captured (date), Status (Sorted). |
| Format Library DB | `41227be0-e133-81a5-b19a-d595964d3d8d` | Title prop `Format`. Reusable hook/re-hook/story structures with creator examples, tiered (P1 = proven for her). E.g. "Myth or real", "Demo, then explain", "Question + 'Well... kinda'", "Series hook", "'The real genius isn't X, it's Y'", "Aesthetic one-liner + trending audio", "'Instead of scrolling' timestamp vlog". |
| Ideation page | `41227be0-e133-816d-a847-e1d3990cfb14` | Child page "Notebook" for photos of her physical notebook. A "Brainstorms with Claude" section sits at the top (one entry, 2026-11-10); no longer used, brainstorms now go to the Brain Dump Inbox. |
| Content Master Strategy page | `41427be0-e133-81f8-bdda-ccb31eeb6a07` | Strategic lens (IVP, follow promise, one-of-one, story). Mirrors `docs/content-master-strategy.md`. |
| Also | | Dashboard, Analytics, Weekly Learnings, System (automation rules), optional Brand partnerships list. Old "content hub" page left untouched. |

### Themes (page IDs for Theme relation)
- You Got Played `41227be0-e133-81fe-b532-f25c55933cf3`
- Your Brain, Explained `41227be0-e133-812e-9658-d83daea99789`
- Study Smarter `41227be0-e133-81db-bb92-e5ec93a14863`
- Science Deep Dives `41227be0-e133-8116-9934-f141c0781975`
- Startup Picks `41227be0-e133-8171-a3ef-d5693f3f2cdc`
- Life at UCLA / LA `41227be0-e133-81be-87e7-dd7babd48b9f`
- Notes to Self `41227be0-e133-8111-9c35-f1a5418e97c2`
- Parking Lot `41227be0-e133-8153-bd1f-e3cdc1b372ff` (off-niche or needs fact-checking)

## Idea capture
1. Brain dump Google Doc (ID `1Cx12Qqqz_PDYbitslOdrfaxebrOos7rpCsNX3pjcS8c`), dated entries like `2026-11-09`. Filed nightly.
2. Message Claude ("brain dump: ...") → filed right away with theme + 2 hook angles, Source = Chat. Same for any idea she brainstorms with Claude (rule set 2026-11-10): one Inbox row per idea, Status Sorted, with the discussion summarized in Raw note.
3. Notebook photo on the Ideation "Notebook" page → transcribed nightly.

## Automations (scheduled tasks in claude.ai, run automatically)
- **Content OS nightly sort**, 9:36pm daily: files new Google Doc / Notebook ideas into the Inbox with a theme and 2 hook angles. Skips duplicates. Full scripts become a "New script draft" row. Never writes scripts.
- **Content OS Sunday reset**, 8:36am Sundays: pulls Instagram insights (incl. trial reels) via her browser into Reels, writes a Weekly Learnings entry, re-tiers formats, drafts next week's film/edit/post blocks in Notion and her GCal "Content" calendar around existing events. If the computer is off, leaves a note asking for an Insights screenshot.
- **Wednesday evening midweek check** of the content schedule.
- **MinoAI nightly hooks + picks** (Claude Code desktop scheduled task, set 2026-11-10), ~10:34pm daily, runs after the nightly sort. Uses MinoAI Frontier + Composio. Appends a dated "MinoAI Frontier notes" block (hook/re-hook critique + options with creator citations) to the bottom of Reels pages in Idea/Scripting/Ready to Film. Since 2026-11-10 it also inserts the same hook/re-hook options as blue lines right after the matching lines in her script (new blocks only). Blue lines hold just the quoted line, no labels or dates, with a blue "OR" between alternatives (format set 2026-11-10). It also marks the parts it suggests replacing or cutting with blue strikethrough, keeping her words identical, and each strike has a blue option or "cut suggestion" line explaining it. If she removes a strikethrough, it isn't re-applied unless she edits that line. Promotes the top 2 Inbox ideas to Reels (Status Idea, preliminary hooks/re-hooks) and marks the Inbox row "Promoted to Reels", linking it to the new reel via "Became reel" (added 2026-11-10). From 2026-11-12 to 2026-12-12 (psych-in-tech month) it promotes tech-angle ideas first (score 6+), fills a slot with a non-tech idea only if needed and adds a "Tech-lens version" line to it; scores stay unchanged. After Dec 12 it goes back to the top 2 by score and flags the review. Sets "Engagement score" (1-10) + "Score why" on pre-filming reels. Only runs while the desktop app is open (catches up on next launch). Task file: `C:\Users\abiga\.claude\scheduled-tasks\minoai-nightly-hooks-and-picks\SKILL.md`.
- Depends on her moving reel cards between statuses after each step.
