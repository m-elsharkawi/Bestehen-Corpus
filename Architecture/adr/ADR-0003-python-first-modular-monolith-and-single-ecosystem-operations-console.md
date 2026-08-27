# ADR-0003 — Python-first modular monolith and single-ecosystem operations console

- **Status:** Accepted
- **Date:** 2026-08-27
- **Owning architecture stage:** Stage 03 — Technology Stack and Repository Strategy
- **Supersedes:** None
- **Superseded by:** None

## Context

Corpus product truth fixes what the system must do but deliberately leaves the technology open. Corpus Stage 17 §7.3 lists the database, object storage, API transport, queue, crawler, parser/OCR/ASR runtimes, model vendors, admin UI technology, deployment topology, cache, analytics engine, telemetry stack and CI mechanism as intentionally open architecture decisions. Nothing in shaping selects a language.

The reuse policy makes the choice unusually explicit. `Architecture/00-app-implementation-tooling-and-account-reuse-policy.md` §2 and §4 state that reuse is strongest for infrastructure and provider relationships, not for the programming language, that Python is a first-class option that may be selected end-to-end without being treated as an exception, and that the winner is the option with the lowest total owner cost rather than the greatest code reuse with Bestehen / App. ADR-0001 sets the reuse-first decision order and the burden of proof on every additional runtime, deployable, control plane and vendor. ADR-0002 makes the Corpus → App boundary a one-way publication of immutable artifacts, which means the two products share no importable code in either direction. Stage 02 CTX-D07 fixes the reuse context as GitHub/Actions, the existing two-VM Coolify boundary, Pangolin private ingress, container packaging, PostgreSQL, Cloudflare R2 EU and the existing AI/STT account relationships. Stage 02 CTX-D08 and §17.6 require a stack that runs as bounded batch work on that containerised boundary without needing an always-on service.

The workload is decisive and not a general web application. Corpus ingests PDFs, scans, images, DOC/DOCX, HTML, archives and audio; performs page- and region-selective OCR with layout preservation; performs selective ASR with coarse-to-fine alignment; runs deterministic structure, fingerprinting, deduplication and analytics over a design centre of 20,000–50,000 canonical Items; and presents a dense, owner-only, WCAG 2.2 AA operations console of roughly 41 surfaces. Corpus Stage 14 §3.3 makes cheap deterministic and local processing the default and budgets stronger-model escalation at ≤10% of newly accepted unique records; Corpus Stage 15 §4.3 and Stage 08 §5.16 require a **local** processing route whenever rights do not permit raw source expression to leave the boundary. A local capability is therefore a rights requirement, not only an economy.

Choosing between a Python-first Corpus, a TypeScript-first Corpus that reuses App's runtime and tooling, and a hybrid with a bounded second-language processor is an architecture decision with consequences for Stages 05, 11–15 and 20–26. It needs a durable record.

## Decision

Bestehen / Corpus SHALL be built on **one primary language and runtime — the Python 3.14 line** — packaged as a **modular monolith** and operated with a **single-ecosystem, server-rendered operations console**.

Specifically:

1. **One primary runtime.** Python, pinned to an exact patch of the 3.14 line, with one environment, dependency and lockfile workflow. No Node.js runtime is added to Corpus for symmetry with App, and no second language runtime is introduced without a superseding ADR.
2. **Modular monolith, three entrypoints, one image.** One Python distribution containing a framework-free domain, contracts and application core plus capability packages, built into one OCI image with three process entrypoints: the owner console, a bounded batch worker that drains queued work and exits, and a one-shot migration runner. No service-per-domain and no per-pipeline-stage deployable.
3. **No always-on requirement.** No product promise depends on a Corpus process being up. The console may idle or be stopped; batch work becomes backlog, which is a normal deferred state; only the published artifact store must be durably readable by App, and that is object storage rather than a Corpus process.
4. **Single-ecosystem operations console.** The owner console is server-rendered semantic HTML produced by the same Python application, with partial swaps and a bounded amount of hand-written progressive-enhancement JavaScript. Corpus introduces no second frontend ecosystem, no JavaScript build pipeline and no npm dependency tree. Design `.dc.html` artifacts and their support runtime remain read-only reference inputs and never become production technology.
5. **Reuse everything operational.** GitHub and GitHub Actions, the existing two-VM Coolify deployment boundary, Pangolin private ingress, OCI packaging, PostgreSQL, the Cloudflare R2 EU account and the existing Gemini and OpenAI account families are reused, with separate least-privilege Corpus resources and credentials inside those accounts. Selecting Python is not a vendor or account deviation and creates no new billing relationship.
6. **Local-first processing capability.** The stack MUST retain a local, permissively licensed route for document parsing, OCR and ASR so that deterministic and local work can remain the first tier and so that rights-restricted material can be processed without external egress. External processors remain optional, deferrable and benchmark-gated.

