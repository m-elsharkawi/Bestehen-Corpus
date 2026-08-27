# Bestehen / Corpus — Architecture Shaping Checklist

> **Purpose:** Execute the 28 architecture-shaping stages in dependency order and leave an implementation-facing architecture that preserves Corpus product truth, design intent, App compatibility, security, rights, benchmark qualification, recoverability, and personal-project cost limits.  
> **Workflow plan:** `Architecture/00-architecture-shaping-plan.md`  
> **Status:** All architecture execution items are intentionally unchecked at master-planning completion.

## Checklist operating rules

- Check `[x]` only after the decision is captured in the stage output or an explicitly referenced ADR/artifact.
- Before changing this file, fetch the current GitHub version and use its current blob SHA. Do not perform parallel writes to this path.
- Leave implementation-only work unchecked with `Deferred — architecture/implementation decision:` and a reason.
- Leave genuine owner blockers unchecked with `Blocked — owner decision required:` plus the precise question and recommended default.
- Every stage must preserve the six independent truth axes: provenance; authenticity/confidence; rights/usage; difficulty/Generic-B1/TELC relevance; extraction/QA capability readiness; identity/derivative lineage/metric-specific independence.
- Every stage must preserve explicit uncertainty/locality and capability-scoped publication. Missing is not false/zero; no universal `production_ready` flag is permitted.
- Corpus remains learner-data-free. Original practice generation/evaluation and Readiness remain Bestehen / App responsibilities.
- Every stage must name cheaper fallback, bounded failure/recovery behavior, security/rights implications, observability/testability consequences, and downstream consumers where relevant.
- Stage outputs are architecture decisions, not production implementation.

---

## 01. Architecture Charter and Quality Attributes

**Objective:** Remove ambiguity about architecture principles, measurable quality priorities, personal-project limits, forbidden shortcuts, and how later decisions are judged.

**Prerequisites:** none.  
**Output:** `Architecture/01-architecture-charter-and-quality-attributes.md`  
**Downstream:** every later stage.

**Committed evidence:** [Stage 01 charter](Architecture/01-architecture-charter-and-quality-attributes.md) and [ADR-0001](Architecture/adr/ADR-0001-offline-first-reuse-first-operating-model.md).

### Inputs
- [x] Read Corpus product specification Stage 17, product mission Stage 01, cost Stage 14, security Stage 15, benchmark Stage 16, product overview, identity, workflow plan, design handoff, and this complete checklist section.
- [x] Record current source SHAs/versions and any contradiction found.

### Decisions
- [x] Define architecture principles that preserve product boundary, six axes, uncertainty/locality, capability-scoped publication, immutable observation history, replaceability, and one-owner maintainability.
- [x] Convert product priorities into measurable quality-attribute scenarios for correctness, provenance, rights safety, security, recoverability, availability/degradation, performance, operability, accessibility, benchmark qualification, and cost.
- [x] Define architecture budget envelopes around the 20k–50k canonical Item design center, approximately `€3/1,000 Items` variable-processing target and approximately `€25/month` normal cash envelope, while marking them recalibratable rather than hardcoded.
- [x] Define decision criteria and precedence when simplicity, quality, cost, rights, security, benchmark evidence, and App compatibility conflict.
- [x] Define forbidden shortcuts: one ready flag, trust=rights coupling, source-volume=independence, destructive rerun, learner-data ingress, live App inference dependency, unbounded paid loops, active source execution, and hypothetical internet-scale overbuilding.

### Product invariants / research / alternatives
- [x] Explicitly list product truths later stages may not reopen and calibration values later stages may tune with evidence.
- [x] Compare at least two architecture operating philosophies (for example modular monolith/offline-first vs distributed service-first) only at principle level; do not select the final stack here.
- [x] Define when current official external research is mandatory and when repository product truth is sufficient.

### Contracts, failure, security, cost, testing
- [x] Define the minimum cross-stage language for stable identity, revision, method/model/rule/taxonomy/contract versions, finding, hold, stale, provisional and superseded state.
- [x] Define graceful-degradation principles: preserve known-valid output, stop unsafe work, defer expensive work, make uncertainty visible, and never convert infrastructure failure into corpus truth.
- [x] Define stage-level security/privacy/rights and audit expectations that every downstream architecture artifact must address.
- [x] Define required observability/cost/testability questions every stage must answer.

### ADRs
- [x] Define when an ADR is required and adopt the `Architecture/adr/` index/template; do not create architecture-choice ADRs before the owning stage decides them.

### Definition of Done
- [x] Artifact contains measurable quality scenarios, budgets, decision rules, forbidden shortcuts, assumptions, empirical calibration needs, and downstream obligations.
- [x] Relevant checklist items are reconciled against the committed output; no later-stage decision is prematurely selected.

---

## 02. System Context and Product Boundaries

**Objective:** Define who/what interacts with Corpus, where trust boundaries lie, and which paths are offline/batch/runtime without leaking App or source responsibilities.

**Prerequisites:** 01.  
**Output:** `Architecture/02-system-context-and-product-boundaries.md`  
**Downstream:** 03–28.

**Committed evidence:** [Stage 02 system context](Architecture/02-system-context-and-product-boundaries.md) and [ADR-0002](Architecture/adr/ADR-0002-one-way-asynchronous-corpus-to-app-publication-boundary.md).

### Inputs
- [x] Read Stages 01–02 product shaping, Corpus/App contract Stage 12, security Stage 15, App product spec, design handoff, Architecture 01, workflow plan and checklist.

### Decisions
- [x] Produce C4-style system-context and trust-boundary views covering owner/operator, source web, manual URL/file/media intake, Corpus processing, storage, scheduler/jobs, operations UI, OCR/ASR/model services, Bestehen / App, and future/non-goal actors.
- [x] Separate discovery/acquisition paths, offline/batch processing paths, owner operations paths, Corpus→App publication paths, and explicitly absent learner-runtime paths.
- [x] Define external dependency inventory and which dependencies receive source content, metadata, secrets, or no sensitive data.
- [x] Define launch boundaries for public API/submissions, paid/private authenticated crawling, multi-user operation, billing and collaboration as absent with explicit future triggers.

### Product invariants / research / alternatives
- [x] Prove Corpus stores no learner profile/attempt/readiness data and App does not make ordinary runtime requests that trigger Corpus inference.
- [x] Compare direct synchronous integration vs asynchronous publication at context level without overriding Stage 19’s detailed contract ownership; record current App bundle-first counterpart as an integration constraint to reconcile later.

### Contracts, failure, security, cost, testing
- [x] Identify trust zones and source/model/operator/App boundaries where authentication, authorization, sanitization, egress control, signing or integrity checks may be required.
- [x] Define system-level outage/degradation expectations for source sites, model/OCR/ASR providers, operations UI, processing workers and Corpus→App delivery.
- [x] Record data-residency/egress/cost questions later stack stages must answer without inventing compliance claims.
- [x] Define context-level observability and end-to-end scenario probes used again in Stage 27.

### ADRs / DoD
- [x] Create an ADR only if a durable system-boundary decision beyond product truth is necessary.
- [x] Artifact names all actors/trust zones/non-goals and has no ambiguous learner-data or live-runtime dependency.
- [x] Checklist is re-fetched and reconciled after commit.

---

## 03. Technology Stack and Repository Strategy

**Objective:** Choose the simplest maintainable technology direction that can implement Corpus truth, secure processing, owner operations, jobs, storage, and App publication without premature distributed infrastructure.

**Prerequisites:** 01,02.  
**Output:** `Architecture/03-technology-stack-and-repository-strategy.md`  
**Downstream:** 05,11–15,19–26.

**Committed evidence:** [Stage 03 technology stack](Architecture/03-technology-stack-and-repository-strategy.md) and [ADR-0003](Architecture/adr/ADR-0003-python-first-modular-monolith-and-single-ecosystem-operations-console.md).

### Inputs
- [x] Read Architecture 01–02, product cost/security/operations/pipeline stages, design handoff, current target repository tree and current official platform/runtime documentation relevant to candidates.

