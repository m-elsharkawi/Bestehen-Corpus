# Bestehen / Corpus — Architecture Shaping Plan

> **Status:** Master workflow plan — architecture stages not yet executed  
> **Product:** Bestehen / Corpus  
> **Target repository:** `m-elsharkawi/Bestehen-Corpus`  
> **Branch:** `main`  
> **Planning source cut:** 2026-08-25  
> **Stage count:** 28  
> **Mode:** single-owner personal project; low-operations, evidence-preserving, cost-bounded

## 1. Purpose and non-implementation boundary

This document defines the complete workflow for shaping the implementation-facing architecture of **Bestehen / Corpus**. It does not itself choose the production framework, database, crawler, OCR/ASR stack, model provider, queue technology, physical schema, hosting topology, or deployment mechanism. Those decisions belong to the numbered architecture stages and must be made with traceability, alternatives, current evidence where facts are mutable, and explicit downstream consequences.

Corpus is an exam-data and intelligence product whose primary downstream customer is Bestehen / App. Its architecture must make broad A2/B1 German exam evidence useful without collapsing provenance, confidence, rights, difficulty/relevance, quality readiness, or analytical independence into one notion of “good data.” It must also remain operable by one owner, safe around untrusted source material, compatible with App without receiving learner data, and economically sane at the product’s intended scale.

This planning run creates the workflow only. Every execution checkbox in `Bestehen_Corpus_Architecture_Checklist.md` begins unchecked. A later architect executes Stage 01, then subsequent stages according to the dependency rules below.

## 2. Run configuration in force

| Variable | Value in force | Planning consequence |
|---|---|---|
| `SOURCE_REPOSITORY` | `m-elsharkawi/Bestehen-Shaping` | Read-only product truth |
| `TARGET_REPOSITORY` | `m-elsharkawi/Bestehen-Corpus` | Architecture outputs, ADRs, checklist, prompts only |
| `APP_REFERENCE_REPOSITORY` | `m-elsharkawi/Bestehen-App` | Read-only integration counterpart |
| `BRANCH` | `main` | Direct sequential workflow unless owner later changes it |
| `ARCHITECTURE_OUTPUT_DIR` | `Architecture/` | One durable Markdown output per stage |
| `ADR_DIR` | `Architecture/adr/` | Lightweight durable decisions only |
| `PROMPT_DIR` | `prompts/architecture/` | One executable prompt per stage |
| `CHECKLIST_PATH` | `Bestehen_Corpus_Architecture_Checklist.md` | Live sequential architecture checklist |
| `STAGE_COUNT_MODE` | `recommended-28` | Retained; no evidence justified a merge/split |
| `DIAGRAM_FORMAT` | Mermaid plus tables | No ASCII-box architecture diagrams |
| `RESEARCH_POLICY` | Current primary official sources for mutable technology/vendor facts | Record links and access date in stage artifacts |
| `PERSONAL_PROJECT_MODE` | `true` | Prefer boring, replaceable, low-maintenance defaults and explicit cash gates |

An ADR index/template is added under `Architecture/adr/README.md` because the prompt pack repeatedly needs a stable decision index. No ADR is created by this planning run because no numbered architecture stage has yet made an architecture decision.

## 3. Preconditions and repository state

### 3.1 Design precondition — satisfied

`Bestehen-Corpus/Design/` contains a complete inspectable handoff, foundations, reusable components, state models, desktop surfaces, workbenches, responsive behavior, prototype flows, accessibility/content/security guidance, and a coverage/handoff page. Architecture planning may therefore proceed.

The design files are specifications of observable state and behavior, not a backend/runtime mandate. `Design/support.js` is generated artifact-rendering support and is explicitly non-authoritative for production architecture.

### 3.2 Existing target inspection

At the planning source cut, the target repository contained `Design/` and `prompts/architecture/00_create_architecture_checklist_and_stage_prompts.txt`. It did **not** yet contain `Architecture/`, architecture ADRs, `Bestehen_Corpus_Architecture_Checklist.md`, or Stage 01–28 architecture prompts. There was therefore no completed Corpus architecture work to preserve or supersede.

No repository-level `AGENTS.md` or `CLAUDE.md` instruction file was found. Later stage agents must still re-check current repository instructions before writing, because the repository can change.

## 4. Source authority and conflict rules

When sources conflict, use this order:

1. `m-elsharkawi/Bestehen-Shaping/corpus/17-bestehen-corpus-product-specification.md` — consolidated Corpus product authority.
2. `corpus/01-*.md` through `corpus/16-*.md` — detailed normative authority where Stage 17 delegates or summarizes; later relevant shaping stages win unresolved earlier wording.
3. `01_Bestehen_Product_Overview.md` — umbrella mission and Corpus/App boundary.
4. `02_Bestehen_Identity.md` — identity, voice, visual and trust posture.
5. `m-elsharkawi/Bestehen-Corpus/Design/DESIGN-HANDOFF.md` and human-authored design artifacts — authoritative design expression where consistent with product truth.
6. Current Bestehen / App product/architecture contract artifacts — integration counterpart, not authority to redefine Corpus semantics.
7. Design artifact runtime/support code — illustrative/rendering support only.

Rules:

- Product truth beats a contradictory design expression; record the mismatch instead of silently redefining product behavior.
- App architecture can constrain the **current counterpart interface** but cannot change Corpus product semantics. A provider-side Corpus decision that would break an accepted App architecture must explicitly identify the incompatibility and the product-contract criterion used to justify it.
- Architecture decisions never overwrite observed evidence. They define how observed, curated, derived, disputed, stale, suppressed, and versioned states are represented and propagated.
- Calibration values remain calibration values. Do not promote provisional product thresholds into immutable architectural constants.

## 5. Source manifest

