# Emily's progress

> The tutor's memory. Read at the start of every session, updated as we
> go. Lives in your project folder so it pushes to GitHub with your work.

- **Started:** 2026-06-11
- **Last updated:** 2026-10-06 (session 34)
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

**Dated items (tutor: check at every session start):** in foster-compare run
`node scripts/check-refresh-due.mjs` and mention anything OVERDUE or DUE IN THE
NEXT 60 DAYS, plus anything listed as unmarked. Register: `docs/freshness-register.md`.

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
After compacting, Emily gave the build instructions: apply the city-pages'
filter bar to `/fostering-agencies-near-me` too, add a distance-radius
filter as a first-position replacement for "Fostering type" (data accuracy
concern), 10 options from 5 to 50 miles, default 25 instead of 20. Checked
with Emily first: Fostering type filter stays on city pages, only dropped
from near-me. **Built and shipped:**
- New reusable `src/components/DistanceFilter.tsx` — a dropdown, so it can
  be reused on the Outstanding-agencies page later with its own default.
- `src/lib/nearbyAgencies.ts`: `buildNearbyResults()` now takes the radius
  as a parameter instead of a hardcoded 20-mile constant.
- `fostering-agencies-near-me.tsx`: new filter bar (Distance first, then
  Organisation Type / Coverage / Ofsted, matching city pages), page copy
  updated to reflect the chosen distance instead of a fixed number, query
  restructured so changing distance re-filters locally with no new
  Supabase call.
- Emily then refined the options twice: dropped the 5-mile increments
  (now 10/20/30/40/50) and changed the default to 30 (not 25).
