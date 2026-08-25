# Bestehen / Corpus — Design Handoff

**For the architecture and engineering agent that implements the Corpus owner console.**

This file is the committable companion to the ten design pages in `Corpus/`. It states what the interface must be able to *say*, which combinations of state are legal, which decisions are load-bearing product truth, and which are presentation defaults you may replace knowingly. It deliberately specifies no endpoints, schemas, queue products, cloud vendors, model providers or frameworks.

---

## 1. Source hierarchy and authority

| Order | Document | Authoritative for |
|---|---|---|
| 1 | `17-bestehen-corpus-product-specification.md` (Stage 17, final) | Corpus behaviour, states, governance, operations, quality, cost, security, App contract, scope |
| 2 | `02_Bestehen_Identity.md` | Brand character, voice, visual direction, naming |
| 3 | `01_Bestehen_Product_Overview.md` | Umbrella purpose, Corpus ↔ App relationship |

Where the specification delegates detail to an earlier Corpus stage, that behaviour is preserved rather than simplified. Where it left an ordinary design choice open, this design chose the clearest low-maintenance default and recorded it in §9.

---

## 2. Artifact index

All files live in `Corpus/` and open directly in a browser.

| Page | File | Contents |
|---|---|---|
| 00 | `Corpus-00-Cover-Principles.dc.html` | Run configuration, six truth axes, eight design principles, information architecture, 41-surface inventory, action-risk matrix, flow map, assumptions |
| 01 | `Corpus-01-Foundations.dc.html` | 74 tokens, eight state-token families, typography, German/source-text rules, density, grid, radii, elevation, focus, diff, icons, motion, visualization rules |
| 02 | `Corpus-02-Components.dc.html` | 34 components with anatomy, variants, states, content constraints, accessibility contract, responsive behaviour; live specimens for shell, queue, evidence, review, pipeline, health, feedback |
| 03 | `Corpus-03-State-Models.dc.html` | Ten inspectable scopes, five state-model tables, uncertainty vocabulary, six capability gates, governance model, duplicate/independence model, audit event contract, change-impact model |
| 04 | `Corpus-04-Desktop-Screens.dc.html` | Twelve full 1440×1024 frames: access/empty, Inbox, specialized queue + drawer, discovery/intake, source registry/detail, runs overview/detail, Record Detail, Health, coverage/cost, benchmark, analytics/App impact, audit/search |
| 05 | `Corpus-05-Workbenches.dc.html` | Authenticity review, rights + takedown, duplicate cluster, taxonomy correction/migration, reprocess composer + run comparison, Record Detail variants, R0–R3 confirmation family, six result states |
| 06 | `Corpus-06-Responsive.dc.html` | 1280×800 and 1024×768 proofs, 390-wide read-only companion, 15-row transformation table, 200% reflow rule, desktop-only justifications |
| 07 | `Corpus-07-Flows.dc.html` | Flows A–H as step maps: 47 steps, 23 named recovery branches, eight cross-flow guarantees |
| 08 | `Corpus-08-Accessibility-Content-Security.dc.html` | WCAG 2.2 AA review (21 criteria), keyboard map, focus contract, announcement table, no-colour proof, accessible alternatives, UX-writing rules, eight security annotations |
| 09 | `Corpus-09-Coverage-Handoff.dc.html` | 37-row coverage matrix, four QC checklists answered with evidence, launch/deferred boundary, twelve load-bearing decisions, assumptions and honest gaps |

---

## 3. Run configuration in force

No run values were supplied, so every recommended default applies. Four were enhanced by professional judgement:

| Variable | In force | Enhancement and rationale |
|---|---|---|
| `BRAND_RELATIONSHIP` | Shared identity, cooler operations surface | **Enhanced.** Warm Paper is the learner surface. Corpus uses a Mist-derived cool neutral family and drops the display face; same ink, same green, denser type. Twelve columns of tabular data on warm cream reads as fatigue. |
| `MOBILE_SCOPE` | Read-only health and urgent triage | **Enhanced narrowly.** Three surfaces only: health vector, hard blockers, single record read-only. No decision controls, no rationale entry. |
| `DENSITY` | Compact but calm | **Enhanced.** Two row heights (32 dense / 40 comfortable) as a token pair, switchable per table. Type size never changes with density; 12px is the floor everywhere. |
| `HANDOFF_FORMAT` | Design pages + this file | **Enhanced.** State contracts, the coverage matrix and the copy library live as structured arrays in each page's logic class, so they can be lifted directly rather than retyped. |
| All others | Recommended default | `DESIGN_ENVIRONMENT` Claude Design; one `Corpus/` project, ten pages; 1440×1024 primary, 1280×800 and 1024×768 proofs; complete light mode, **dark mode deliberately not designed**; high-fidelity flows A–H; English operations UI with German source verbatim. |

