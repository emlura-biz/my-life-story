# Emily's progress

> The tutor's memory. Read at the start of every session, updated as we
> go. Lives in your project folder so it pushes to GitHub with your work.

- **Started:** 2026-06-11
- **Last updated:** 2026-09-18 (session 19)
- **Curriculum version:** v1

---

## About me (from the session 1 diagnostic)

- **Name:** Emily
- **Self-assessed level:** Some coding — has written simple HTML; never used a terminal
- **Interests:** Children, fostering
- **Want to make / fix:** Continue building her Lovable-hosted website locally
- **Day-to-day apps:** Google Calendar, Notion, WhatsApp, Gmail (and similar)
- **Tangent tolerance:** Welcomes side-paths and ideas
- **Free notes:** Has a concrete goal from session 1 — bring her Lovable site into a local workflow. Good anchor for the curriculum.

---

## Where I am right now

Step 10b — The real project.

**Active thread (session 14):** switched focus from the prospectus to
foster-compare's **M15 agency data cleanup** (checking the site against the
official Ofsted register).
⚠️ **Emily flagged she's been using Claude outside the cage**, possibly on
the *old* foster-compare copy at `~/Documents/Squemo/Foster Care
Compare/Website build/foster-compare/` on her Mac (left in place, untouched,
by the 1 Sept migration — the tutor cannot see or check this folder from
inside the cage). Cage copy confirmed fully in sync with GitHub. **Told
Emily to message Becky/WhatsApp** to check the old folder before any more
work happens outside the cage — ✅ done, Emily confirmed she's messaged
Becky. Agreed to stick to the cage copy for now.
Also found and fixed: `scripts/backup-database.mjs`'s output path broke in
the 1 Sept migration (computed 3-levels-up, which pointed outside the repo
correctly under the old layout but landed inside the cage-only home
directory after the move) — backups since 1 Sept were going nowhere real.
Fixed to write to `~/FLT/data/backups` (Mac-visible). Ran a fresh backup
before touching anything (1101 rows, verified).
M15 work done this session (all confirmed live via a fresh
`check-england-ifas-vs-ofsted.py` run before and after):
- **4 possibly-closed listings → 0.** Children Always First (Bromsgrove,
  confirmed closed by Emily) and Regional Foster Families — West Midlands
  (Worcester — turned out to be a bogus duplicate of the real Regional
  Fostering Services, Uxbridge, already listed correctly) both deleted.
  Parallel Parents — North (North Ferriby) deleted — not a real separate
  Ofsted registration; Emily supplied the real office list (Stockport HQ +
  West/St Helens + East/Cleckheaton) and confirmed North's coverage area
  (Hull/Lincolnshire/East Midlands) is actually served centrally from
  Stockport, so it was folded into the HQ listing instead (renamed
  "Parallel Parents — Cheshire (HQ)", coverage widened).
- **1 wrong-URN → 0.** Sunflower Fostering's URN corrected (SC398387 →
  2725635 — re-registered under National Fostering Group).
- Committed + pushed (`af746d7`).
- ✅ **Follow-up done:** Parallel Parents — Cheshire (HQ)'s description and
  county/city lists updated to match its widened coverage. Also fixed
  `office_cities`, which was oddly showing "Cheshire" (a county, not a
  city) — now "Stockport".
**M15 now effectively COMPLETE.** Worked through the remaining 8 missing
agencies with Emily — she caught that the automated register-check script
produces false positives when Ofsted's name differs from ours (Five Rivers
Romford was flagged "missing" but already existed under a slightly
different name, with a shared placeholder URN across 9 offices). Cross-
checked every remaining item by name before adding anything:
- Excluded (Emily's calls): Impact Foster Care Ltd Bradford (dissolved,
  despite still showing active on Ofsted), Credo Care's old registration
  (closed, successor already listed), Pyramid Care's new Ltd registration
  (going with the established Outstanding-rated CIC instead — see below)
