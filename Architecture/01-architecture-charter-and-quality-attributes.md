# Bestehen / Corpus — Stage 01: Architecture Charter and Quality Attributes

- **Status:** Accepted architecture charter
- **Date:** 2026-08-25
- **Owning stage:** Stage 01 of 28
- **Applies to:** every later Corpus architecture artifact, ADR, implementation plan, data model, aggregate, index, contract, cache, UI state, test and operational control
- **Durable operating decision:** [ADR-0001](adr/ADR-0001-offline-first-reuse-first-operating-model.md)
- **Implementation status:** architecture only; no production code, infrastructure, account, resource, key, deployment or provider call was created

## 1. Purpose, scope, and non-implementation boundary

This charter defines how later decisions are judged. It removes ambiguity about product boundaries, independent truth semantics, measurable quality priorities, personal-project limits, forbidden shortcuts, decision precedence, graceful degradation, research, ADR use, App implementation reuse, and proof obligations.

Corpus is the exam-data and intelligence product behind Bestehen / App. It gathers and structures broad German A2/B1 exam evidence and publishes governed pattern intelligence. App owns learner identity/state, attempts, coaching, Readiness, original-practice generation, delivery and evaluation.

This stage deliberately does **not** select a language, framework, ORM/query layer, physical database layout, queue library, object layout, OCR/ASR/model stack, provider, endpoint style, deployment topology, backup product, monitoring product or UI framework. Those choices remain with their owning stages and must satisfy this charter.

Normative words are used deliberately:

- **MUST / MUST NOT**: a product, safety, rights, privacy or architecture hard gate.
- **SHOULD / SHOULD NOT**: the default; deviation requires measured evidence recorded in the owning stage.
- **MAY**: an allowed choice, not a commitment.

## 2. Inputs, source cuts, authority, and reconciliation

### 2.1 Repository source cuts

| Repository | Current main commit read | Role |
|---|---|---|
| m-elsharkawi/Bestehen-Shaping | f9a468ee63a4c4c778b1a535e13c419bb50cd703 | Read-only product truth |
| m-elsharkawi/Bestehen-Corpus | 16c7a7c846c5efde1941654301039625e5c6076e before Stage 01 writes | Architecture target; Design read-only |
| m-elsharkawi/Bestehen-App | cb2e9a7a88fc384d9cad155647e4a6acccf6b5c3 | Read-only implementation/integration reference |

### 2.2 Mandatory input manifest

| Repository path | Blob SHA read | Use |
|---|---|---|
| Bestehen-Shaping/corpus/17-bestehen-corpus-product-specification.md | 537b5185313097d043748f9dc9f9fdaf432ee71d | Consolidated Corpus authority |
| Bestehen-Shaping/corpus/01-product-mission-and-boundaries.md | 180900725eefd27ad9b5f50456efdc7dd30b02e9 | Mission, scope, non-goals |
| Bestehen-Shaping/corpus/12-corpus-app-contract.md | 7add217f62118e5abe100680d2e8230a93b8c280 | Pattern-first learner-data-free boundary and compatibility |
| Bestehen-Shaping/corpus/14-cost-scale-and-automation.md | 63fd7e8b8d5239ca1883000c98d058000d5a91a2 | Scale, cost, retry and owner-time guardrails |
| Bestehen-Shaping/corpus/15-security-privacy-and-abuse-boundaries.md | fee944281e46ecb48febd89dec269d5f302c2431 | Untrusted-input, privacy and authority boundaries |
| Bestehen-Shaping/corpus/16-initial-corpus-benchmark.md | b596fe8349ee394fd92ce3ea1ef16ea0ff676770 | Benchmark composition and hard qualification gates |
| Bestehen-Shaping/01_Bestehen_Product_Overview.md | 42f15da945e03f1d8e32dfe010f95aae6b87daa3 | Umbrella Corpus/App purpose |
| Bestehen-Shaping/02_Bestehen_Identity.md | f8799407f7b4a5a657f8c81439425d5a004f4e1c | Trust posture, language and accessible identity |
| Bestehen-Corpus/Architecture/00-architecture-shaping-plan.md | 5c13d2f5d5f6b85c966508a97a9cded6c6f443d5 | Workflow, authority, ADR and research rules |
| Bestehen-Corpus/Architecture/00-app-implementation-tooling-and-account-reuse-policy.md | d93c6084aa6b5603a86fdc080c1f70aa91ca2cc8 | Mandatory reuse/no-provisioning policy |
| Bestehen-Corpus/Bestehen_Corpus_Architecture_Checklist.md | d578cf444c6f0bd56520a7beea6afbcea400f86b | Complete Stage 01 section |
| Bestehen-Corpus/Design/DESIGN-HANDOFF.md | fc573707efcf0c632384dfc1fd45ab6595b11369 | Observable states, interaction and accessibility contract |
| Bestehen-Corpus/Design/Corpus-00-Cover-Principles.dc.html | 607677ae02534c27ce5c42c965e31d10591f4c04 | Six-axis display, principles and scope |
| Bestehen-Corpus/Design/Corpus-09-Coverage-Handoff.dc.html | 29d57384aaa45c199baa400c09688d96eb4c9ff3 | Coverage, launch/deferred boundary and gaps |
| Bestehen-Corpus/Architecture/adr/README.md | b89a4d0b3219f84db07d9159ffcc8f420ddb0e49 | ADR criteria/template before Stage 01 writes |
| Bestehen-App/Implementation/Personal/02-provider-service-setup/handoff.md | f538df5be3ada4c26891e3f4a2ab1d800f244f24 | Accepted provider/runbook baseline and readiness caveats |
| Bestehen-App/docs/setup/personal/README.md | 269542c44492bbd2b6df3492c1e7dea9312530b6 | Safe sequence, isolation, evidence and owner actions |
| Bestehen-App/.env.example | 015c5e1cda1a4cca38162c664e40ed7fa6916958 | Synthetic configuration groups, fake defaults and paid-envelope conventions |
| Bestehen-Corpus/prompts/architecture/01_define_architecture_charter_and_quality_attributes.txt | 3639ebd10f85af2d8e8e1e7d9e6aa82cb57feca4 | Current executable Stage 01 instructions |

