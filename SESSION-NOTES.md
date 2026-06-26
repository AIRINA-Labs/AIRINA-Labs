# Session notes — site state, 2026-06-26

Fresh snapshot. Supersedes earlier (2026-06-06 and 2026-06-24) snapshots — those are preserved in git history. The repository was destroyed and recreated on 2026-06-25 to flush a stale collaborator entry; the local commit graph and content were re-pushed intact from the backup bundle `AIRINA-Labs-backup-2026-06-25.bundle` (kept in the parent directory). Contributors list since rebuild: `ai-technipreneurs` only.

## Top-line architecture

Every page in the site carries a two-tier sticky nav. Top row (subdued): brand mark + the five-entry feature nav (`About / Pillars / Training / People / Contact`) + EN/FR + theme. Second row (MIT-style menu-bar, khaki): the three-entry audience strip — `Programs · For Individuals · For Organizations` (FR: `Formations · Pour particuliers · Pour organisations`). Both rows sticky together.

Four dedicated audience landing pages exist alongside the feature pages: `for-individuals.html`, `for-organizations.html`, `pour-particuliers.html`, `pour-organisations.html`.

## Course catalog (MIT-style)

`training.html` and `formations.html` are now real MIT-Professional-Education-style catalog pages, not tier-accordion brochures. Each carries:

- A title bar with the catalog promise + lede + meta (cost-to-trainees zero, languages, locations, cohort size).
- A filter strip (vanilla JS): search input + Topic dropdown + Format dropdown + Reset. Live row hiding.
- A 7-column catalog table: `Course | Topic | Dates·Length | Format | Lead Instructor(s) | Fee | Status`. **Fee column is blank for every row** by design (the "no trainee writes a check" refusal). Status pills: `Open` (green), `Planned` (muted), `Future` (dim).
- Ten course rows across three tiers — six AIRINA-native programs + four adapted from MIT's catalog for mission relevance.
- Charter-restatement band ("what this catalog is not").
- "How a cohort works" three-step explainer + contact block.

The ten courses:

| # | Course | Tier | Status |
|---|---|---|---|
| /01 | TDA for Data Scientists | I | Open (Q3 2026) |
| /02 | Interpretable ML for Regulated Industries | I | Open (Q4 2026) |
| /03 | Topological Foundations of Deep Learning | II | Planned (Summer 2027) |
| /04 | Quantum-Topological Methods for Finance | II | Planned (2027) |
| /05 | Applied AI & Data Science for African Systems | II | Planned (2027) — adapted from MIT |
| /06 | Mathematics and Modeling for Modern AI | II | Planned (2027) — adapted from MIT |
| /07 | Ethics, Risks & Regulation of AI for West African Institutions | II | Planned (2027) — adapted from MIT |
| /08 | AI for Engineers — Cotonou Edition | II | Planned (2027) — adapted from MIT |
| /09 | Asymmetric Topology & Complexity — Research School | III | Future (2027–28) |
| /10 | TDA for Robust & OOD-Aware ML | III | Future (when research matures) |

## Course detail subpages (MIT-style two-column)

All 20 detail subpages (10 EN + 10 FR) are on a uniform MIT-Professional-Education-style template:

- Dark forest title bar with tier tag + course title + italic tagline + "Back to Course Catalog" link.
- Sticky left sidebar with the **Register Interest** button, then seven metadata fields (Lead Instructor(s), Date(s), Registration Deadline, Location, Course Length, Course Fee `[blank]`, Certificate), then a "Sign up for course updates" button.
- Right content: two intro paragraphs + 4-tab content. **The four tabs are fixed everywhere**: `Program Overview · Learning Outcomes · Who Should Attend · Brochure` (FR: `Aperçu du programme · Acquis pédagogiques · À qui s'adresse cette formation · Brochure`). Tab IDs `tab-overview/outcomes/audience/brochure` are language-stable because the tab-switching JS depends on them.
- Mobile (<960px): sidebar drops to top, tabs scroll horizontally, nav-links hide.
- Brochure tab is a dashed-border placeholder card pointing to a mailto for the PDF on request. No fake download links.

The 12 existing AIRINA detail pages had their original content (audience, prerequisites, curriculum, certificate language) preserved during migration — restructured into the 4 tabs, not rewritten. The 4 new courses (training-08/09/10 + training-07-applied-aids) have AIRINA-voice content generated from briefs, FR mirrors created in parallel.

## Audience landing pages

| File | Scope | Three paths in |
|---|---|---|
| `for-individuals.html` | scope-training (gold) | 01 Take a cohort → `training.html` · 02 Read with us → `paper-club.html` · 03 Apply for a position → mailto |
| `for-organizations.html` | scope-products (amber) | 01 Deploy a product → `pillar-products.html` · 02 Co-design research → `pillar-research.html` · 03 Sponsor a cohort → mailto |
| `pour-particuliers.html` | scope-training | FR mirror, links to `groupe-de-lecture.html` |
| `pour-organisations.html` | scope-products | FR mirror |