### Decisions
- [x] Compare viable language/runtime/backend stacks against parser/media ecosystem, type safety, job support, testability, owner familiarity/maintenance burden, security patching, and portability.
- [x] Compare operations-UI strategies against the design’s dense desktop-first/accessibility contract without treating design HTML/runtime as production code.
- [x] Compare managed vs self-hosted candidates for relational persistence, object/blob storage, job scheduling/execution, search/index needs and hosting; avoid selecting extra services without measured need.
- [x] Choose repository/module/package boundaries and local-development strategy compatible with a modular personal project and later isolated workers where justified.
- [x] Define dependency/licensing/update policy and export/exit strategy for durable data and critical processing.
- [x] Define deployment candidates and constraints while leaving final environment/release operationalization to Stage 26.

### Research / alternatives
- [x] Use current primary official sources for framework support, hosting/service limits, pricing/licensing and security lifecycle; record access dates.
- [x] Include recurring cash, variable-processing, maintenance-time and lock-in comparisons for the recommended default and at least two credible alternatives.

### Contracts, failure, security, cost, testing
- [x] Define how the chosen direction supports background work, partial success, content-addressed reuse, safe isolation and App bundle publication without microservice-per-domain sprawl.
- [x] Define cheap/local fallback when a managed dependency is unavailable or exceeds budget.
- [x] Define minimum local reproducibility, test tooling and observability hooks required of the selected stack.

### ADRs / DoD
- [x] Create ADR(s) for durable stack/repository/operations-UI strategy decisions where cross-cutting.
- [x] Artifact makes a recommended default, not a shopping list, and names upgrade triggers rather than designing for hypothetical millions of records.
- [x] Checklist is re-fetched/reconciled.

---

## 04. Domain Model and Bounded Contexts

**Objective:** Establish architecture language and ownership so evidence, governance, processing, quality, analytics and publication cannot overwrite one another’s truth.

**Prerequisites:** 01,02.  
**Output:** `Architecture/04-domain-model-and-bounded-contexts.md`  
**Downstream:** 05–28.

### Inputs
- [ ] Read Corpus shaping Stages 02–13 and 17, design state-model page/handoff, Architecture 01–02, workflow plan and checklist.

### Decisions
- [ ] Define bounded contexts/modules for source acquisition, provenance/evidence, rights/governance, canonical content, taxonomy/relevance, processing, quality/findings, identity/independence, analytics, publication/contracts, operations/audit, benchmark and cost/automation.
- [ ] Define ubiquitous language for Observation, Document, Exam, Section, Part, Task, Item, Instruction, Stimulus, Option, Answer/Scoring, Asset, Finding, Decision, Derivation, Revision, Capability Eligibility, Cluster, Independence and Publication.
- [ ] Identify aggregate/value-object/policy boundaries without forcing a physical schema.
- [ ] Define anti-corruption boundaries between observed source state, curated decisions and derived intelligence.
- [ ] Define which context owns stable IDs/revisions and which contexts consume references rather than cloning authoritative state.

### Invariants / alternatives
- [ ] Demonstrate that the six truth axes remain separately owned/composable and that rights/confidence/QA/independence cannot mutate one another implicitly.
- [ ] Compare a single undifferentiated domain model with modular bounded contexts and justify the chosen degree of separation for one owner.

### Failure/security/cost/testing
- [ ] Define cross-context behavior for unknown/disputed/provisional/stale/superseded/held states and local-scope defects.
- [ ] Identify sensitive trust boundaries inside the domain and where audit is mandatory.
- [ ] Keep boundaries coarse enough to avoid service sprawl; record only measured future split triggers.
- [ ] Define invariant/property tests Stage 25 must later implement.

### ADRs / DoD
- [ ] Record a durable context/ownership ADR only if useful across many stages.
- [ ] Artifact includes context map, ownership matrix and prohibited cross-context writes.
- [ ] Checklist reconciled.

---

## 05. Data Ownership, Persistence, Storage, and Schema Evolution

**Objective:** Choose logical/physical persistence boundaries that preserve observations, revisions, local evidence, history, replay, rights deletion/suppression and cost without unnecessary polyglot sprawl.

**Prerequisites:** 03,04.  
**Output:** `Architecture/05-data-ownership-persistence-storage-and-schema-evolution.md`  
**Downstream:** 06–28.

### Inputs
- [ ] Read Architecture 03–04 plus shaping canonical model, pipeline, dedup, rights, analytics, cost, security and design audit/diff contracts.

### Decisions
- [ ] Choose primary durable store strategy and justify when relational/document/blob/search/vector/graph capabilities are truly needed vs derivable from the primary store.
- [ ] Define data ownership and identifiers/revisions for observed, curated and derived records; immutable history vs mutable projections; transactional boundaries; append-only audit.
- [ ] Define raw/source artifact, normalized artifact, extracted representation, media and generated derivative storage responsibilities and content-addressed reuse.
- [ ] Define schema/version migration strategy across data, taxonomy, processing method, analytics and App contract versions.
- [ ] Define retention, suppression, takedown deletion, privacy deletion, provenance/audit preservation, backups and reproducibility boundaries.
- [ ] Define what is backed up, reproducible from raw evidence, safely ephemeral, cached, suppressed or physically deleted.

### Research / alternatives
- [ ] Compare at least two persistence/storage shapes using current official service/runtime limits/pricing where mutable.
- [ ] Reject warehouse/lakehouse/vector/search proliferation unless a measured query/scale need is documented.

### Failure/security/cost/testing
- [ ] Define restore, migration rollback/forward-fix, corrupted object, orphan reference and partial-write behavior.
- [ ] Define encryption/access/secret separation and how prohibited/takedown material is prevented from ordinary resurfacing.
- [ ] Estimate base-envelope storage/backup/egress costs and lifecycle policies.
- [ ] Define migration, backup/restore, retention/deletion and invariant tests.

### ADRs / DoD
- [ ] Create ADR for primary persistence/storage/content-addressing strategy if selected.
- [ ] Artifact proves stable identity and historical truth survive reprocessing/migration/removal semantics.
- [ ] Checklist reconciled.

---

## 06. Source Registry, Discovery, and Acquisition Architecture

**Objective:** Turn source strategy into bounded, auditable discovery/acquisition architecture without equating access policy with trust or rights.

**Prerequisites:** 02,04,05.  
**Output:** `Architecture/06-source-registry-discovery-and-acquisition-architecture.md`  
**Downstream:** 07–13,17,20,23–27.

### Inputs
- [ ] Read shaping source strategy, mission, rights/security/cost stages, design Source Controls & Intake surfaces, Architecture 02/04/05.

### Decisions
- [ ] Define Source Family, Source Observation/location, discovery candidate and acquisition-policy ownership/state transitions.
- [ ] Define automated discovery vs owner URL/file intake, provider prioritization, mirror/dead-source handling, allow/block scopes and discovery budgets.
- [ ] Define robots/access/rate-limit behavior and explicit prohibition on authenticated paid/private crawling at launch.
- [ ] Define canonical URL/location normalization without losing observation history or treating mirror copies as corroboration.
- [ ] Define acquisition scheduling/backoff/defer behavior and source-level health without inventing authenticity/rights.

### Research / alternatives
- [ ] Use current official protocol/provider guidance where robots/rate/access behavior is mutable or provider-specific.
- [ ] Compare broad crawling vs coverage-driven bounded discovery and justify the low-ops default.

### Failure/security/cost/testing
- [ ] Define dead/redirecting/rate-limited/blocked/changed source behavior and manual recovery.
- [ ] Hand unsafe URL/file checks to Stage 12 before deep retrieval; no bypass from owner intake.
- [ ] Define host/source crawl budgets, duplicate fetch avoidance and productive-yield cost metrics.
- [ ] Define tests for allow/block precedence, rate limits, observation preservation and no trust/rights side effect.

### ADRs / DoD
- [ ] Create ADR only if acquisition topology/scheduling choice is durable cross-cutting.
- [ ] Artifact supports designed discovery/intake/source registry states and preserves access-policy independence.
- [ ] Checklist reconciled.

---

## 07. Provenance, Authenticity, and Confidence Architecture

**Objective:** Represent claimed/evidenced origin and multidimensional confidence locally, audibly and independently from rights/QA.

**Prerequisites:** 04,05,06.  
**Output:** `Architecture/07-provenance-authenticity-and-confidence-architecture.md`  
**Downstream:** 08–10,15–21,25–28.