---

## 4. Product-truth contract — do not re-decide these

These twelve decisions change what the product *means*. Page 09.4 states them on screen; they are repeated here verbatim.

1. **Six axes stay separate.** Eight state-token families, each with its own hue, marker glyph and closed vocabulary: pipeline, confidence, rights, difficulty/relevance, QA severity, identity/independence, eligibility, security/governance. One green shared across "trusted", "rights-cleared", "QA-qualified" and "published" is the single most damaging possible change.
2. **Unknown is a value.** `unknown` stays in denominators and contributes no evidence; `not_applicable` leaves the denominator. Neither ever renders as 0, false, blank, passed or failed. `not_run` is never a green tick.
3. **Locality.** Defects travel up as counts and links, never as verdicts. Trust travels down as an *inherited* value, marked as inherited; a child may cap below its parent and may never exceed it without its own local evidence.
4. **Eligibility is six answers.** Structure analytics, correctness/scoring, taxonomy publication, pattern intelligence, exact source reuse, independent prevalence — each reads a different subset of axes (page 03.4). There is no seventh, aggregate answer and no universal "production ready" switch.
5. **Rights.** Unknown is never permission; public accessibility is not a licence; an override may only tighten, never loosen. Rights never influence confidence and confidence never influences rights.
6. **Governance has four strengths of "no":** owner exclusion (R1, reversible) → ordinary block (R2, governed) → security hard-block (R3) → takedown/prevention fingerprint (R3, strongest). A weaker control may never clear a stronger one.
7. **Duplicates are three decisions,** never one: relationship class, canonical provenance anchor, preferred processing representation — plus per-metric independence. All observations remain visible; mirrors never increase prevalence; the anchor is a citation choice and raises nobody's tier.
8. **Automation proposes, never decides.** A rule or model may raise a finding, set provisional state, or record a candidate. It may not clear a hard block, overwrite a curated override, or publish anything.
9. **Audit is append-only.** No edit, no delete. A rights event never prints a confidence delta; a rerun reports which curated overrides it *retained* rather than replaced; a correction supersedes rather than rewrites.
10. **Source content has no authority.** Previews are inert, sanitized and non-focusable. Extracted text — including text that addresses automated systems — can never reach a control that sets a status. Security states are never rendered as ordinary extraction failures.
11. **Risk tier decides the confirmation.** R0 inline with 8-second undo; R1 inline panel; R2 modal with enumerated scope and required rationale; R3 two-step typed identity confirmation. The tier is a property of the action.
12. **No aggregate health score, ever.** Hard blockers sit above the seven vectors and cannot be averaged. "Insufficient data" and "not instantiated" are valid terminal states, not zeros.

---

## 5. State contracts (UI data requirements)

Page 03 carries the full tables. Summary of the required value sets:

- **Pipeline state:** `QUEUED · RUNNING · COMPLETE · PARTIAL · FAILED · BLOCKED · STALE · SUPERSEDED`. `PARTIAL` must always carry scope counts and the affected capability. `STALE` must carry its *cause*, not just an age.
- **Confidence:** eight weighted dimensions, each `0–4 | unknown | not_applicable`; tier `A | B | C | D`; plus `CAPPED (with reason)`, `DISPUTED (both assertions retained)`, `QUARANTINED`. Score is never shown without its tier. Key consistency is a **gate**, not a weight.
- **Rights:** `REUSABLE · REUSABLE_WITH_CONDITIONS · REFERENCE_ONLY · UNKNOWN_REVIEW_REQUIRED · PROHIBITED · LEGAL_REVIEW_REQUIRED · TAKEDOWN_HOLD`, plus per-action permissions (redistribution, derivative, commercial, attribution, conditions, abstract intelligence) and component/asset overrides with their own scope.
- **QA severity:** `Q0 (correctness — cannot be waived) · Q1 · Q2 · Q3 · INCOMPLETE · BLOCKED_DEPENDENCY · NOT_RUN`, each at the smallest scope where it occurs.
- **Identity/independence:** `INDEPENDENT · EXACT · REFORMATTED · DERIVATIVE · RE_RECORDED · FRAGMENT · RELATED_VARIANT · UNRESOLVED`, with independence recorded **per metric** (lexical, grammar, structure, acoustic, visual).
- **Eligibility per capability:** `E eligible · L limited · P provisional · H held · B blocked · — n/a · ○ never assessed`, plus a local/inherited flag and a text reason. Inherited limits link to the ancestor that caused them.
- **Uncertainty vocabulary (fixed words):** `unknown · not_applicable · disputed · review_required · unresolved_dependency · incomplete · provisional · not_run`. One word, one meaning, one rendering rule, everywhere.
- **Audit event fields:** `event_id · timestamp · actor_class {human|rule|model|import|reprocess} · actor · scope · action · previous→new per axis · rationale · versions {method, model, rule, taxonomy, dedup, analytics, contract} · linked · supersedes · downstream_effect · risk_tier`.
- **Change impact:** nine change types with their invalidates / leaves-untouched / App-effect triples (page 03.8). Every R2 and R3 confirmation renders its row of that table before commit.