This ADR does **not** decide: the ASGI framework, template engine or client library; the SQL access layer, migration tool or driver; the job-table design or any substitutable PostgreSQL-backed job library; the concrete parser, OCR, ASR, layout or model libraries; the physical schema, bucket layout or jurisdiction; the console's information architecture, component inventory or authentication mechanism; the publication packaging or signature algorithm; or the final environment and release topology. Those are stage-local selections recorded in `Architecture/03-technology-stack-and-repository-strategy.md` and owned by Stages 05, 11–15, 19–20 and 22–26. It authorises no provisioning of any account, resource, database, bucket, credential, image or deployment.

## Alternatives Considered

### TypeScript-first Corpus on Node.js, reusing App's runtime and tooling

The most obvious option and the one the reuse instinct favours: one language across both products, one set of tooling habits, one advisory feed, direct familiarity with App's package boundaries and CI shape. Its runtime lifecycle is not a weakness — Node 24 and 22 are current LTS lines.

It is rejected because the processing ecosystem gap is real, one-directional and documented by the projects themselves. Mozilla describes PDF.js as a platform for parsing and rendering PDFs, not for structured extraction; tesseract.js states that it does not support PDF files and does not modify the recognition model, and refers users elsewhere for those needs. A TypeScript-first Corpus can close that gap only by shelling out to the same C/C++/Python binaries — which reintroduces a second ecosystem with worse integration than choosing it deliberately — or by routing OCR and ASR to paid providers by default. The second path fails hard gates rather than merely costing more: Corpus Stage 15 §4.3 and Stage 08 §5.16 require a local route when rights forbid external processing of raw source expression; Architecture 01 P6 makes local and deterministic work the first tier; Stage 14 §4.1 budgets ≤10% stronger-model escalation; and QA-CST-01 caps paid variable processing at ≤€3 per 1,000 canonical Items. Under Stage 01 §8.1, rights and correctness outrank convenience, so the option is vetoed independently of any weighted score.

The expected reuse benefit also turns out to be smaller than it looks. ADR-0002 makes the product boundary an artifact publication, so there is no module either product could import from the other. App owns learner identity, coaching, Readiness and a learner-facing design system; Corpus owns provenance, rights, extraction, deduplication and capability eligibility. Sharing a language would have shared operational habits, not code — and those habits transfer to Python unchanged: frozen lockfile installs, pinned toolchains, deterministic fake adapters, non-root read-only images, named blocking CI gates.

### Hybrid: Python processing core with a TypeScript console

Credible, and rejected only for now. It would be justified if the console genuinely required a JavaScript component framework, but the design contract is dense semantic tables, drawers, split panes, focus management, live-region announcements and inline SVG charts with table alternatives — none of which is easier to make correct in a component framework, and all of which benefit from the reading and tab order being the DOM order. A second runtime would add a second lockfile, a second advisory feed, a second build, a second container concern and a second failure mode for a user interface that one person uses. Reopen only on measured evidence: a launch-required interaction that server-rendered HTML plus bounded scripting cannot make accessible, or repeated accessibility regressions attributable to the approach.

### A new managed platform: document-AI service plus serverless runtime

Evaluated to show why it is not justified rather than to short-list it. It would add a new vendor, a new billing relationship, per-page pricing on exactly the operation Corpus intends to perform locally, an availability dependency where CTX-D08 has deliberately removed one, and a weaker exit than portable files and SQL. ADR-0001 requires a measured Corpus-specific blocker before a new vendor; none exists.

### No deployed service: owner-workstation scripts only

The cheapest option and not viable as the launch shape, because Corpus Stage 13 requires a governed operations surface with append-only audit, override precedence, safe scoped actions and no raw-row editing, which scripts cannot enforce. It is retained as the cheapest degraded fallback if capacity or cost pressure ever demands it.