### Inputs
- [ ] Read shaping trust/authenticity/confidence, source strategy, dedup and final spec; design authenticity workbench/state models; Architecture 04–06.

### Decisions
- [ ] Define claimed vs evidenced origin, authenticity categories, confidence dimensions `0–4|unknown|not_applicable`, tiers/caps/dispute/quarantine and evidence records.
- [ ] Define local vs inherited evidence and rules preventing a parent from rescuing defective children or children from exceeding parent claims without local evidence.
- [ ] Define corroboration/contradiction using underlying independent evidence rather than host/mirror count.
- [ ] Define curated confidence/authenticity overrides, evidence/rationale, versioning and rerun conflict behavior.
- [ ] Define hard use gates and how confidence influences a capability without becoming rights or QA.

### Alternatives / research
- [ ] Compare normalized evidence records vs a flattened score-only design and explicitly reject any model that cannot explain/cap/dispute locally.
- [ ] Preserve empirical calibration of weights/thresholds for benchmark work rather than inventing precision.

### Failure/security/cost/testing
- [ ] Define missing/conflicting/late evidence, stale provenance and disputed-origin behavior.
- [ ] Prevent source text/model output from self-asserting authoritative origin without evidence and governed validation.
- [ ] Favor deterministic evidence and cached comparisons before model escalation; account for human review.
- [ ] Define tests for mirrors not increasing corroboration, unknown in denominator and override survival.

### ADRs / DoD
- [ ] ADR only for durable evidence-model strategy if necessary.
- [ ] Artifact maps to design eight-dimension review and keeps rights untouched.
- [ ] Checklist reconciled.

---

## 08. Rights, Usage, Attribution, Takedown, and Removal Architecture

**Objective:** Build conservative action-level rights/governance and removal semantics that never infer permission from public access, trust or acquisition policy.

**Prerequisites:** 04,05,06,07.  
**Output:** `Architecture/08-rights-usage-attribution-takedown-and-removal-architecture.md`  
**Downstream:** 09–12,15–28.

### Inputs
- [ ] Read shaping rights Stage 04, App contract Stage 12, security Stage 15, final spec, design rights/takedown workbench and governance model, Architecture 04–07.

### Decisions
- [ ] Define operational rights statuses including reusable, conditional, reference-only, unknown/review, prohibited, legal-review and takedown hold where current product/design requires them.
- [ ] Define action-level permissions/conditions for storage, transformation, internal analysis, exact reuse, asset exposure, App delivery, attribution and derived abstract intelligence.
- [ ] Define component/asset/local overrides that may tighten but never silently loosen parent rights.
- [ ] Define evidence/rationale, attribution, legal-review and curated override audit/version semantics.
- [ ] Define takedown/security hold, suppression, purge, recompute, downstream change notification and prevention fingerprint/mirror re-ingestion behavior.
- [ ] Distinguish rights-only removal from trust/correctness invalidation and define what legitimate provenance/audit/derived truth may remain.

### Research / alternatives
- [ ] Research only implementation/legal-technical facts needed for architecture; do not invent legal certainty or claim legal compliance.
- [ ] Compare hard physical deletion everywhere vs governed suppression/selective purge/recompute and justify according to product semantics.

### Failure/security/cost/testing
- [ ] Define unknown/disputed/mixed-rights/default-deny behavior and what happens if rights evidence disappears or changes.
- [ ] Ensure takedown/security controls outrank reprocess/acquisition automation.
- [ ] Define low-cost rights evidence storage/review and no live legal/model inference on ordinary App use.
- [ ] Define tests for unknown≠permission, local tightening, mirror prevention, takedown propagation and audit immutability.

### ADRs / DoD
- [ ] ADR if removal/suppression architecture is a durable cross-cutting decision.
- [ ] Artifact has exact downstream effects and App implications without changing authenticity/confidence.
- [ ] Checklist reconciled.

---

## 09. Canonical Exam, Content, Answer, and Asset Model

**Objective:** Translate the product’s semantic exam hierarchy into stable architecture entities/relationships that preserve source fidelity, partial structures, scoring and asset dependencies.

**Prerequisites:** 04,05,06,07,08.  
**Output:** `Architecture/09-canonical-exam-content-answer-and-asset-model.md`  
**Downstream:** 10–28.

### Inputs
- [ ] Read shaping canonical exam model/final spec, design ten inspectable scopes, Architecture 04–08.

### Decisions
- [ ] Define Source Observation → Document → Exam → Section → optional Part → Task → Item identity/revision relationships and incomplete/composite exam behavior.
- [ ] Model Instructions, Stimuli, Response Options, Answers/Scoring, Rubrics, Assets, provenance observations, interpretations, findings, derivations and decisions as first-class where product truth requires.
- [ ] Define shared/reused stimuli/instructions and many-to-many content/asset dependencies without layout-driven duplication.
- [ ] Define objective answers, multiple acceptable answers, rubric/scoring relationships, missing/disputed keys and source-vs-curated answer interpretation.
- [ ] Define source expression vs curated correction vs derived intelligence and stable IDs across re-extraction/revision.
- [ ] Define asset completeness/linkage and provider-specific fidelity without making provider layout canonical.

### Alternatives / failure / security / cost / testing
- [ ] Compare semantic model vs page/layout-shaped storage and justify semantic canonicalization with retained source anchors.
- [ ] Define partial/broken/missing/composite content behavior at smallest scope and capability effect.
- [ ] Preserve rights/security metadata on source components/assets and prevent unsafe preview from becoming canonical content execution.
- [ ] Define storage/query efficiency and content-addressed reuse implications without duplicating large source/media payloads.
- [ ] Define schema/property tests for hierarchy, answer links, shared stimuli, revisions and local incompleteness.

### ADRs / DoD
- [ ] ADR only if a durable identity/revision strategy deserves separate record.
- [ ] Artifact supports all designed Record Detail scopes and leaves taxonomy/difficulty to Stage 10.
- [ ] Checklist reconciled.

---

## 10. Taxonomy, Difficulty, Relevance, and Versioning Architecture

**Objective:** Define a governed shared skill/taxonomy graph and separately version difficulty, CEFR, Generic-B1 and TELC relevance without creating learner mastery in Corpus.

**Prerequisites:** 04,05,07,09.  
**Output:** `Architecture/10-taxonomy-difficulty-relevance-and-versioning-architecture.md`  
**Downstream:** 11,15–22,25–28.

### Inputs
- [ ] Read shaping taxonomy and difficulty/relevance stages, App learner-model/product contract, design taxonomy migration surfaces, Architecture 04/05/07/09.

### Decisions
- [ ] Define taxonomy node/edge/assignment model across provider, section/task, topic, grammar, vocabulary, receptive/productive skills, strategy, reasoning and distractor families.
- [ ] Preserve assignment role/confidence/origin/evidence and taxonomy version.
- [ ] Define governed node lifecycle: add, rename, merge, split, retire, map and migration/change-impact semantics.
- [ ] Define separate CEFR/difficulty dimensions and separate Generic-B1/TELC relevance with uncertainty/currentness and calibration version.
- [ ] Define Corpus→App shared-node mapping that sends no learner data and does not dictate how App migrates mastery after splits/merges.
- [ ] Define how taxonomy/relevance changes stale/recompute dependent analytics/publications without rewriting historical observations.

### Alternatives / research / failure / cost / testing
- [ ] Compare rigid flat enums vs governed versioned graph and justify complexity at the low-hundreds-node product scale.
- [ ] Define unknown/provisional/conflicting assignments and manual review/migration rollback behavior.
- [ ] Keep classification/calibration cheap-first and defer model routing to Stage 22.
- [ ] Define migration, backward-compatibility, graph integrity and App mapping tests.

### ADRs / DoD
- [ ] ADR if taxonomy version/migration strategy is durable cross-cutting.
- [ ] Artifact separates learner-specific state from Corpus taxonomy truth.
- [ ] Checklist reconciled.

---

## 11. Pipeline Orchestration, State Machines, Idempotency, and Reprocessing

**Objective:** Choose physical work orchestration that preserves the conceptual lifecycle, partial success, replay, curated overrides, bounded retries and earliest-stage reprocessing.

**Prerequisites:** 03–10.  
**Output:** `Architecture/11-pipeline-orchestration-state-idempotency-and-reprocessing.md`  
**Downstream:** 12–28.