---

## 6. Component and interaction contracts

Page 02 documents all 34 components. Non-negotiable behaviours:

- **Queue table.** Real table semantics (`th scope`, caption naming the view and its active filters). Sortable headers are buttons with `aria-sort`. Row actions reachable without hover. Priority is border + marker + word + reason string; never colour alone. Row states: rest, hover, keyboard cursor (dashed, no tint), selected (tint + left marker), acted-upon, muted-deferred.
- **Queue context object.** One persisted object per saved view: filters, sort, density, page, scroll offset, focused row. Restored after a detail visit, a reload, and a session expiry.
- **Bulk actions.** Only `Defer`, `Add note`, `Open as a slice`. No bulk publish, quarantine, rights or takedown action exists.
- **Record Detail.** One framework, ten scopes (Source Observation, Document, Exam, Section, Task, Item, Stimulus, Option, Answer/Scoring, Asset). Scope decides which panels appear and the smallest unit an action may touch. Maximum six axis chips in the header, in fixed axis order.
- **Observed vs active.** Observed is never editable and never disappears. A correction adds an interpretation with actor, rationale and version. A derivation row states which capability consumes which value. Diff is underline weight + label — never red/green fill.
- **Decision panel.** Recommendation labelled as *suggested*, with at least one alternative safe action of equal reachability. No destructive default button.
- **Rationale.** 240 characters, required at R2+, optional at R1 unless the change contradicts the observed value. Two-click evidence attachment (finding, source region). Drafts survive navigation, reload, network loss and session expiry, and are listed in the header until submitted or deliberately discarded.
- **Background work.** Anything slower than a few seconds runs in the background, states "safe to leave" as text, and reports through the job tray. **No indefinite spinner exists anywhere.**
- **Result states.** succeeded · partially succeeded (remainder listed and separately retryable) · conflict (curated value retained, candidate recorded beside it) · failed (ownership named: system, automation, source, or the decision) · refused by a stronger rule · draft preserved.
- **Sanitized preview.** Inert region labelled "quoted source evidence, inert". Scripts, embeds, forms, iframes, remote fonts and handlers removed — not disabled. Nothing inside is focusable. States: inert render, text-only, unsupported, encrypted, unsafe held, rights-suppressed, asset missing.

---

## 7. Responsive rules

Breakpoints: **≥1400** full (rail 240 + evidence rail) · **1320–1399** evidence rail becomes a drawer · **1140–1319** rail collapses to 64px (icon + three-letter label, never icon-only) · **900–1139** top rail, tables fold four columns into the record cell · **<900** read-only companion only.

- Narrowing never removes information; it changes how information is reached. Columns become a second line, panes become drawers, matrices become lists.
- **Desktop-only by design, with the reason stated on screen:** duplicate comparison, rights/takedown, reprocess composer. Below 1140 they open read-only and refuse the decision — a wrong relationship decision silently distorts every prevalence figure, and a squeezed R3 dialog makes a consequential action feel casual.
- **Mobile companion (<900):** health vector, hard blockers, single record read-only. No decision controls, no rationale entry, nothing queued for later.
- **200% zoom at any width:** reflows to the next narrower layout. Only a table body scrolls horizontally, with its header pinned; action bars move above the content rather than off-screen.
- Touch targets: 24×24 minimum with spacing in dense desktop rows; 44×44 on tablet.

---

## 8. Accessibility and content contracts

Full review on page 08 (21 WCAG 2.2 AA criteria, each with the design decision that satisfies it).