Repository source cuts used for this planning run:

- `m-elsharkawi/Bestehen-Shaping@f9a468ee63a4c4c778b1a535e13c419bb50cd703`
- `m-elsharkawi/Bestehen-Corpus@28a595132411db0d95837be1f1eb0c0290f259a6` before this planning run wrote architecture files
- `m-elsharkawi/Bestehen-App@cb2e9a7a88fc384d9cad155647e4a6acccf6b5c3`

### 5.1 Shared and Corpus product sources

| Repository / path | Blob SHA | Authority / architectural relevance | Status |
|---|---|---|---|
| `Bestehen-Shaping/01_Bestehen_Product_Overview.md` | `42f15da945e03f1d8e32dfe010f95aae6b87daa3` | Umbrella mission; Corpus evidence vs App exercise bank | Active shared authority |
| `Bestehen-Shaping/02_Bestehen_Identity.md` | `f8799407f7b4a5a657f8c81439425d5a004f4e1c` | Calm, direct, evidence-based identity; internal Corpus role | Active shared authority |
| `Bestehen-Shaping/Bestehen_Corpus_Product_Shaping_Checklist.md` | `d7ff5c2f957e8157f6ef84fc3e027b7c02828981` | Confirms product shaping complete and scope settled | Status reference |
| `Bestehen-Shaping/Bestehen_App_Product_Shaping_Checklist.md` | `f73ad7b50f2ebb9309b16ba5ab98e070a40008bb` | Cross-product status only | Status reference |
| `Bestehen-Shaping/corpus/01-product-mission-and-boundaries.md` | `180900725eefd27ad9b5f50456efdc7dd30b02e9` | Mission, scope, non-goals, App boundary | Active detailed authority |
| `corpus/02-source-strategy.md` | `7b38c9756fa39b63b7389c8c1e0a79dbe89ef6d4` | Source families, discovery, acquisition policy, observations | Active detailed authority |
| `corpus/03-trust-authenticity-confidence.md` | `a771657c20845f118fcada3c1271dc82208604c1` | Authenticity, confidence dimensions/tiers/caps/local evidence | Active detailed authority |
| `corpus/04-rights-and-usage-metadata.md` | `dd24089ea0ce370fbe3306fb39197d9a14f6c86f` | Rights states, action permissions, attribution, takedown | Active detailed authority |
| `corpus/05-canonical-exam-model.md` | `d440b81d93fdb892eb4a9e8794fc43214a5c0d38` | Canonical hierarchy and first-class content/asset/scoring objects | Active detailed authority |
| `corpus/06-exam-and-skill-taxonomy.md` | `40ecccc788e9185e1de9dde5475e39d07e867183` | Versioned multi-axis taxonomy and App mapping | Active detailed authority |
| `corpus/07-difficulty-and-relevance-models.md` | `040f3aad1fa22d82200d61b7506f6ee2983c4712` | Difficulty dimensions; CEFR/Generic-B1/TELC separation | Active detailed authority |
| `corpus/08-ingestion-and-extraction-pipeline.md` | `f705a970b6755758dc8025176be96c9991efe6ee` | Conceptual lifecycle, partial success, review, reprocessing | Active detailed authority |
| `corpus/09-deduplication-strategy.md` | `cecfdefd03ed441aafc55404101d5c0ecda611bd` | Identity, derivative lineage, metric-specific independence | Active detailed authority |
| `corpus/10-validation-and-quality-assurance.md` | `7dc03aa6420cae0083698a327647bb24bc2932e7` | Q0–Q3 findings, use-specific gates, no scalar ready flag | Active detailed authority |
| `corpus/11-corpus-analytics.md` | `cbae6083c3ad356c5d1e46b59e871375d67eb90a` | Evidence-aware denominators, decision-grade envelopes | Active detailed authority |
| `corpus/12-corpus-app-contract.md` | `7add217f62118e5abe100680d2e8230a93b8c280` | Pattern-first Corpus→App product contract | Active detailed authority |
| `corpus/13-operations-and-review-experience.md` | `67e271422075242dda311c8318252c3ef557063c` | Owner-only Inbox/review/source-control/health requirements | Active detailed authority |
| `corpus/14-cost-scale-and-automation.md` | `63fd7e8b8d5239ca1883000c98d058000d5a91a2` | Low/base/high scale, cheap-first ladder, human-review cost | Active detailed authority |
| `corpus/15-security-privacy-and-abuse-boundaries.md` | `fee944281e46ecb48febd89dec269d5f302c2431` | Untrusted input, preflight, prompt injection, near-zero personal data | Active detailed authority |
| `corpus/16-initial-corpus-benchmark.md` | `b596fe8349ee394fd92ce3ea1ef16ea0ff676770` | 16-slot seed, 12–14 package gold core, qualification gates | Active detailed authority; benchmark not yet instantiated |
| `corpus/17-bestehen-corpus-product-specification.md` | `537b5185313097d043748f9dc9f9fdaf432ee71d` | Consolidated Corpus product specification | **Primary authority** |

### 5.2 Prompt-workflow references