### Inputs
- [ ] Read product pipeline/final spec, cost/security/operations, design run/reprocess states and Flows A/B, Architecture 03–10.

### Decisions
- [ ] Map conceptual lifecycle to physical jobs/stages without losing Discover→…→Publish semantics.
- [ ] Choose scheduler/queue/job/state-machine model and unit-of-work granularity; define ownership of runs, attempts and stage outputs.
- [ ] Define idempotency keys, content/version inputs, work deduplication and replay safety.
- [ ] Define pipeline states including queued/running/complete/partial/failed/blocked/stale/superseded and retry/defer/review/quarantine/hold semantics.
- [ ] Define partial success at smallest meaningful scope and downstream eligibility propagation.
- [ ] Define scoped reprocessing from earliest affected stage, stale/recompute/invalidate propagation and run comparison.
- [ ] Define curator-override conflict handling: retained active correction plus reviewable candidate, never silent overwrite.
- [ ] Define bounded retry/escalation/backoff/dead-letter/manual recovery and no expensive failure loops.

### Research / alternatives / cross-cutting
- [ ] Compare in-database job runner, managed queue/workflow and heavier orchestration candidates using current official limits/pricing; choose simplest adequate default.
- [ ] Define security isolation handoff to Stage 12 and model-cost gates handoff to Stage 22.
- [ ] Define structured logs/metrics/cost attribution per run/stage and test hooks for deterministic replay.

### ADRs / DoD
- [ ] Create ADR for chosen orchestration model if durable.
- [ ] Artifact includes state machine, sequence/reprocess diagrams and failure matrix proving unaffected outputs survive.
- [ ] Checklist reconciled.

---

## 12. Secure Fetch, File, Archive, and Content Intake

**Objective:** Ensure every URL/file/archive/content input is bounded and rendered/processed as untrusted data before expensive or active processing.

**Prerequisites:** 02,03,05,06,08,11.  
**Output:** `Architecture/12-secure-fetch-file-archive-and-content-intake.md`  
**Downstream:** 13–17,21–27.

### Inputs
- [ ] Read product security/source/pipeline/rights stages, design security preflight/inert preview contracts, Architecture 02/03/05/06/08/11.

### Decisions
- [ ] Define outbound URL policy: scheme, DNS resolution/rebinding defense, IP/network allow/deny, redirect limits, egress, time/size bounds and host rate controls.
- [ ] Define file magic/type/extension checks, size bounds, quarantine and supported/unsupported/encrypted/unsafe states.
- [ ] Define archive recursion/member/expanded-size/path-traversal/password/bomb protections and refusal behavior.
- [ ] Define Office/PDF/HTML/rich-media active-content neutralization and safe transfer to parsers.
- [ ] Define malware scanning/sandbox/isolation boundary proportional to personal-project risk and residual-risk statement.
- [ ] Define inert/sanitized preview pipeline: strip active elements/handlers/embeds/forms/iframes/fonts as required; source content never focusable/authoritative.
- [ ] Define acquisition credential/secret isolation and source-text prompt-injection boundary before any model/tool use.

### Research / alternatives / failure / cost / testing
- [ ] Use current OWASP/platform/file-format guidance and official runtime/cloud docs for mutable security behavior.
- [ ] Compare process/container/VM/managed isolation levels and choose risk-proportionate default plus escalation trigger.
- [ ] Define refusal vs quarantine vs retry for unsafe/oversized/encrypted/unsupported inputs; security failure is not extraction failure.
- [ ] Bound scan/sandbox/transfer cost and cache security results by immutable content identity where safe.
- [ ] Define adversarial tests for SSRF, redirect loops, DNS rebinding, archive bombs/path traversal, polyglots, active HTML/Office/PDF and prompt-injection transfer.

### ADRs / DoD
- [ ] ADR for durable execution-isolation/egress boundary if selected.
- [ ] Artifact proves unsafe input cannot reach parser/model/tool through an ordinary retry path.
- [ ] Checklist reconciled.

---

## 13. Document, Image, OCR, Layout, and Structure Extraction

**Objective:** Choose a benchmarkable extraction architecture for native/scanned documents and images that preserves German meaning, layout relationships, partial results and method lineage.

**Prerequisites:** 05,09,11,12.  
**Output:** `Architecture/13-document-image-ocr-layout-and-structure-extraction.md`  
**Downstream:** 15–18,21–28.

### Inputs
- [ ] Read product canonical model/pipeline/QA/benchmark/cost, design extraction failure/reprocess flows, Architecture 05/09/11/12.

### Decisions
- [ ] Define native PDF/DOCX/image/scanned-PDF normalization/extraction paths and selection criteria.
- [ ] Define layout/reading-order/table/region/anchor representation sufficient to segment canonical exam scopes without making layout canonical truth.
- [ ] Define OCR method ladder, German language handling, meaning-critical character/number preservation and confidence/uncertainty capture.
- [ ] Define segmentation from document regions to canonical hierarchy with partial/error outputs and traceable source anchors.
- [ ] Define method/tool/version/input lineage, cached artifacts and reprocessing triggers.
- [ ] Define manual fallback/escalation for low-confidence or meaning-critical failures.

### Research / alternatives / failure / cost / testing
- [ ] Compare current native parsers/OCR/layout candidates using official capability/licensing/pricing docs; final qualification depends on Stage 21 benchmark.
- [ ] Define page/region-level partial success, unsupported/encrypted/broken document behavior and no fabricated missing text.
- [ ] Ensure extraction runs only after Stage 12 security controls and external OCR receives only permitted content.
- [ ] Estimate base-envelope CPU/storage/paid OCR cost and cheap-first/local/batch fallback.
- [ ] Define benchmark slices and tests for structural precision/recall and meaning-critical fidelity.

### ADRs / DoD
- [ ] ADR only for durable extraction architecture/provider abstraction choices.
- [ ] Artifact is compatible with parallel Stage 14 and exposes a clean handoff to Stage 15.
- [ ] Checklist reconciled.

---

## 14. Audio, Video, ASR, and Media Processing

**Objective:** Define rights-aware, cost-bounded media extraction/transcription/alignment that distinguishes script/language evidence from acoustic independence.

**Prerequisites:** 05,09,11,12.  
**Output:** `Architecture/14-audio-video-asr-and-media-processing.md`  
**Downstream:** 15–18,21–28.

### Inputs
- [ ] Read product pipeline/dedup/QA/cost/security/benchmark, design media/asset failure states, Architecture 05/09/11/12.

### Decisions
- [ ] Define audio/video discovery/extraction, media metadata, immutable content identity and storage/streaming/preview boundaries.
- [ ] Define ASR/caption/source-script pathways, segmentation/alignment and relationship to Tasks/Items/Assets.
- [ ] Preserve acoustic evidence separately from lexical/script evidence so re-recordings can differ by metric independence.
- [ ] Define ASR confidence/uncertainty, method/model/version lineage and missing/broken/partial media states.
- [ ] Define when video needs audio/caption/selected-frame processing vs full-video analysis; reject unnecessary full-video understanding by default.
- [ ] Define large-media batching/cache/content reuse and manual fallback.

### Research / alternatives / failure / security / cost / testing
- [ ] Compare local/open-source and managed ASR/media candidates from current official docs/pricing; qualification remains benchmark-gated.
- [ ] Define provider outage, long-media timeout, missing channel/caption, bad alignment and partial-transcript recovery.
- [ ] Respect rights/privacy/egress boundaries for external media processing and Stage 12 safe intake.
- [ ] Model hours-of-audio processing costs against Stage 14 product envelopes and budget-defer behavior.
- [ ] Define benchmark tests for meaning-critical ASR fidelity, segmentation/link precision and acoustic independence.

### ADRs / DoD
- [ ] ADR if media/ASR provider abstraction or processing topology is durable.
- [ ] Artifact cleanly hands structured media evidence to Stage 15/16 without equating transcript identity with recording identity.
- [ ] Checklist reconciled.

---

## 15. Semantic Enrichment, Classification, and Answer Mapping

**Objective:** Define deterministic/model-assisted enrichment that produces structured candidates with confidence/evidence, never fabricated truth or tool authority.

