# Session notes — site state, 2026-06-24

Snapshot at end of the cleanup + MIT-inspired IA pass. Supersedes the earlier (June 6) snapshot; that one is preserved in git history.

## Top-line architecture change

The site is now audience-first, not feature-first. The nav across all 28 pages is a 3-entry audience strip:

- EN: `Programs · For Individuals · For Organizations`
- FR: `Formations · Pour particuliers · Pour organisations`

The old 5–6-entry feature nav (`About / Pillars / Training / People / [Work] / Contact`) is gone. The brand mark still routes home from every page; contact and content sections remain discoverable by scroll or via the audience landings.

### New audience landing pages

| File | Scope | Three paths in |
|---|---|---|
| `for-individuals.html` | scope-training (gold) | 01 Take a cohort → training.html · 02 Read with us → #paper-club · 03 Apply for a position → mailto |
| `for-organizations.html` | scope-products (amber) | 01 Deploy a product → pillar-products.html · 02 Co-design research → pillar-research.html · 03 Sponsor a cohort → mailto |
| `pour-particuliers.html` | scope-training | FR mirror |
| `pour-organisations.html` | scope-products | FR mirror |

Each new page reuses the existing design system (IBM Plex serif + mono, warm-paper palette, scope variables, sticky nav, dark-mode toggle). Each carries a `who-list` (honest-fit list) and at least one `contact` block with two specific inboxes.

`for-organizations.html` adds a `refusals-band` section restating the five charter refusals — institutional readers see the non-negotiables before they hit the contact form.

## Palette (unchanged from June 6)

| Token | Light | Dark | Role |
|---|---|---|---|
| `--bg` | `#F2EBD3` | `#14180D` | Page paper / forest-black |
| `--bg-soft` | `#E9DFBE` | `#1E2415` | Deeper khaki / lifted forest |
| `--ink` | `#1F2A18` | `#ECE3C5` | Deep forest / warm khaki text |
| `--ink-soft` | `#2E3D25` | `#CDC4A4` | |
| `--muted` | `#6B6A47` | `#8E8A6E` | Olive |
| `--surface` | `#FFFFFF` | `#1E2415` | Cards, avatars, portraits |
| `--accent` (default) | `#C97A1F` | `#E5A94E` | Burnt amber / gold |
| `--research` | `#2D6A4F` | `#6FBF8E` | Forest green |
| `--training` | `#C8A24A` | `#E8C778` | Warm gold |
| `--products` | `#C97A1F` | `#E5A94E` | Burnt amber |

Scope system (`.scope-research / .scope-training / .scope-products`) rebinds `--accent` to a pillar's color for any subtree. Applied at `<body>` level on pillar pages and on the new audience pages; at element level on homepage hero cards, path-router cards, now-strip rows, Paper Club, and the new training Open Cohorts strip.

## Brand mark + wordmark (unchanged)

Trefoil knot — (2,3)-torus knot, three colored thirds with proper over/under crossings, right-handed handedness, 3-fold rotational symmetry. Lives identically in all 28 HTML files and `favicon.svg`.

"AIRINA Labs" wordmark: `AI` green (research) / `RIN` gold italic (training) / `A` amber (products). Locked to pillar colors, constant across all pages regardless of body scope.

## Homepage (`index.html` / `accueil.html`) component order

Down from 18 sections to **13**. What's left:

1. Announce bar — Cohort 1 of TDA training
2. Nav — brand mark + AIRINA Labs wordmark + 3-entry audience nav + EN/FR + theme
3. Hero — "The shape of African data" + lede + coords
4. Path router — 4-up "What brings you here?" (bank / researcher / trainee / funder). Now reinforces the audience nav rather than being the only audience signal.
5. Refusals (Charter) — "Five things we will not do"
6. **Pillars (4-up)** — Research / Products / Training / Incubator. Each card now carries a `pillar-visual` SVG glyph above the numeral (research-manifold / orbit-torus / ascending-lines / dormant-seed for Incubator).
7. Now strip — present-tense status with pulse indicator
8. Paper Club — featured "next session" card is now a **TBA state** ("Cycle 1 in progress · Next paper announced via mailing list"), followed by the full Cycle 1 (6 papers) + Cycle 2 (4 papers) reading list, then a "How to join" white card
9. Updates — timeline news items
10. Roadmap — three-phase plan
11. Values — four-up grid
12. People — director + 1 collaborator + Open Positions callout (placeholder Team grid removed)
13. Tech — "What's on the bench" (5 identity-forward groups: For TDA / For interpretable ML / For modeling / For data & shipping / Languages)
14. Contact — auto-fit grid with email / HQ / office hours / web / code
15. Footer

(The "Open repositories" 4-card section was removed — the AIRINA-Labs org currently contains only this website repo, so the section was fiction.)

## Training catalog (`training.html` / `formations.html`)

New section above the principle band: **Open Cohorts strip**. 5-column desktop grid collapsing to a stacked mobile layout. Card with 4px gold left bar, khaki header (eyebrow + "No trainee writes a check" reassurance), two rows for Tier-I programs:

- /01 TDA for Data Scientists · 3 days · Cotonou · Cohort ~12 · Q3 2026 · Open · Full curriculum →
- /02 Interpretable ML for Regulated Industries · 3 days · Cotonou · Cohort ~12 · Q4 2026 · Open · Full curriculum →

The existing per-tier accordions and Catalog-at-a-glance snapshot are unchanged below.

## Component specs of note

### Refusals block (homepage)