| Path | Blob SHA | Why inspected |
|---|---|---|
| `Bestehen-Shaping/prompts/corpus/01_lock_the_product_mission_and_boundaries.txt` | `1d79bea5c0ab35e4ec6526e1c248a422dd0d54a1` | Standalone context, mandatory reads, live checklist workflow |
| `prompts/corpus/08_define_the_ingestion_and_extraction_pipeline.txt` | `2ede47e37b53ea3f6457aba8f5eaaf5a08fcc3c3` | Failure/review/reprocess/cost conventions |
| `prompts/corpus/12_define_the_contract_with_bestehen_app.txt` | `ec49e323c9401a812228973c83232ab99b77c675` | Cross-product contract handoff convention |
| `prompts/corpus/13_define_corpus_operations_and_review_experience.txt` | `29f3d0e0671bf3553e2e126efe27949c9be7dfb9` | Owner-operations scope convention |
| `prompts/corpus/14_decide_cost_scale_and_automation_principles.txt` | `db9e507283846faede7639646b28e463cdedc9ea` | Current-pricing and cheap-first convention |
| `prompts/corpus/16_establish_the_initial_corpus_benchmark.txt` | `4b4f8fea4e0bedb4f8c5352ef802cb6078f4618e` | Benchmark handoff/qualification convention |
| `prompts/corpus/17_produce_the_final_product_specification.txt` | `d3a0d29f2d961cbafa449988702eaa6bf5373868` | Final reconciliation and DoD convention |
| `Bestehen-App/prompts/architecture/00_create_architecture_checklist_and_stage_prompts.txt` | `d1159d4f0293de800327f9ee6e4f5a8ce8053c2f` | Proven 28-stage architecture-workflow convention |
| `Bestehen-App/prompts/architecture/10_define_corpus_integration_compatibility_cache_and_rights.txt` | current on App source cut | Representative executable architecture stage prompt |
| `Bestehen-Corpus/prompts/architecture/00_create_architecture_checklist_and_stage_prompts.txt` | `86bd172797b4bf90b83cdec2637ba1a2f5dfcc17` | Master instruction for this planning run | Retained unchanged |

### 5.3 Corpus design sources

| Path | Blob SHA | Architectural contract read from it |
|---|---|---|
| `Design/DESIGN-HANDOFF.md` | `fc573707efcf0c632384dfc1fd45ab6595b11369` | Canonical design handoff; states, invariants, responsiveness, security, open assumptions |
| `Design/Corpus-00-Cover-Principles.dc.html` | `607677ae02534c27ce5c42c965e31d10591f4c04` | Design run config, six axes, principles, IA |
| `Design/Corpus-01-Foundations.dc.html` | `a7378bc93af80362e497b4b3afe54d11a45927f7` | Tokens, typography, state-family separation, German/source text rules |
| `Design/Corpus-02-Components.dc.html` | `921e885434bbd715f334e1745eb0fdc92cf86a87` | 34 reusable components, queue/detail/action contracts |
| `Design/Corpus-03-State-Models.dc.html` | `7a3459d4b175e08ab381e0b9cc7d0fddf34fabca` | Inspectable scopes, state vocabularies, six capability gates, governance |
| `Design/Corpus-04-Desktop-Screens.dc.html` | `ef69c8585b04f61ec1b35ff0b47d97f9611037d3` | Owner access, Inbox, intake, runs, records, health, benchmark, impact, audit surfaces |
| `Design/Corpus-05-Workbenches.dc.html` | `2a1d53c611e187b1f1033056d7171cf7711ade97` | Authenticity, rights/takedown, duplicate, taxonomy, reprocess workbenches and confirmation tiers |
| `Design/Corpus-06-Responsive.dc.html` | `882e5ece14ba2070073a4851266adda8a54c7adc` | Desktop-first breakpoints; <900 read-only; consequential mobile restrictions |
| `Design/Corpus-07-Flows.dc.html` | `badd43f944e2dc5d7cabdb6f8d61688937a6425d` | Flows A–H, partial success, safe-leave background work, recovery branches |
| `Design/Corpus-08-Accessibility-Content-Security.dc.html` | `1928b3c5dbab2aed7884949db6ff9e9acf04749e` | WCAG 2.2 AA, focus/keyboard/announcements, non-color states, inert preview/content rules |
| `Design/Corpus-09-Coverage-Handoff.dc.html` | `29d57384aaa45c199baa400c09688d96eb4c9ff3` | 32-area coverage matrix, launch/deferred boundary, load-bearing decisions, assumptions/gaps |
| `Design/support.js` | `cb009b69ec6b5e00f48c6287a587fe7e0c6c421b` | Generated dc-runtime support only | Non-authoritative runtime support |

### 5.4 App boundary sources

| Path | Blob SHA | Current counterpart contract |
|---|---|---|
| `Bestehen-Shaping/app/28-bestehen-app-product-specification.md` | `18ae80cc2fd63cecd76c297c3e56d44a68367856` | App owns learner state/coaching/Readiness/original practice; Corpus supplies rights-safe intelligence |
| `Bestehen-App/Architecture/10-corpus-integration-compatibility-cache-and-rights.md` | `d4e1ab25e359dcfcc506ee29462760a41647138d` | Current App architecture chooses asynchronous bundle-first import, immutable compatible snapshots, no learner-profile/runtime Corpus dependency |
| `Bestehen-App/Architecture/12-api-contracts-jobs-events-and-idempotency.md` | `c640da01d6eb6d71a5e2ea7a0dcf19147d6d7528` | App-side import/job/idempotency conventions; not a mandate for Corpus internals |
| `Bestehen-App/Architecture/28-bestehen-app-architecture-specification.md` | `89a761d64767e048b59338ec13e61b1b06472dbd` | Consolidated current App architecture and integration assumptions |

No independent duplicate authority was found among these human-authored inputs. The final Corpus specification explicitly reports no Stage 01–16 reversal; detailed stage documents remain normative for depth.

## 6. Product and design invariants architecture cannot reopen

### 6.1 Product boundary

- Corpus is exam-data/intelligence, not a learner course, public mirror, generic scraper, learner-attempt store, or certification authority.
- Launch acquisition covers German A2, B1 and mixed A2–B1; A1 scaffolding belongs to App.
- TELC B1 is the strongest target signal but not the only source family.
- App is the primary downstream customer; one owner is the initial operator.
- Launch excludes public submission/API/research UI, multi-tenancy, billing, collaboration, authenticated paid/private crawling, and enterprise controls.