**Prerequisites:** hard: 09,10,11,13,14; also consume 07,08,12.  
**Output:** `Architecture/15-semantic-enrichment-classification-and-answer-mapping.md`  
**Downstream:** 16–18,21–28.

### Inputs
- [ ] Read product taxonomy/difficulty/pipeline/QA/benchmark/security, Architecture 07–14 and design candidate/override/review semantics.

### Decisions
- [ ] Define classification/enrichment responsibilities: provider/level/task, taxonomy candidates, grammar/vocab/topic/reasoning/distractor, difficulty/relevance estimates and answer/scoring mapping.
- [ ] Define deterministic-first rules vs model-assisted work and structured output schemas with evidence/confidence/origin.
- [ ] Define answer/key/rubric linking, disagreement detection and the rule that source/model ambiguity remains unknown/disputed rather than fabricated.
- [ ] Define confidence/disagreement/escalation and human-review triggers per capability risk.
- [ ] Define method/model/prompt/rule/taxonomy version lineage and cache/reprocess invalidation.
- [ ] Define prompt-injection isolation: source text is quoted data, tool access absent/allowlisted, structured output validated before persistence.

### Alternatives / failure / security / cost / testing
- [ ] Compare deterministic/local/small-model/strong-model/human paths by expected quality and cost; Stage 22 later centralizes provider routing/governance.
- [ ] Define invalid structured output, disagreement, timeout, provider failure and budget refusal as provisional/review states, not truth.
- [ ] Prevent external model output from changing rights/security/publishing directly.
- [ ] Attribute cost per productive enrichment and avoid re-running unchanged immutable inputs.
- [ ] Define benchmark/evaluation requirements for high-impact taxonomy, answer mapping and calibration.

### ADRs / DoD
- [ ] ADR only for durable semantic-processing abstraction or structured-output contract if cross-cutting.
- [ ] Artifact provides candidates/findings, not unreviewable AI authority.
- [ ] Checklist reconciled.

---

## 16. Duplicate, Derivative, Identity, and Analytical Independence

**Objective:** Preserve every observation while architecture determines identity/lineage and metric-specific independence without mirror inflation.

**Prerequisites:** 07,09,10,11,13,14,15.  
**Output:** `Architecture/16-duplicate-derivative-identity-and-analytical-independence.md`  
**Downstream:** 17–21,25–28.

### Inputs
- [ ] Read product dedup/analytics/trust stages, design duplicate workbench/state model, Architecture prerequisites.

### Decisions
- [ ] Define exact/content/near/structural/semantic/media fingerprint pipelines and relationship classes for independent, exact, reformatted, derivative, re-recorded, fragment, related variant and unresolved dependency.
- [ ] Separate Source Observation identity, content identity, derivative lineage, canonical provenance anchor and preferred processing representation.
- [ ] Define per-metric independence for lexical/grammar/structure/acoustic/visual and any additional product metric families.
- [ ] Define cluster membership, canonical-anchor/preferred-representation changes, reversible owner review and recalculation.
- [ ] Define answer disagreement inside otherwise same content without inventing a new independent Item.
- [ ] Define downstream independence recomputation/versioning and how changed clusters stale analytics/publications.

### Research / alternatives / failure / cost / testing
- [ ] Compare deterministic hashes/fingerprints, similarity methods and selective model-assisted comparisons; benchmark thresholds rather than vendor claims decide promotion.
- [ ] Define unresolved/ambiguous cluster behavior and prevent automatic destructive collapse.
- [ ] Prevent takedown-blocked fingerprints from mirror re-ingestion by integrating Stage 08/12 controls.
- [ ] Use cheap exact/structural passes before expensive semantic/media comparison and record avoided duplicate-processing cost.
- [ ] Define precision-oriented benchmark gates and tests including 20 mirrors=one occurrence and re-recorded script/acoustic split.

### ADRs / DoD
- [ ] ADR for durable content-identity/fingerprinting strategy if warranted.
- [ ] Artifact supports design cluster comparison and makes analytical independence metric-specific.
- [ ] Checklist reconciled.

---

## 17. Validation, QA, Findings, and Capability-Scoped Publication

**Objective:** Define the architecture that turns local findings into capability-specific eligibility/promotion/revocation without one global readiness flag.

**Prerequisites:** 07–16.  
**Output:** `Architecture/17-validation-qa-findings-and-capability-scoped-publication.md`  
**Downstream:** 18–28.

### Inputs
- [ ] Read product QA/final spec/benchmark, design state models/eligibility/health, all Architecture 07–16 outputs.

### Decisions
- [ ] Define validation layers and Q0–Q3 plus incomplete/blocked-dependency/not-run findings at smallest meaningful scope.
- [ ] Define structural, correctness/scoring, taxonomy, OCR/ASR, asset, identity/independence and governance gates.
- [ ] Define six capability eligibility answers with eligible/limited/provisional/held/blocked/not-run semantics, reasons and local/inherited evidence.
- [ ] Define promotion/revocation/quarantine/restore and local defect propagation; unaffected capabilities remain usable where evidence allows.
- [ ] Define publication manifests/snapshots/versions and stale/superseded/invalidated semantics.
- [ ] Define incident response when a published capability later fails a gate.

### Alternatives / failure / security / cost / testing
- [ ] Explicitly compare and reject universal `production_ready` or scalar quality score designs.
- [ ] Define missing dependency/benchmark not instantiated/uncertain evidence as honest non-passing states rather than green defaults.
- [ ] Rights/security holds override ordinary publication paths without mutating confidence.
- [ ] Define validation cost tiers and incremental recomputation rather than full-corpus validation on every change.
- [ ] Define benchmark-backed gate tests and no-Q0-escape release expectation where product Stage 16 requires it.

### ADRs / DoD
- [ ] ADR for durable publication eligibility/snapshot model if cross-cutting.
- [ ] Artifact proves disputed answer can block correctness while unaffected language/topic/structure evidence remains usable.
- [ ] Checklist reconciled.

---

## 18. Analytics and Exam-Intelligence Architecture

**Objective:** Produce reproducible, evidence-aware exam intelligence whose denominators, independence, confidence, freshness and applicability remain visible.

**Prerequisites:** 07,08,09,10,16,17.  
**Output:** `Architecture/18-analytics-and-exam-intelligence-architecture.md`  
**Downstream:** 19–22,24–28.

### Inputs
- [ ] Read product analytics/dedup/trust/taxonomy/final spec, design analytics/health/App-impact surfaces, Architecture prerequisites.

### Decisions
- [ ] Define analytical computation/recomputation boundaries and materialized vs on-demand result strategy appropriate to scale.
- [ ] Define result envelope: subject/metric/scope/counting unit/raw/canonical/independent counts/denominator/evidence mass/source/provider mix/confidence/uncertainty/version/freshness/applicability.
- [ ] Define exploratory vs decision-grade results and sufficiency/concentration rules.
- [ ] Define vocabulary/grammar/topic/task/skill/provider/progression/TELC-vs-generic/reasoning/distractor/co-occurrence/difficulty families and which independence metric each consumes.
- [ ] Define source/provider concentration, explainability and no mirror/derivative inflation.
- [ ] Define recomputation triggers from rights, trust, taxonomy, dedup, QA and source changes with stale/previous-version visibility.

### Alternatives / failure / cost / testing
- [ ] Compare query-time analytics with incremental/materialized aggregates and select a simple reproducible default.
- [ ] Define insufficient evidence/empty denominator/stale input/partial recompute behavior; no misleading zero or chart.
- [ ] Ensure restricted source expression is not leaked through non-permitted analytics output.
- [ ] Bound compute/storage cost with incremental recompute/cache and productive decision-grade output metrics.
- [ ] Define reproducibility tests, denominator/independence properties and known mirror-inflation counterexamples.

### ADRs / DoD
- [ ] ADR if analytical materialization/versioning architecture is durable.
- [ ] Artifact supports Stage 19 pattern-first contract and design chart/table accessibility expectations.
- [ ] Checklist reconciled.

---

## 19. Corpus → App Contract, API, Bundles, Compatibility, and Change Propagation

**Objective:** Implement the provider-side versioned boundary that supplies eligible pattern-first intelligence to App without learner data or live Corpus runtime dependence.

**Prerequisites:** 05,08,09,10,17,18.  
**Output:** `Architecture/19-corpus-app-contract-api-bundles-and-change-propagation.md`  
**Downstream:** 20,23–28 and Bestehen / App.