### 2.3 Authority and contradictions

The workflow authority order applies: Corpus Stage 17, delegated detailed shaping stages, umbrella overview, identity, design, then App counterpart. Product truth wins over design; App constrains compatibility but not Corpus semantics.

No unresolved product/design contradiction was found. The following current-state wording needed explicit reconciliation:

- The App provider handoff records its accepted candidate as not merged, deployed or service-ready and uses owner_pending/not_admitted evidence. The file is nevertheless present on current App main. Current GitHub branch state is authoritative for file presence; the handoff/setup evidence is authoritative for the narrower claim that repository/runbook acceptance is **not proof of live resources**. Corpus therefore treats the tool/account family as the reuse baseline while requiring later live-state verification.
- Design renders the benchmark as not instantiated and shows 11 of 16 seed slots acquired. Shaping Stage 16 defines a future benchmark contract rather than claiming a released gold/holdout set. Architecture MUST NOT claim production qualification until Stage 21 creates and releases the required evidence.
- Design choices such as 50-row paging, an eight-second R0 undo, and selected desktop-only workbenches are observable design defaults, not backend/runtime mandates. Later architecture may replace an explicitly replaceable choice only while preserving accessibility and safety outcomes.

## 3. Architecture context and product boundary

The normal flow is:

**untrusted external evidence → inert intake and preserved observation → bounded deterministic/local processing → explicit findings and capability-scoped decisions → versioned precomputed pattern intelligence → App-owned original practice**

Corpus MUST NOT become:

- a learner product, learner profile/attempt/Readiness store or coaching engine;
- a public file mirror, generic scraper, public search engine or public submission service;
- a live per-session inference dependency for App;
- the owner of learner-facing generation/evaluation;
- a claim of provider affiliation, official certification or legal certainty.

The normal Corpus → App contract is pattern-first. App may ask for a desired exam/learning pattern, but learner attributes stay in App. Corpus publishes use eligibility and governing context; App must not reconstruct Corpus rights, trust, QA or independence rules.

## 4. Product invariants and calibratable policy

### 4.1 Truths later stages may not reopen

1. **Six independent axes.** Every durable model, projection, aggregate, index, API, cache and UI state keeps separate: source/provenance; authenticity/evidence confidence; rights/usage; difficulty plus Generic-B1/TELC relevance; extraction/QA readiness by capability; content identity/derivative lineage/metric-specific analytical independence.
2. **Unknown is data.** Unknown, disputed, review_required, incomplete, unresolved_dependency, provisional and not_run are explicit. Missing is not false, zero, passed or permission. Not_applicable alone may leave a denominator.
3. **Locality.** A defect blocks or limits the smallest affected scope/capability. Parent state may be inherited and named, but a child cannot become more trusted without local evidence.
4. **Capability publication.** Structure analytics, correctness/scoring, taxonomy, pattern intelligence, exact source reuse and independent prevalence have distinct gates. No universal production-ready field exists.
5. **Observations are immutable.** A new fetch, parse, classification, correction or model output adds a revision/derivation/finding; it does not rewrite what was observed.
6. **Audit is append-only.** Consequential changes record actor class, scope, before/after per affected axis, rationale, versions, links, risk tier and downstream effect. Corrections supersede; they do not erase.
7. **Reruns are replayable and non-destructive.** Curated decisions survive unless a governed later decision explicitly supersedes them. Same inputs and governing versions must reproduce the same result or expose the reason they do not.
8. **Automation proposes.** Rules/models may produce candidates, findings and provisional state; they cannot clear stronger holds, loosen rights, overwrite curated decisions or auto-publish consequential output.
9. **Evidence independence is metric-specific.** Mirrors never increase prevalence. Relationship class, provenance anchor, processing representation and independence contribution remain distinct.
10. **Learner-data-free boundary.** Corpus does not receive learner profiles, attempts or Readiness. App sessions do not trigger live Corpus inference.
11. **External input is untrusted.** Files, URLs, archives, media, extracted text and model output are inert data. Source content has no authority to invoke tools or set state.
12. **Pattern-first App contract.** Known eligible non-reconstructive pattern intelligence is the default output; exact source expression is exceptional and separately rights/capability gated.
13. **One-owner architecture.** Minimum operational surface, explainability, replayability, replaceability and owner recovery outrank hypothetical scale.
14. **No silent hard deletion.** Where stronger legal/privacy/security disposition permits, retired identities remain non-content tombstones and impact records. Required purge wins over reproducibility and is evidenced.

### 4.2 Values later stages may calibrate with evidence

The following are versioned policy, not code constants or immutable topology assumptions:

- low/base/high volume and storage envelopes;
- approximately €3 paid variable processing per 1,000 canonical Items;
- approximately €25 normal monthly Corpus cash and exception bands;
- retry counts, crawl pacing, batch sizes, review sampling and backlog thresholds;
- performance targets, recovery windows and backup/drill frequency;
- benchmark precision/recall thresholds only through an explicit shaping/product change or a later superseding authority—not by quiet implementation convenience;
- model, rule, taxonomy, analytics and relevance thresholds;
- owner-time targets and escalation ratios.

