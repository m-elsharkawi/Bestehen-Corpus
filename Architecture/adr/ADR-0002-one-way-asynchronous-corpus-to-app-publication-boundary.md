# ADR-0002 — One-way asynchronous Corpus → App publication boundary

- **Status:** Accepted
- **Date:** 2026-08-27
- **Owning architecture stage:** Stage 02 — System Context and Product Boundaries
- **Supersedes:** None
- **Superseded by:** None

## Context

Corpus product truth fixes what crosses the Corpus → App boundary but deliberately leaves how it crosses open. Corpus Stage 12 defines a capability-oriented, pattern-first contract in which Corpus returns use eligibility rather than ingredients, and states explicitly that its capability catalogue describes "conceptual product capabilities, not mandated endpoints." Corpus Stage 17 §7.3 lists API transport — REST, GraphQL, RPC, shared data, bundle or otherwise — as an intentionally open architecture decision. Corpus Stage 01 Rule 9 requires that stable exam intelligence normally be generated offline and reused, and Corpus Stage 17 §1.5 states that Corpus is not an always-on AI service. Corpus Stage 15 §3.11 limits App to consuming published contract outputs, with no access to raw source storage, ingestion queues, operator controls, secrets or arbitrary database writes.

All of that is satisfiable by more than one architecture. A synchronous Corpus capability API that served only precomputed snapshots would satisfy every product rule above while still creating an always-on authenticated Corpus service, a request surface that could drift toward learner-specific parameters, and an availability dependency between two products operated by one person. Choosing between that and a one-way asynchronous publication boundary is therefore an architecture decision, not a restatement of product truth, and it governs Stages 19, 23, 24, 26, 27 and 28.

The accepted Bestehen / App counterpart has already fixed the consumer side as bundle-first asynchronous pull with signed immutable capability artifacts, a signed publication index, independent version axes, atomic promotion and a deny-by-schema learner-field boundary. App architecture constrains the current counterpart interface but cannot define Corpus semantics, so the provider-side boundary still needs its own decision.

## Decision

The only product boundary between Bestehen / Corpus and Bestehen / App SHALL be a **one-way, asynchronous publication of precomputed, capability-scoped, eligibility-carrying artifacts that App pulls on its own schedule**.

Specifically:

1. Corpus publishes complete, versioned, immutable artifacts to a private publication channel. App discovers and pulls them asynchronously. Corpus initiates no call into App.
2. Corpus exposes **no synchronous App-facing query, capability or inference surface** at launch, and no always-on service is required for App to consume Corpus output.
3. Corpus accepts **no inbound request, command, callback or write path from App**. App holds a read-only, least-privilege credential scoped to published artifacts.
4. **No learner data crosses in either direction**, and no Corpus output is parameterised by an individual learner. A conceptual App "pattern request" is resolved by App locally against imported Corpus intelligence.
5. Corpus availability is **not** on any App critical path. Corpus may be entirely stopped without any App effect beyond the age of the last imported artifact.
6. Every published artifact carries the governance context that makes it usable without reconstructing Corpus rules: provenance summary, confidence, rights and action eligibility, difficulty and relevance, QA readiness, independence, currentness, and the governing version axes. Exact source expression is exceptional and separately rights-gated.
7. Rollback is a **new** publication naming a prior still-eligible artifact. An artifact identity is never reused with different content, and an older publication never rewinds a consumer.

This ADR does **not** decide the packaging format, serialisation, canonicalisation rule, signature algorithm, transport product, storage layout, partitioning strategy, publication cadence, freshness objective, version-negotiation mechanism, or the expedited path for rights and correctness impacts. Those belong to Stage 19, with key custody and operations in Stages 23 and 26. It also authorises no provisioning of any channel, bucket, credential or key.

## Alternatives Considered

### Synchronous Corpus capability API

An authenticated Corpus service answering capability requests from App. It offers the freshest possible propagation of changes and a single place to enforce eligibility. It is rejected at launch because it requires an always-on authenticated Corpus service with rate limiting, retries, monitoring and an implied availability posture; it puts Corpus availability on App's path unless App caches everything anyway, which reproduces the publication model with extra machinery; and it creates a request surface whose parameters would face continuous pressure to become learner-specific. It also contradicts the accepted counterpart without a product-contract justification.

### Shared database or direct table access

Cheapest to start and rejected outright. It exposes Corpus internals as a de facto contract, forces App to reconstruct rights, trust, deduplication and eligibility rules that Corpus owns, breaks silently on internal migration, and makes a Corpus outage an App outage.

### Manual file exchange

Simplest possible mechanism, retained only for one-time fixtures. Rejected as the product boundary because mutable, unaudited files cannot support version compatibility, withdrawal propagation, impact classes or replay.