### Inputs
- [ ] Read Corpus shaping Stage 12 and Stage 17, App final product spec, current App Architecture 10/12/28, Architecture prerequisites, design Corpus→App impact surface.
- [ ] Record current App counterpart versions/SHAs and any actual incompatibility rather than assuming one.

### Decisions
- [ ] Define capability catalogue and request/publication envelopes for pattern-first blueprints, structured intelligence, governance/eligibility, provenance summaries, versions and exceptional raw/reference path.
- [ ] Define stable opaque IDs, revisions, taxonomy/contract/analytics/publication versions and compatibility matrix.
- [ ] Reconcile current App **bundle-first asynchronous pull** architecture: publication index, immutable capability-scoped bundles/snapshots, integrity/signing expectations, import compatibility and last-known-compatible behavior; recommend the simplest provider implementation unless a coordinated change is justified.
- [ ] Define exact-source reuse path only where rights/capability permit; original practice generation remains App-owned.
- [ ] Define material-change manifests for reclassification, rights/takedown, identity/independence, taxonomy, target-format and analytics changes.
- [ ] Define Corpus outage, stale bundle, no decision-grade pattern, incompatible consumer and revocation/removal behavior.
- [ ] Define hard schema/data-minimization rule that learner/session/profile/attempt/readiness fields are not accepted by Corpus.

### Research / alternatives / failure / security / cost / testing
- [ ] Use current official cryptographic/serialization/object-delivery guidance for mutable implementation choices; do not blindly inherit primitives from App without validation.
- [ ] Compare live API, export files, signed bundles and hybrid provider paths against product/App constraints; document why the recommended launch contract is compatible and low-ops.
- [ ] Define signing/integrity/replay/key-rotation requirements while deferring system-wide key custody to Stage 23.
- [ ] Keep ordinary App delivery precomputed/cached/batched; no per-session Corpus AI cost.
- [ ] Define contract/schema/compatibility/removal/idempotent-import tests jointly interpretable by App.

### ADRs / DoD
- [ ] Create ADR for provider contract/publication style if durable.
- [ ] Artifact documents any App mismatch with exact source authority; otherwise states compatibility explicitly.
- [ ] Checklist reconciled.

---

## 20. Operations Console, Review Workflows, Audit, and Source Controls

**Objective:** Map the complete design handoff to a maintainable owner-only internal architecture without raw-row surgery, unsafe mobile decisions or per-screen backend forks.

**Prerequisites:** hard 05,11,16,17,18,19; consume relevant 03–19.  
**Output:** `Architecture/20-operations-console-review-audit-and-source-controls.md`  
**Downstream:** 23–28.

### Inputs
- [ ] Read design `DESIGN-HANDOFF.md` and Corpus-00 through Corpus-09 human-authored content, product operations Stage 13, Architecture prerequisites and current ADR index.

### Decisions
- [ ] Map five primary destinations, one prioritized Inbox/saved views, ten-scope Record Detail, Source Controls & Intake, Runs/Reprocessing/Change Actions, Health/Benchmark/Analytics/App Impact/Audit to modules/queries/commands/background jobs.
- [ ] Define reusable query/view architecture and avoid one backend fork/endpoint per screen or queue.
- [ ] Define queue-context persistence, filters/sort/density/page/scroll/focus restoration and draft persistence across reload/network/session expiry.
- [ ] Define observed vs curated vs derived diff/edit model; corrections create governed interpretations and never erase observation.
- [ ] Define R0–R3 action commands, scope enumeration, rationale/evidence, safe alternative, stronger-control refusal and append-only audit.
- [ ] Define background-job UX contract and six result states: success, partial, conflict, failure, refused, draft preserved.
- [ ] Define source preview API/data path as inert/sanitized/non-focusable with unsupported/encrypted/unsafe/rights-suppressed/missing states.
- [ ] Preserve desktop-first consequential work, <900 read-only companion, WCAG 2.2 AA, keyboard/focus/announcement/non-color/chart-table alternatives.
- [ ] Define owner authentication boundary assumption; Stage 23 owns final mechanism and key/secret threat design.
- [ ] Define health as hard blockers plus vectors, never scalar score.

### Alternatives / failure / cost / testing
- [ ] Compare polling vs realtime and server-rendered/thin-client vs richer client state using actual owner workload; choose simplest behavior-preserving default.
- [ ] Define offline/network/session-conflict/changed-record behavior and optimistic/concurrency protection for governed actions.
- [ ] Prevent source text from becoming UI command/policy and ensure high-risk actions require server-side authorization/validation.
- [ ] Keep steady-state operator workload near product expectations; measure queue/review time as cost.
- [ ] Define accessibility/browser/state-workflow tests against Flows A–H and designed breakpoints.

### ADRs / DoD
- [ ] Create ADR for operations UI architecture if durable.
- [ ] Artifact includes design-to-architecture coverage matrix and explicitly labels design presentation assumptions accepted/replaced.
- [ ] Checklist reconciled.

---

## 21. Benchmark, Gold Data, Reproducibility, and Capability Qualification

**Objective:** Turn the Stage 16 benchmark contract into a versioned architecture/release process that can actually qualify parsers, models, dedup and publication capabilities.

**Prerequisites:** 08,09,10,12–18.  
**Output:** `Architecture/21-benchmark-gold-data-reproducibility-and-capability-qualification.md`  
**Downstream:** 22,25–28.

### Inputs
- [ ] Read product benchmark Stage 16/final spec, rights/security/QA/cost, Architecture prerequisites and design benchmark/health surfaces.

### Decisions
- [ ] Define lawful source manifest/acquisition linkage for the 16 seed slots and 12–14-package gold core; do not pretend files are already acquired.
- [ ] Define annotation schemas, adjudication, uncertainty, provenance and gold-correction history.
- [ ] Define content-family-disjoint 70/30 development/holdout split, negative/uncertain cases and leakage prevention.
- [ ] Define immutable benchmark releases starting with `corpus-benchmark-1.0.0`, checksums/manifests, tool/data/config lineage and retirement/supersession.
- [ ] Define evaluation harness and capability/slice gates for structure, correctness links, taxonomy, text/OCR/ASR fidelity, metadata, assets/audio, dedup and Q0 escape.
- [ ] Define candidate promotion/rollback and incident-replay addition without tuning on holdout.
- [ ] Define takedown/removal handling that preserves reproducibility lawfully without retaining prohibited bytes unnecessarily.

### Alternatives / failure / security / cost / testing
- [ ] Compare repository/object-store/artifact-release approaches and choose a personal-project maintainable benchmark release method.
- [ ] Define missing benchmark slot, insufficient gold, changed rights, annotation dispute and failed slice behavior; qualification remains absent/limited only for affected capability.
- [ ] Isolate holdout and secrets/rights evidence appropriately.
- [ ] Budget human annotation/adjudication as explicit cost and prefer a small high-quality gold core over large weak labels.
- [ ] Define self-tests proving release immutability, split disjointness, deterministic evaluation and result lineage.

### ADRs / DoD
- [ ] Create ADR for benchmark release method if durable.
- [ ] Artifact distinguishes benchmark architecture from actual benchmark-content bootstrap work and names implementation/bootstrap steps later roadmap must include.
- [ ] Checklist reconciled.

---

## 22. AI and Automation Gateway, Model Governance, and Cost Controls

**Objective:** Centralize model/automation routing so deterministic/cheap paths win by default, stronger models are benchmark-gated, and paid work stops safely at budget/circuit-breaker boundaries.

**Prerequisites:** 03,11,13,14,15,17,18,21.  
**Output:** `Architecture/22-ai-automation-gateway-model-governance-and-cost-controls.md`  
**Downstream:** 23–28.

### Inputs
- [ ] Read product cost/pipeline/security/benchmark/final spec, Architecture prerequisites and current official candidate model/OCR/ASR/provider docs/pricing.