Every output affected by a tunable value records the policy/rule/method version used. A calibration change does not rewrite prior evidence.

## 5. Architecture principles

| ID | Principle | Required consequence |
|---|---|---|
| P1 | Product truth before implementation convenience | Schemas and APIs represent all six axes and uncertainty even when a single boolean would be easier. |
| P2 | Preserve evidence; supersede interpretations | Raw/source observations and audit history are immutable/append-only; corrections and derivations are revisioned. |
| P3 | Capability-local safety | Holds and eligibility attach to the smallest affected scope/capability; unrelated known-valid outputs continue. |
| P4 | Replay before repair | Idempotency, governing versions, input identity, retained overrides and deterministic fakes make failure/reprocessing reproducible. |
| P5 | Offline/precomputed App intelligence | App uses versioned eligible snapshots/capabilities; ordinary learner sessions never wait for Corpus inference. |
| P6 | Cheap deterministic/local first | Reject/defer, hash/parse/rule, local processing and cache/reuse precede bounded paid capability and selective human review. |
| P7 | Minimum operational surface | Prefer a modular single system, one primary runtime, existing control planes and bounded background work; distribute only on measured proof. |
| P8 | Reuse relationships, isolate resources | Prefer the App ecosystem/account family, but use separate least-privilege resources/credentials where learner/source, rights, metering or blast-radius separation requires it. |
| P9 | Failure is not truth | Infrastructure/provider/quota/time-out states are operational facts only; they never become negative corpus assertions. |
| P10 | Explain every consequential decision | A human can trace current state to evidence, rules/methods/models, findings, holds, versions, rationale and supersession. |
| P11 | Benchmark before qualification | Candidate tools/methods remain unqualified until relevant seed, gold, holdout and incident-replay gates pass by slice. |
| P12 | Design outcomes, not runtime mimicry | Preserve observable safety, uncertainty, accessibility and recovery contracts without treating design artifact code as production architecture. |

## 6. Measurable quality-attribute scenarios

Targets below are architecture acceptance criteria. An owning later stage may tighten them. Relaxation requires traceable evidence, preserved hard product gates and, when durable, an ADR/product-authority change.

| ID / attribute | Stimulus and operating condition | Required measurable response | Evidence/fallback owner |
|---|---|---|---|
| QA-COR-01 Correctness | A parser/model/rule/taxonomy/dedup change can alter meaning | Before promotion, all applicable Stage 16 hard gates pass on development gold and frozen holdout; zero accepted Q0 regressions/escapes; no new systematic Q1 class. Otherwise keep last-known-good and hold/review affected output. | Stages 21, 22, 25 |
| QA-COR-02 Meaning-critical fidelity | OCR/ASR/extraction handles answer- or meaning-critical content | At least 99% exact correctness on annotated critical tokens/relations; structural extraction at least 98% precision/97% recall; answer/key/scoring linking at least 99% precision/97% recall; required metadata 100% for a claimed capability. Unlinked/held beats wrong. | Stages 12–15, 21, 25 |
| QA-PROV-01 Provenance integrity | A decision-grade output or App pattern is inspected | 100% resolves through stable identities to source observation(s), governing revisions and derivation/method versions; a broken lineage holds that output rather than fabricating provenance. | Stages 04–05, 17–19, 25 |
| QA-RGT-01 Rights safety | Exact/derivative/direct use is requested or rights change | Zero unsafe reuse upgrades; automatic learner-facing direct reuse has 100% precision on gold; 100% prohibited/takedown cases block affected use; unknown remains review-required. | Stages 08, 17, 19, 23, 25 |
| QA-IND-01 Analytical independence | Mirrors/derivatives enter a prevalence computation | Automatic zero-additional-evidence collapse has at least 99% precision and zero genuinely independent benchmark cases collapsed; exact/reformatted mirror recall at least 97%; unresolved cases contribute conservatively, never as full independent evidence. | Stages 16, 18, 21, 25 |
| QA-SEC-01 Untrusted input security | A URL/file/archive/media/source-text/model-output fixture is hostile or malformed | 100% of the maintained malicious/active-content fixture set is rejected, quarantined or rendered inert before deep processing; zero source-controlled tool/status action; zero secrets/private identifiers in repository, payload logs or rendered evidence. Unsafe work stops. | Stages 06, 12, 15, 20, 23, 25 |
| QA-REC-01 Recoverability | A process, host, queue, database or provider fails during work | No accepted observation/audit/curated decision is silently lost or overwritten. At the base envelope, architecture targets metadata/audit RPO ≤24h, operational metadata RTO ≤4h and full retained-evidence replay/restore RTO ≤48h; restore/replay drills prove this before productive admission. | Stages 05, 11, 24–26 |
| QA-AVL-01 Availability/degradation | Corpus or a paid provider is unavailable | App ordinary sessions continue from last-known-valid compatible Corpus output or an App-curated fallback; no live inference dependency. Corpus shows explicit stale/provider_unavailable scope within five minutes of detection and preserves known-valid outputs. No false corpus assertion is emitted. | Stages 19, 24, 26 |
| QA-PERF-01 Owner interaction | One owner browses/reviews at the base envelope | Provisional architecture target: p95 saved-view/queue reads ≤2s and record drill-down ≤3s; governed background action acknowledgement ≤2s; work lasting more than a few seconds becomes a job with first progress/heartbeat ≤60s; no indefinite spinner. Measure on target deployment and recalibrate without weakening safety. | Stages 03, 05, 20, 24–26 |
| QA-PERF-02 App capability retrieval | App requests precomputed pattern intelligence under normal base load | Provider-side p95 response target ≤1s excluding App network, with no model call or per-learner computation. Unsupported major contract versions fail closed to last-supported snapshot/fallback. Stage 19 may tighten after contract/load tests. | Stages 18–19, 24–26 |
| QA-OPS-01 Operability | Routine steady-state operation at base scale | Routine review/maintenance normally fits approximately 1 owner-hour/week and exception review averages ≤30 minutes/1,000 Items outside gold work; ordinary recovery and curation require no direct database surgery. A failed output is traceable to run, scope, method and cause within ten minutes. | Stages 11, 20, 24–26 |
| QA-A11Y-01 Accessibility | Owner uses keyboard, 200% zoom, no color, reduced motion or assistive technology | Owner console satisfies WCAG 2.2 AA design contract; all states use marker + word + hue; all decisions are keyboard reachable; 200% reflow preserves information; charts have finding sentence and table alternative; automated and manual checks have zero launch-blocking violations. | Stages 20, 25 |
| QA-BEN-01 Benchmark qualification | A capability/method/provider is labeled qualified | A released versioned seed/gold/holdout benchmark exists, applicable per-slice hard gates pass, exact numerators/denominators are reported for small slices, incident replay passes, and insufficient support is not called success. Until Stage 21 instantiates it, status is not qualified, not failed. | Stages 21, 22, 25, 28 |
| QA-CST-01 Cost | Paid mixed-modality processing runs over a rolling ≥5,000-Item cohort | Target ≤€3/1,000 newly processed canonical Items; warning >€3–4; optimize/escalate >€4–5; stop/review >€5 absent documented high-value exception. Paid retries count. | Stages 14, 22, 24, 26 |
| QA-CST-02 Monthly envelope | Forecast/actual Corpus-specific cash grows | Normal target ≤€25/month; amber before forecast breach; pause nonessential paid work above €25; no paid work beyond €50/calendar month without explicit owner override; one-off benchmark/backfill ≤€75 when separately initiated. Local/deterministic work may continue safely. | Stages 14, 21–22, 24, 26 |
| QA-RPL-01 Replayability | The same immutable input and governing versions are reprocessed | Deterministic stages reproduce semantically identical output; non-deterministic/model stages retain request/response schema, model/method version and validation evidence sufficient to explain differences; 100% curated overrides are retained or explicitly superseded. | Stages 05, 11–15, 22, 25 |
| QA-OBS-01 Observability | A capability becomes stale, held, costly or wrong | 100% consequential actions and state transitions have correlation/event identity, affected scope/capability, actor class, before/after axes, governing versions, rationale/cause and downstream effect. Hard blockers remain separate from health vectors. | Stages 11, 20, 24–25 |
| QA-APP-01 Boundary/compatibility | App integrates or contract semantics change | Zero learner-profile/attempt/Readiness ingress; versioned contract and payload revisions remain visible; incompatible major semantics are rejected, not silently reinterpreted; exact-source bytes never cross merely because accounts are shared. | Stages 02, 19, 23, 25, 27 |

