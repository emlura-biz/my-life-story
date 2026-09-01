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

⚠️ **Launcher changed (2026-09-01):** Becky had Emily run
`sed -i '' '/alias tutor=/d' ~/.zshrc`, which removed the `tutor` shortcut from
`~/.zshrc`. Backup at `~/.zshrc.backup-2026-09-01`. Emily was going to clear/exit
and run "Becky's next prompt" — presumably a new launcher setup. If the learner
can't get back in, that's why; point them to Becky / the WhatsApp group.

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