### Decisions
- [ ] Define capability-based automation gateway and deterministic/local/cheap-managed/stronger-model/human escalation ladder.
- [ ] Define provider/model abstraction only where substitution is useful; avoid lowest-common-denominator abstractions that hide capability differences.
- [ ] Define structured request/output schemas, prompt/model/tool/rule versions, source-data isolation and output validation.
- [ ] Define batching, cache keys, deduplication, retry limits, one/escalation caps, confidence/disagreement and human-review handoff.
- [ ] Define benchmark release gates for candidate promotion/demotion and vendor/model substitution.
- [ ] Define paid-job gate, monthly/variable-processing budgets, cost ledger, productive-output attribution, circuit breaker and budget-exhausted defer/provisional behavior.
- [ ] Define external-provider outage/rate-limit/failure fallback without retry storms or silent quality downgrade.

### Research / alternatives / security / testing
- [ ] Use current primary provider/runtime pricing, limits, data-use/security and model capability documentation with access dates.
- [ ] Compare no-gateway/direct calls vs small internal capability gateway and justify the simplest maintainable default.
- [ ] Ensure source prompt injection cannot request tools/policy changes/secrets and models cannot publish/clear rights/security holds.
- [ ] Define evaluation/cost regression tests and per-capability fallback drills.

### ADRs / DoD
- [ ] Create ADR for model-provider abstraction/gateway strategy if durable.
- [ ] Artifact quantifies cheap default and upgrade trigger for each material model-assisted capability.
- [ ] Checklist reconciled.

---

## 23. Security, Privacy, Access, Secrets, Retention, and Threat Model

**Objective:** Validate end-to-end security/privacy/rights boundaries and choose owner access/secrets/retention controls proportional to a private one-owner Corpus.

**Prerequisites:** 02,03,05,06,08,11,12,19,20,22.  
**Output:** `Architecture/23-security-privacy-access-secrets-retention-and-threat-model.md`  
**Downstream:** 24–28.

### Inputs
- [ ] Read product security Stage 15/final spec, design accessibility/content/security page, all prerequisite architecture including secure intake/ops/App/model paths, current primary security guidance.

### Decisions
- [ ] Produce end-to-end data-flow/trust-boundary threat model covering source network/files/archives/media, parsers, models, stores, operations UI, App publication and backups.
- [ ] Choose owner authentication/authorization/session architecture and high-risk action authorization; preserve draft/session-expiry design behavior safely.
- [ ] Define secret/credential/key custody, rotation, least privilege, environment isolation and source-data separation.
- [ ] Define incidental personal-data detection/minimization/redaction and prove Corpus receives no learner data.
- [ ] Define encryption transport/at-rest expectations, security/audit logging and sensitive-log redaction.
- [ ] Define retention, suppression, physical deletion, backup deletion/proof and provenance/audit preservation interactions with rights/takedown/privacy.
- [ ] Define dependency/container/model-artifact supply-chain controls and vulnerability/update policy.
- [ ] Define abuse/rate limits and explicit future security triggers before public submissions, multiple operators, commercial reuse or paid/private crawling.
- [ ] Define incident response proportional to a personal project and residual risks; make no unsupported compliance/malware-safety claims.

### Alternatives / failure / cost / testing
- [ ] Compare authentication/secret/isolation options using current official guidance and operational burden.
- [ ] Define auth provider outage, lost credential/key, compromised source/provider and security-hold recovery.
- [ ] Keep security controls low-ops but do not weaken R3/takedown/secret boundaries for convenience.
- [ ] Define adversarial/threat-model tests and deletion/restore proof consumed by Stage 25.

### ADRs / DoD
- [ ] Create ADRs for authentication, secret/key custody or isolation topology only when durable/cross-cutting.
- [ ] Artifact reconciles Stage 12,19,20,22 assumptions and names changes explicitly.
- [ ] Checklist reconciled.

---

## 24. Observability, Performance, Reliability, Backup, and Cost Operations

**Objective:** Make one owner able to detect stuck/unsafe/expensive work, recover data, understand capability health and operate within bounded performance/cost envelopes.

**Prerequisites:** 03,05,11–14,18–20,22,23.  
**Output:** `Architecture/24-observability-performance-reliability-backup-and-cost-operations.md`  
**Downstream:** 25–28.

### Inputs
- [ ] Read product cost/operations/QA/security, design Health/Run/Cost states, Architecture prerequisites and current platform observability/backup docs.

### Decisions
- [ ] Define structured log/metric/trace correlation for source, run, stage, Item/scope, capability, model job, publication and App bundle without leaking sensitive/source payloads.
- [ ] Define quality/capability health vectors and hard blockers, stuck work detection, queue/backlog age, failure/retry rates and stale publications; no scalar health score.
- [ ] Define practical SLO-style scenarios for owner console, processing throughput, publication freshness and recovery rather than enterprise vanity uptime.
- [ ] Define capacity envelopes for base/high product scale, concurrency/rate controls and graceful degradation under provider/storage/worker outages.
- [ ] Define backup scope/frequency/retention/encryption, restore drills and what can be regenerated vs must be restored.
- [ ] Define cost attribution by stage/provider/capability/productive output, monthly/variable budgets, alerts/gates and abnormal retry/reprocess detection.
- [ ] Define low-ops runbooks for stuck work, provider outage, cost spike, failed restore, stale publication and security/rights blocker.

### Alternatives / failure / cost / testing
- [ ] Compare minimal hosted observability vs self-hosted/heavier stacks with current pricing/retention; choose proportional default.
- [ ] Define telemetry outage behavior so missing monitoring never becomes green health.
- [ ] Keep high-cardinality/source-content logging bounded/redacted.
- [ ] Define load/capacity, backup/restore, alert and cost-envelope tests.

### ADRs / DoD
- [ ] ADR for observability/backup topology only if durable.
- [ ] Artifact provides measurable owner-facing signals matching designed Health/Run/Cost surfaces.
- [ ] Checklist reconciled.

---

## 25. Testing, Evaluation, and Quality Gates

**Objective:** Define a layered proof strategy that catches domain, extraction, model, contract, security, accessibility, migration, cost and recovery regressions before release.

**Prerequisites:** 01–24; hard 17,19,21–24.  
**Output:** `Architecture/25-testing-evaluation-and-quality-gates.md`  
**Downstream:** 26–28.

### Inputs
- [ ] Read all architecture outputs needed by each test family, product benchmark/QA/security/design flows, and current test-tool official docs where choices are mutable.

### Decisions
- [ ] Define unit/domain invariant/property/state-machine tests for six-axis separation, locality, transitions, idempotency, overrides and versioning.
- [ ] Define parser/OCR/ASR/semantic/answer/dedup evaluations using dev/holdout/incident replay discipline.
- [ ] Define schema/contract/migration/taxonomy/publication compatibility tests including App bundle import/removal/revocation.
- [ ] Define security/adversarial tests for intake, prompt injection, authorization, secret leakage, takedown and deletion proof.
- [ ] Define operations UI browser/accessibility/keyboard/focus/responsive tests against design Flows A–H and desktop/read-only boundaries.
- [ ] Define performance/reliability/backup/restore/cost regression tests and failure-injection/recovery scenarios.
- [ ] Define release-blocking vs warning gates by capability/scope so one failed slice does not falsely block unrelated capabilities.
- [ ] Define test data governance so restricted/holdout/source material is handled lawfully and not copied into logs/snapshots casually.

### Alternatives / failure / cost
- [ ] Compare testing levels/tools only where architecture must choose them; prefer deterministic cheap suites before expensive benchmark/model runs.
- [ ] Define flaky/non-deterministic external evaluation handling and reproducibility requirements.
- [ ] Budget full benchmark runs vs targeted changed-capability suites and define when each runs.

### ADRs / DoD
- [ ] ADR rarely required; create only for durable test/evaluation architecture that affects releases broadly.
- [ ] Artifact maps every product/architecture invariant and major failure path to a proof mechanism and owner.
- [ ] Checklist reconciled.

---

## 26. Environments, CI/CD, Release, and Operations

**Objective:** Define reproducible environments and release ordering for code, schema, taxonomy, processing methods/models, benchmark and App contracts with rollback/forward recovery.

**Prerequisites:** 03,05,11,17,19,21–25.  
**Output:** `Architecture/26-environments-ci-cd-release-and-operations.md`  
**Downstream:** 27–28.

### Inputs
- [ ] Read stack/persistence/orchestration/publication/benchmark/model/security/observability/testing outputs and current official deployment/platform docs.