## 7. Architecture budgets and personal-project guardrails

### 7.1 Planning envelopes, not growth targets

| Envelope | Canonical Items | Retained raw + derived | Interpretation |
|---|---:|---:|---|
| Low / useful seed | 3,000–8,000 | ≤25 GB | Enough to exercise the pipeline and instantiate the benchmark; not enough to settle many prevalence questions. |
| Base / design center | 20,000–50,000 | 50–150 GB | Optimize architecture, operations, load tests and owner experience here. |
| High / review trigger | 120,000–200,000 | 300–750 GB | Trigger measured topology/storage/throughput review; not an acquisition target and not internet scale. |

Coverage and marginal information value outrank count. Reaching the high envelope does not automatically justify distribution; failing a base-envelope hard quality gate may justify change earlier.

### 7.2 Budget dimensions every cost-sensitive stage records separately

- recurring fixed/semifixed cash;
- paid variable processing by productive canonical Item and modality-specific units;
- storage, retrieval and egress;
- retry, failed and reprocessed work;
- local compute/capacity consumption;
- owner maintenance and review time;
- switching/exit and duplicated-control-plane burden.

The cost denominator is paid variable processing per 1,000 newly processed canonical Items reaching validated or stable limited/provisional state. Shared document/media work is allocated; App generation/evaluation is excluded.

### 7.3 Guardrail behavior

- Budget values live in versioned policy/owner-approved configuration; algorithms read them and outputs record the policy revision. They are never scattered literals.
- At amber, defer low-priority paid enrichment and inspect dedup/cache/media/reprocessing waste.
- At red, pause nonessential paid bulk work. Deterministic/local work and explicitly high-impact benchmark/Q0 cases may continue within a documented exception.
- Budget exhaustion is a normal deferred state, not an incident and never a reason to lower rights, security, correctness or benchmark gates.
- Storage alerts at 150 GB and review at >250 GB or >€10/month do not authorize silent deletion. Retention, rights, evidence and deletion proof decide disposition.
- A service/scale upgrade requires measured inability to meet a hard scenario or lower total owner cost. Promotional pricing alone is insufficient.

## 8. Decision precedence and reusable decision method

### 8.1 Precedence

Hard gates are vetoes, not weighted preferences:

1. **Lawful/rights-safe disposition, security and privacy boundaries.** Unknown rights is not permission; unsafe input stops.
2. **Product truth and correctness.** Six-axis separation, learner-data boundary, immutable evidence, audit and capability locality cannot be traded away.
3. **Benchmark evidence and provenance integrity.** Prefer a smaller/held result over unsupported certainty.
4. **App semantic compatibility and known-valid continuity.** Preserve the pattern-first contract and safe fallback; compatibility never authorizes false Corpus truth.
5. **Recoverability, replayability and explainability.**
6. **One-owner simplicity and maintenance effort.**
7. **Total cost**, including cash, retries, storage and owner time.
8. **Performance, feature breadth and scale convenience** beyond measured requirements.

Within a tier, choose the option with the smaller blast radius and more reversible exit. If two options meet every higher tier, prefer fewer services/runtimes/control planes and lower owner effort; then lower cash.

### 8.2 Decision record

Every material later-stage decision states:

- scope and owning stage;
- governing product/design/ADR constraints;
- alternatives including no-change/no-service;
- applicable quality scenarios and hard gates;
- evidence, assumptions and unknowns;
- effect on each of the six axes and affected capabilities;
- failure/degradation/recovery behavior;
- security/privacy/rights and audit effects;
- App compatibility and learner-data boundary;
- cost dimensions and cheaper fallback;
- App implementation reuse assessment when sensitive;
- validation/benchmark plan, exit and supersession trigger.

A decision that cannot answer these stays provisional/held; it is not silently completed.

## 9. Forbidden shortcuts

The following are architecture violations:

1. one universal ready/valid/trusted/health flag or scalar health score;
2. deriving rights from authenticity/trust, or trust from rights/public reachability;
3. treating source or mirror count as independent evidence or prevalence;
4. merging relationship class, provenance anchor, processing representation and analytical independence;
5. destructive reruns, mutable observations/audit, silent hard deletion, or replacement of curated overrides;
6. learner profiles, attempts or Readiness entering Corpus;
7. App ordinary sessions depending on live Corpus/model inference;
8. automatic publication or removal of a stronger hold from model/rule output;
9. active execution of source files/content, source-controlled tools, unsanitized previews or arbitrary network retrieval;
10. unbounded retries, model voting, paid loops, crawl expansion, concurrency or storage growth;
11. retrying an unchanged deterministic failure without a changed input/dependency/method or explicit operator decision;
12. treating infrastructure/provider failure, timeout, quota or missing object as negative corpus evidence;
13. granting permission because an item is official, public, easy to parse or widely mirrored;
14. copying restricted source expression into App because infrastructure/accounts are shared;
15. speculative microservices, warehouses, search clusters, vector databases, public APIs, multi-tenant auth, collaboration workflows or new vendor accounts for hypothetical scale;
16. a second CI/deployment/observability/queue/email/control-plane subscription when the accepted App ecosystem or no service meets the need;
17. hardcoding recalibratable budgets, thresholds or model/provider claims into identity or irreversible schema semantics;
18. aggregate success hiding a failing provider/modality/section/level/uncertain slice;
19. calling the benchmark qualified before its released gold/holdout evidence exists;
20. weakening accessibility, uncertainty language or safe confirmation because a backend choice is easier.

## 10. Minimum cross-stage language and version semantics

| Term | Required meaning |
|---|---|
| Stable identity | Non-reused identifier for a conceptual entity/observation/pattern. Ordinary metadata correction does not change it; material meaning split may create a successor. |
| Observation | Immutable claim about what was fetched/seen, with source, time and content/input identity. It is never silently edited into a curated interpretation. |
| Revision | Ordered state of the same stable identity. It names cause, previous revision and governing versions. |
| Derivation | Output produced from identified inputs under a method/model/rule/taxonomy/contract set. |
| Method version | Version of deterministic/procedural processing behavior, including parser/OCR/ASR configuration where meaningful. |
| Model version | Provider/model identifier plus Corpus prompt/schema/gateway revision needed to interpret a model-derived result; secrets are excluded. |
| Rule version | Version of policy/decision logic, including budgets, eligibility and classification rules. |
| Taxonomy version | Released meaning/structure of nodes and relationships; assignments may have their own revision. |
| Contract version | Semantic version of the Corpus → App behavior/payload agreement. Major incompatibility cannot be ignored. |
| Finding | Non-authoritative evidence that a state may require review/change. It has severity, scope, capability, producer and versions. |
| Hold | A gate preventing named capabilities/actions for a stated reason and strength. A weaker actor/control cannot clear a stronger hold. |
| Stale | Previously valid output whose dependency/currentness changed. It names cause, affected scope and last-known-valid revision; stale is not false. |
| Provisional | Usable only for explicitly named limited capabilities under uncertainty. It is neither published generally nor failed. |
| Superseded | Historical revision replaced by a named successor; retained for lineage/audit and excluded from current selection unless requested. |
| Disputed | Conflicting assertions are retained; no forced winner without governed evidence. |
| Review_required | Automation lacks authority/evidence for the consequential decision. |
| Incomplete | Known missing required component/scope; not equivalent to false or failed. |
| Unresolved_dependency | Identity/lineage/independence or prerequisite is uncertain and downstream contribution is conservatively bounded. |
| Not_run | Capability/method was never executed; never rendered or counted as success/failure. |
| Not_applicable | Capability genuinely does not apply and may leave its denominator; distinct from unknown. |
| Capability eligibility | Per-capability outcome such as eligible, limited, provisional, held, blocked, not applicable or never assessed, with local/inherited reason and governing revision. |
| Tombstone | Non-content historical identity/status/successor/impact record retained only where rights/privacy/security disposition permits. |
| Snapshot | Immutable, versioned set of known-valid published outputs consumable without live inference. |

State names may be refined by owning stages, but their meanings cannot be collapsed. Every cache/index/materialized projection records enough governing revisions to detect staleness and supersession.