### 6.2 Six independent truth axes

Architecture must keep separate:

1. source/provenance;
2. authenticity/evidence confidence;
3. rights/usage;
4. difficulty plus Generic-B1/TELC relevance;
5. extraction/QA readiness per capability;
6. content identity, derivative lineage and metric-specific analytical independence.

No persistence model, aggregate, index, DTO, cache, view, or publication switch may erase these distinctions.

### 6.3 Uncertainty, locality, and capability publication

`unknown`, `not_applicable`, `disputed`, `review_required`, `unresolved_dependency`, `incomplete`, `provisional`, and `not_run` are meaningful states. Missing is not false or zero. High-risk use is controlled at the smallest relevant scope. Parent trust cannot rescue a defective child, and one local defect does not invalidate unrelated sibling capabilities.

There is no universal `production_ready=true`. At minimum the architecture must be able to answer separately for structure analytics, correctness/scoring, taxonomy publication, pattern intelligence, exact source reuse, and independent prevalence.

### 6.4 Provenance, correction, governance, audit

Observed source expression stays distinct from curated interpretation/correction and derived intelligence. Stable identity and mutable revisions survive reprocessing. Curated overrides survive reruns until explicitly superseded. Consequential changes are auditable with actor/time/scope/old-new state/rationale/evidence and method/model/rule/taxonomy/dedup/analytics/contract versions.

Security and takedown controls outrank ordinary acquisition/reprocessing. Weak controls cannot clear stronger holds. Audit is append-only; supersede rather than rewrite history.

### 6.5 Identity, deduplication, and analytics

Preserve all observations while separating content identity, derivative lineage, canonical provenance anchor, preferred processing representation, and metric-specific independence. Mirrors and derivatives cannot create prevalence, corroboration, or diversity. Decision-grade analytics carry denominator, independent evidence, confidence/uncertainty, source/provider mix, versions, freshness, and applicability.

### 6.6 Corpus → App

App requests desired exam/learning patterns, not learner profiles. Corpus returns eligible structured intelligence, generation/constraint blueprints, governance envelopes, versions, and change impact. Original practice generation/evaluation and Readiness remain App responsibilities. Corpus stores no learner data. Ordinary App sessions do not trigger live Corpus inference.

### 6.7 Pipeline, security, benchmark, and cost

Preserve the conceptual lifecycle **Discover → Fetch → Normalize → Parse → Segment → Classify → Extract Answers → Extract Assets → Enrich → Validate → Deduplicate → Review → Publish** while permitting a different physical implementation. Work must be idempotent/replayable, partially successful at smallest meaningful scope, versioned, bounded in retry, and reprocessable from the earliest affected stage without destroying valid unaffected outputs.

Every external input is untrusted. Security preflight precedes deep/expensive processing. Source text cannot command tools, policy, publishing, or secrets.

No automated production capability can claim qualification without the instantiated benchmark/gold core and its applicable gates. `corpus-benchmark-1.0.0` is a bootstrap obligation, not an existing completed artifact.

Design center is roughly 20k–50k canonical Items. Target variable processing is approximately `€3 / 1,000 Items` or less under the measurement policy and normal Corpus cash envelope is approximately `€25/month`, subject to measured recalibration. Human review time counts as cost. Prefer deterministic/local/open-source work, content-addressed reuse, batching, caching, deferred enrichment, bounded crawling, and risk-triggered escalation.

## 7. Design-to-architecture traceability

Every stage artifact must include a **Source Traceability** section mapping architecture decisions to product/design anchors. Stage 20 additionally owns a design coverage matrix from the 41 designed surfaces and 34 component patterns to architectural routes/modules/queries/commands/background jobs without creating one backend endpoint per screen.

Architecture must support these design contracts in particular:

- one prioritized owner Inbox plus specialized saved views;
- one reusable Record Detail framework across ten inspectable scopes;
- observed vs curated vs derived values and explicit diffs;
- exact uncertainty vocabulary and six capability-gate answers;
- R0–R3 governed-action confirmation behavior;
- drafts that survive navigation/reload/network/session expiry;
- background work that is safe to leave and reports a named result state;
- partial success, conflict, failure, refusal and draft-preserved outcomes;
- inert/sanitized source previews, never active content;
- health as blocker list + vector, never one score;
- desktop-first consequential review and <900px read-only companion;
- WCAG 2.2 AA, keyboard/focus restoration, non-color redundancy, accessible chart alternatives.

Design presentation assumptions—cool surface palette, light-only launch, exact rail widths, specific component composition, typography implementation, polling vs realtime, and the illustrative `owner@bestehen.internal` identity—do not silently become backend/runtime requirements. Stage 20 may accept or replace implementation assumptions while preserving the behavioral/accessibility contract.

## 8. Corpus → App reconciliation approach

The product contract is technology-neutral and pattern-first. Current App architecture has already chosen a **bundle-first asynchronous pull** model for launch: signed immutable capability-scoped bundles plus a small publication index, imported into a last-known-compatible App snapshot; the App does not perform live Corpus search or send learner/session state to Corpus.

This is not a Corpus product-semantic mismatch. It is a current counterpart architecture commitment that Stage 19 must explicitly reconcile provider-side. Stage 19 must:

1. read App Architecture Stages 10, 12 and 28 at current `main`;
2. verify the six capability families, governance envelope, stable IDs/revisions, contract/taxonomy versions, rights/takedown propagation and material-change semantics against Corpus product Stage 12/17;
3. compare provider-side publication mechanisms and recommend the simplest one compatible with App’s accepted bundle-first import unless current evidence justifies a coordinated contract change;
4. treat App signing/hash choices as counterpart expectations to validate, not as permission to skip current official security research;
5. define Corpus downtime, stale-bundle, revocation/removal, incompatibility and no-decision-grade-pattern behavior;
6. never introduce learner-data ingress merely to simplify personalization.