- **Every state carries marker + word + hue — all three.** Page 08.3 renders all eight families with no hue at all; each remains identifiable.
- **Focus contract:** drawer open → heading; drawer close → the originating row (its new position if the queue re-sorted); R3 → scope table first, confirm disabled until the identity matches; action completes → focus unchanged, result announced politely; row removed → next row, announced with the remaining count.
- **Announcements:** polite for progress, counts, completion, staleness and partial success; assertive only for security holds and session expiry. Nothing steals focus; nothing is announced twice.
- **No drag-only interaction.** Taxonomy assignment, cluster relationships and column order are all select-then-apply.
- **No shortcut exists** for publishing, quarantining, suppressing, purging, blocking or any R3 action.
- **Charts:** a finding sentence precedes every graphic in the DOM, and a real table follows behind "Show as table". No pie, donut, gauge or aggregate speedometer. Confidence and independence render as ranges with the point marked. Below the sufficiency threshold the chart is suppressed and the reason shown.
- **Copy:** state scope in numbers; name the owner of the problem; print why an item is prioritized; label recommendations as suggestions; use the exact uncertainty word; stay flat during failure; never imply legal certainty or telc affiliation. Banned: `Fix`, `Resolve`, `Make valid`, bare `Retry`, `Delete`, "Something went wrong", "Trusted ✓", "Ready for production", "No data", "Processing…".
- **German:** `lang="de"` on source-derived strings, `hyphens:auto`, never `overflow-wrap:anywhere`. Provider, exam, section and task names never truncate — the row grows. IDs, URLs and hashes truncate in the middle with a copy control whose accessible name contains the value once. Numbers, dates, times, negation and option cardinality are meaning-critical and never normalised away in a preview or abbreviated in a diff.
- **Fonts and icons:** IBM Plex Sans + IBM Plex Mono (SIL OFL 1.1, self-hostable, tabular figures, full umlaut/ß coverage at 12px). Icons: 22-glyph Lucide subset (ISC), 1.75px stroke on a 24 grid, rendered at 16/20/24. No emoji.

---

## 9. Assumptions an architect may accept or replace

1. **Impact ranking** is a five-factor sort — severity, capability breadth, target relevance, evidence uniqueness, age — and the UI always prints the reason string, so weights can change without redesign.
2. **Undo is 8 seconds, R0 only.** Nothing that changes eligibility, rights or the audit record is undoable; those get a governed inverse action logged as a separate event.
3. **Paging over infinite scroll:** 50-row pages with a persistent position marker, because a queue position must survive a detail visit and a reload.
4. **Rationale required at R2+,** 240 characters, optional at R1 unless the value contradicts the observation.
5. **Staleness is expressed as its cause** ("stale since taxonomy v4.2 · 82 outputs"), never as an age alone.
6. **Cost is shown per action before commit,** with the current month envelope beside it (design uses a €25 monthly envelope, €3 per 1 000 items as the target).
7. **Three surfaces are desktop-only** (§7), with the reason shown rather than a disabled control.
8. **The mobile companion is three read-only surfaces** and holds no draft state.
9. **The benchmark release is presented as not instantiated** — 11 of 16 seed slots acquired, gold core not adjudicated, holdout not constituted, so every capability reads "not qualified", never "failed". The design refuses to imply a dataset that does not yet exist.

---

## 10. Honest gaps

| Gap | Status |
|---|---|
| Dark mode | Not designed. Token structure is mode-ready; contrast pairs need re-verification for all eight state families. |
| Clickable prototype wiring | Flows A–H are documented as step maps naming screen + state + decision + recovery exit. Every step points at a designed surface. |
| Icon glyphs drawn | Specified by name, licence and size rules; represented by geometric markers in these pages. |
| Real exam content | All German copy is original or safely abstracted. No substantial protected exam material is reproduced; no telc affiliation implied. |
| German UI localisation | Readiness rules documented (expansion budget, no fragment assembly, locale-aware numbers); the translated string set is not produced. |
| Chart implementations | Semantics, series palette and accessible-alternative rules specified; only the small multiples needed to prove the rules are drawn. |

**No genuine blocker remains.** Every item above is either explicitly deferred by the specification or a presentation choice recorded for a later decision.

---

## 11. Coverage

Page 09 carries the full 37-row matrix mapping each specification area to screen(s), component/pattern, responsive coverage, accessibility coverage, prototype flow and status (`Complete` · `Variant` · `Deferred`), plus four QC checklists answered with on-screen evidence rather than assertions.

Totals: **32 specification areas** mapped · **41 surfaces** (22 full 1440×1024 frames, 19 states proven as variants) · **34 components** · **8 flows with 23 named recovery exits** · **74 tokens** in 8 state families · **21 WCAG 2.2 AA criteria** reviewed.