## 11. Graceful degradation and failure ownership

| Failure/constraint | Required response | Forbidden interpretation |
|---|---|---|
| Unsafe/malformed input or security preflight failure | Stop affected work, quarantine/hold smallest safe scope, preserve safe metadata/evidence, require governed override if allowed. | Extraction failure, low confidence or harmless source. |
| Unknown/revoked rights or takedown | Stop affected exact/derivative use immediately; propagate impact; retain only disposition-allowed tombstone/analytics; recompute where needed. | Low trust, temporary provider failure or permission because public. |
| Paid model/OCR/ASR unavailable, quota-limited or over budget | Defer expensive enrichment; continue qualified deterministic/local work; keep prior valid outputs marked current/stale as warranted. | Negative semantic result or permission to lower gates. |
| Parser/method regression | Hold new affected output, retain last-known-good, record finding, replay benchmark/incident cases and compare revisions. | Rewrite prior observations or retry unchanged forever. |
| Queue/process/host/database interruption | Stop unsafe commit boundary, recover idempotently from durable identity/checkpoint, surface operational status and duplicate-prevented outcome. | Source absence, invalid record or corpus incompleteness. |
| Object/source provider unavailable | Preserve prior source observation and last-known-valid derivations; mark retrieval operationally unavailable/stale only where dependency requires. | Deleted/rights-revoked content. |
| Corpus unavailable to App | Serve compatible last-known-valid snapshot or App-curated fallback; disable only affected Corpus-dependent feature if no safe fallback. | Trigger live recomputation or send learner data. |
| Contract major mismatch | Reject semantic reinterpretation; use explicitly compatible snapshot or safe App fallback. | Ignore changed eligibility/status meaning. |
| Partial batch success | Commit/report valid independent units only when atomicity rules permit; enumerate remainder and separately retryable scope. | Whole-batch green success or silent loss. |
| Cost/owner-time saturation | Defer lower information-value work, reduce acquisition, improve cache/dedup or choose smaller corpus. | Add speculative infrastructure or weaken truth gates. |

Known-valid outputs survive unrelated failure. Failure ownership is explicit: source, infrastructure/provider, automation/method, governance/rights, or human decision. A generic error state is insufficient.

## 12. Security, privacy, rights, accessibility, and audit obligations

Every relevant stage MUST address:

- URL redirect/DNS/SSRF/egress policy; type, magic, size, archive expansion and active-content controls;
- inert/sanitized preview with scripts, embeds, forms, iframes, remote fonts and handlers removed;
- prompt-injection and model/tool separation; source text is quoted data and cannot grant authority;
- least privilege, secret/source separation and redaction; no private identifiers in GitHub/examples/logs;
- near-zero personal-data footprint and handling of incidental names/contact details;
- rights action/scope/conditions/attribution, most-restrictive composite behavior, takedown propagation, retention and deletion proof;
- stronger-control precedence from owner exclusion through ordinary block, security hard block and takedown/prevention;
- high-impact actor/rationale/version/scope audit and governed inverse actions rather than audit deletion;
- dependency/model/container/supply-chain evidence and rollback;
- future threat-model trigger before public submissions, multiple operators, commercial reuse, private/paid crawling or public API;
- WCAG 2.2 AA outcomes, no-color semantics, keyboard/focus/announcement/reflow contracts and accessible data alternatives.

Architecture does not claim complete malware safety or legal compliance. It records technical controls, decision evidence, residual risk and escalation ownership.

## 13. Mandatory App implementation and account-reuse assessment

### 13.1 Baseline

The reusable default is the current accepted App implementation/runbook family:

- GitHub/GitHub Actions;
- existing two-VM Coolify deployment boundary;
- Pangolin/Newt private ingress;
- Docker/Compose/OCI-compatible packaging;
- Node.js/TypeScript/pnpm for App, with Python equally eligible for Corpus;
- PostgreSQL/Kysely/pg-boss as App technology reality;
- Cloudflare R2 EU;
- Auth0 EU;
- AWS SES Frankfurt;
- Gemini;
- OpenAI STT/TTS;
- deterministic fake adapters;
- existing protected-ledger/least-privilege secret custody and repository-safe readiness evidence.

This is a reuse and comparison baseline, not proof that any live resource is provisioned or service-ready. Stage 03 must compare coherent Python-first and TypeScript-first Corpus shapes. A hybrid needs measured proof because two ecosystems increase owner burden.

### 13.2 Required decision order

1. no external service;
2. reuse accepted App tool/control plane/account/billing relationship;
3. reuse an existing physical resource only if data, rights, audit, cost and blast-radius boundaries stay correct;
4. otherwise use a separate least-privilege Corpus resource/credential inside the same account;
5. only then consider a new vendor/account.

Same account never implies same database, schema/user, bucket/prefix credential, API key/project, auth client, environment group or service identity.

### 13.3 Reusable assessment template

Every technology/provider-sensitive stage includes and completes this table:

| Need/capability | Existing App tool/account and current repository-safe status | No-service/local option | Reuse relationship? | Separate Corpus resource/credential needed? | Measured blocker/gate | Incremental recurring + variable + owner cost | Failure/degradation and exit | Decision/reason |
|---|---|---|---|---|---|---|---|---|
| Example placeholder only | Name baseline; status verified, owner_pending, not_admitted or unknown—never invent live state | Describe | yes/no | least-privilege boundary | Benchmark/operational evidence | Cash, retries, storage, maintenance | Cheap fallback/export/migration | Provisional/accepted/rejected |

The assessment also answers:

- Could existing VM/container capacity and batch scheduling meet the need?
- Does reuse mix App learner data with Corpus source/reference data or broaden either credential?
- Can usage and cost be attributed separately?
- Are provider inputs permitted by rights/privacy/security policy?
- Can deterministic fakes exercise timeout, quota, malformed, retryable and permanent failure without live calls?
- Is the dependency replaceable through Corpus-owned contracts and exportable data?
- What official mutable fact was rechecked, when, and why did it matter?
- What measured event triggers reassessment?

A new vendor/account is incomplete without explicit reuse rejection, incremental cost/operations, ADR and exit path. Selecting Python is not a vendor exception. No assessment authorizes provisioning.

## 14. Operating-philosophy alternatives and recommendation

| Criterion | Modular/offline-first/reuse-first | Distributed/service-first/new-vendor |
|---|---|---|
| Product fit | Matches finite evidence universe, batch enrichment and precomputed App contract | Optimizes for concurrency/scale not currently required |
| Truth/replay | Easier atomic revision, deterministic replay and one lineage model | Cross-service versioning/partial failure adds proof burden |
| Security/rights | Fewer trust boundaries; separate resources still available | More credentials, egress paths and data copies |
| Availability | Known-valid snapshots decouple App; Corpus downtime is tolerable | Higher component count can add failure modes despite isolation |
| Cost | Reuses control planes/capacity/accounts; paid work remains bounded | Adds fixed subscriptions, duplicated dashboards and owner work |
| Operability | One owner can understand, restore and patch it | On-call/coordination burden exceeds personal-project posture |
| Evolution | Modules can be extracted after measurement | Early distribution makes reversal and local replay harder |
| Best use | Default now | Only a bounded measured capability whose hard gate cannot be met otherwise |

**Recommendation:** adopt the modular/offline-first/reuse-first philosophy in ADR-0001. Start with the minimum operational surface that can preserve product truth and safe failure. The burden of proof is on every additional runtime, deployable, queue/control plane, always-on worker, public boundary, provider and account. This recommendation does not select the final stack or physical topology.

Cheapest fallback: smaller high-value corpus, deferred enrichment, deterministic/local processing, existing capacity, cached/batched work and manual review for rare high-impact ambiguity.

## 15. Research and ADR policy

### 15.1 Research rule

Repository product truth is sufficient for stable mission, semantics, boundaries, quality gates and cost envelopes. Current primary official research is mandatory when a decision depends on mutable pricing, service limits, runtime support, security guidance, file/media support, licensing, regional behavior or model capability. Record title, URL, access date, exact fact used and whether it is documented fact or benchmark hypothesis.

Do not reopen the App provider baseline because of popularity or temporary promotion. Vendor claims do not qualify a parser/model/capability; Corpus benchmark evidence does.

### 15.2 Current official research snapshot

Accessed 2026-08-25:

- GitHub, **GitHub Actions billing**, https://docs.github.com/en/billing/concepts/product-billing/github-actions — documented fact: hosted minutes/storage are plan/meter dependent and self-hosted runner use is not billed by GitHub. Architecture implication: reuse does not mean cost-free; later CI stages must measure underlying capacity and retained artifacts. No runner topology is selected here.
- Cloudflare, **R2 Pricing**, https://developers.cloudflare.com/r2/pricing/ — documented fact at access: charges are separated across stored volume and operation classes, with storage-class retrieval differences; direct R2 egress is documented as free. Architecture implication: later storage decisions must model storage, operations and retrieval rather than use one price headline. No bucket/class/layout is selected here.
- NIST, **SP 800-218 Secure Software Development Framework v1.1**, https://csrc.nist.gov/pubs/sp/800/218/final — official guidance supplies cross-lifecycle secure-development vocabulary. Architecture implication: security proof must span preparation, protection, production and response; it supplements, never overrides, Corpus product security requirements.
- PostgreSQL Global Development Group, **PostgreSQL 18.6 Documentation**, https://www.postgresql.org/docs/18/ — documented current-version reference for the accepted App baseline at access. Architecture implication: later stages must recheck supported-version and upgrade facts; this charter does not select a PostgreSQL layout or require App runtime identity.

Prices/versions above are mutable research observations, not product policy and not hardcoded assumptions.

### 15.3 ADR criteria

Create an ADR only for a durable choice with meaningful cross-stage consequences: persistence, content identity, orchestration, secure execution, deployment topology, publication contract style, operations UI architecture, model gateway, benchmark release method, or an exception to the reuse operating model.

Stage-local thresholds and checklist interpretations stay in the stage artifact. A change creates a superseding ADR; history is not rewritten. ADR-0001 is justified because the operating philosophy and new-vendor burden apply to every later stage. No other Stage 01 ADR is needed.

## 16. Cross-stage proof obligations and downstream requirements

### 16.1 Proof obligations every stage must answer

| Proof family | Required evidence/questions |
|---|---|
| Failure/recovery | What fails, at what smallest scope, what remains valid, what is idempotent, what checkpoint/backup exists, what are RPO/RTO targets, and how are restore/replay/partial success tested? |
| Security/privacy/rights | Which inputs/actors/trust boundaries exist; how are active content, SSRF, archives, prompt injection, secrets, incidental personal data, rights/takedown, retention/deletion and stronger holds controlled and audited? |
| Observability/reliability | Which events, metrics, logs and correlation/version fields prove state; how are hard blockers kept separate; what alert/action owner exists; how are stale and provider failure distinguished from corpus truth? |
| Cost | Fixed, variable, storage/retrieval/egress, retry/reprocess, local capacity, owner time; per-productive-unit denominator; cheap fallback; budget exhaustion behavior; measured upgrade trigger. |
| Testing/qualification | Unit/property/contract/integration/fake/failure-injection/benchmark/holdout/incident/accessibility/load/restore evidence; slice reporting; last-known-good and rollback. |
| Reuse | Completed Stage 13 template, current App handoff status, isolation analysis, no-service option, official mutable fact check and exit. |
| Product/design traceability | Exact invariant/quality-scenario mapping; six-axis/local capability impact; uncertainty and design outcome preserved. |