App Stage 12’s internal JSON/HTTP and job choices do not mandate Corpus internals. Corpus only needs a versioned provider-side contract compatible with the import boundary.

## 9. Architecture concern ownership

| Concern | Primary stage | Named consumers |
|---|---:|---|
| Charter, principles, measurable quality attributes | 01 | all stages |
| System context, trust zones, boundaries | 02 | 03–28 |
| Stack/repository/deployment candidates | 03 | 05, 11–15, 19–26 |
| Domain language/bounded contexts | 04 | 05–28 |
| Data ownership/storage/schema evolution | 05 | 06–28 |
| Source registry/discovery/acquisition | 06 | 07–13, 17, 20, 23–27 |
| Provenance/authenticity/confidence | 07 | 08–10, 15–21, 25–28 |
| Rights/takedown/removal | 08 | 09–12, 15–28 |
| Canonical content/answers/assets | 09 | 10–28 |
| Taxonomy/difficulty/relevance/versioning | 10 | 11, 15–22, 25–28 |
| Orchestration/state/idempotency/reprocessing | 11 | 12–28 |
| Secure intake | 12 | 13–17, 21–27 |
| Document/OCR/layout extraction | 13 | 15–18, 21–28 |
| Audio/video/ASR | 14 | 15–18, 21–28 |
| Semantic enrichment/answer mapping | 15 | 16–18, 21–28 |
| Duplicate/derivative/independence | 16 | 17–21, 25–28 |
| QA/findings/capability publication | 17 | 18–28 |
| Analytics/exam intelligence | 18 | 19–22, 24–28 |
| App contract/bundles/change propagation | 19 | 20, 23–28; Bestehen / App |
| Operations console/review/audit/source controls | 20 | 23–28 |
| Benchmark/gold/reproducibility/qualification | 21 | 22, 25–28 |
| AI/model governance/cost controls | 22 | 23–28 |
| Security/privacy/access/secrets/retention/threat model | 23 | 24–28 |
| Observability/performance/reliability/backup/cost ops | 24 | 25–28 |
| Testing/evaluation/release gates | 25 | 26–28 |
| Environments/CI/CD/release/operations | 26 | 27–28 |
| End-to-end validation | 27 | 28 |
| Consolidated architecture + implementation roadmap | 28 | implementation |

## 10. Stage sequence, dependencies, parallel-safe work, and critical path

### 10.1 Dependency rules

A stage must not depend on a later undecided architecture choice. When a later stage owns a refinement, the earlier stage must state a bounded temporary assumption and name the reconciliation point. In particular:

- Stage 20 may rely on the product requirement “single-owner authenticated internal console,” but Stage 23 owns the final authentication/secret/threat architecture.
- Stage 19 owns contract-integrity requirements and provider-side compatibility; Stage 23 later validates key custody and system-wide threat controls without changing contract semantics silently.
- Stage 21 defines benchmark release/reproducibility semantics before Stage 26 decides CI/environment implementation.
- Stage 03 chooses stack/repository direction and deployment candidates; Stage 26 owns environment/release operationalization.

### 10.2 Parallel-safe points

The default execution is sequential because each stage consumes prior decisions. Limited parallelism is safe only after prerequisite outputs are committed:

- **Stages 03 and 04** may be researched in parallel after Stages 01–02, but Stage 05 must reconcile both before persistence decisions.
- **Stages 13 and 14** may execute in parallel after Stages 09, 11 and 12 because document/image extraction and media processing have separate primary ownership; Stage 15 reconciles both.
- **Stages 18 and 21** may execute in parallel after Stage 17 because analytics design and benchmark instantiation/release architecture have different ownership; Stage 22 must consume both before model qualification/cost routing.

Do not parallelize checklist writes to the same path. Each stage’s final checklist reconciliation remains sequential.

### 10.3 Critical path

`01 → 02 → (03 + 04) → 05 → 06 → 07 → 08 → 09 → 10 → 11 → 12 → (13 + 14) → 15 → 16 → 17 → (18 + 21) → 19 → 20 → 22 → 23 → 24 → 25 → 26 → 27 → 28`

Stage 19 depends on Stage 18 because the provider contract exposes exam intelligence and change semantics. Stage 22 depends on Stage 21 because model/provider promotion must be benchmark-gated rather than chosen from vendor claims alone.

## 11. Naming and artifact conventions

- Stage outputs: `Architecture/XX-kebab-case-title.md`.
- ADRs: `Architecture/adr/ADR-NNNN-short-title.md`.
- Stage prompts: `prompts/architecture/XX_snake_case_action.txt`.
- IDs, enum examples, contract snippets, SQL-like queries and pseudocode are illustrative unless the stage explicitly records them as a decision.
- Every architecture output records input source paths and current SHAs/versions where practical.
- Mermaid is used for context/container/component, state, sequence, lineage, trust-boundary and deployment diagrams. Tables are used for alternatives, ownership, version maps, state transitions, failure matrices, cost and security controls.

## 12. ADR strategy

Use an ADR only for durable choices with cross-stage consequences, such as the primary persistence strategy, content-addressing approach, orchestration model, execution-isolation boundary, deployment topology, Corpus→App publication contract style, operations UI strategy, model-provider abstraction, or benchmark release method.

Do not create an ADR for every checklist item. A stage output is the normal place for local decisions. When a durable choice changes, create a new ADR that supersedes the old one; never delete history.

The index/template is `Architecture/adr/README.md`.

## 13. Research rules

### 13.1 Mutable technology/vendor facts