- Committed + pushed (`4869426`).
- Caught after pushing: a much more detailed, pre-existing plan for this
  exact feature at `docs/search-radius-plan.md` (20/30/40/Whole UK, radius
  saved in the URL, one-tap widen buttons, `llms.txt` update) that wasn't
  checked before building. `public/llms.txt` was genuinely stale ("within
  20 miles") — fixed. Checked for a real conflict with
  `docs/mobile-comparison-blueprint.md` (signed off, unexecuted, touches
  the same file's mobile cards) — no actual clash since that's untouched
  card markup, just flagged for whoever builds it later to preserve the
  new filter bar. Updated `search-radius-plan.md` with a "what actually
  got built" section so it's not mistaken for a live spec. Committed +
  pushed (`49abdb6`).
- Asked Emily about the two real remaining gaps (URL persistence for the
  radius, one-tap widen buttons on no-results) — **decision: leave both
  out for now.** Recommended revisiting URL persistence specifically for
  the Outstanding-agencies Ads page later, since a link opening straight
  at a fixed 50-mile radius is exactly what that page needs it for.
  **Emily confirmed: happy with the search feature as shipped.**

**Lesson for next time (self-correction, logged deliberately):** built a
feature from Emily's direct instructions without first checking `docs/`
for an existing plan covering the same page. Should grep `docs/` for
related plans before starting a build, even when given specific
instructions — a stale-but-relevant doc can carry real requirements
(here: the `llms.txt` line) that direct instructions don't repeat.

**Still open / not raised again this session:** Scotland/Wales/NI import
(blocked), the outside-cage duplicate-copy question to Becky (unconfirmed
as of session 14 — see memory), and the prospectus thread (group B
claims, content gaps, PDF re-export).

**Session 20 (2026-09-23):** Emily had been building the Outstanding-
agencies page (plan #22) herself in a Claude Code session since session 19
— well beyond what this file had recorded. That session got cut short by
Claude freezing, so she cleared it without a proper end-lesson wrap-up,
which is why this file was out of date, not because anything was lost:
git had everything safely committed throughout. Caught up by reading the
live repo instead of trusting this file (branch
`outstanding-agencies-seo-table`, PR #12, open): the page is built —
hero redesign, UK-wide static Outstanding-agencies table for SEO, a
persistent shortlist/compare explainer, and a 3-step "How it works"
section (the screenshot Emily opened this session with). Found and saved
one loose end: an uncommitted wording tweak to
`PostcodeSearchBox.tsx` (helper text moved above the form) — committed
and pushed (`b0e3f11`).
⚠️ `docs/outstanding-agencies-page-plan.md` itself is a little behind
the actual build too — its "How it was actually built" / "SEO revamp"
notes stop before the persistent explainer and "How it works" commits.
Worth a tidy pass next time something touches that doc, same pattern as
the M15 docs in session 19.
Per the plan doc's own "Still open" list, real remaining work on this
page: move the postcode search box out of the hero to sit closer to the
results table (flagged by Emily, not done), and a genuine browser
click-through (postcode search, mobile layout, no-results state) — so
far only checked via SSR HTML output, never live in a browser.
Next up: pick up one of those two items with Emily.

Continued straight on (same session, 2026-09-23) with live review on
localhost — Emily driving from the browser, iterating fast. Landed:
"How it works" section widened to match the filter bar/results below
and condensed on mobile (padding, gaps, number-beside-title layout,
blobs hidden on mobile); hero/subheading copy reshuffled a few times
before settling (subheading text moved to "How it works", removed a
redundant "See agencies near you" line, shortened the intro paragraph);
the shortlist toast reworked to wait for the results table to scroll
into view before a postcode search, and to word itself differently
before vs. after a search; a scroll-to-results jump added on mobile
when the search button is tapped, so results don't feel a distant
scroll away from the search box.
Then ran the page against `docs/seo-master-checklist.md` and
`docs/blog-post-checklist.md` (Emily's request — "check this against
the SEO checklist") — found and fixed 5 real gaps (title tag too long
and had an em dash, meta description too long, one more em dash in a
live FAQ answer, missing from `sitemap.xml`, missing from `llms.txt`)
plus 3 follow-ups (stale `dateModified`, blog index card excerpt out
of sync, post missing from blog-post-checklist.md's own list). Talked
through 3 judgement calls with Emily rather than assuming: skip the
site-wide sticky postcode bar and the location-directory CTA (both
would duplicate what this page's own search already does), but do add
a "Read next" card (linking to "How to Choose a Fostering Agency") for
consistency. Also added a new permanent rule to
`seo-master-checklist.md` Part 2: keep `dateModified` current whenever
a page is meaningfully edited after publishing, not just at first
publish — came directly out of catching it stale on this page.
All committed and pushed to PR #12's branch (`outstanding-agencies-seo-table`,
commits `b0e3f11` and `f34fcdd`). Not yet done: Emily's still-open
"move postcode box near results" idea from earlier in the session
wasn't picked back up (superseded in practice by the scroll-to-results
jump link, which solves the same problem more simply) — worth checking
with Emily next time whether that's still wanted or the jump link is
enough. PR #12 itself not yet merged.

**Session 21 (2026-09-23):** Small, focused request — cross-link the
`how-to-choose-a-fostering-agency` blog post to the new Outstanding-agencies
post (still on PR #12's branch, not merged). Emily's ask evolved through the
conversation: started as "add a link" with 2 read-next posts, then she
specified she wanted the existing Birmingham card swapped out entirely and
replaced with two side-by-side cards — Outstanding-agencies and
local-authority-vs-independent-fostering-agency — styled like the homepage's
"From the blog" cards rather than the site's usual single curved card. Emily
herself flagged the side-by-side might be too narrow in the blog's `max-w-3xl`
column; agreed to stack on mobile/tablet and only go side-by-side from `md`
up (homepage grid starts side-by-side at `sm`, narrower here on purpose).
Reused existing image/title/excerpt text from the homepage and the
Outstanding post itself rather than writing new copy, for consistency.
Removed the now-unused Birmingham image import. Checked with `tsc --noEmit`
first — pre-existing unrelated type errors elsewhere (Supabase `Agency` type
mismatch, several other route files), nothing from this file. Emily reviewed
live on localhost before it was committed. Committed + pushed to PR #12's
branch (`outstanding-agencies-seo-table`, `b9838e1`). PR #12 still not merged.

**Session 22 (2026-09-23):** Picked up from session 21's three open items —
Emily chose "decide on merging PR #12" first. Checked the PR live rather than
assuming: 9 files changed (+494/−156) across 7 commits, no merge conflicts
with `main` (clean), all 3 checks passing (Semgrep, TruffleHog, Cloudflare
Workers build). Flagged the one gap: the browser click-through test
(postcode search, mobile layout, no-results state) still hadn't happened as
its own dedicated pass. Emily chose to merge now and treat the click-through
as a normal live-site check afterwards. Checked `main`'s history first (no
merge commits — past PRs were squash-merged) and matched that convention.
**Squash-merged PR #12** (`gh pr merge 12 --squash --delete-branch`) →
commit `f13853e` on `main`, branch deleted both locally and on GitHub, local
`main` fast-forwarded to match. Cloudflare will auto-build/deploy from
`main`. Then asked Emily about the "move postcode box near results" question
— **decided: not needed, the scroll-to-results jump already covers it.**
(Only ever tracked here in progress.md, not in the project's own docs, so
nothing to update there.) Emily then did the click-through test on the live
site — **found a real, pre-existing bug**, unrelated to today's merge: the
enquiry form (the "request a call/email" flow) throws "Missing Supabase
server environment variables. Ensure SUPABASE_URL and
SUPABASE_SERVICE_ROLE_KEY are set." on submit.
Traced it: `src/integrations/supabase/client.server.ts` (added 2026-04-23,
untouched since — confirmed not touched by PR #12) needs
`SUPABASE_SERVICE_ROLE_KEY`. Local `.dev.vars` has a similarly-named
`SUPABASE_SECRET_KEY` instead (Supabase's newer naming) — looks like a
name mismatch between what the code expects and what's actually configured.
**This form is site-wide**, not just on the new page — it's rendered from
`src/routes/__root.tsx` (`LeadFlowModal`), used via `src/lib/leads.functions.ts`
and shared by `contact`/`reviews`/`area-request` functions too. Postcode
search itself is unaffected (uses the public client, not this one).
Couldn't confirm what's actually set on the live Cloudflare Worker —
`wrangler secret list` needs Node 22, this machine only has v20.20.2, no
nvm/volta installed to get a newer one. Nothing in git history or
`docs/security-plan.md` records this secret being set up, so unclear how
long it's been broken.
Emily said the value is saved in a file on her Mac "I could access but not
read" — checked `~/FLT/` for it: no clear match. `.flt-projects.json` looks
like project registry metadata; `.flt-sentinel` (permissions 600, 20 bytes,
modified same day) is unidentified — did NOT open either without
confirming, since this is real secret-handling territory. Asked Emily to
clarify which file / who set it up; **unresolved when the session ended.**
**⚠️ Important for next session:** (1) confirm what that file actually is
before touching it: if it holds the real Supabase service role key, it must
never be pasted into chat — only used to set the Cloudflare secret directly
(e.g. via `wrangler secret put`, which prompts and never echoes the value —
though that needs Node ≥22 sorted first, or doing it via the Cloudflare
dashboard by hand). (2) This is a real, live, business-impacting bug — the
enquiry form may have been silently failing since April. **Recommended
Emily also flag this to Becky/WhatsApp**, both because it may need someone
who already knows the correct secret name, and because it's exactly the
kind of "you might be the thing failing" situation the safety net exists
for.

**Session 23 (2026-09-23): enquiry-form bug RESOLVED.** Emily asked to
"recover the secret keys without reading them" from a file she believed the
tutor had saved. Corrected that: the tutor has no record of saving keys
anywhere; the local key is `SUPABASE_SECRET_KEY` in foster-compare
`.dev.vars` (name only checked, never the value). `~/FLT/.flt-sentinel` is
only 20 bytes and was modified 2 min after session 22 ended, so it's a
cage/setup marker, **not a key file**. Stop wondering about it.
**Safety guard:** Claude Code's auto-mode guard blocked the tutor
("Credential Materialization") from reading anything in foster-compare's
secret-adjacent area, including `.env`, `wrangler.jsonc` and even
`client.server.ts`. Didn't try to get around it. Key/secret jobs now go
through Emily by hand in the Cloudflare dashboard, with the tutor guiding.
Emily checked Cloudflare → Workers & Pages → Settings → Variables and
Secrets. Live has ADMIN_PASSCODE, GOOGLE_PLACES_API_KEY, RESEND_API_KEY,
SUPABASE_PUBLISHABLE_KEY, SUPABASE_SERVICE_ROLE_KEY (secret), SUPABASE_URL
(variable). So nothing was missing and the name-mismatch theory from
session 22 was wrong. Emily retested the live form: **it works, and the test
enquiry arrived.** Most likely someone set or fixed the settings after
session 22 (not confirmed who). No secret value ever passed through chat.
Emily shared names only, never values, which was exactly right.
Recorded in foster-compare `docs/security-plan.md` §5: the live setting
names plus an outage note. Also fixed the backup path there to
`~/FLT/data/backups`. ⚠️ **Open question for Becky:** that FLT location may
NOT be iCloud-synced (the old Documents path was), so backups might only
exist on the laptop. Committed `7a434a6`. The guard blocked the tutor's
push ("Out-of-Place Publication"), so **Emily ran `git push` herself** via
`!`: her first git command. Pushed OK, live site HTTP 200 afterwards.
Next up: back to Step 10b (the prospectus content gaps).

**Session 24 (2026-09-23):** Emily asked to check a list of recently-created
pages against the SEO checklist — the six new city pages (Gloucester, Bath,
Canterbury, Brighton and Hove, Reading, Portsmouth) plus the
outstanding-fostering-agencies blog post. Checked live against
`docs/seo-master-checklist.md` Part 2 and `docs/blog-post-checklist.md`
rather than assuming. Blog post: clean, session 20's fixes held. City pages:
all correctly in `sitemap.xml` and `llms.txt`; all correctly linked from the
homepage's "Search by city" section (confirmed via `AvailableAreas.tsx` —
a first grep for hardcoded links found nothing and looked like a gap, but
the links are generated from each city's `homepageGroup`, not hardcoded, so
double-checked before reporting a false alarm).
Two real, template-wide findings, both resolved as Emily's deliberate
decisions rather than fixes:
- The shared `$citySlug.tsx` template's default title tag contains an em
  dash ("Fostering Agencies in {City} — Compare & Shortlist"). **Emily's
  call: added as a permanent exception** in `seo-master-checklist.md` Part 2
  — title tags are now explicitly exempt from the no-em-dash rule, since
  that rule is really about body copy sounding AI-written.
- Longer city names push the default meta description over 160 characters
  by 1-2 characters. **Emily's call: added a 1-2 character tolerance**
  exception to the same checklist line, rather than rewriting for it.
- Title tag's 60-character limit stayed strict (Emily's explicit choice, not
  extended the same tolerance). Brighton and Hove's default title was 61
  chars — fixed with a `metaTitle` override ("Brighton & Hove" instead of
  "Brighton and Hove") bringing it to 59.
Also discussed, no action taken: only 4 of the 42 city pages (Walsall,
Dudley, Sandwell, Stoke-on-Trent — all West Midlands) have real
city-specific FAQ facts; the other 38, including all six new ones, run on
generic boilerplate FAQs. Confirmed this is the checklist's known
pre-existing weakness, not something the six new pages introduced, and
declined to fabricate "quick" city facts to paper over it — the FAQ code
itself is written to stay generic until Emily has verified real facts per
city. Emily then asked about live per-city foster-home shortfall data (to
publicise local need). Researched rather than guessed: no live feed exists
anywhere in the codebase; real data does exist (DfE's "Children looked
after by local authorities" release, SSDA903 collection) but it's an
**annual statistical release, not live**, and local-authority boundaries
don't map cleanly onto the city pages (same cross-boundary issue already
seen with agency postcode coverage, e.g. Reading/Hampshire, Canterbury/
Kent). Offered to scope it as a proper plan doc; **Emily declined** ("no
don't worry") — not pursued further.
Committed + pushed to the foster-compare repo (`173b563`): the two
checklist exceptions plus the Brighton and Hove `metaTitle` fix.
No curriculum step advanced — pure Step 10b real-project work. Next up:
whatever Emily picks next time — the prospectus content gaps are still the
longest-standing open thread if nothing more pressing comes up.

**Session 25 (2026-09-23): Google Ads keyword research → plan PAUSED.**
Emily asked for "Google Ads forecasting". Checked docs first: `google-ads-plan.md`
appendix Steps 1–5 already covered it, and nothing had been executed yet. Emily
used her old Ads account first, to protect the new-customer £400 credit. It
turned out to be **closed and in USD**, which made the data unreliable, and I
walked back a conclusion I'd drawn from it. Then she created a **new GBP account**:
skipped campaign creation, no billing, no promo code, so the credit is untouched
(section 10 confirms the clock starts at the first ad, not at account creation).
Findings: the plan's comparison keywords get almost no UK searches. Real volume
exists only for recruitment keywords. Creative round: pay/not-for-profit searches
are High competition, complaints/directory/charity return no data. **Real lead:**
"fostering agencies northampton/walsall/bristol" get 10–100/mo, Low, no bids,
while "foster carer northampton" is High. Agencies bid on recruitment wording,
not agency wording. West Midlands is High (up to £46.47), so organic only.
**Emily's calls:** (1) never bid on agency brand names, because agencies are
her customers. Her idea, and I should have raised it myself. (2) **Pause the Ads
plan**: a £2/day city test can't meet the £400-in-60-days credit rule, and
running it first would forfeit the credit.
Recorded in foster-compare (`4d04fba`, pushed): pause box + findings in
`google-ads-plan.md`; new DRAFT `docs/keyword-map.md` (SEO checklist Phase 2,
still needs the Search Console check). Organic gaps: **UK foster carer pay
(~5,000/mo)**, North East + South West regional pages (~500/mo), UK-wide A–Z
list. Also updated `open-plans.md` (#2, #3, #4) and the SEO checklist's status box.
Emily's Keyword Planner CSV + screenshots are in foster-compare's `Google ads/` and
`screenshots/` folders, **untracked in git on purpose**.
Next up: one of the organic gaps (UK pay page is the biggest), or the
prospectus content gaps.

**Session 25 cont. (2026-09-25): first inbound agency.** Heart And Home Fostering
Group Ltd (Milton Keynes) asked to join. Their website is "coming soon". Emily
confirmed their URN (2850766), and I checked it on Ofsted: Open, IFA, registered
23 June 2026, not yet inspected. Drafted the reply; Emily edited it (added an
allowances question, attached the partner prospectus) and sent it from hello@.
Logged in a new "Inbound requests" section of foster-compare
`docs/outreach-log.md`, with the follow-up due 2026-10-02. Also fixed the "what's
your traffic?" reply (template 3b + roadmap 3e), which still said "weeks into
paid promotion" after the Ads pause. Pushed `0f517d2`.
**Next:** build their listing when they reply (rating "Not yet inspected").
Emily attached `public/agency-partner-prospectus.pdf` (the 4 Sept export, the
same one on `/agency-partner`). Reminded her it still has the group B claims
("regularly scans…", "proved", "Instant" heading) and no legal footer. Her
earlier "leave for now" decision stands, and I didn't push it. Heart and Home
can't have the Good/Outstanding badge until inspected. **Open:** offered to note
"prospectus attached (4 Sept PDF)" in their outreach-log row; not answered, not
done.
Session ended with "sign off". No curriculum step advanced; all Step 10b
real-project work.

**Session 26 (2026-09-30): Wiltshire Council profile — real SEO work, from the
paused Ads research.** Emily wanted to make use of last session's keyword
findings on the organic (non-paid) side: optimise agency profile pages to be
found on Google, prioritising large councils and charities. Checked live
Supabase before trusting the docs (`docs/keyword-map.md` still said ~385
agencies; live count is 524: 354 IFA, 108 council, 47 charity, 15 social
enterprise). Identified 60 "large" profiles by the existing `scale` field —
32 regional-scale councils + 28 national-scale charities (Emily's own
definition, confirmed).
**Blocker found before any keyword work could matter:** agency profile pages
are noindexed site-wide except one, `wiltshire-council-fostering-service` —
a deliberate gate (`docs/launch-roadmap.md` M9, set 2026-07-21, three
conditions: data verified, template not too thin/duplicate, pages generally
improved). None confirmed cleared. **Emily's call: leave the other 523
noindexed for now** — this session only touched the one live page.
Real SEO work on Wiltshire: Search Console data (Emily's export) showed
"fostering wiltshire" already ranking ~position 6 with 8 impressions, 0
clicks. New title swaps the old "...in Trowbridge" (nobody searches the
council's office town, and it was over the checklist's 60-char limit) for
"...— Ofsted Outstanding". New meta description leads with pay
(£420–£780/week) instead of repeating "Outstanding" twice; deliberately does
NOT mention reviews (no review data exists for this listing — would have
been the same kind of overclaim as the prospectus "Instant" wording). Added
a coverage-area sentence naming the towns actually served — checked against
wiltshire.gov.uk's own recruitment campaign pages (not just our database,
which was missing Warminster/Calne/Westbury/Melksham). Database's
`coverage_cities` and `coverage_postcode_prefixes` updated to match (script
`scripts/update-wiltshire-seo-2026-09-30.mjs`, backup saved first). Pushed
`7d76bb9`.
**Environment issue found, not fixed:** tried to preview on localhost first,
per the project's own rule. This cage machine's Node 20 can't run pages that
query Supabase during server-side rendering (missing native `WebSocket`) —
homepage loads fine, but any agency profile page 500s in dev mode here.
Confirmed this is pre-existing, not caused by this session's changes.
**Next up (Emily's request):** fix the localhost preview environment first
thing next session, before any further building. Also: GitHub flagged 2
Dependabot vulnerabilities (1 high, 1 moderate) on push — not investigated
this session, worth a look. Emily to check the live Wiltshire page herself.

**Session 27 (2026-09-30): both open items from session 26 resolved.**
No curriculum step — pure Step 10b real-project work, both tasks Emily's own
direct requests.
**Dependabot (`let's fix dependabot`):** checked live via `gh api` rather than
trusting the 2-alert count from session 26's push message — found 9 open
alerts, not 2 (Dependabot had since found new problems in packages already
pinned for older issues, plus more that only surfaced on closer digging).
Fixed in two commits: (1) `fast-uri` 3.1.6→3.1.8 and `undici` 7.29.0→7.29.1
in `package.json`'s two `overrides` blocks (`58181a7`-style pins from
earlier sessions had themselves become vulnerable to newer CVEs) — commit
`74c26f3`; (2) `brace-expansion` and `engine.io` (7 alerts, all transitive
dev-tooling pulled in via `react-email`→`glob`/`socket.io`) — these didn't
need new overrides, a plain `npm update` picked up already-compatible safe
patch versions — commit `2b6c205`. `npm audit` now clean (0 vulnerabilities).
Confirmed via `gh api` after both pushes: **0 open Dependabot alerts.**
`tsc --noEmit` showed the same pre-existing `Agency`-type errors before and
after (session 21's known issue) — nothing new introduced.
**Localhost preview (`let's fix the preview`):** root-caused properly before
fixing — reproduced the 500 live, found the real error in the SSR output:
`@supabase/realtime-js` requires a global `WebSocket`, which Node only has
natively from v22+; this cage is deliberately pinned to Node 20
(`/etc/flt-cage-provisioned` says `node-major: 20`) with no `sudo`/nvm/volta
available to change that — a genuine platform constraint, not something
fixable from inside the cage. Fixed at the application level instead: new
`scripts/dev-websocket-polyfill.cjs` hands Node the `ws` package's
`WebSocket` before Vite starts, wired in via the `dev` script's
`NODE_OPTIONS`. Dev-only — production (Cloudflare Workers) already has a
native `WebSocket`, untouched. Also pinned `ws` as an explicit
`devDependency` (previously only present incidentally through another
package). Verified live: homepage, the Wiltshire agency page (full real
data — pay rates, coverage towns, everything), and a city page all return
200 with a clean log, using the actual `npm run dev` command Emily would
type. Committed + pushed (`34611fb`).
An aside mid-session: Emily asked whether tasks like these could be pushed
to the background so she could work on something else in parallel —
explained the conversation is inherently turn-based (that's also *why* the
review-before-it-happens safety net works), background-running a whole
independent task isn't something a single session supports, and a second
terminal/`tutor` session touching the same repo at once carries real risk
(cited the session 12 Finder-reorg scramble) — recommended sticking to one
thread at a time given how quick these particular tasks were anyway.
**Next up:** whatever Emily picks — no open thread was pressing at session
end.
**Follow-up same session:** Emily asked to save the "flag background jobs"
preference to memory — then corrected it once it was saved: she doesn't
want them narrated/announced, she wants slow jobs actually run non-blocking
so the conversation keeps moving (speed, not visibility). Memory rewritten
to match. Session ended with "sign off" (this project's established
equivalent of "End lesson" — used the same way at the end of session 25).

**Session 28 (2026-09-30): launch re-plan, traffic-first.** Emily's single
highest priority: gain traffic to show domain authority to agency partners.
Reviewed `launch-roadmap.md` against reality: its only traffic engine was
Google Ads, paused 23 Sept, and nothing replaced it. Wave 1 pitches never
went out. Explained that domain authority comes from backlinks, not visits,
and that new pages take 2–4 months to rank, so backlinks are the fastest
credibility before the 31 Dec early-adopter deadline. Agreed priority list:
(1) chase the 3 Tier 1 charity follow-ups, (2) UK foster carer pay page
(~5,000+/mo), (3) unhide agency profiles in stages (unlocks the
already-built `/agency-badge`), (4) council FIS directory listings,
(5) North East + South West regional pages, (6) first inclusion page (early
Nov). Parked: Ads, Bing, quiz, Facebook, Why Foster phases 2–3, and the
`/impact` page unless UnLtd shortlists her.
**UnLtd: submitted** (Emily confirmed), no reply yet.
**(1) DONE:** all three follow-ups sent 30 Sept, with a no-reply cut-off of
10 Oct. Addresses verified live: Fostering Network to campaigns@, CC info@.
FosterTalk to marketing@, forwarded to enquiries@. Become: campaigns@
bounced, and info@ is no longer on their site, so the August email probably
never arrived. The original was re-sent fresh to hello@. Logged in
foster-compare `outreach-log.md` + `backlink-plan.md`.
Roadmap rewrite to match the new plan: offered, not done yet.
**Next up:** the UK foster carer pay page. Also still open: Emily's Search
Console baseline (impressions/clicks, last 3 months).

**Session 29 (2026-09-30): Search Console baseline recorded.** Emily
exported it herself (foster-compare `Google exports/30.09.26/`, untracked on
purpose). Last 3 months: **36 clicks, 19,587 impressions, avg position ~25**.
Monthly: Jul 8 clicks / Aug 11 / Sep 17, with Sep position improving to
21.8. Only 74 of 854 queries reach page one. It confirms the pay gap: the
London pay post got 361 impressions and 0 clicks, and national pay searches
sit at position 87–90. Added as a baseline section in
`docs/keyword-map.md`, pushed `edca127`.
Then gap-reviewed Emily's own pay page plan
(`docs/uk_foster_care_pay_rates_webpage_plan.md`). Emily asked whether the
database has enough pay data. Checked live: only **47/524 agencies (9%)**
have a real £ figure (IFAs 15/354), so no per-agency pay table. **Emily's
idea instead:** a national minimum allowance table covering **all four
nations**. Her Keyword Planner pay export (`Google exports/Exported pay
keywords/`, untracked) showed "allowance" wording is as big as "pay"
(~5,000 each), so the page targets both. Tax gets a full section. **Kinship
kept off the page** (Emily's call) apart from one signpost sentence, and
logged as keyword-map gap #6. Emily added an agency comparison CTA; I
adjusted it to use `PostcodeSearchBox`, "Google reviews" not "carer
reviews", and no em dash. The postcode "highlight my area" box on the table
is a later step. All recorded as a "Decisions" section 0 in the plan. The
plan's tax figures are 2025/26, so everything must be verified against
gov.uk for 2026/27 before building. Pushed `cf82fb3`. Emily decided to
leave the London pay post's "income" wording for now (recorded in the plan).
**Figures verified (all from official sources):** 2026/27 minimum allowances
for England (the plan's figures were right), Scotland, Wales and NI, now in
plan section 0. NI's Model Scheme gives a real spending split (food 40% etc.)
that replaces the plan's unsourced one. **Not found:** the official list of
"South East" councils. **Accuracy fix shipped:** HMRC hasn't published
2026/27 Qualifying Care Relief figures. The £20,440/£435/£515 figures on the
site came from an agency website (Capstone), so all 3 pages were corrected to
the 2025/26 figures (£19,690/£415/£495) with a note: the London pay post (also
redid Sarah's worked sum to £67,010, and dateModified is now 30 Sept),
`/west-midlands-fostering-agencies` and `/london-fostering-agencies`. Previewed
on localhost, pushed `0e94579`.
**Found, not fixed (pre-existing):** the `/london-fostering-agencies` FAQ
data for Google uses `a.join()` on page elements, so the live page sends
Google "[object Object]" in place of some answers. Worth fixing separately,
and other city pages may use the same pattern.
**FAQ bug FIXED (Emily approved):** new `src/lib/nodeToText.ts` flattens
formatted FAQ answers to plain text (keeps the words, drops SourceCite
pills). Used on all 11 pages that build FAQ schema, not just the 2 that were
broken (London and West Midlands, 3 answers each), so it can't come back.
Verified with before/after snapshots on localhost: 0 "[object Object]", the
other 9 pages byte-identical, tsc error count unchanged (10 before and after,
all the old known ones). Pushed `0cff991`.
NI verified on gov.uk: foster carers can get free Class 3 NI credits (form
CF411A), and voluntary Class 2 is £3.65/week in 2026/27. Plan updated
(`3b8d60a`), so all figures are now verified.
**UK pay page BUILT on branch `uk-foster-carer-pay-page`** (`b86eb15`, pushed
to GitHub, NOT merged, not live): `src/routes/blog.foster-carer-pay-uk.tsx`.
All text drafted by the tutor; Emily still to review it on localhost. It has
the four-nation table, NI spending split, tax/NI/council tax sections, the
kinship signpost, the CTA with PostcodeSearchBox, 5 FAQs via nodeToText, and
a Read next card to the London post. Hero image is the bedtime-story photo
(placeholder). Also: added to the blog index, sitemap, llms.txt and
checklist, with a link back from the London post. Checks passed: title 44
chars, description 159, 0 em dashes, 0 "[object Object]". Left out of v1:
council rate examples (unverified), Staying Put, benefits/Universal Credit
FAQ (unverified), and the postcode highlight on the table.
⚠️ **Deploy issue:** the `main` pushes `0e94579` (tax fix) and `0cff991` (FAQ
fix) were NOT live 10+ min after pushing (14:13 → 14:23 UTC), although
earlier changes today (Wiltshire) are live. Emily to check the Cloudflare
dashboard (Workers & Pages → Deployments).
**⚠️ CORRECTION (same session): the QCR "accuracy fix" above was WRONG.**
The 2026/27 figures £20,440/£435/£515 ARE law: *The Income Tax (Indexation
of Qualifying Care Relief Amounts) Order 2026* (SI 2026/39), "has effect for
the tax year 2026-27". HMRC's HS236 and BIM52765 just hadn't caught up. I
had only checked HMRC guidance, not legislation.gov.uk. Emily pasted a
second opinion (another AI) that flagged it, and I verified it against the
SI itself. Restored on all 3 pages and the new UK page, now cited to the SI
(better than the original Capstone source), with the false "not yet
published" note removed. `main` `5b1cfb5`, branch `521bbfa`. Plan doc
corrected too. The same second opinion suggested relabelling NI's "16+" as
"16 to 17": declined, because NI's scheme says 16+. **The wrong version
never went live**, because Cloudflare didn't build any of those pushes.
**Deploy issue, continued:** Cloudflare has built nothing since the 15:07
push (9c38ae8). Pushes 0e94579, 0cff991, 3b8d60a, the empty trigger e9ffb34
and 5b1cfb5 all got no "Workers Builds" check-run. Emily's Deployments page
showed nothing queued or failed. Live site = the 15:07 version, which has
correct figures but still sends Google "[object Object]" on 2 pages.
Emily pasted Cloudflare's Settings warning about a name mismatch, so
`wrangler.jsonc` `name` was changed from "foster-care-compare" to "fcc" (`0fa9e8c`). A
manual deploy would otherwise have gone to a second Worker. Build settings
were all correct (repo, `main`, watch paths `*`). Cloudflare status showed
Workers Builds operational, R2 degraded. Emily pasted a second AI's
troubleshooting list. Tutor advised against `wrangler deploy` from the cage
(it would ship the local branch; also needs a Cloudflare login and Node 22)
and against disconnect/reconnect (the Git link was proven working because
the branch push DID get a preview build, b86eb15 at 14:35 UTC). Emily
thinks it's lag, and that fits: builds seem to run one at a time and slowly,
dropping pushes that arrive mid-build.
Branch previews exist:
`uk-foster-carer-pay-page-fcc.fostercarecompare.workers.dev`. They're
preview-only and never went live (confirmed the page was 404 on the real site).
**PUBLISHED: Emily said "publish" (sign-off).** PR #15 was squash-merged,
giving `a6c37e3` on `main`, and the branch was deleted. Checks passed. This
build carries the UK page, the 2026/27 QCR figures cited to SI 2026/39, and
the FAQ "[object Object]" fix.
✅ **LIVE 15:02 UTC.** `a6c37e3` built, about 50 minutes after the merge, with
no manual build needed. So the "stall" was Cloudflare running very slowly,
not skipping pushes. All live checks passed: page 200, blog index, SI cite,
0 "[object Object]".
**Emily's edits round (PR #16 → `01ac40b`, "publish" = sign-off).** Emily
directed ten changes herself, pasting exact before/after copy. The tutor
checked each one and pushed back where the copy went beyond the facts:
- NI breakdown: checked against the DoH NI 2026/27 Model Scheme PDF. Her
  "(bills, maintenance, extra utilities)" and "savings for the child" aren't in
  the source, and "should be spent" became "meant to cover". She accepted the
  sourced version.
- Council vs agency section: charities can't give council tax discounts, so
  that was reattributed to councils. Em dashes became commas, and the two
  internal links (LA vs IFA guide, London pay post) were kept.
- CTA: "View pay rates" became "published pay rates", because only about 9%
  of agencies have an allowance figure. The title and hint line were removed;
  `PostcodeSearchBox` got a `showHint` prop, default on, so the homepage and
  transfer page are unchanged.
- Practical things: bold lead-in titles (option 1, matches the West
  Midlands post).
- Keyword pass from her Keyword Planner export: the table heading, "Breakdown
  of the fostering allowance", "foster carers/parents allowance", "foster
  carer tax allowance" and "Council tax for foster carers". The meta
  description was rewritten and is 157 characters; she spotted the filler
  "in each nation" herself.
- Skipped on purpose: "wages" (carers are self-employed), "benefits" (UC
  isn't covered) and kinship (her earlier decision).
Skill note: she's now writing and editing the copy herself, and batching
tweaks so they go out in one push. That's the directing → leading shift.
**End of session 29:** at sign-off, the `01ac40b` Cloudflare build hadn't
started yet (only the two security checks had passed). **First job next
session:** check the live page for the new description and the "Breakdown of
the fostering allowance" heading. If it's still not live, use the manual build
of `main` in the Cloudflare dashboard. Then Emily requests indexing in
Search Console for /blog/foster-carer-pay-uk. Emily decided to **keep the
placeholder hero image** and called the page done. Still open, for a possible
v2: the South East council list, council rate examples, Staying Put, the
benefits FAQ.

**Session 30 (2026-09-30): pay page confirmed live, business listings logged.**
No curriculum step, pure Step 10b real-project work.
**Pay page LIVE:** the `01ac40b` build (PR #16) went live at 16:05 UTC. Checked
directly on the live page: new "Breakdown of the fostering allowance" heading,
the rewritten meta description, 0 "[object Object]", and it's in the sitemap.
(Some early checks wrongly showed zero matches. That was a bad search command,
not the site: re-checked with Python.) **Emily requested indexing** in Search
Console for `/blog/foster-carer-pay-uk`. Watch the Performance report for
impressions in a few days.
**Listings and Reddit logged** in foster-compare `docs/outreach-log.md`
section 1: Reddit (Emily still posting; subreddits/dates/page not recorded),
Yell, Google Business Profile, Bing Places (confirmed), Cylex, Apple Business
Connect and FreeIndex. Emily did all of them herself. Apple's domain-validation
step rejected fostercarecompare.co.uk ("Unable to add domain", cause never
found); it was added some other way, method not recorded. My first guess that
she was on the wrong Apple screen was wrong. All are mostly `nofollow`, so
they're citations and visitors, not backlinks, and don't count towards the
domain-authority goal. Master business details (name, registered-office
address, phone, site) recorded at the top of that section so every listing
matches. Saved to memory as "Business listings tracker".
**Open:** (1) the phone number 01638336031 isn't on the site itself, so Emily
to decide if it should be; (2) FreeIndex confirmation email not checked;
(3) an untracked `public/web-logo.png` in foster-compare, which would go live
if committed, so move it out of `public/` or commit it on purpose; (4) the
foster-compare listing checkpoints (`83c1b0b` to `31a7fdd`) are local only, not
pushed. Emily to run `! git push` in that folder; (5) subreddits, dates and
which page was linked for Reddit, still to fill in.
**Next up:** unhide agency profiles in stages (item 3 of session 28's plan).
Session ended with "sign off".

**Session 31 (2026-09-30): reciprocal outreach logged.** No curriculum step,
pure Step 10b real-project work. Emily asked "what's next?" and got a steered
choice: start the unhide-agency-profiles conversation (M9's three gates still
need her sign-off) or clear loose ends first. She went straight to outreach
notes instead.
**Outreach logged** (foster-compare `docs/outreach-log.md` section 1 and
`docs/backlink-plan.md` Tier 3): Emily emailed **Foster Care Matters**
(fostercarematters.com) and **Fostering Hope** (fosteringhope.co.uk) herself,
same reciprocal-swap email with names swapped, both 30 Sep. Follow-up due
2026-10-14, one at most. Contact addresses not recorded, and what kind of
organisation Fostering Hope is hasn't been checked. Flagged honestly that the
offer is conditional, against backlink-plan section 6 ("feature first, ask
second"). Emily asked whether Google would know: corrected my earlier
overstatement. Google can't see the email, only the resulting links, and one
relevant swap at this scale is low risk. Emily's call: fine to send both.
**Coram (parked):** Emily wants to approach Coram with her life story tool
but may turn it into an app first. Noted under Tactic C in `backlink-plan.md`.
Which part of Coram is undecided. Nothing sent.
Commits `c225fb6` and `a832f4e`, both pushed by Emily (`! git push`).
**Open:** (1) Emily to give the contact addresses for the two emails;
(2) web-logo.png untracked in `public/`; (3) phone number not on the site;
(4) FreeIndex confirmation email; (5) Reddit details; (6) 14 Oct follow-up
on both swap emails, plus the 10 Oct no-reply cut-off on the Tier 1 charities
and the 2 Oct Heart and Home follow-up.
**Next up:** unhide agency profiles in stages, or the loose ends above.
Session ended with "sign off".

**Session 32 (2026-09-30): loose ends cleared.** Emily asked for 10-minute quick
wins; went through the open list from session 31 and logged her answers in
foster-compare `outreach-log.md` and `backlink-plan.md`:
- **Correction:** Foster Care Matters and Fostering Hope were approached via
  **website contact forms**, not email (session 31 said emailed). Wording not
  saved, summary only, so the 14 Oct follow-up can't quote it.
- **Reddit:** r/fosteringuk, 30 Sep, linking `/transfer-fostering-agencies`.
- **Phone number:** Emily's decision, NOT going on the site; listings only.
- **FreeIndex:** submitted, not yet live.
- **web-logo.png:** Emily moved it out of `public/`; checked, repo clean.
**Still open:** 14 Oct follow-up on both swap forms, 10 Oct Tier 1 charity
cut-off, 2 Oct Heart and Home follow-up, FreeIndex going live.
**Next up:** unhide agency profiles in stages (M9's three gates need Emily's
sign-off).

### Session 32 (cont.): unhide batch of 9 started (2026-09-30)
Batch of 9 agreed with Emily: Wiltshire (live), Bristol, Dorset, Somerset, Oxfordshire,
Hampshire, Gloucestershire CC + Swindon BC (need NEW rows), Sandwell (check).
Dropped Bath (no search data) and West Berkshire (no data). Keyword files in
foster-compare/Google ads/Keywords for council pages/.
**Bristol DONE, committed 3ad8bba, NOT pushed:** DB copy updated (backup in FLT/data/backups),
indexable + linked + new title. Pay figures verified on bristol.gov.uk.
**Blocked:** current pay figures for Dorset, Somerset, Oxfordshire, Hampshire, Sandwell
not readable by my tools (pages point to PDFs/403). No text written for them.
Ofsted URNs for Dorset/Somerset/Oxfordshire/Hampshire in DB look wrong ("70","74","68","60").

### Session 32 (cont.): batch of 9, Bristol built, data fixed (2026-09-30)
**Council rating rule A (Emily):** show the council's latest Ofsted "children in care" judgement,
labelled council-wide. Checked: Dorset Outstanding (Mar 2025), Somerset Requires improvement
(Apr 2026), Oxfordshire Good, Hampshire Outstanding, Sandwell Good. Fixed URNs: Dorset 2533840,
Somerset SC041894, Oxfordshire SC048223, Hampshire SC061164 (Sandwell URN unchecked). I wrongly
set Dorset to "not yet inspected" first, then restored Outstanding. Somerset STAYS in the batch.
**Pay rule:** no pay figures on councils unless verified + dated; councils get an "Ask about
current rates" button (adds to shortlist -> existing request-a-call bar), never "contact them
directly". Bristol + Wiltshire keep dated figures (checked Sept 2026; re-check each April).
**CTAs built:** blog StickyPostcodeBar on all profile pages + council pay box button
(GenericAgencyProfile). Wiltshire/Sandwell use custom profiles, NO pay button yet.
**Bristol copy:** short hero intro (hard-coded), pay/matching/support in lower boxes, start-up grant
in Allowances box, cautious coverage line. Gemini coverage list NOT published (unverified).
Reviews left out (no fostering-specific Google listing; council testimonials are marketing).
Preview branch: bristol-preview-fcc.fostercarecompare.workers.dev/agencies/foster-bristol (works).
**Still to do:** page copy for Dorset, Oxfordshire, Hampshire, Somerset, Sandwell (no pay figures);
new rows for Gloucestershire CC + Swindon BC; add Wiltshire/Sandwell pay button; audit the other
~100 council ratings (none show Requires improvement); Bristol/Wiltshire April figure re-check.

**Heart and Home (5 Oct 2026):** ~~they replied asking Emily to HOLD OFF~~ **WRONG (corrected 6 Oct): tutor
mixed them up with Step by Step Fostering. Heart and Home sent full details 28 Sep and never asked to wait: ready to list.** LISTED 6 Oct (free, noindexed); Emily emailed Augustina 6 Oct. Decided: paid profile links rel="sponsored" (roadmap M16, before first Enhanced member). Fusion: Emily replied to Lydia 6 Oct (her own wording: postcode search = office within up to 50 miles, city pages = coverage; asked for missing city pages + other hubs); the July reply HAD arrived (tutor wrongly thought it bounced). Thrive already listed (14 Sep); Emily replied 6 Oct (offered Enhanced, sponsored link, PDF attached). FosterWiki (info@fosterwiki.com) added to backlink plan Tier 1: approach with FOI findings after 3 Nov. Ideas parked, not decided: coverage-by-council in postcode search; "Satellite office" label wording. Logged in foster-compare docs/outreach-log.md. Remaining dated items: 10 Oct
Tier 1 charity cut-off, 14 Oct swap-form follow-up, FreeIndex going live.

### Session 32 — sign off (2026-10-05)
**Live now:** Foster Bristol + Wiltshire indexable and in sitemap.xml; sticky postcode bar on every profile page;
council pay box with "Ask about current rates" (generic layout only); repeated "supports X arrangements"
line removed from all generic profiles. Wiltshire layout checked by Emily: fine.
**Hidden (noindex) but reviewable:** Dorset, Somerset, Oxfordshire, Hampshire, Sandwell profiles. Data fixed
(ratings/URNs), copy NOT yet written. Emily was going to review them and send notes.
**Next up (in order):** (1) Emily's notes on the five hidden pages; (2) write their copy, no pay figures,
only verified facts; (3) Hampshire allowance still says "contact direct for 2025-26 rates" and Oxfordshire
has none: replace with the ask-about-rates wording; (4) add pay button to Wiltshire/Sandwell custom layouts;
(5) new rows for Gloucestershire CC + Swindon BC; (6) Sandwell URN unchecked; (7) audit ~100 other council
ratings; (8) Search Console "Request indexing" for Bristol (Emily). Reviews: left out. Coverage: Gemini list
unpublished; cautious line live; Emily may ask Foster Bristol directly.
**Dates:** 10 Oct Tier 1 charity cut-off; 14 Oct swap-form follow-up; FreeIndex going live. Heart and Home on hold (WRONG, corrected 6 Oct: ready to list).
**Push state at sign-off:** both repos have ONE unpushed log-only commit each (Heart and Home on hold).
**Curriculum:** no step advanced (still 10b real project).

### Session 33 (2026-10-05): profile links locked down, council pay layout, yearly refresh plan
No curriculum step (10b real project). All in foster-compare, committed locally (not yet pushed at time of logging):
- **Profile links gap found + fixed (`c36f026`):** near-me + Outstanding pages linked EVERY agency name to its
  (noindexed, unverified) profile since they were built. Now use one shared approved list,
  `src/lib/profileLinks.ts` (Sandwell, Wiltshire, Foster Bristol). Indexable list (`INDEXABLE_SLUGS`) is separate:
  only Wiltshire + Bristol. Sandwell = linked but noindexed (Emily not yet asked whether to keep it linked).
- **Council "Shortlist" button (`0c112a8`, `2f4b81a`, `96ca62b`):** shared `AskAboutRatesButton.tsx`; bold line
  "Shortlist to check current rates" + button "Shortlist" → "Shortlisted" with tick. Now on Wiltshire, Sandwell and
  all generic council profiles. Pop-up wording matches ("check").
- **Bristol allowances in Wiltshire card layout (`61f0a44`), Wiltshire moved onto it too (`2f4b81a`):** figures for
  both councils now live in `src/data/councilPay.ts`, drawn by `CouncilPaySection.tsx`. Wiltshire verified identical
  before/after. Tutor wrote Bristol's intro + short card notes (restating old text only); Emily to read them.
- **Yearly refresh plan (#23, `docs/yearly-refresh-plan.md`):** REFRESH markers + one register + combined monthly
  GitHub-issue email (assigned to Emily) + push warning + GOV.UK alerts + tutor session check. Ofsted ratings point
  to plan #8. **Emily's setup all done:** GOV.UK alerts (HS236, Fostering topic, DfE CLA stats), GitHub email,
  two calendar events. Pending her sign-off: rating-date DB column; unlinked custom profiles marked when unhidden;
  Walsall fix; keep commercial/legal in register.
- **Found:** Walsall city page pay quoted an Oct 2023 PDF (£159–£233.15) → plan action #1. (Tutor first said it was
  "below the legal minimum" — wrong comparison, corrected; Walsall pays a fee on top and uses different age bands.) Security quarterly spot-check due early Oct 2026 (now). Ofsted's GOV.UK dataset is yearly only.
- **Tutor mistakes, logged:** called Walsall "out of date" before checking its note (turned out right, for a better
  reason); recommended a GOV.UK search alert without checking it keeps the keyword (it doesn't). Emily caught it.
**Next up:** push; build refresh Phase 1; Walsall; Emily's notes on the 5 hidden council pages; Sandwell link call.

### Session 33 (cont.): pushes, Walsall fixed, refresh Phase 1 built (2026-10-05)
- Emily pushed `5563a80` (live, verified: Bristol/Wiltshire "Shortlist to check current rates"; Outstanding page links
  only Wiltshire) and `160e3cb` Walsall fix (April 2026 fees + allowances, first REFRESH marker; was still building).
- Found: Outstanding page shows "…Ask about current rates." from a council's DB `allowance` text (old wording, not a
  code bug). Offered to update DB rows to "check" wording — Emily not yet decided.
- **Refresh Phase 1 built (foster-compare, committed locally):** `scripts/check-refresh-due.mjs`,
  `.github/workflows/refresh-reminders.yml` (1st of month issue to emlura-biz + push warnings, never blocks),
  `docs/freshness-register.md`, 29 markers. Emily asked about new cities → added a safety net (city FAQs with £ and
  `councilPay.ts` entries with no marker get flagged) + a step in all 3 checklists. Build + tsc (10 known) fine.
- First email will list: security spot-check (Oct), Wiltshire Ofsted (Nov), £295 offer + "81,000 children" (Dec).
- Emily pushed `fde8dda`; reminders workflow passed on push; she ran it by hand → issue #17 "Refresh due: October
  2026" created + assigned (Gmail arrival not yet confirmed).
- **Security spot-check DONE, all 9 clear** (`22de539`): rate limit burst-tested (6th → 429), MFA on all 5, only fcc
  worker, logs normal (Emily exported CSV; crawler burst 22:33, a contact form submission 4 Oct 20:09). Backup was 18
  days old → new full backup 2026-10-05 (needed the WebSocket polyfill; command fixed in security plan `fc2bf28`).
  Branch protection not available on free private repo → recorded as accepted.
- Emily pushed `22de539`. Contact submission 4 Oct 20:09 confirmed received by Emily.
- **DB wording done:** Dorset + Somerset allowance "Ask about current rates." → "Shortlist to check current rates."
  (only 2 rows had it; rows backed up; script committed). Live Outstanding page verified: old 0, new 2.
- **Sandwell unlinked** (Emily's call): removed from `profileLinks.ts` until she's happy with the page. Page still
  exists at its URL, still noindexed. Clickable now: Wiltshire + Foster Bristol only (both indexed).
- Emily pushed Sandwell unlink etc. (`26a76e5`). **Foster Bristol Mockingbird section** (`2ccdfd5`): shared
  `MockingbirdSection`, Bristol wording softened after web check (first constellation 2024), marker 2027-04.
- **Shortlist fix** (`b81c055`): council pay-card "Shortlist" button couldn't un-shortlist (`if (shortlisted) return`)
  → now toggles + "removed" toast. Audited every other shortlist button: all already toggle. Pushed.
- **Council profile template** (Emily: "Wiltshire as the gold star"). Asked the tutor to scrutinise as a content
  specialist → found: Areas covered / DB allowance fallback / ILACS note would be lost; DB vs hand-typed fostering
  types; generic "24/7 support" cards unverified for 100+ councils (Wiltshire says until midnight); stale content in
  `agencies.$slug.tsx` too. Emily: keep all, add Areas covered to Wiltshire, drop generic support cards.
  Plan `docs/council-profile-template-plan.md` (`f769b69`). **Step 1 done** (`bd401eb`): `GenericLAProfile` +
  `src/data/councilProfiles.ts` (two markers per council; Ofsted wording built from DB rating; summary only shows if
  rating still matches), Wiltshire switched over, old component deleted, check warns on missing markers. Pushed.
- Emily asked: batches or all at once? Tutor: all at once (one code path, pages hidden, easy undo; real risk is
  data gaps). Emily: "just do it then push without my permission" (guard still blocks tutor push → she pushes).
- **Step 2 done** (`b391f7d`, local): Bristol entry (heading, subtitle, intro, photo, Mockingbird, ILACS quotes),
  all councils → `GenericLAProfile`, DB allowance fallback → `CouncilAllowanceSection`. Previewed 7 pages: all render;
  108 councils show 4–5 sections except 1 (Homes and Horizons: 2). Bristol lost its generic support cards (as agreed).
  Found: Foster Birmingham (hidden, hand-built) has headcounts (594 households etc.) → step 3 with Sandwell.
- Emily pushed `b391f7d`. **Bristol support + Ofsted date** (`7298059`): 6 support cards from
  bristol.gov.uk support page (own wording, no prices); last full ILACS 16 Jan 2023 (reports.ofsted.gov.uk, focused
  visits since); new full ILACS reported due by mid-2026 → Ofsted marker due 2026-12 (may land any time).
- **Step 3 done** (2026-10-06, `6235530`, local): Sandwell re-checked against fostersandwell.co.uk + Oct 2024 Ofsted
  PDF (WebFetch wrongly said the quotes weren't in it — extracted text by hand: all 4 there, one had been shortened
  inside quote marks → fixed). Dropped unconfirmed claims (six-stage, practice model, step-down). DB: Sandwell
  fostering_types + allowance filled (backup in data/backups). Sandwell → GenericLAProfile, old component deleted.
  Foster Birmingham stats (594/819/90%) removed; Birmingham still hand-built.
- Emily pushed `6235530`. **Foster Birmingham moved onto template** (local commit, see foster-compare log): Ofsted
  had a NEW full inspection (27–31 July 2026, published 24 Sept): overall Good, helped & protected RI, leaders Good →
  old "Good in all areas" + 2024 quotes replaced from the new report. Dropped "one of the largest" (site only says the
  Trust is the biggest children's service). Every council now on `GenericLAProfile`.
- Tooling note: old preview servers left running → tsc OOM-killed ("0 errors" was a false pass). Killed them; tsc 10.
- Emily pushed `3180654` (all template work live once Cloudflare builds). Session ended 2026-10-06 ("End lesson").
**Next up:** Emily checks live Bristol (support cards), Wiltshire (Areas covered), Sandwell + Birmingham (unlinked;
read Birmingham's new Ofsted wording); decide whether to relink Sandwell; confirm issue #17 email; notes on hidden
council pages. Due soon: Wiltshire Ofsted (Nov), Bristol Ofsted + £295 offer + 81,000 stat (Dec).

### Session 34 (2026-10-06): FOI track (backlink Tactic H) started
- Emily wants FOIs to **all 153** councils (plan had said West Midlands first). Her source: mySociety
  `data/local authorities.xlsx` (no FOI emails in it). Filter: her 4 type labels gave 131, because the dataset says
  "County", not "County council". Added 21 counties + City of London = 153. Dataset had Lincolnshire (Y&H) and
  Derbyshire (WM) in the wrong regions; fixed. All 9 regions now match official counts.
- **Checked Ofsted's "Fostering in England" underlying data (LA_Data tab):** it already publishes, per council, newly
  approved households, total de-registrations + de-registration reasons (no financial category). So Emily's Q1 was
  dropped. Redraft: 3 Qs (tenure bands at de-registration 23/24–25/26; financial/housing exit reasons 25/26;
  discretionary hardship payments count + £ 22/23 and 25/26) + section 16 "answer the rest" line. **Emily said yes to
  redrafting; final wording NOT yet approved.** Open: optional Q4 on recruitment marketing spend (fits her
  "councils compete for carers online" angle); confirm sign-off name.
- Emily: FOI files go *inside* foster-compare, back up everything. Commit `ad46c53` (local): `data/foi/foi-tracker.csv`
  (153 rows, FOI email/form columns still empty), the xlsx, Google ads/GSC export CSVs, plan line updated,
  `.gitignore` adds `data/foi/replies/` and `screenshots/` (Supabase log export has IPs, so kept off GitHub).
- Pushed `ad46c53`. West Midlands FOI contacts filled (`f741333`): 10 email, 4 web-form only (Dudley, Shropshire,
  Warwickshire, Worcestershire). Search summaries were wrong for Dudley + Warwickshire; council pages checked directly.
- **FOI wording APPROVED** (3 Qs, no marketing Q, signed Emily Browne), saved in backlink plan Tactic H. Pushed.
  Emily is watching context/credits: send West Midlands first, other 139 addresses later.
- FOI wording v3 final (all 5 Qs on 2023/24–2025/26, incl. marketing spend + exit interviews), saved in plan.
  **SENT 2026-10-06** to all 14 West Midlands (10 Bcc email, 4 forms). Tracker + outreach log updated, pushed.
  Reply due 2026-11-03. Emily drafting a purpose paragraph for future FOIs (tutor flagged: "aggregated" vs
  council-by-council publishing; "independent"; Ramsden vs Browne name check).
- Purpose paragraph approved (batch 2+). **Batch 2 SENT 2026-10-06: 10 East Midlands** (8 Bcc, 2 forms). Leicester
  FOIA@ + Derbyshire access.2info@ unverified: Emily watching for bounces; chase if no ack by ~13 Oct.
  Leicester FOIA@ BOUNCED (tutor guess) → resent via council form. Leicester asked for ID: told Emily not
  needed for FOI (s8). Northants → Northamptonshire Children's Trust (one request for both).
  **Batch 3 (15 Yorkshire, Bradford via its children's trust) + batch 4 (12 North East) SENT 6 Oct.**
  Batches 5 (24 NW) + 6 (11 EoE) SENT 6 Oct. Batch 7 (15 SW, 14 Bcc + Somerset form) SENT 6 Oct. Batch 8 (19 SE, 14 Bcc + 5 forms) SENT 6 Oct. Batch 9 (27 London Bcc) SENT 6 Oct; IoW resent to information@iow.gov.uk. London web forms (Hackney, H&F, Harrow, Havering, Redbridge) + Enfield SENT 6 Oct. **ALL 153 of 153 contacted (Tactic H sending complete), all replies due 2026-11-03.** Derbyshire RESENT to access2info@ 6 Oct (Derby City also got a duplicate by mistake). Kingston, Richmond, RBWM redirected to Achieving for Children (AfC) form; resubmitted 6 Oct as one request asking for per-council figures. Web-search budget ran out this session. Acks: 45 reference numbers logged in tracker (+Rutland, Oxfordshire, Somerset, Halton, Kirklees later on 6 Oct); S Glos sent a 2nd auto-reply; auto-replies (no ref yet) from Barnsley, Calderdale, Dorset, Ealing, N Yorks, Staffs, S Glos. Ack emails now in data/foi/replies/ (gitignored).
- **Session 34 ended (End lesson).** Skill note: Emily found Enfield's FOI form herself on the council site, and asked
  good "is this council in scope?" questions (city vs county unitary). Lesson she met: same-name city/county councils
  (Derby vs Derbyshire) are separate; check the tracker row before sending.
**Next up (FOI):** log acknowledgement reference numbers as Emily pastes them; handle bounces (most likely: Brent,
Tower Hamlets, Waltham Forest, Wandsworth; also Kent, W Berks, BANES, Wiltshire, Bedford, Norfolk, Southend, N Lincs,
Sunderland, Manchester, NE watch list). Richmond confirmed live (replied). Check AfC reply gives per-council figures.
**3 Nov 2026: replies due**, then chase non-responders from the tracker. Offer: plan the reply analysis for the
press release. Web searches may be limited per session: read council sites directly when they are.
**Session 34 continued (same day, after the first End lesson):** 45 FOI references logged; agency emails all
answered (Heart and Home told they're live; Fusion: Emily rewrote the reply herself, clearer than tutor's draft,
explaining postcode search = office distance vs city pages = coverage; Thrive: offered Enhanced with sponsored link,
PDF attached). FosterWiki added to backlink plan Tier 1 (FOI findings angle, after 3 Nov). Skills shown: she pushed
back on over-engineered suggestions (coverage-by-council) and chose the simplest honest answer; spotted partial-council
coverage flaw herself; spotted a new backlink target from an agency's site. **Next session:** new FOI acks; Lydia's
reply (add city-page coverage + any hubs, show changes first); parked ideas: "Satellite office" label wording,
coverage in postcode search.
**Session 35 (2026-10-06):** 5 more FOI acks logged (S Tyneside, Manchester, Milton Keynes, Bexley = refs; City of London no ref, Square Mile only so may say "not held"). Bexley, S Tyneside, Manchester confirmed live (were bounce-watch). Commit `9bfc7d1`.
**Session 35 cont. (2026-10-06), site changes (all pushed):**
- Agency profile shortlist buttons now always orange, both states (`488363e`). City/search pills unchanged: clear, turns orange.
- Sandwell profile linked + indexed (`profileLinks.ts`, `INDEXABLE_SLUGS`, sitemap). Live set now: Wiltshire, Bristol, Sandwell. Foster Birmingham added by mistake (Emily meant Bristol), then reverted (`e315cb7`).
- Foster Birmingham rates added to DB (was "Enquire for rates"), taken from their site calculator (page last edited Oct 2025, above 2026/27 NMA). Script `scripts/update-foster-birmingham-rates-2026-10-06.mjs`. FOI tracker Birmingham row reminds us to swap in FOI figures (due 3 Nov). Emily says the page otherwise looks good. **Next: link + index Birmingham when she confirms.**
- Rates button heading on all council profiles: "Shortlist to confirm what you'd be paid" (was "…check current rates", which contradicted "Figures checked"). One size bigger (`22313d9`). Wiltshire now shows its "Figures checked September 2026" line.
- Lesson: my CSV edit turned the tracker's Windows line endings into Unix ones (whole-file diff), so I restored them (`2d906f6`). **Always keep CRLF in foi-tracker.csv.**
- **Badges decided:** use the criteria on /agency-badge (Ofsted Good counts for both tiers). Wiltshire = Exceptional (out-of-hours needn't be 24/7, Emily's call). Bristol and Birmingham = Trusted. **Sandwell = no badge**: no therapeutic model found, and Ofsted Oct 2024 flagged out-of-hours as inconsistent (Reg 17 requirement). Caseloads unknown for all four.
- Badge now sits at the page bottom with an agency-specific `badgeText` + "How we award badges →" link. The photo keeps the top right and is hidden on phones. Wiltshire got a hero photo (girl with a magnifying glass, from screenshots/…049). Commit `0fe4e5e`.

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