Every relevant stage records residual risk and names the downstream owner. “Stage 25 will test it” is insufficient unless the owning stage first defines the invariant and observable evidence.

### 16.2 Downstream stage requirements

- **02:** freeze system boundaries, actors, trust/data flows and learner-data prohibition.
- **03:** compare Python-first/TypeScript-first coherent shapes, reuse accepted CI/deployment/network/account ecosystem, and avoid hybrid/new service without proof.
- **04–05:** make six axes, stable identity, immutable observations, revision/supersession/tombstone and governing versions first-class.
- **06–10:** preserve source, confidence, rights, taxonomy/relevance and capability-local uncertainty without cross-axis shortcuts.
- **11–15:** make orchestration/security preflight/extraction/model/QA replayable, bounded, costed and non-destructive.
- **16–18:** model metric-specific independence and analytics sufficiency so mirrors cannot manufacture prevalence.
- **19:** provide precomputed versioned pattern-first capabilities, compatibility/fallback/change impact, no learner ingress and no live inference.
- **20:** implement design-observable state, safe action tiers, append-only audit, accessibility and no scalar health/ready state.
- **21–22:** instantiate/release the benchmark before qualification; gate model/provider escalation by slice and cost, with deterministic fakes.
- **23:** prove end-to-end threat/privacy/rights boundaries and future expansion triggers.
- **24:** implement vector health, correlation, reliability and cost ledger/alerts without inventing corpus truth.
- **25:** build the layered verification matrix and negative/incident/restore/replay/accessibility/load evidence.
- **26:** select minimum deployment/recovery topology, reuse existing boundary by default, and prove base-envelope RPO/RTO/capacity.
- **27:** reconcile requirements, design, App and implementation handoff without changing semantic authority.
- **28:** verify all charter scenarios, ADR exceptions, calibrations, residual risks and implementation deferrals.

## 17. Assumptions, calibration plan, risks, deferrals, and completion

### 17.1 Assumptions requiring later measurement

- Base workload modality mix and the fraction needing OCR/ASR/semantic escalation are not yet measured.
- Existing App VM, account and provider live readiness/capacity is unknown until owner-safe implementation verification.
- QA-PERF and QA-REC numeric targets are provisional architecture objectives; Stages 24–26 must test them on the chosen topology and may tighten or propose evidence-based revision.
- The benchmark/gold/holdout/incident set is not yet released; all tool/provider qualification is provisional/not qualified.
- Provider pricing, included allowances, region/support details and model identifiers can change and must be rechecked at the owning stage.
- Rights classification is operational evidence handling, not legal advice; legal review triggers remain first-class.
- Routine owner-time targets require measurement after backlog and source mix exist.

### 17.2 Unresolved risks

| Risk | Current control | Downstream owner |
|---|---|---|
| Later schema/API collapses axes for convenience | P1, forbidden shortcuts, traceability and contract tests | 04, 05, 19, 25, 28 |
| Benchmark remains too small/uninstantiated | not-qualified state, exact slice counts, incident growth | 21, 25 |
| Shared accounts create cross-product blast radius | separate resource/credential default and reuse assessment | 03, 05, 19, 23, 26 |
| Existing capacity cannot meet recovery/performance | measure at base; bounded extraction/new service ADR only on proof | 24–26 |
| Paid/media-heavy work breaches envelope | cheap-first, cache/dedup, paid gates and defer state | 14, 22, 24 |
| Rights/security deletion harms replay | disposition wins; deletion proof and partial non-replayability recorded | 08, 21, 23, 26 |
| Provider/model drift changes meaning/cost | governing versions, benchmark requalification and current official research | 13–15, 22, 24–25 |
| Owner workload exceeds one-hour posture | value-based acquisition, prioritization, deferred ambiguity and simpler topology | 20, 24, 26 |

No owner decision blocks Stage 01. Later owner actions include approving productive paid envelopes, verifying live resource readiness and accepting any documented hard-ceiling exception.

### 17.3 Implementation deferrals

Deferred — architecture/implementation decision:

- final language/framework/runtime and repository strategy (Stage 03);
- physical persistence/object/job/orchestration/deployment/backup topology (Stages 05, 11, 26);
- acquisition/extraction/model/provider choices and thresholds (Stages 06, 12–15, 22);
- exact Corpus → App delivery mechanism (Stage 19);
- operations UI architecture (Stage 20);
- benchmark instantiation and qualification evidence (Stage 21);
- concrete observability/cost-control and test tooling (Stages 24–25).

These are deliberate ownership boundaries, not checklist blockers.

### 17.4 Stage 01 completion test

Stage 01 is complete when:

- this charter and ADR-0001 are committed on Corpus main;
- every Stage 01 checklist item maps to committed evidence;
- no later-stage technology/topology is prematurely selected;
- the checklist is re-fetched and reconciled using its current blob SHA;
- later stages have measurable quality scenarios, veto/precedence rules, vocabulary, degradation behavior, reuse template, proof obligations, calibration ownership and explicit deferrals.

The selected minimum philosophy preserves product truth while keeping the cheapest safe fallback available: do less, defer expensive ambiguity, use deterministic/local/cached work, reuse accepted control planes/account relationships with isolated resources, and add operational surface only after measured proof.