When a decision depends on current pricing, framework/runtime support, hosting limits, security guidance, file/media support, licensing, OCR/ASR/model capability, browser behavior or managed-service limits:

- research current **primary official sources**;
- record source URL/title and access date in the stage artifact;
- distinguish documented facts from benchmark hypotheses;
- do not use a blog/comparison article as sole evidence for a durable platform choice;
- preserve uncertainty where Corpus’s benchmark must decide whether a tool is good enough.

Stable product rules already in GitHub do not need web re-research.

### 13.2 Benchmark evidence

Architecture may propose candidates and qualification harnesses before the benchmark is instantiated, but it must not claim a parser/model/threshold/vendor is production-qualified until the relevant `corpus-benchmark-1.0.0` slice exists and passes the applicable gate.

## 14. Cost-control rules for every relevant stage

Each cost-sensitive stage must separate:

- recurring cash cost;
- variable processing cost;
- storage/egress cost;
- human-review time;
- failed/retried/reprocessed work;
- maintenance/operator burden.

Use low/base/high workload assumptions tied to product Stage 14. Report cost per productive/qualified Item or capability output where meaningful. Always name a free/cheap default and the measured trigger that justifies upgrading.

Preferred escalation ladder:

1. reject/defer clearly low-value or unsafe work;
2. deterministic metadata/parser/hash/rule work;
3. local/open-source processing where operationally sane;
4. cached/batched inexpensive managed capability;
5. selective stronger model/service;
6. human review for high-impact ambiguity or gold truth.

The architecture must make budget exhaustion a normal state: defer expensive enrichment, preserve provisional results, and avoid retry storms or hidden paid loops.

## 15. Security/privacy/rights rules for the workflow

Security appears in intake design before parsing and again end-to-end in Stage 23. Every relevant stage must address:

- untrusted URLs/files/archives/media and source text;
- SSRF/redirect/DNS/egress bounds;
- type/size/magic/archive controls and non-execution of active content;
- prompt-injection/tool isolation and structured output validation;
- quarantine and inert preview boundaries;
- least privilege and source-data/secret separation;
- rights/attribution/takedown propagation;
- minimal incidental personal data, retention/deletion and deletion proof;
- auditability for high-impact human/automated actions;
- supply-chain/model/dependency artifact risk;
- future triggers before public submissions, multi-operator, commercial reuse, or paid/private crawling.

Do not claim legal compliance or complete malware safety. Architecture records technical controls, residual risk and escalation conditions.

## 16. Checklist mechanics and definition of done

For each stage agent:

1. fetch `Bestehen_Corpus_Architecture_Checklist.md` and read the **complete** stage section before deciding;
2. fetch the exact product/design/prior-architecture sources named in the prompt;
3. make decisions in the primary stage output and any justified ADRs;
4. update `[ ]` to `[x]` only when the corresponding decision is captured;
5. leave implementation-only items unchecked with `Deferred — architecture/implementation decision:` and a reason;
6. leave genuine owner blockers unchecked with `Blocked — owner decision required:` plus the precise question and recommended default;
7. write checklist updates sequentially using current file/blob SHA;
8. re-fetch the checklist after the stage output commit and reconcile every item;
9. do not alter unrelated stage sections except a documented cross-stage correction;
10. report output, ADRs, assumptions/calibration needs, unresolved risks, cost fallback, downstream dependencies, contradictions and commits.

A stage is done only when its exact output exists on GitHub, every checked item has evidence in that output/linked ADR, prerequisites are honored, no product/design invariant is silently reopened, and the final checklist re-read matches the committed artifact.

## 17. Planning risk register

| Risk | Why it matters | Workflow control | Primary owner |
|---|---|---|---:|
| Six axes collapse into convenience status | Corrupts truth and rights | Charter + domain/data/QA/contract checks | 01,04,05,17,19 |
| Physical pipeline chosen before evidence model | Produces brittle schemas/workflows | Domain/data stages precede orchestration | 04,05,11 |
| Rights treated as trust or vice versa | Unsafe reuse/false certainty | Separate stages and explicit cross-checks | 07,08,17,19 |
| Mirrors inflate prevalence/corroboration | Bad exam intelligence | Metric-specific independence stage before analytics | 16,18 |
| Curator corrections erased by rerun | Destroys auditability | Orchestration/reprocessing contract + tests | 11,20,25 |
| Unsafe source reaches parser/model/tool | Security incident/prompt injection | Security preflight stage precedes extraction | 12,23,25 |
| Expensive model becomes default path | Violates personal-project budget | Benchmark-gated AI gateway + cost ledger/circuit breakers | 21,22,24 |
| Benchmark treated as already complete | False qualification claims | Stage 21 explicitly instantiates/releases it | 21,25,28 |
| App and Corpus drift | Breaks downstream coaching/content | Dedicated provider-contract reconciliation | 19,27 |
| App counterpart architecture mistaken for Corpus internals | Over-constrains provider | Stage 19 separates interface compatibility from internals | 19 |
| Ops UI creates per-screen backend forks | High maintenance burden | Domain commands/queries + reusable record/view architecture | 20 |
| Mobile enables unsafe consequential decisions | Violates design safety | Preserve <900 read-only boundary until explicitly redesigned | 20,25 |
| “Health score” hides blockers | Q0/rights/security failures disappear | Health remains vector + hard blocker list | 20,24 |
| Retention/deletion erases legitimate audit/provenance or retains prohibited content | Legal/security/data-integrity risk | Rights + persistence + threat model + deletion proof | 05,08,23 |
| Architecture assumes hypothetical internet scale | Overbuilds personal project | Scale envelope and upgrade triggers in charter/stack/ops | 01,03,24,26 |
| Stage dependency cycle | Later agents must invent assumptions | Explicit prerequisite graph and reconciliation points | 00,27 |