Light khaki band with 4px left accent bar, "Charter" eyebrow, headline *"Five things we **will not** do."* / *"Cinq choses que nous **ne ferons pas**."* Five large declarative sentences each starting with italic-accent prefix `No` / `Aucun`.

### Pillars 4-up (homepage)

Each `.pillar` now contains a `.pillar-visual { color: var(--accent); height: 56px; display: block; margin-bottom: 0.95rem; }` slot above the numeral. SVGs are inline, use `currentColor`, sit at ~130px max width and 56px height. The Incubator glyph (new) is a solid center circle, two concentric dashed rings, dashed cardinal ticks — visual cue for "germination potential, not yet activated."

### Paper Club next-session card (homepage)

Same visual shell as before (white card, green left bar, pulse dot). Content rewritten to an honest TBA state — no specific date, just "Cycle 1 in progress · Next paper · date announced via mailing list" plus "Subscribe →" + "See the reading list ↓" (anchors to `#paper-club-list`). When a real next session is scheduled, restore the specific-session shape.

### Training Open Cohorts strip (training catalog)

CSS lives in `training.html` and `formations.html`. Classes: `.open-cohorts-band / .open-cohorts / .open-cohorts-head / .open-cohorts-eyebrow / .open-cohorts-note / .cohort-row / .cohort-num / .cohort-body / .cohort-meta / .cohort-when / .cohort-status / .cohort-cta`. Mobile breakpoint at 800px collapses the 5-col grid to a 2-col (num + stacked body).

## Removed in earlier (June 24) session passes

- Placeholder Team grid in `index.html` (10 "Name to be announced" slots + leaked placeholder-note divs).
- `#positions` section on the homepage — duplicated the Pillars section's content with different visualization. SVG glyphs preserved by porting into the Pillars cards.
- `#repos` section on the homepage — fabricated four cards all pointing to the same org URL; the AIRINA-Labs org has only the website repo. Contact section still carries the org link.
- Stale "Thu 11 Jun 2026" Paper Club next-session date — replaced with TBA state.
- The original 5–6-entry nav-links block on every page (replaced with the 3-entry audience nav).
- 6 commits' worth of AI-assistant co-author trailers (history rewrite + force-push to main).

## File inventory

**28 HTML pages** (14 EN + 14 FR mirror) + `favicon.svg` + `README.md` + this file + `.claude/` config dir.

Pages by group:

- **Homepages**: `index.html` (EN), `accueil.html` (FR)
- **Audience landings (NEW)**: `for-individuals.html`, `for-organizations.html`, `pour-particuliers.html`, `pour-organisations.html`
- **Training catalogs**: `training.html`, `formations.html`
- **Training detail pages**: `training-01-tda.html` through `training-06-robust.html` (EN), `formation-01-atd.html` through `formation-06-robuste.html` (FR)
- **Pillar pages**: `pillar-research.html`, `pillar-training.html`, `pillar-products.html`, `pillar-incubator.html` (EN) + `pilier-*.html` (FR)

## Outstanding (priority order)

1. **Extract shared CSS to `styles.css`.** Now an even bigger win: ~78% of each file's CSS is identical boilerplate × 28 files = roughly 340 KB total CSS payload. Single source would cut to ~115 KB (66% reduction) and turn the next brand-token change from a 28-file sweep into a 1-file edit.
2. **EN/FR mirror drift**, still present:
   - `accueil.html` has a `<section id="work">` (publications profile list) absent from `index.html`.
   - `index.html` uses `.hero-cards.asym`; `accueil.html` uses symmetric `.hero-cards`. The `.asym` CSS in `index.html` is now mostly dead code (the section that used it was deleted).
   - Section-head pattern inconsistent — EN uses `class="headline"`, FR uses `class="section-head"` with eyebrow.
3. **Dead CSS sweep on homepage**: `.team-grid`, `.team-member`, `.team-portrait`, `.placeholder-note`, `.repos`, `.repo`, `.hero-cards.asym` rules are now unused on `index.html` after the cleanup. Inert but cruft.
4. **Inline styles to move to classes** (12 training detail files): `style="max-width:760px"` on `<ul class="bullets">`, `style="margin-top:..."` on `<p class="prose">`.
5. **Self-host IBM Plex.** Removes Google Fonts CDN dependency.
6. **Open Cohorts strip data** is hard-coded in `training.html` + `formations.html`. When a cohort closes or new dates are confirmed, edit the two `<a class="cohort-row">` blocks in each file. Future: a tiny JSON/YAML manifest driving both files.

## Commit trail (June 24 session)

Working chronologically backward from HEAD:

- `4b74761` — Nav: rewrite 24 pages to audience-first IA (Programs / For Individuals / For Organizations)
- `38a2639` — Add audience landing pages: For Individuals + For Organizations (EN + FR)
- `759da50` — Training: add an 'Open cohorts' schedule strip above the principle band
- `e564cd3` — Repos: drop the fictitious 4-card section
- `7182c15` — Paper Club: swap the stale dated card for an honest TBA state
- `b5d58c1` — Pillars: absorb the SVG glyphs from Positions, drop the duplicate section
- `4eda89c` — Homepage: kill placeholder Team grid and leaked internal notes
- (preceded by the filter-branch rewrite that stripped AI-assistant co-author trailers from `4536776..b5195df`)

All commits author `ai-technipreneurs <ai.technipreneurs@gmail.com>`. None carry an AI-assistant co-author trailer. Going forward: the `hooks/commit-msg` hook rejects any commit message that contains one — see that file for the enforced patterns. Activate the hook in any fresh clone with `git config core.hooksPath hooks`.
