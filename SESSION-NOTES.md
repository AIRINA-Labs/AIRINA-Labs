# Session notes — design overhaul (late May → early June 2026)

End-of-session snapshot. Use this to pick up where the design iteration left off.

## Where the site stands

### Palette (final)

| Token | Light | Dark | Role |
|---|---|---|---|
| `--bg` | `#F2EBD3` | `#14180D` | Page paper / forest-black |
| `--bg-soft` | `#E9DFBE` | `#1E2415` | Deeper khaki band / lifted forest |
| `--ink` | `#1F2A18` | `#ECE3C5` | Deep forest / warm khaki text |
| `--ink-soft` | `#2E3D25` | `#CDC4A4` | |
| `--muted` | `#6B6A47` | `#8E8A6E` | Olive |
| `--surface` | `#FFFFFF` | `#1E2415` | Cards, avatars, portraits |
| `--accent` (default) | `#C97A1F` | `#E5A94E` | Burnt amber / gold |
| `--research` | `#2D6A4F` | `#6FBF8E` | Forest green |
| `--training` | `#C8A24A` | `#E8C778` | Warm gold |
| `--products` | `#C97A1F` | `#E5A94E` | Burnt amber |

Pillar-soft variants (`--research-soft`, etc.) at 10–12% opacity for tinted section backgrounds.

### Functional color assignment

One job per color:

- **White** → active content surfaces (hero cards, path-router cards, avatars, team portraits, featured cards)
- **Khaki** → page paper, soft bands
- **Forest green** → ink, headings, watermark strokes
- **Green / Gold / Orange** → pillar identity. Green = Research (rigor, depth). Gold = Training (cohorts, graduation). Orange = Products (deployment, action).

### Scope system

Three classes that rebind `--accent` to a pillar's color for any subtree:

```css
.scope-research { --accent: var(--research); }
.scope-training { --accent: var(--training); }
.scope-products { --accent: var(--products); }
```

Applied:
- At `<body>` level on pillar pages (`pillar-research.html` → scope-research; all `training-*.html` + `pillar-training.html` + `training.html` + `formations.html` + FR mirrors → scope-training; products pages → scope-products).
- At element level on the homepage hero cards, pillar list items, path-router cards, now-strip rows, and the Paper Club section.
- `pillar-incubator.html` + FR mirror stay default amber (the incubator is dormant).

### Brand mark

A **trefoil knot** — (2,3)-torus knot projection drawn as polyline with 36 sample points. Three colored thirds, three crossings with proper over/under (gaps on the under-strand), right-handed handedness. 3-fold rotational symmetry. Lives identically in all 24 HTML files and `favicon.svg`.

Coordinates computed from `x(t) = -(2+cos(3t))*sin(2t)/3` and `y(t) = (2+cos(3t))*cos(2t)/3`, scaled into a 40×40 viewBox centered at (20,20) with scale 12 and y-flip. The colored "thirds" each correspond to a 120° arc of the parameter, with two interior gaps per third indicating where that strand passes under the next.

### Wordmark

"AIRINA Labs" rendered as three colored segments:
- `AI` in green (`--research`)
- `RIN` in gold italic (`--training`)
- `A` in orange (`--products`)

Colors are locked to `--research/--training/--products`, not `--accent`, so the wordmark stays constant across all pages regardless of body scope.

## Homepage components (current order)

1. **Announce bar** — gold scope, Cohort 1 cohort 1 of TDA training
2. **Nav** — brand mark + AI/RIN/A wordmark + 5 nav links + EN/FR toggle + theme button
3. **Hero** — H1 "The shape of African data" + lede + coords
4. **Path router** — 4-up white-card grid "What brings you here?" (bank → products, researcher → research, trainee → training, funder → contact)
5. **Refusals block** — replaces the old "commitments" block. "Five things we will not do." Khaki band, 4px accent bar left, large declarative serif sentences each starting with italic-accent "No" / "Aucun".
6. **Hero pillar cards** — 3 asymmetric (research wide on left, training + products stacked on right)
7. **Pillars 4-up grid** — Research / Products / Training / Incubator with numbered headings
8. **Now strip** — present-tense status ("Currently drafting / teaching / deploying") with pulse indicator
9. **Paper Club** — bold green-tinted band with stamp + featured next-session card. See dedicated section below.
10. **Updates** — timeline news items
11. **Roadmap** — three-phase plan
12. **Values** — four-up grid
13. **People** — director and collaborators (avatars now on white surfaces)
14. **Team grid** — 10-member placeholder portrait grid
15. **Tech** — language/lib/infra columns
16. **Repos** — open GitHub links
17. **Contact** — auto-fit grid with email / HQ / office hours / web / code
18. **Footer**

## Notable component specs

### Refusals block (replaces old Commitments)

Light khaki band with thick top/bottom rules and 4px left accent bar. Eyebrow "Charter" / "Charte". Title with italic-accent emphasis: *"Five things we **will not** do."* / *"Cinq choses que nous **ne ferons pas**."*

Five large declarative sentences (`clamp(1.4rem, 2.6vw, 1.9rem)`) each starting with italic-accent prefix:
- EN: "No" — "No program runs longer than two weeks." etc.
- FR: "Aucun" — "Aucun programme ne dépasse deux semaines." etc.

The leading negation word is the visual entry point of every line; the prefix repetition is the rhetorical move.

### Paper Club section

Visible green-tinted band (`background: var(--research-soft)`) with 3px solid accent rules top and bottom. Scoped to `scope-research`.