## 18. Stage and prompt index

| Stage | Title | Prerequisite architecture stages | Output | Prompt |
|---:|---|---|---|---|
| 01 | Architecture Charter and Quality Attributes | none | `Architecture/01-architecture-charter-and-quality-attributes.md` | `prompts/architecture/01_define_architecture_charter_and_quality_attributes.txt` |
| 02 | System Context and Product Boundaries | 01 | `Architecture/02-system-context-and-product-boundaries.md` | `prompts/architecture/02_define_system_context_and_product_boundaries.txt` |
| 03 | Technology Stack and Repository Strategy | 01,02 | `Architecture/03-technology-stack-and-repository-strategy.md` | `prompts/architecture/03_decide_technology_stack_and_repository_strategy.txt` |
| 04 | Domain Model and Bounded Contexts | 01,02 | `Architecture/04-domain-model-and-bounded-contexts.md` | `prompts/architecture/04_define_domain_model_and_bounded_contexts.txt` |
| 05 | Data Ownership, Persistence, Storage, and Schema Evolution | 03,04 | `Architecture/05-data-ownership-persistence-storage-and-schema-evolution.md` | `prompts/architecture/05_define_data_ownership_persistence_storage_and_schema_evolution.txt` |
| 06 | Source Registry, Discovery, and Acquisition Architecture | 02,04,05 | `Architecture/06-source-registry-discovery-and-acquisition-architecture.md` | `prompts/architecture/06_define_source_registry_discovery_and_acquisition_architecture.txt` |
| 07 | Provenance, Authenticity, and Confidence Architecture | 04,05,06 | `Architecture/07-provenance-authenticity-and-confidence-architecture.md` | `prompts/architecture/07_define_provenance_authenticity_and_confidence_architecture.txt` |
| 08 | Rights, Usage, Attribution, Takedown, and Removal Architecture | 04,05,06,07 | `Architecture/08-rights-usage-attribution-takedown-and-removal-architecture.md` | `prompts/architecture/08_define_rights_usage_attribution_takedown_and_removal_architecture.txt` |
| 09 | Canonical Exam, Content, Answer, and Asset Model | 04,05,06,07,08 | `Architecture/09-canonical-exam-content-answer-and-asset-model.md` | `prompts/architecture/09_define_canonical_exam_content_answer_and_asset_model.txt` |
| 10 | Taxonomy, Difficulty, Relevance, and Versioning Architecture | 04,05,07,09 | `Architecture/10-taxonomy-difficulty-relevance-and-versioning-architecture.md` | `prompts/architecture/10_define_taxonomy_difficulty_relevance_and_versioning_architecture.txt` |
| 11 | Pipeline Orchestration, State Machines, Idempotency, and Reprocessing | 03–10 | `Architecture/11-pipeline-orchestration-state-idempotency-and-reprocessing.md` | `prompts/architecture/11_define_pipeline_orchestration_state_machines_idempotency_and_reprocessing.txt` |
| 12 | Secure Fetch, File, Archive, and Content Intake | 02,03,05,06,08,11 | `Architecture/12-secure-fetch-file-archive-and-content-intake.md` | `prompts/architecture/12_define_secure_fetch_file_archive_and_content_intake.txt` |
| 13 | Document, Image, OCR, Layout, and Structure Extraction | 05,09,11,12 | `Architecture/13-document-image-ocr-layout-and-structure-extraction.md` | `prompts/architecture/13_define_document_image_ocr_layout_and_structure_extraction.txt` |
| 14 | Audio, Video, ASR, and Media Processing | 05,09,11,12 | `Architecture/14-audio-video-asr-and-media-processing.md` | `prompts/architecture/14_define_audio_video_asr_and_media_processing.txt` |
| 15 | Semantic Enrichment, Classification, and Answer Mapping | 07–14 as relevant; hard prereqs 09,10,11,13,14 | `Architecture/15-semantic-enrichment-classification-and-answer-mapping.md` | `prompts/architecture/15_define_semantic_enrichment_classification_and_answer_mapping.txt` |
| 16 | Duplicate, Derivative, Identity, and Analytical Independence | 07,09,10,11,13,14,15 | `Architecture/16-duplicate-derivative-identity-and-analytical-independence.md` | `prompts/architecture/16_define_duplicate_derivative_identity_and_analytical_independence.txt` |
| 17 | Validation, QA, Findings, and Capability-Scoped Publication | 07–16 | `Architecture/17-validation-qa-findings-and-capability-scoped-publication.md` | `prompts/architecture/17_define_validation_qa_findings_and_capability_scoped_publication.txt` |
| 18 | Analytics and Exam-Intelligence Architecture | 07,08,09,10,16,17 | `Architecture/18-analytics-and-exam-intelligence-architecture.md` | `prompts/architecture/18_define_analytics_and_exam_intelligence_architecture.txt` |
| 19 | Corpus → App Contract, API, Bundles, Compatibility, and Change Propagation | 05,08,09,10,17,18 | `Architecture/19-corpus-app-contract-api-bundles-and-change-propagation.md` | `prompts/architecture/19_define_corpus_app_contract_api_bundles_compatibility_and_change_propagation.txt` |
| 20 | Operations Console, Review Workflows, Audit, and Source Controls | 03–19 as relevant; hard prereqs 05,11,16,17,18,19 | `Architecture/20-operations-console-review-audit-and-source-controls.md` | `prompts/architecture/20_define_operations_console_review_workflows_audit_and_source_controls.txt` |
| 21 | Benchmark, Gold Data, Reproducibility, and Capability Qualification | 08,09,10,12–18 | `Architecture/21-benchmark-gold-data-reproducibility-and-capability-qualification.md` | `prompts/architecture/21_define_benchmark_gold_data_reproducibility_and_capability_qualification.txt` |
| 22 | AI and Automation Gateway, Model Governance, and Cost Controls | 03,11,13,14,15,17,18,21 | `Architecture/22-ai-automation-gateway-model-governance-and-cost-controls.md` | `prompts/architecture/22_define_ai_automation_gateway_model_governance_and_cost_controls.txt` |
| 23 | Security, Privacy, Access, Secrets, Retention, and Threat Model | 02,03,05,06,08,11,12,19,20,22 | `Architecture/23-security-privacy-access-secrets-retention-and-threat-model.md` | `prompts/architecture/23_define_security_privacy_access_secrets_retention_and_threat_model.txt` |
| 24 | Observability, Performance, Reliability, Backup, and Cost Operations | 03,05,11–14,18–20,22,23 | `Architecture/24-observability-performance-reliability-backup-and-cost-operations.md` | `prompts/architecture/24_define_observability_performance_reliability_backup_and_cost_operations.txt` |
| 25 | Testing, Evaluation, and Quality Gates | 01–24; hard prereqs 17,19,21–24 | `Architecture/25-testing-evaluation-and-quality-gates.md` | `prompts/architecture/25_define_testing_evaluation_and_quality_gates.txt` |
| 26 | Environments, CI/CD, Release, and Operations | 03,05,11,17,19,21–25 | `Architecture/26-environments-ci-cd-release-and-operations.md` | `prompts/architecture/26_define_environments_ci_cd_release_and_operations.txt` |
| 27 | End-to-End Architecture Validation | 01–26 | `Architecture/27-end-to-end-architecture-validation.md` | `prompts/architecture/27_validate_end_to_end_architecture.txt` |
| 28 | Final Architecture Specification and Implementation Roadmap | 01–27 | `Architecture/28-bestehen-corpus-architecture-specification.md` | `prompts/architecture/28_produce_final_bestehen_corpus_architecture_specification.txt` |

