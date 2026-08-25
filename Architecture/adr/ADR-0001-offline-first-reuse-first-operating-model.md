# ADR-0001 — Offline-first, reuse-first personal-project operating model

- **Status:** Accepted
- **Date:** 2026-08-25
- **Owning architecture stage:** Stage 01 — Architecture Charter and Quality Attributes
- **Supersedes:** None
- **Superseded by:** None

## Context

Bestehen / Corpus must turn broad German A2/B1 exam evidence into governed pattern intelligence while preserving six independent truth axes, uncertainty, local capability eligibility, immutable observations, append-only audit, replayability, and the learner-data-free Corpus → App boundary. It begins as a single-owner personal project with a 20,000–50,000 canonical-Item design center and tight cash and owner-time envelopes.

The accepted App implementation/runbook already provides an ecosystem that may be reused: GitHub/GitHub Actions, a two-VM Coolify boundary, Pangolin private ingress, container packaging, PostgreSQL, R2 EU, existing provider account relationships, deterministic fakes, and owner secret-custody conventions. Repository acceptance does not prove that any external resource is live. Sharing an account also must not collapse least privilege or mix learner and source data.

A durable operating philosophy is required before later stages choose language, framework, persistence layout, orchestration, deployment topology, or providers.

## Decision

Corpus architecture SHALL use a boring modular, offline-first, replayable, reuse-first personal-project operating model.

The default decision order for every technology or external dependency is:

1. no new service when deterministic/local/batch work is sufficient;
2. reuse the accepted App tool, control plane, or account/billing relationship;
3. reuse a physical resource only when least privilege, data separation, rights, audit, metering, and failure isolation remain correct;
4. otherwise use a separate least-privilege Corpus resource in the same account;
5. introduce a new vendor/account only after a measured Corpus-specific blocker, explicit incremental cash and owner-operations cost, an accepted ADR, and a tested exit path.

The logical shape defaults to one understandable deployable system with bounded background processors and precomputed/published outputs, not a network of independently operated services. Work is batch/offline/on-demand unless a later stage proves a product latency need. Provider/model unavailability must defer work rather than become corpus truth. App ordinary sessions must not require live Corpus inference.

This ADR does **not** select the final language, framework, database/schema layout, job library, object layout, CI runner, cloud topology, model, or provider. Python and TypeScript remain first-class Stage 03 alternatives. It also does not authorize provisioning.

## Alternatives Considered

### Distributed/service-first/new-vendor philosophy

Potential benefits are independent scaling, specialized managed features, and failure isolation at very large scale. It is rejected as the default because current product volume and latency requirements do not justify multiple deployables, queues, control planes, subscriptions, credentials, dashboards, or distributed consistency failure modes. Later stages may introduce a bounded service only when measurements demonstrate that the modular/reuse shape cannot meet a hard quality, security, rights, recovery, or cost requirement.

### App-stack identity by construction

Forcing every Corpus component into the App language and exact physical resources would maximize superficial symmetry. It is rejected because document/OCR/ASR/data-processing tool fit may make a Python-first Corpus simpler, and shared credentials/resources could broaden access or mix learner/source data. Reuse is a control-plane/account default, not a mandate to share code, runtime, database, bucket, or key.

### Fully local/no-provider architecture

This is the cheapest fallback and remains preferred for qualified deterministic/local capabilities. It is not mandatory for every workload because benchmark-critical OCR/ASR/model gaps may justify bounded use of already accepted provider relationships.

## Consequences

Positive consequences:

- minimum recurring operational surface for one owner;
- stronger replayability, cost attribution, and provider replaceability;
- App continuity through precomputed/versioned outputs rather than live inference;
- strong burden of proof against duplicated accounts/subscriptions;
- technology choices remain evidence-driven and compatible with either Python or TypeScript.

Negative consequences:

- some work will be deferred instead of processed immediately;
- one system may need vertical optimization before decomposition;
- shared account relationships require careful separate resource/credential boundaries;
- later stages must document an explicit reuse assessment even when retaining the default.

Exit and evolution:

- modules must expose stable internal contracts and versioned derivations so a measured hot/risky capability can be extracted later;
- provider-specific inputs/outputs must be contained behind Corpus-owned contracts and exportable data;
- a new vendor or service needs a migration/exit plan and cannot be justified by popularity or promotional pricing.

## Product / Design Traceability

- Bestehen-Shaping/corpus/17-bestehen-corpus-product-specification.md
- Bestehen-Shaping/corpus/01-product-mission-and-boundaries.md
- Bestehen-Shaping/corpus/12-corpus-app-contract.md
- Bestehen-Shaping/corpus/14-cost-scale-and-automation.md
- Bestehen-Shaping/corpus/15-security-privacy-and-abuse-boundaries.md
- Bestehen-Corpus/Architecture/00-app-implementation-tooling-and-account-reuse-policy.md
- Bestehen-Corpus/Design/DESIGN-HANDOFF.md
- Bestehen-App/Implementation/Personal/02-provider-service-setup/handoff.md
- Architecture/01-architecture-charter-and-quality-attributes.md

## Cost

Normal Corpus-specific recurring cash remains governed by the approximately €25/month product envelope and paid variable processing by approximately €3/1,000 newly processed canonical Items. Those values are recalibratable product policy, not constants in code or topology.

The cheaper fallback is deferred/local/deterministic processing on existing capacity. A higher-cost service is considered only after a measured quality, backlog, recovery, security, or owner-time blocker, with fixed, variable, retry/reprocessing, storage/egress, and maintenance cost recorded separately.

## Security / Rights / Privacy

Reuse never means shared secrets by default. Corpus must use separate least-privilege database identities, schemas/databases, buckets/prefixes, provider keys/projects, auth clients, and service identities wherever cross-product access, rights isolation, cost attribution, or failure containment requires it. App learner data never enters Corpus. Untrusted external content stays inert and cannot execute or control status-setting tools. Unknown rights never become permission.

## Validation

Every technology/provider-sensitive stage must complete the reuse assessment in the Stage 01 charter. Every exception must show:

- the measured baseline blocker;
- benchmark/operational evidence;
- incremental cash and owner-time cost;
- least-privilege and data-boundary analysis;
- bounded failure/recovery behavior;
- a cheaper fallback;
- an exit/export path;
- an ADR when durable.

Stage 28 must verify that the final architecture did not add a control plane, always-on service, or vendor without this evidence. Implementation qualification must use benchmark slices, failure injection, restore/replay drills, contract compatibility tests, cost-ledger evidence, and deterministic fakes before productive admission.

## Supersession Notes

None. A future ADR may supersede this operating model only after a measured scale, security, recovery, rights, or product-latency requirement demonstrates that the minimum operational surface cannot satisfy a hard gate. Historical rationale and migration obligations remain visible.