### Decisions
- [ ] Define local/dev/preview/staging/production/benchmark environment needs; avoid duplicate always-on environments without benefit.
- [ ] Define configuration/secrets isolation, deterministic fixtures and safe use of source/benchmark data outside production.
- [ ] Define CI gates and release ordering for application code, infrastructure, schema migrations, taxonomy, model/rule/method versions, analytics and Corpus→App contract/bundles.
- [ ] Define migration/feature-flag/compatibility/rollback or forward-fix strategy and last-known-compatible App publication behavior.
- [ ] Define scheduled jobs/backfills/reprocessing controls, budget gates and deployment interaction with running work.
- [ ] Define backup/restore before destructive migrations and release runbooks/change log/incident procedure.
- [ ] Define dependency/security update cadence and personal-project maintenance burden.

### Alternatives / failure / security / cost / testing
- [ ] Compare simple CI/deploy paths and managed/self-hosted runners based on current official limits/pricing and untrusted-source isolation.
- [ ] Define failed deploy/migration/job/version incompatibility and rollback/recovery without corrupting historical truth.
- [ ] Prevent production secrets/source content from leaking into PR/preview jobs.
- [ ] Keep environment cash cost proportional; define triggers for adding more dedicated infrastructure.
- [ ] Define deployment/migration/rollback smoke tests and release evidence consumed by Stage 27.

### ADRs / DoD
- [ ] Create ADR for deployment topology/release strategy if durable.
- [ ] Artifact operationalizes earlier choices without reopening their semantics.
- [ ] Checklist reconciled.

---

## 27. End-to-End Architecture Validation

**Objective:** Prove the 26 architecture outputs compose coherently across representative source-to-App, failure, rights, security, cost and owner-operation scenarios and repair contradictions before final consolidation.

**Prerequisites:** 01–26.  
**Output:** `Architecture/27-end-to-end-architecture-validation.md`  
**Downstream:** 28.

### Inputs
- [ ] Read every Architecture 01–26 output, current ADR index/ADRs, product final spec/detailed stages, design handoff and Flows A–H, current App boundary architecture.

### Validation
- [ ] Build a concern/ownership/dependency audit and detect cycles, duplicated authority or missing owners.
- [ ] Walk Design Flow A discover→capability publication including partial answer extraction and App impact.
- [ ] Walk Flow B scoped reprocessing with retained curated overrides, changed method, budget gate and partial repeat failure.
- [ ] Walk authenticity uncertainty, rights/takedown, duplicate/re-recorded independence, taxonomy migration, benchmark regression and source-control/security flows.
- [ ] Prove official-but-reference-only, disputed-answer/local-capability, 20-mirror/one-occurrence and script-vs-acoustic-independence scenarios.
- [ ] Prove stable IDs/revisions through reprocessing, taxonomy migration, analytics recompute and App publication.
- [ ] Prove rights-only removal differs from trust/correctness invalidation and takedown blocks mirror re-ingestion.
- [ ] Prove SSRF/archive/active-content/prompt-injection boundaries prevent unsafe source authority/tool use.
- [ ] Prove App last-known-compatible behavior during Corpus outage and no-decision-grade-pattern cases with no learner-data ingress.
- [ ] Prove benchmark failed slice blocks only applicable capability/scope and budget exhaustion defers expensive work safely.
- [ ] Prove owner can complete designed operations, drafts, R0–R3 actions, keyboard paths and <900 read-only behavior without raw DB edits.
- [ ] Prove backup/reproducible/ephemeral/suppressed/deleted categories and restore/deletion semantics.

### Corrections / testing / DoD
- [ ] Amend earlier architecture artifacts/ADRs when validation finds a contradiction; document authority and do not patch only Stage 27 text.
- [ ] Re-run App contract compatibility check against current App `main` and record any new mismatch.
- [ ] Confirm every product/design invariant has an architecture owner and Stage 25 proof method.
- [ ] Confirm cost/security/privacy/rights/reliability/accessibility implications are coherent end-to-end.
- [ ] Artifact records passed/failed scenarios, corrections made, residual risks and implementation deferrals.
- [ ] Checklist reconciled only after corrected earlier artifacts are committed.

---

## 28. Final Architecture Specification and Implementation Roadmap

**Objective:** Consolidate the validated architecture into the single authoritative implementation-facing Corpus architecture and a phased vertical roadmap without losing stage detail or product traceability.

**Prerequisites:** 01–27.  
**Output:** `Architecture/28-bestehen-corpus-architecture-specification.md`  
**Downstream:** implementation.

### Inputs
- [ ] Read every Architecture 00–27 output, every current ADR, final/detailed Corpus product sources, current design handoff, current App boundary architecture and complete checklist.

### Consolidation decisions
- [ ] Produce authoritative C4-style context/container/component and deployment views consistent with accepted ADRs.
- [ ] Consolidate bounded contexts/modules, data ownership/stores, canonical identity/revision model, pipeline/jobs/state machines and reprocessing.
- [ ] Consolidate six axes, uncertainty/locality, rights/takedown, identity/independence, QA/capability publication and analytics semantics.
- [ ] Consolidate secure intake, document/OCR, media/ASR, semantic/model gateway, benchmark qualification and threat model.
- [ ] Consolidate Corpus→App provider contract, bundle/API/file compatibility, change propagation, outage and learner-data prohibition.
- [ ] Consolidate operations-console architecture/design traceability, accessibility, audit, owner controls and health vectors.
- [ ] Consolidate observability, reliability, backup/restore, cost budgets/gates, testing/release gates and environments/CI/CD.
- [ ] Create ADR index summary with superseded decisions preserved.

### Implementation roadmap
- [ ] Define vertical implementation slices ordered by dependency and risk rather than component silos; each slice has entry/exit proof and rollback/defer behavior.
- [ ] Include explicit bootstrap work for lawful acquisition/annotation/release of `corpus-benchmark-1.0.0` before automated production qualification claims.
- [ ] Identify critical path, parallel-safe implementation work, migration/bootstrap sequence, App integration checkpoint and operations-console minimum usable slice.
- [ ] Carry forward open questions, empirical calibration work, cheaper fallbacks, security/legal escalation triggers and deferred future scope without presenting them as already solved.

### Final validation
- [ ] Produce final source/design/ADR/architecture traceability matrix and verify no product invariant is left to implementation invention.
- [ ] Verify final spec contains no framework/vendor/schema contradiction with accepted earlier stages; if it does, fix the owning earlier artifact/ADR first.
- [ ] Verify no learner data, public launch scope, enterprise machinery, universal ready flag or live App inference dependency has been introduced.
- [ ] Verify cost design still targets personal-project scale and names measured upgrade triggers.
- [ ] Re-fetch the complete checklist and reconcile all 28 sections against committed artifacts.
- [ ] Record any remaining `Deferred — architecture/implementation decision:` and `Blocked — owner decision required:` items precisely; do not mark them complete by wording around them.

---

# Global Architecture Completion

The architecture-shaping workflow is complete only when all applicable stage items above are checked or explicitly documented as a genuine blocker/implementation deferral and the following are true:

- [ ] `Architecture/01` through `Architecture/28` exist and are internally consistent.
- [ ] Every checked item is supported by a committed architecture artifact or ADR.
- [ ] The ADR index is current and superseded decisions are preserved.
- [ ] Six truth axes remain independent across persistence, processing, analytics, UI and App contracts.
- [ ] Unknown/local/provisional/disputed states and capability-scoped eligibility remain first-class.
- [ ] Corpus→App remains pattern-first, learner-data-free and compatible with the current accepted App boundary.
- [ ] Untrusted inputs cannot become active authority or bypass security preflight.
- [ ] Rights/takedown, curated overrides, metric-specific independence and audit survive replay/reprocessing.
- [ ] `corpus-benchmark-1.0.0` architecture/bootstrap path exists and no unqualified automation is represented as production-proven.
- [ ] Personal-project cash, review-time and operational budgets have enforceable architecture gates/fallbacks.
- [ ] Design Flows A–H, desktop/read-only responsive behavior and WCAG 2.2 AA obligations have architecture support and test coverage.
- [ ] Backup/restore/deletion/reproducibility semantics are explicit and tested in the architecture plan.
- [ ] Stage 27 end-to-end validation has no unresolved architecture contradiction.
- [ ] Stage 28 is the authoritative implementation-facing architecture specification and roadmap.