## 19. Architecture completeness questions

Stage 27 must prove the architecture can answer, with an owning artifact and executable state/flow, all of the following:

- an official source can remain reference-only without losing authenticity evidence;
- a disputed answer can block correctness while language/topic structure remains usable;
- twenty mirrors remain preserved yet count as one occurrence where the metric requires independence;
- a re-recorded listening script can be dependent for lexical evidence yet independent for acoustic evidence;
- stable IDs/revisions survive reprocessing, taxonomy migration, analytics recomputation and App publication;
- curated overrides survive reruns and conflicts become reviewable rather than silently overwritten;
- scoped reprocessing starts at the earliest affected stage and leaves unaffected outputs untouched;
- rights-only removal propagates differently from trust/correctness invalidation;
- takedown fingerprints prevent mirror re-ingestion where required;
- PDFs/DOCX/ZIP/HTML/media reach parsers/models without active execution or uncontrolled network behavior;
- source prompt injection cannot invoke tools/change policy/publish/access secrets;
- capability-scoped publication survives bundle/cache/import boundaries;
- App continues safely when Corpus is unavailable or no decision-grade pattern exists;
- shared taxonomy changes do not send learner data to Corpus or clone learner mastery after node splits;
- `corpus-benchmark-1.0.0` is instantiated, immutable/versioned and used for candidate promotion;
- a failed benchmark slice blocks only the relevant capability/scope;
- OCR/ASR/model costs stop/defer cleanly when the budget is exhausted;
- the owner can operate safely without raw database-row edits;
- design tables, comparison workbenches, governed actions and keyboard paths do not create per-view backend forks;
- the final data lifecycle distinguishes backed-up truth, reproducible derivation, intentional ephemera, suppression, retention and physical deletion.

If any question has no primary owner by Stage 27, the architecture is incomplete and Stage 27 must amend the appropriate earlier artifact before Stage 28 consolidates it.

## 20. Source reconciliation result

No product-level contradiction requiring an owner decision was found in the current Corpus shaping record. Stage 17 remains consistent with Stages 01–16 and explicitly preserves their detailed rules.

No design/product contradiction was found that blocks architecture planning. The design’s 12 load-bearing decisions are compatible with product truth. Design-specific presentation assumptions remain architecture/implementation choices where the handoff says they may be accepted or replaced.

No Corpus/App **product-semantic** mismatch was found. The important current architecture-side integration commitment is that Bestehen / App already expects a bundle-first asynchronous, compatible-snapshot import path rather than live Corpus runtime dependency. Stage 19 must reconcile Corpus’s provider side to that accepted App architecture or document a coordinated incompatibility; it must not rediscover the boundary from scratch.

The benchmark remains intentionally uninstantiated. That is a planned Stage 21 bootstrap obligation, not a blocker for architecture workflow planning.

## 21. Master-planning definition of done

This workflow plan is internally complete when:

- the design precondition is satisfied;
- every Corpus shaping stage and required design/App counterpart source has a place in the source manifest;
- each architecture concern has one primary stage owner and named consumers;
- prerequisites point only backward or to explicit external sources;
- the checklist has exactly 28 numbered stage sections with execution items initially unchecked;
- `prompts/architecture/` has exactly one Stage 01–28 executable prompt in addition to the retained Stage 00 master prompt;
- prompt stage number/title/output/prerequisites match this index and the checklist one-to-one;
- every stage prompt contains the mandatory live-checklist workflow, source reads, non-implementation boundary, current-research rule where relevant, failure/uncertainty handling, cost/security/rights implications, and handoff requirements;
- no planning artifact modifies Shaping, App, or Corpus Design files;
- Stage 28’s destination is exactly `Architecture/28-bestehen-corpus-architecture-specification.md`.

There is no deviation from the recommended 28-stage baseline.