`for-organizations.html` carries a `refusals-band` restating the five charter refusals — institutional readers see the non-negotiables before they hit the contact form.

**Color-scope decision (2026-06-26, settled):** the audience pages' body scope class maps to the first/dominant path-card's pillar. For Individuals leads with "Take a cohort" → `scope-training` (gold). For Organizations leads with "Deploy a product" → `scope-products` (amber). Considered and rejected: both pages `scope-research` (would make them look like the research pillar page), and dropping the scope class altogether (kills the audience-routing visual signal). Current mapping is the only one that keeps the two pages visually distinct, ties the accent to the visitor's dominant action mode, and avoids misleading about which pillar the page belongs to.

## Paper Club (dedicated pages)

`paper-club.html` (EN) and `groupe-de-lecture.html` (FR) — dedicated reading-group destination pages, both scope-research (green). Seven sections each:

1. Dark-forest title bar with the Vol. I N°01 stamp + h1 "We read what we want to write." / "Nous lisons ce que nous voulons écrire."
2. **How a session works** — five-column timeline of one session's hour (arrivals/framing, first discussant, second discussant, open discussion, close). Not on the homepage section.
3. **Format & logistics** — six terse items (cadence, where, languages, preparation, notes/archive, cost). Also not on the homepage section.
4. Next session TBA card.
5. Reading list — full Cycle 1 (6 papers) + Cycle 2 (4 papers), citations verified.
6. **Two ways in** — Subscribe + Propose-a-paper CTA cards. Propose-a-paper for Cycle 3 is new; not exposed anywhere else.
7. Past sessions — archive-in-progress placeholder, honest about being in Volume I.

The homepage `#paper-club` section is unchanged in structure (full reading list still on the homepage) but its primary CTA now points to the dedicated page. `for-individuals.html` and `pour-particuliers.html` "Read with us" path cards link directly to the dedicated pages.

## Research pillar — Foundation band

`pillar-research.html` and `pilier-recherche.html` carry a new `#foundation` section between the hero and the six-themes block: eyebrow "Fundamental sciences" / "Sciences fondamentales", h1 *"Underneath every technology, mathematics."* / *"Sous chaque technologie, des mathématiques."* The body paragraph carries the institute's first public mention of the **Mathematical Residency** program (FR: "Résidence mathématique"), inviting and gathering leading researchers in the fundamental sciences.

## Palette + brand mark (unchanged from 2026-06-06)

| Token | Light | Dark | Role |
|---|---|---|---|
| `--bg` | `#F2EBD3` | `#14180D` | Page paper / forest-black |
| `--bg-soft` | `#E9DFBE` | `#1E2415` | Deeper khaki / lifted forest |
| `--ink` | `#1F2A18` | `#ECE3C5` | Deep forest / warm khaki text |
| `--muted` | `#6B6A47` | `#8E8A6E` | Olive |
| `--surface` | `#FFFFFF` | `#1E2415` | Cards, avatars, portraits |
| `--accent` (default) | `#C97A1F` | `#E5A94E` | Burnt amber / gold |
| `--research` | `#2D6A4F` | `#6FBF8E` | Forest green |
| `--training` | `#C8A24A` | `#E8C778` | Warm gold |
| `--products` | `#C97A1F` | `#E5A94E` | Burnt amber |

Scope system (`.scope-research / .scope-training / .scope-products`) rebinds `--accent` for any subtree. Trefoil-knot brand mark + AI/RIN/A wordmark identical across all 38 HTML files and `favicon.svg`.

## Repository hygiene

- **Sole contributor**: `ai-technipreneurs`. Enforced by `hooks/commit-msg` (version-controlled in `hooks/`), which rejects any commit message containing AI-assistant attribution patterns. Activate in any fresh clone with `git config core.hooksPath hooks`.
- **`.gitignore`**: excludes local AI-assistant config dirs (`.claude/`, `.cursor/`, `.aider*`), backup bundles (`*.bundle`), OS cruft, editor settings.
- **Backup bundle**: `../AIRINA-Labs-backup-2026-06-25.bundle` (414 KB) — complete history at the pre-rebuild HEAD plus the `backup-pre-destroy-2026-06-25` tag. Restore command: `git clone <bundle> AIRINA-Labs-restored && cd AIRINA-Labs-restored && git config core.hooksPath hooks`.

## File inventory

**38 HTML pages** (19 EN + 19 FR mirror) + `favicon.svg` + `README.md` + this file + `.gitignore` + `hooks/commit-msg` + `.claude/` (local config dir, gitignored).