### Batteries-included Python framework instead of a thin one

A framework supplying ORM, migrations, forms, sessions and CSRF in one dependency would reduce assembly work for a solo owner, and its release line carries a longer support guarantee. It was rejected at stage level, not ADR level, because its largest wins do not apply here — its admin interface is not an acceptable operations surface under Corpus Stage 13 §5.10, its authentication layer is not needed at launch, its ORM-shaped modelling works against the explicit constraints the six-axis evidence model requires, and touching its models would force every batch command to import a web framework. This ADR fixes the language and the shape; the framework selection remains a replaceable stage-local choice.

## Consequences

Positive:

- the processing work that dominates Corpus can be done locally, deterministically and cheaply, keeping paid escalation a bounded exception and keeping a lawful route open for rights-restricted material;
- no always-on process is required by any product promise, which is the largest single operations and cost saving available;
- one ecosystem end to end: one lockfile, one advisory feed, one build, one image, one set of CI gates;
- every operational relationship stays shared with App — one control plane, one ingress model, one relational technology, one object-storage account, one CI system, one secret-custody practice — so reuse is preserved exactly where it is expensive to duplicate;
- the batch surface is a command, so the same code path serves scheduled work, owner-triggered work, benchmark replay and local development.

Negative and operational:

- the owner maintains two language ecosystems across the two products, meaning two dependency-update routines and two security-advisory feeds; this is a real recurring attention cost, not a rounding error;
- a thin framework means CSRF, session integrity and form binding become explicitly owned code rather than framework defaults, and must be tested as such;
- container images carry OCR language data, media tooling and model artifacts, so builds are larger and slower and consume more CI minutes than an application-only image;
- licence care is required: the local document toolchain has AGPL-licensed neighbours that must be routed around or explicitly accepted, and the PostgreSQL driver is LGPL, which is acceptable for a self-operated non-distributed service but must be recorded;
- no code is shared with App, so any convention that should be common must be maintained deliberately in both places.

Exit and evolution:

- the artifacts are portable: standard Python, reviewed SQL, PostgreSQL, an OCI image, S3-compatible objects and immutable published files. Nothing about the language choice binds Corpus to a host, a control plane or a vendor;
- a later move to a second runtime, an always-on service, a broker, a search engine or a managed OCR/ASR default requires a superseding ADR with measured evidence, and may never weaken the rights, correctness, benchmark or accessibility gates.

## Product / Design Traceability

- Bestehen-Shaping/corpus/17-bestehen-corpus-product-specification.md — §1.5, §4.13.2, §7.3, §8.1
- Bestehen-Shaping/corpus/08-ingestion-and-extraction-pipeline.md — §4.5, §4.6, §4.11, §5.16
- Bestehen-Shaping/corpus/13-operations-and-review-experience.md — §1.2, §3.1, §3.4, §3.5, §5.10
- Bestehen-Shaping/corpus/14-cost-scale-and-automation.md — §3.1, §3.3, §4.1, §4.9, §4.13, §4.16
- Bestehen-Shaping/corpus/15-security-privacy-and-abuse-boundaries.md — §3.3, §3.10, §4.3, §4.5
- Bestehen-Shaping/corpus/16-initial-corpus-benchmark.md — §4.12 regression layers the stack must be able to replay
- Bestehen-Corpus/Design/DESIGN-HANDOFF.md — §4 product-truth contract, §6 component contracts, §7 responsive rules, §8 accessibility contracts
- Bestehen-Corpus/Architecture/00-app-implementation-tooling-and-account-reuse-policy.md — §2, §3, §4, §5, §9, §10
- Bestehen-Corpus/Architecture/01-architecture-charter-and-quality-attributes.md — P6, P7, P8, P12, QA-CST-01, QA-OPS-01, QA-A11Y-01, §8.1
- Bestehen-Corpus/Architecture/02-system-context-and-product-boundaries.md — CTX-D01, CTX-D07, CTX-D08, CTX-D09, §10, §11, §17.6
- Bestehen-Corpus/Architecture/03-technology-stack-and-repository-strategy.md — STK-D01 to STK-D14
- Bestehen-App/Implementation/Personal/02-provider-service-setup/handoff.md and docs/setup/personal/ — reused infrastructure reality and readiness caveats

## Cost