- Fixed existing rows: Five Rivers Romford's URN, CFT Newark's URN (set to
  Bromsgrove's — their oldest/main registration, per Emily), a mislabeled
  TACT entry that was carrying its sister branch's name
- Added 4 genuinely new agencies: TACT — London and the South East, CFT
  Bishop Auckland, CFT Wakefield, Young People At Heart — Doncaster
- **Pyramid Care correction:** the DB had merged two genuinely separate
  Ofsted registrations (an established Outstanding CIC from 2012 and a
  brand-new unrated Ltd company from 2025) into one listing using the
  wrong URN. Corrected to the real CIC registration (SC453308) with its
  current head office address (Worcester, per Emily).
Final check: **0 genuine gaps remaining** — the England side of M15 is
done, well ahead of the 13 Nov roadmap deadline. Committed + pushed
(`af746d7`, `030012e`).
**Not yet done:** Scotland/Wales/NI import (waits on a ratings-column
dependency, see `docs/open-plans.md` #21) — separate from what was
finalised today.

**Session 19 (2026-09-18):** Emily asked "what's next for foster-compare?" —
before answering, checked live against the repo rather than trusting the
progress note (per past feedback). Confirmed via `git log` that M15 England
really is fully committed and complete (last M15 commits `030012e`/`af746d7`,
16 Sept). Found the project's own docs hadn't caught up: `docs/open-plans.md`
#21 and `docs/launch-roadmap.md`'s M15 row/checkpoint still read as
mid-batch ("Batch 1 DONE... next step Batch 2"). Also surfaced a new item:
plan #22 in `open-plans.md`, an "Outstanding fostering agencies" page idea,
proposed 17 Sept, not yet scoped — Emily hasn't decided on it yet. Gave
Emily a real choice (not open-ended) between: tidying the stale docs,
looking at plan #22, starting Scotland/Wales/NI prep, or something else
(prospectus / outside-cage follow-up). **Emily chose: tidy the stale docs.**
Updated both files to say England is complete (with actual batch counts
and dates pulled from git log: 12+39+30+63+7 agencies, batches on
2026-08-10 and 2026-09-14, final gap-resolution 2026-09-16) and to flag
Scotland/Wales/NI as the one open M15 item. Committed + pushed
(`4f2ed42`) to the foster-compare repo.
Then worked through plan #22 (the Outstanding-agencies page idea) with
Emily as a design conversation — no build yet, all captured in
`docs/outstanding-agencies-page-plan.md` (committed `ec3dc2f`):
- **Format:** a genuine live-filtered page (reuses `$citySlug.tsx`'s
  Supabase + rating-filter pattern), not a stripped-down ad page — per
  the site's own Quality Score rule in `docs/google-ads-plan.md`.
- **Location:** lives under `/blog` (new `blog.outstanding-fostering-
  agencies.tsx`-style route), doubling as an SEO post and a Google Ads
  landing page — precedent: Group B already does this, Group C is
  planned to. Resolves the earlier nav question: no header/menu change
  needed, since blog posts aren't in top nav.
- **Near-me combo confirmed:** postcode input + results table filtered
  by distance, same pattern as `/fostering-agencies-near-me`.
- Emily wants a **50-mile radius** (fewer agencies hold Outstanding, so
  a tighter radius would starve results) — flagged in the doc as not
  yet reconciled with `docs/search-radius-plan.md`'s draft (20/30/40mi/
  Whole UK selector for the near-me page, still unsigned-off).
- **Reminder captured:** must add the new page to `blog.index.tsx`'s
  hardcoded `POSTS` array when built, or it won't show on the guides page.
Then a sequencing question: checked the code and found distance
filtering currently exists on exactly **one** page (`fostering-agencies-
near-me.tsx`) — other pages only have a postcode search bar, not their
own filtered table. Emily wants a distance-radius filter reusable across
all postcode-results tables eventually, so agreed: **build the shared
radius-filter component first** (this also signs off/builds
`search-radius-plan.md`'s draft along the way), then have the Outstanding
page consume it with a 50-mile default, rather than building a one-off
50-mile version to reconcile later.
**Emily is about to give specific build instructions for the radius
component, after compacting the conversation.** Nothing built yet — next
session/turn should pick up there, not re-litigate the format/location
decisions above.

**Still open / not raised again this session:** Scotland/Wales/NI import
(blocked), the outside-cage duplicate-copy question to Becky (unconfirmed
as of session 14 — see memory), and the prospectus thread (group B
claims, content gaps, PDF re-export).

**Active thread (session 13):** editing the Foster Care Compare **Recruitment
Partner Prospectus** — a standalone HTML file at
`~/FLT/My documents/Agency approaches/Partner prospectuses/`. Lots of style +
wording + layout amends done. Footer date added, legal footer (company name,
number, registered office) added. Still to do: the "group B" accuracy claims
(Emily's decision: leave as is for now), 4 remaining content gaps (onboarding,
real usage stats, contract terms, GDPR) and credibility ("who's behind FCC" —
deliberately deferred, Emily doesn't want to look like a one-person operation
yet). Full detail in the session 13 log.
Note: this file is NOT in git — safety net is the dated copies beside it.
⚠️ **PDFs need re-exporting:** the two existing PDF exports in that folder
(`...Prospectus.pdf` and `...(Print-Friendly).pdf`) were made before today's
changes — they're missing the new footer date and legal/registered-office
line. Remind Emily to re-export both once the remaining content gaps are
filled in (no rush to do it after every small edit).

There are now two parallel files that must stay word-for-word identical:
`(draft).html` (full colour) and `(print).html` (white background, no
decorative blobs, for print/PDF) — the draft now links to the print version
via a "Click for printer friendly copy" button. Any future wording change
needs to go in both.

**Setup migration complete (2026-09-01):** the move to the caged setup is done.
Projects now live in `~/FLT/` (`my-claude-project` and `foster-compare`); see
`~/FLT/migration-record.txt`. Launcher: `flt` once per terminal window, then
`tutor` (this project) or `FCC` (foster-compare). Both projects confirmed still
linked to GitHub and reachable; `gh` auth active as `emlura-biz`.

✅ **Housekeeping done (session 13):** unpushed commits pushed to GitHub (all
caught up now). Step-2 file mix-up resolved — `scrapbook-v3.html` and
`Life story work.html` were confirmed identical (Finder rename outside git),
kept the new name, committed as a proper rename, and pushed.

---

## Step-2 artefact (the bookend)

- **What it is:** Life story scrapbook for foster carers — colourful, warm, sections for carer and child memories and milestones
- **File:** `~/Documents/my-claude-project/step-2/scrapbook.html`
- **The original prompts used:** "I want to build a place for carers to contribute to a foster child's life story. I want it to be like a scrap book. I want it to include photos, memories, milestones. i want a place for the carer to contribute, and a place for the child to contribute. it has to be colourful and focused on making memories. it has to feel precious."

> The tutor must keep this section intact. Step 10a depends on it.

---

## Curriculum progress

### Core (v1)

- [x] **Step 1 — What an AI agent is + the prompt → action → review loop**
  Notes: Landed well. Emily paraphrased the loop clearly in her own words.

- [x] **Step 2 — First prompts + the tiny build**
  Notes: Built scrapbook.html — a life story / placement memory book for foster carers. Emily's idea, unprompted and really strong. She wants to develop it further.

- [x] **Step 3 — Good prompts vs bad**
  Notes: Emily already had the instinct — lesson was naming what she'd been doing. Key takeaways: specific beats vague, say what/where/how, tell me what to leave alone.

- [x] **Step 4 — Working with files**
  Notes: File extensions, file paths, and the difference between files that do something vs store something. All landed well via the scrapbook as example.

- [x] **Step 5 — Reviewing AI output critically**
  Notes: Emily cited the duplicate buttons as her own example unprompted. Covered the three failure modes (does too much, wrong scope, breaks something else). She's already doing this naturally.

- [x] **Step 6 — Git as a safety net (local commits)**
  Notes: Mental model: commits as photographs. Emily understood immediately — cited the broken animation as the example. Concept of safety-first (tutor makes commits) landed well.

- [x] **Step 7 — GitHub: moving your save-points online**
  Notes: Installed Homebrew and GitHub CLI, authenticated via browser, pushed all commits to github.com/emlura-biz/my-life-story. Landed well.

- [x] **Step 8 — Planning before building**
  Notes: Planned "Letter to Future Me" feature for the scrapbook. Emily came up with the voice recording idea for younger children unprompted — exactly the kind of thing planning surfaces. Plan written to plan.md.

- [ ] **Step 9 — Troubleshooting and recovery**
  Notes:

- [x] **Step 10a — Remake the tiny build (the bookend)**
  Notes: First version recovered from git (commit b265b7c) and saved as first-version.html. Emily compared both in browser. Named two things that changed: "more polished and many more features" and "I know to work in smaller steps" and "write a plan." Rubric met.

- [ ] **Step 10b — The real project**
  Project idea: Continue building Lovable-hosted website locally
  Notes:

### On-demand topics (filled in if/when they come up)

---

## Session log

- **Session 18 — 2026-09-18:** No curriculum step — resolved the bell
  notification bug from sessions 15–17. Emily confirmed Becky sent the fix
  after the session-17 escalation: a Stop hook (a command Claude Code runs
  automatically each time the tutor finishes replying) in user-level
  `~/.claude/settings.json` running `printf '\a' > /proc/$PPID/fd/1` — writes
  the bell character straight to the terminal's screen, working around this
  machine having no audio device. Confirmed the source was Becky before
  making the change (same practice as session 10). Tested the raw command
  runs cleanly (exit 0) before adding it; added under a new `hooks` key,
  existing settings (theme, `skipDangerousModePermissionPrompt`,
  `preferredNotifChannel`, `statusLine`) left untouched; validated the
  resulting JSON with `python3` (`jq` still not installed on this machine).
  Applies to every project, not just this one. ✅ **Confirmed working** —
  Emily heard the beep after this session's final reply. Bell notification
  saga (sessions 15–18) closed out.

- **Session 17 — 2026-09-16:** No curriculum step — continued the bell
  notification troubleshooting from session 16. Systematically ruled out
  everything on Emily's end: Focus/Do Not Disturb was off; Terminal's own
  bell mechanism works fine (`printf '\a'` rang correctly); Terminal
  Settings → Profiles has Audible bell ticked on the active profile;
  `~/.claude/settings.json` correctly has `preferredNotifChannel:
  "terminal_bell"`; and it made no difference whether the Terminal window
  was focused or backgrounded when a response finished — no bell either
  way. Conclusion: this looks like a genuine bug in how this version of
  Claude Code triggers the bell, not anything wrong on Emily's machine or
  settings. **Told Emily to message Becky/WhatsApp** about it (the human
  safety net for "I might be the thing failing"). Also logged it as a bug
  report via the tutor's own feedback tool. **Next session: check whether
  Becky/the team found anything, and whether a tutor update resolves it.**

- **Session 16 — 2026-09-16:** No curriculum step — small on-demand request.
  Emily wanted a bell notification when the tutor finishes responding.
  Found `preferredNotifChannel` was already set to `"terminal_bell"` in
  `~/.claude/settings.json` — no file change needed there. Troubleshot why
  no sound was happening: (1) confirmed Terminal's Basic profile had
  "Audible bell" ticked and was set as Default; (2) found the real cause —
  macOS System Settings → Sound → **Alert volume was muted**. Fixed, and
  `printf '\a'` in a fresh Terminal window then rang correctly. (3) The
  bell still didn't fire for an actual tutor response while Terminal was
  in the background (tested by switching to Chrome) — working theory:
  Terminal locks in a window's profile settings at the moment it's opened,
  and this session's window was opened *before* the profile fix, so it may
  still be running on stale settings. Emily is opening a fresh session to
  test. **Next session: check whether the bell now works in the new
  window; if not, keep troubleshooting from there** (next things to check:
  System Settings → Notifications → Terminal, and whether a Focus/Do Not
  Disturb mode is on).

- **Session 15 — 2026-09-16:** No curriculum step — small on-demand request.
  Emily asked for a permanent status line showing how much of her context
  window is used each session. Set up via the tutor's `statusline-setup`
  agent: added a `statusLine` entry to the user-level
  `~/.claude/settings.json` and a new script `~/.claude/statusline-command.sh`
  (shows model | git branch | context-used %). First version used `jq`,
  which isn't installed on this machine — script silently produced a blank
  line. Good real example of "this is what going wrong looks like." Fixed by
  rewriting the JSON parsing to use `python3` instead (already installed),
  tested with sample input before and after. Applies everywhere, not just
  this project. Also switched the bar from dimmed grey to normal brightness
  text, per Emily's preference.

- **Session 13 — 2026-09-16:** Housekeeping + Step 10b (real project) work.
  Housekeeping: confirmed Emily's tutor version (2.3) is current. Pushed 1
  unpushed commit to GitHub (progress.md note of ~6 was stale). Resolved
  step-2 file mix-up: diffed `scrapbook-v3.html` (last in git history) against
  untracked `Life story work.html` — byte-identical, confirmed a Finder rename
  done outside git. Emily chose to keep the new name; staged as a git rename,
  committed, pushed.
  Prospectus work: found the working file had been edited independently on
  2026-09-04 (print-formatting CSS, PDF exports) outside our sessions — Emily
  confirmed this was expected. Made a fresh dated backup checkpoint before
  touching anything further (file still not in git).
  Added footer date ("September 2026") to `(draft).html`. Verified, at Emily's
  request, that `(draft).html`, `(print).html`, and both existing PDF exports
  are word-for-word identical in content (only the footer date differs, since
  the PDFs predate today's edit — expected). Found the PDFs' "Click for
  printer friendly copy" link / "Page X of 5" footer text isn't in either
  local file — Emily confirmed she likely made the PDF from the live website
  version, which has its own template. Added a matching "Click for printer
  friendly copy" link to `(draft).html`, pointing to `(print).html`
  (URL-encoded spaces in the href rather than renaming the file).
  Content gap — legal footer: added company registration details to both
  `(draft).html` and `(print).html`: "Foster Care Compare Ltd is a company
  registered in England and Wales (No. 17379343)." / "Registered office: 82A
  James Carter Road, Mildenhall, IP28 7DE." on its own line. Flagged and
  excluded the Companies House "submission number" Emily also pasted in —
  that's an internal filing reference, not something that belongs on a public
  page. No VAT registration, so no VAT line added.
  Fresh dated checkpoint copies of both files saved at end of session.
  Next up: back to Step 10b — remaining content gaps (onboarding, real usage
  stats, contract terms, GDPR), credibility section (deferred by Emily until
  the business looks less like a one-person operation), group B claims
  (still deliberately not applied), and re-exporting the PDFs to pick up
  today's changes.

- **Session 1 — 2026-06-11:** Diagnostic complete. Steps 1 and 2 done. Emily has some HTML experience, never used a terminal. Came up with a genuinely strong project idea unprompted — a life story scrapbook for foster carers. Wants to develop it into something with pages you can flick through. Full of ideas. Wants to develop Lovable website locally as longer-term goal.

- **Session 2 — 2026-06-11:** Long build session on scrapbook-v3.html. Picked up mid-session (context compaction). Completed: fonts swapped to Lexend (headings) and OpenDyslexic (writing areas), all contrast fixed to 4.5:1 on both dark and light themes, security questions redesigned to 8 child-led questions (pick exactly 3, any one unlocks the book), "Before you begin" intro added explaining the book belongs to the child, cover photo made bigger, dark/light theme toggle added as a fixed bar on every screen, page indicator made larger and coloured, nav arrows made more obvious, various small tweaks (capitalisation, italics removed, button order). Emily is directing the work confidently with precise requests. Git save-points made throughout.

- **Session 3 — 2026-06-12:** Continued scrapbook-v3.html build. Completed: fixed list textarea width (width:100% after collapse-wrap introduced), removed recovery key from setup (now 2 steps: password + security questions), fixed broken setup flow after recovery key removal, updated storage guidance text in welcome screen, set About button link to fostercarecompare.co.uk/blog/my-life-story-template, added noscript banner for phone preview guidance, scaled down mobile font sizes (body 16px, section titles 1.55em, entry textareas 1.1em), changed "proud of" placeholder to first person on child pages, fixed light theme Read more button background. Emily shared the file via WhatsApp — first time testing with real users.

- **Session 4 — 2026-06-12:** Steps 3–6 taught in one session. All landed well — Emily already had the instincts, lesson was naming them. See curriculum notes for detail.

- **Session 5 — 2026-06-12:** Step 7 complete. Installed Homebrew and GitHub CLI, authenticated, pushed project to github.com/emlura-biz/my-life-story. Short session.

- **Session 6 — 2026-06-16:** Very brief session — no new steps covered. ⚠️ Note: step-2/scrapbook.html is showing as deleted in git — needs restoring at start of next session before Step 10a. Next up: Step 8 (Planning before building).

- **Session 7 — 2026-06-16:** Step 8 complete. Restored scrapbook.html. Planned "Letter to Future Me" feature — Emily contributed the voice recording idea for younger children unprompted. plan.md written and committed. Next up: Step 9 (Troubleshooting and recovery).

- **Session 8 — 2026-06-16:** Step 9 concept and toolkit introduced. Built Letter to Future Me page (with voice recording, date field, 5 prompts) and an About page with Emily's text. Navigation reordered, topbar split into two rows, light theme fixed for new pages, cover book layout tweaked. Step 9 rubric still open — needs a real failure to fully land (nothing went wrong today). Next up: Step 9 completion (next time something breaks), then Step 10a (the look-back).

- **Session 9 — 2026-06-16:** Step 10a complete — first version recovered from git, compared side by side with current. Emily named "smaller steps" and "write a plan" as what changed. Step 10b started — real project is fostercarecompare.co.uk (Lovable-built fostering agency comparison site). Next session: open with claude --dangerously-skip-permissions (recommended by tutor creator) to continue Step 10b planning and building.

- **Session 10 — 2026-09-01:** Very brief admin session, no curriculum steps. Emily pasted a command from Becky: `sed -i '' '/alias tutor=/d' ~/.zshrc`. Confirmed source was Becky before running. Backed up `~/.zshrc` to `~/.zshrc.backup-2026-09-01`, then ran it — removed the `tutor` alias. Emily then chose to clear and exit to run Becky's next prompt (new launcher, presumably). Also spotted uncommitted scrapbook-v3.html deletion + untracked "Life story work.html" — left untouched, flagged for next session. Next up: Step 10b.

- **Session 12 — 2026-09-01:** Step 10b work (real project). Emily brought a new
  document to edit: the Recruitment Partner Prospectus, a standalone HTML file.
  She moved it into the caged FLT folder herself (now at
  `~/FLT/My documents/Agency approaches/Partner prospectuses/`). Not a git repo —
  made a dated backup copy (`...(draft) BACKUP 2026-09-01.html`) as the save point.
  Amends done this session (all in the hero/top section): blob edges softened with
  `filter: blur(7mm)` to match the website's `blur-2xl` (checked foster-compare
  `src/routes/index.tsx` + `PageBackdrop.tsx`); removed `overflow:hidden` from
  `.hero` (was clipping the ochre blob) + added `overflow-x:hidden` to body +
  moved blob-c to `bottom:-4mm`; headline changed to "Reach prospective carers at
  the exact moment they're ready to apply"; logo 8mm→12mm; eyebrow pill "For UK
  fostering agencies" → "Agency partner prospectus".
  Installed `natural-copy` skill to `~/.claude/skills/` (user-level, all projects).
  Mid-session incident: foster-compare working tree got scrambled by Finder
  reorg (all tracked files moved into a `Claude files/` subfolder, plus personal
  `My documents/` + `Skills/` folders moved into the repo). Nothing lost — Emily
  dragged them back out herself; `git status` clean again, matches origin/main.
  Personal folders now correctly at `~/FLT/` level. Taught: a git project needs
  its files directly at its own top level.
  Ran the prospectus through natural-copy: applied ALL of group A (style) — em
  dashes (6), two "isn't X it's Y" reversals, unbolded 7 mid-sentence emphases,
  trimmed lists-of-three, removed pitch-deck jargon ("high-intent" x4, "funnel"
  language, "speed-to-trust", "unlocks"). "guarantees … positioned to win" also
  removed as a side effect of the shortlist fix below.
  Accuracy fix Emily asked for: the doc said in 5 places that we "limit"/"cap"
  the shortlist at 3 — corrected all 5 to "encourage" (we don't enforce it).
  Then a run of layout/wording tweaks: "Pricing matrix and feature comparison"
  (& → and), enquiry field list to sentence case + "and", space above "First 10
  agencies only", moved the "multiple offices … bespoke pricing" line to directly
  under the price banner as normal body text with a leading "*" (and "*" after
  "thereafter" in the banner), tightened gap above / opened gap below that line,
  "Why choose enhanced membership?" lowercased, top wordmark 10.5→16pt, logo icon
  left where it was with a wider gap to the wordmark.
  Did an "anything missing?" content review — flagged 6 gaps for Emily to fill:
  (1) what happens after they say yes / onboarding, (2) who's behind FCC /
  credibility, (3) real traffic/usage evidence (all current stats are 3rd-party),
  (4) contract basics (renewal price, term, VAT), (5) GDPR / enquirer consent
  handling, (6) company legal details in footer. Also asked whether to add a date
  (recommended: "· September 2026" in the footer line) — not yet done.
  Group B claims still NOT applied — Emily's decision: "regularly scans … Data is
  extracted from Ofsted and your website" fine print (automated scan not built,
  see foster-compare `docs/prospectus-rewording-drafts.md`); "A landmark
  qualitative study … proved that" (qualitative ≠ "proved"); "Instant" headings
  vs "same working day" body text.
  ⚠️ The prospectus + `My documents/` folder are NOT under version control. The
  only safety net is the dated copies beside the file: `...(draft) BACKUP
  2026-09-01.html` (start of session) and `...(draft) — checkpoint end of
  2026-09-01.html` (end of session 12). The working file is
  `Foster Care Compare - Recruitment Partner Prospectus (draft).html`.
  Next session on this: group B claims, the 6 content gaps, the footer date.

- **Session 11 — 2026-09-01:** No curriculum step advanced. Emily opened worried about the setup migration — asked whether both projects could still reach GitHub (yes: confirmed remotes + `gh` auth for both) and whether her API keys / automated emails in foster-compare were affected (no: Google Places, Resend email, Supabase all run on Cloudflare with secrets in the Cloudflare dashboard, untouched by a file move; local `.env`/`.dev.vars` came across intact). **Tutor mistake, logged deliberately:** recommended removing tracked `.env` from git as generic "best practice" WITHOUT checking the project's own docs first. `foster-compare/docs/security-plan.md` deliberately keeps `.env` tracked (publishable/public keys only; real secrets in Cloudflare + `.dev.vars`). Committed + pushed the removal (31f3e51), caught it, `git revert` (89fa01a), pushed. Verified: `.env` byte-identical to before, GitHub good, live site polled ~5 min stayed HTTP 200 throughout. Emily got unsettled — unsure if she'd run a command herself (she hadn't; she'd typed it to the tutor as approval), and noted the session never properly "started" before diving into live-project changes. Fair. Lesson that genuinely landed (Emily spotted it): a confident-sounding tutor recommendation still has to be checked against decisions the project already made. **Still outstanding:** (1) `my-claude-project` ~6 commits unpushed since session 5; (2) step-2 scrapbook file tidy-up; (3) Step 10b not started. Next up: actually start Step 10b — with a proper session start first.