### Hybrid live API plus published artifacts

Deferred rather than rejected. It would add a second contract, a second incident path and a second security surface before any measured need. Reconsider only when a measured operator drill-down or latency requirement cannot be met by partitioning and local indexes.

## Consequences

Positive:

- no always-on Corpus service is required by any product promise, which is the largest single operations and cost saving available at context level;
- Corpus and App fail independently in both directions;
- there is no request surface into which learner data could leak;
- publication is replayable and auditable: the same artifact identity always means the same content;
- Corpus may change its internals freely as long as published meanings remain compatible.

Negative and operational:

- Corpus becomes a signing authority and inherits private-key custody, rotation and revocation duties that no Corpus product document anticipated;
- withdrawal latency is bounded by publication cadence plus consumer polling, so rights and correctness impacts need an expedited publication path and measurement;
- publishing complete artifacts can transfer redundant bytes until capability partitioning is tuned;
- provenance drill-down for App is limited to what is published, by design.

Exit and evolution:

- artifacts remain portable files with digests, so the transport location and storage provider can change without changing artifact meaning or identity;
- adding a query surface later remains possible, but requires measured evidence, a superseding ADR, and it may never become a learner-runtime dependency or carry learner data.

## Product / Design Traceability

- Bestehen-Shaping/corpus/12-corpus-app-contract.md — §1.2, §1.3, §3.1–§3.6, §4.12–§4.15
- Bestehen-Shaping/corpus/17-bestehen-corpus-product-specification.md — §1.5, §4.11, §7.2, §7.3
- Bestehen-Shaping/corpus/01-product-mission-and-boundaries.md — §3.2, §3.6, Rule 9, Rule 10
- Bestehen-Shaping/corpus/15-security-privacy-and-abuse-boundaries.md — §3.1, §3.11
- Bestehen-Shaping/app/28-bestehen-app-product-specification.md — §1.1, §14.2
- Bestehen-Corpus/Design/DESIGN-HANDOFF.md — §4 product-truth contract; Design page 07 cross-flow guarantee "No learner data, ever"
- Bestehen-Corpus/Architecture/01-architecture-charter-and-quality-attributes.md — P5, QA-AVL-01, QA-PERF-02, QA-APP-01
- Bestehen-Corpus/Architecture/02-system-context-and-product-boundaries.md — CTX-D05, §7.2, §8, §12
- Bestehen-App/Architecture/10-corpus-integration-compatibility-cache-and-rights.md — ARCH-S10-D01 to D10, ADR-0017
- Bestehen-App/Architecture/12-api-contracts-jobs-events-and-idempotency.md — Corpus import idempotency and sequence rules

## Cost

The boundary adds no fixed subscription. Its cost dimensions are artifact bytes produced and stored, duplicate transfer until partitioning is tuned, retained artifact generations, and owner time for key custody and publication review. It removes the recurring cost of an always-on authenticated service, its monitoring and its availability posture.

The cheapest safe fallback is lower publication frequency with App-curated content on the consumer side. It is never live per-request Corpus access, and never a weakened rights, eligibility or accessibility gate.

## Security / Rights / Privacy

The boundary is outbound-only and read-only from the consumer's side. App receives no Corpus write capability, no raw source store access, no operator surface, no secrets and no unpublished or quarantined material. Only capability-eligible, non-reconstructive output crosses by default; exact source expression is exceptional and separately rights-gated per action.

Corpus holds the publication signing material; App holds only public verification material and a read-only transport credential. A shared symmetric secret is rejected because it would give the consumer forging power and blur incident attribution. Rights withdrawal and takedown propagate as published impacts that stop downstream use; a rights change is never expressed as a trust or correctness change.

## Validation

- A downtime exercise in which Corpus is entirely stopped and App continues from its imported artifacts with no learner-visible effect.
- Negative boundary tests: no learner-data field is accepted anywhere; no App write or enumeration beyond the published scope succeeds; artifact identity reuse with different content is treated as an incident, not an update.
- Compatibility tests: an artifact the consumer cannot interpret is withheld with a stated reason rather than downgraded.
- Impact tests: a rights or correctness withdrawal reaches consumer denial within its risk-class objective, measured rather than assumed.
- Replay tests: republishing from retained inputs and governing versions reproduces the same artifact meaning or explains the difference.

## Supersession Notes

None. A future ADR may supersede this boundary only after measured evidence that asynchronous publication cannot meet an accepted requirement — for example a rights-withdrawal objective unreachable by expedited publication, or an operator drill-down need unmeetable by partitioning. Any successor must preserve the learner-data prohibition and must not place Corpus on a learner-runtime path.