EN files:
- Homepage: `index.html`
- Audience landings: `for-individuals.html`, `for-organizations.html`
- Catalog: `training.html`
- Training detail (10): `training-01-tda.html` through `training-06-robust.html`, plus `training-07-applied-aids.html`, `training-08-math-modeling.html`, `training-09-ethics-ai.html`, `training-10-ai-engineers.html`
- Pillar pages (4): `pillar-research.html`, `pillar-products.html`, `pillar-training.html`, `pillar-incubator.html`
- Paper Club: `paper-club.html`

FR files (same structure, mirror filenames):
- `accueil.html` · `pour-particuliers.html` · `pour-organisations.html` · `formations.html`
- `formation-01-atd.html` through `formation-06-robuste.html`, plus `formation-07-ia-ds-appliquee.html`, `formation-08-maths-modelisation.html`, `formation-09-ethique-ia.html`, `formation-10-ia-ingenieurs.html`
- `pilier-recherche.html`, `pilier-produits.html`, `pilier-formation.html`, `pilier-incubateur.html`
- `groupe-de-lecture.html`

## Outstanding (priority order)

1. **Extract shared CSS to `styles.css`.** Each page carries ~250 lines of identical CSS boilerplate × 38 files ≈ 460 KB total CSS payload. Single source cuts to ~150 KB (~67% reduction) and turns the next brand-token change from a 38-file sweep into a 1-file edit. Higher leverage than ever given the page count.
2. **EN/FR mirror drift on homepage.**
   - `accueil.html` carries an extra `<section id="work">` (publications profile list) absent from `index.html`.
   - `index.html` uses `.hero-cards.asym`; `accueil.html` uses symmetric `.hero-cards`.
   - Section-head pattern inconsistent — EN uses `class="headline"`, FR uses `class="section-head"` with eyebrow.
4. **Dead CSS sweep on `index.html`**: `.team-grid`, `.team-member`, `.team-portrait`, `.placeholder-note`, `.repos`, `.repo`, `.hero-cards.asym` rules are unused on the homepage after earlier cleanup. Inert but cruft.
5. **Inline styles to move to classes** (12 training detail files): `style="max-width:760px"` on `<ul class="bullets">`, `style="margin-top:..."` on `<p class="prose">`.
6. **Self-host IBM Plex.** Removes Google Fonts CDN dependency.
7. **Catalog cohort dates hard-coded** in `training.html` + `formations.html` rows. When a cohort closes or new dates firm up, edit the relevant `.catalog-row` blocks in both files. Future: small JSON manifest driving both.
8. **Paper Club archive** — currently a placeholder. Once Cycle 1 closes, populate with discussion notes + contested points + follow-up references per session.

## Commit trail (2026-06-24 → 2026-06-26)

Working chronologically forward from the cleanup-pass entry point:

- `4eda89c` — Homepage: kill placeholder Team grid + leaked internal notes
- `b5d58c1` — Pillars: absorb the SVG glyphs from Positions, drop the duplicate section
- `7182c15` — Paper Club: swap the stale dated card for an honest TBA state
- `e564cd3` — Repos: drop the fictitious 4-card section
- `759da50` — Training: add an 'Open cohorts' schedule strip above the principle band
- `38a2639` — Add audience landing pages: For Individuals + For Organizations (EN + FR)
- `4b74761` — *(reverted by `64eeac5`)* Nav: rewrite 24 pages to audience-first IA
- `64eeac5` — Revert the above (audience nav was meant to be additive, not replacement)
- `c4a9b69` — Add menu-bar audience strip below the main nav, keep the feature nav
- `5a71012` — SESSION-NOTES: fresh snapshot dated 2026-06-24
- `80662ed` — Course Catalog: rebuild training.html as MIT-style 10-course catalog + demo detail page
- `c7249cb` — Course Catalog Phase B: all 19 detail pages on the MIT-style template
- `f52ee9e` — Add commit-msg hook to enforce no-AI-attribution policy
- `b2893cc` — Scrub literal AI-assistant references from SESSION-NOTES; add .gitignore
- `609dd98` — Scrub remaining literal AI-assistant tool name from SESSION-NOTES commit trail
- `c62be09` — gitignore: also exclude `*.bundle`
- *(2026-06-25: repo destroyed + recreated; same content re-pushed)*
- `8bac93b` — Research pillar: add 'Underneath every technology, mathematics' band + Mathematical Residency announcement
- `8d90f61` — Paper Club: add dedicated `paper-club.html` + `groupe-de-lecture.html`

All commits author `ai-technipreneurs <ai.technipreneurs@gmail.com>`. None carry an AI-assistant co-author trailer (enforced by the hook since `f52ee9e`). Going forward: the hook rejects any commit message with such a trailer — see `hooks/commit-msg` for the enforced patterns. Activate in any fresh clone with `git config core.hooksPath hooks`.