- **Stamp**: italic serif "№ 01" on a white card with green border, "Vol. I · 2026" mono subtitle
- **H1 title** (`clamp(2.2rem, 4.5vw, 3.2rem)`): *"We read what we **want to write**."*
- **Featured "Next session" card** — white surface with 5px green left bar:
  - Pulsing accent dot + "NEXT SESSION" pill badge
  - Date: Thu 11 Jun 2026 · 16:00 WAT
  - H2 paper title with citation, note, and two CTAs (filled green "Register →" + outlined "Read the paper →")
- **Cycle 1 list (6 papers)** + **Cycle 2 list (4 papers)** — full curated reading list, see SESSION-NOTES Paper Club appendix below
- **Bottom CTA box** — white card "How to join"

### Training catalogs (`training.html` + `formations.html`)

- **Principle-light box** — light khaki paper + left accent bar. Lede paragraph + motto closer separated by a top rule. Strategic gold `<strong>` on load-bearing phrases.

## Paper Club starter reading list

Cycle 1 — Foundations → deployment:

1. **Carlsson, G. (2009)** — *Topology and Data*, Bull. AMS 46(2), 255–308
2. **Edelsbrunner, H., Letscher, D., Zomorodian, A. (2002)** — *Topological persistence and simplification*, DCG 28(4), 511–533
3. **Carlsson, G., Ishkhanov, T., de Silva, V., Zomorodian, A. (2008)** — *On the local behavior of spaces of natural images*, IJCV 76(1), 1–12
4. **Singh, G., Mémoli, F., Carlsson, G. (2007)** — *Topological methods for the analysis of high-dimensional data sets and 3D object recognition*, Eurographics SPBG
5. **Adams, H., Emerson, T., Kirby, M., et al. (2017)** — *Persistence Images*, JMLR 18(8), 1–35
6. **Björkegren, D., Grissen, D. (2020)** — *Behavior revealed in mobile phone usage predicts credit repayment*, World Bank Econ. Review 34(3), 618–634

Cycle 2 — On deck:

7. **Cohen-Steiner, D., Edelsbrunner, H., Harer, J. (2007)** — *Stability of persistence diagrams*, DCG 37(1), 103–120
8. **Bubenik, P. (2015)** — *Statistical TDA using persistence landscapes*, JMLR 16, 77–102
9. **Rudin, C. (2019)** — *Stop Explaining Black-Box ML Models for High Stakes Decisions and Use Interpretable Models Instead*, Nat. Mach. Intell. 1(5), 206–215
10. **Nicolau, M., Levine, A. J., Carlsson, G. (2011)** — *Topology-based data analysis identifies a subgroup of breast cancers with a unique mutational profile and excellent survival*, PNAS 108(17), 7265–7270

All citations verified, none invented.

## Removed in earlier session passes

- Original `.manifesto` dark-forest-band rules
- `.principle-box` intermediate variant (superseded by `.principle-light`)
- `.hero-watermark` giant outline text on homepage hero
- `<section id="work">` from `index.html` (FR mirror still carries a version)
- Empty `.roadmap {}` rule, duplicate `.contact { repeat(4) }`
- Dead `.work-profile*` rules from `index.html`
- The "Commitments" block — replaced with "Refusals" (the framing the user explicitly rejected: *"Five things, written down so we can be held to them"* with `01 · Length. The longest...` template)

## Universal fixes (all 24 files)

- **Theme FOUC fix**: inline `<script>` in `<head>` reads `localStorage` and sets `data-theme` before first paint.
- **`will-change: backdrop-filter`** on `.site-nav` to promote nav to GPU layer upfront.
- Token system: `--research / --training / --products` (+ soft variants), `--surface / --surface-shadow`.

## Open items (priority order)

1. **Extract shared CSS to a single `styles.css`.** ~78% of each file's CSS is identical boilerplate. Would cut total CSS payload across a 24-page session from ~302KB → ~104KB (66% reduction) and turn the next brand-token change from a 24-file PowerShell sweep into a 1-file edit. Risk: per-file work to remove interleaved duplicates without breaking page-specific CSS. Best done as a dedicated session.

2. **EN/FR mirror drift.**
   - `accueil.html` has a `<section id="work">` (publications profile list) absent from `index.html`.
   - `index.html` uses `.hero-cards.asym` (1-large + 2-small grid); `accueil.html` uses symmetric 3-column `.hero-cards`. The `.asym` CSS is also missing from `accueil.html`.
   - Section-head pattern inconsistent — EN uses `class="headline"`, FR uses `class="section-head"` with eyebrow.

3. **Inline styles to move to classes.**
   - `style="max-width:760px"` repeated on `<ul class="bullets">` in 12 training detail files → should be a `.bullets` rule.
   - `style="margin-top:..."` on `<p class="prose">` in 4+ pillar/training-detail files.

4. **Self-host IBM Plex.** Removes Google Fonts CDN dependency.

5. **Paper Club next-session date is hard-coded** (Thu 11 Jun 2026). Will need updating each cycle. Future: a small CSV or YAML file driving the next-session card, or — since this is a static site — a clear comment marking the line to update each cycle.

## File inventory

24 HTML pages (12 EN + 12 FR mirror) + `favicon.svg` + `README.md` + this file + `.claude/` config dir.

Pages by section:
- **Homepages**: `index.html` (EN), `accueil.html` (FR)
- **Training catalogs**: `training.html`, `formations.html`
- **Training detail pages**: `training-01-tda.html` through `training-06-robust.html` (EN), `formation-01-atd.html` through `formation-06-robuste.html` (FR)
- **Pillar pages**: `pillar-research.html`, `pillar-training.html`, `pillar-products.html`, `pillar-incubator.html` (EN) + `pilier-*.html` (FR)

## Uncommitted work

All session changes are in the working tree, not committed. Session totals roughly: brand mark + palette + scope system + path router + commitments→refusals + now-strip + office hours + team grid + Paper Club + theme FOUC fix + dead-code cleanup + brand-mark iterations.