The decision adds **no fixed subscription and no new billing relationship**. Its cost dimensions are: owner attention for a second dependency-update routine and advisory feed; longer container builds and larger images carrying OCR, media and model artifacts, consuming private-repository CI minutes from the existing plan allowance; and object storage for evidence, publication and backup inside the reused Cloudflare account.

It removes the dimension that would otherwise dominate: paid OCR per page and paid ASR per audio minute as the default processing route, together with the provider availability dependency that would accompany them. At the base envelope, Corpus-specific recurring cash is dominated by paid processing rather than infrastructure, so keeping that processing local is the largest cost lever available at this stage.

The cheapest safe fallbacks are, in order: defer low-information-value work; reduce acquisition rather than add capacity; keep fields unknown, broader or provisional; run the worker on demand instead of on a cadence; and operate the pipeline as owner-invoked commands with the console stopped. None weakens a rights, security, correctness, benchmark or accessibility gate.

Upgrade triggers are measured, not anticipatory: another host only after a high-value backlog stays more than fourteen days behind for two consecutive cycles with compute proven as the bottleneck; a managed OCR/ASR default only for a slice that repeatedly misses its benchmark gate locally while the paid route passes at acceptable cost; a second runtime only on demonstrated console inaccessibility.

## Security / Rights / Privacy

Keeping a local processing route is a **rights control**, not a convenience: Corpus Stage 15 §4.3 permits external processing only when rights, minimisation, budget and secret-isolation gates all pass, and Stage 08 §5.16 requires local processing or derived abstractions otherwise. A stack that could not process locally would convert a rights boundary into a capability gap.

The modular monolith keeps the untrusted-input boundary explicit: the intake package that handles Z0 → Z1 material is a separate module that runs with the narrowest credentials and performs no semantic decision, and no capability package may import it to reach the network. Source content is data everywhere: it is never executed, never rendered live in the owner context, and never permitted to reach a control that sets a status.

Single-ecosystem packaging narrows the supply-chain surface to one lockfile, one advisory feed and one image, with pinned system packages, checksummed model artifacts referenced by digest as part of the recorded method version, an SBOM at build time, a blocking critical-severity advisory audit against the exact lock, and a non-root read-only container. Secrets live only in the deployment platform's locked runtime variables and the owner's protected ledger; distinct Corpus values are used everywhere, and no credential is shared with App merely because the accounts are shared.

The console remains owner-only behind private ingress with no public surface of any kind. Because the chosen framework does not supply them, CSRF protection and session integrity are explicitly owned obligations with negative tests, recorded as a residual risk rather than assumed.

## Validation

- **Benchmark qualification.** Local OCR, ASR and extraction are qualified per slice against the Stage 16 gold, holdout and incident-replay layers before any capability claim. Ecosystem availability is not qualification; until Stage 21 releases the benchmark, every capability is `not qualified`, which is distinct from failed.
- **No-always-on proof.** A downtime exercise in which every Corpus process is stopped, showing that App continues from published artifacts, that queued work resumes idempotently, and that no product promise was violated.
- **Boundary enforcement.** Import-contract checks in CI proving that the domain, contracts and application packages import no web framework, ORM, provider SDK or network client, and that intake is not reachable from capability packages.
- **Reproducibility.** A locked install that fails when the lockfile is stale, an empty-database migration run, and an image built from an exact commit and a digest-pinned base.
- **Cost.** Measured paid variable processing per 1,000 newly processed canonical Items against the ≤€3 target, with the local-versus-paid share reported by modality, once real volume exists.
- **Accessibility.** Automated and manual checks over rendered console HTML covering keyboard operation, focus outcomes after partial swaps, announcement politeness, no-colour state identification, 200% reflow and table alternatives for every chart.
- **Capacity.** Stage 26 measurement of VM headroom for OCR and ASR batches before the existing boundary is confirmed at the base envelope.

## Supersession Notes

None. A future ADR may supersede this decision only on measured evidence — for example a benchmark result showing the local processing ecosystem cannot meet a required gate at acceptable cost, a demonstrated console requirement that server-rendered HTML plus bounded scripting cannot make accessible, or a capacity finding that the existing containerised boundary cannot host this stack. Any successor must preserve the reuse-first order of ADR-0001, the one-way asynchronous publication boundary of ADR-0002, and the requirement that no always-on Corpus process is needed for any product promise.
