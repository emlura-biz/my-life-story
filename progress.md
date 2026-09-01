# Emily's progress

> The tutor's memory. Read at the start of every session, updated as we
> go. Lives in your project folder so it pushes to GitHub with your work.

- **Started:** 2026-06-11
- **Last updated:** 2026-09-01
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

**Active thread (session 12):** editing the Foster Care Compare **Recruitment
Partner Prospectus** — a standalone HTML file at
`~/FLT/My documents/Agency approaches/Partner prospectuses/`. Lots of style +
wording + layout amends done. Still to do: the "group B" accuracy claims, 6
content gaps (onboarding, who's behind FCC, real usage stats, contract terms,
GDPR, legal footer), and a footer date. Full detail in the session 12 log.
Note: this file is NOT in git — safety net is the dated copies beside it.

**Setup migration complete (2026-09-01):** the move to the caged setup is done.
Projects now live in `~/FLT/` (`my-claude-project` and `foster-compare`); see
`~/FLT/migration-record.txt`. Launcher: `flt` once per terminal window, then
`tutor` (this project) or `FCC` (foster-compare). Both projects confirmed still
linked to GitHub and reachable; `gh` auth active as `emlura-biz`.

⚠️ **`my-claude-project` unpushed commits:** local `main` is ~6 commits ahead of
GitHub (last push was session 5). Not a fault — just needs a push. Offer to do it.

⚠️ **To tidy next session:** `step-2/scrapbook-v3.html` is deleted in the working
tree (safe in git history, last at commit c2ded56). New untracked file
`step-2/Life story work.html` — looks like a rename done outside git. Sort out
which is the file to keep before doing more scrapbook work.

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
