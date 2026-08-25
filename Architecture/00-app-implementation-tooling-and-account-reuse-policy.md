# Bestehen / Corpus — App Implementation Tooling and Account Reuse Policy

> **Status:** Mandatory architecture-workflow constraint  
> **Scope:** Architecture prompts and architecture decisions only — **not implementation or provisioning**  
> **Owner intent:** Reuse the same provider accounts/billing relationships, infrastructure, deployment/network boundary, CI, storage and operating practices already selected for Bestehen / App whenever they fit Corpus. Keep Corpus as simple and cost-efficient as possible. **Corpus may use Python end-to-end if Stage 03 determines that Python produces the simpler/better implementation for document, OCR, ASR, data-processing and ML-heavy work, provided it remains containerized and deployable through the existing Coolify environment.**

## 1. Core rule

Bestehen / Corpus and Bestehen / App are separate products but one personal project operated by one owner. The default architecture should reuse existing accounts, infrastructure and control planes instead of opening duplicate subscriptions or creating a second operations ecosystem.

This is a planning constraint. Architecture stages may research, compare and recommend. They must **not** provision resources, create accounts/projects/tenants/keys/buckets/databases, enter dashboards, deploy, rotate credentials, make live provider calls, or write production configuration/code.

## 2. What “same tools and accounts” means

Reuse is strongest for **infrastructure and provider relationships**, not for forcing Corpus into the same programming language.

The current App implementation/runbook family is:

| Concern | Reuse baseline | Corpus default |
|---|---|---|
| Source control / CI | GitHub + GitHub Actions | Reuse; no second CI SaaS |
| Deployment/control plane | Existing two-VM **Coolify** boundary | Reuse before paying for another host/control plane |
| Private ingress/network | **Pangolin / Newt** | Reuse owner-only private ingress; no public admin console by default |
| Containers/local runtime | Docker/Compose/OCI-compatible processes | Reuse packaging/deployment approach |
| Application language/runtime | App uses Node.js 24 + TypeScript | **Not binding for Corpus. Stage 03 must compare TypeScript and Python as first-class options. Python may be selected for the whole Corpus if it reduces complexity or materially improves the parsing/OCR/ASR/data/ML toolchain.** |
| Package/tooling | App uses pnpm/Node tooling | Reuse only if TypeScript is selected. If Python is selected, choose one simple pinned Python environment/package workflow in Stage 03; do not add Node merely for symmetry |
| Owner operations UI | App uses Next.js/React | Reuse if it materially lowers total complexity. A Python-native server-rendered/internal UI is allowed if it meets the design/accessibility contract with less operational burden. Do not create two frontend stacks without reason |
| Relational persistence | PostgreSQL 18 + Kysely | Reuse **PostgreSQL technology/infrastructure/account**; Python may use a thin Python PostgreSQL layer selected in Stage 03/05. Prefer separate Corpus DB/schema/user boundary |
| Durable jobs | App uses pg-boss on PostgreSQL | Reuse PostgreSQL-backed job semantics where sensible. If Python is selected, Stage 03/11 may choose the simplest Python-compatible PostgreSQL job approach; do not add Redis/managed queue merely to mirror App |
| Object storage | Cloudflare R2 EU, S3-compatible | Same Cloudflare account/billing relationship; separate Corpus bucket/prefix/credential when rights/security isolation needs it |
| Identity | Auth0 EU Passwordless Email OTP | Same Auth0 account family if auth is actually needed. Compare Pangolin owner access alone first for the internal-only Corpus console |
| Email | AWS SES Frankfurt | Same AWS account/region only if Corpus genuinely needs email; otherwise use none |
| General bounded AI | Gemini Developer API / current App-approved route | Same Google AI account/billing relationship; separate project/key only for least privilege/metering when needed |
| STT/TTS | OpenAI current App-approved routes | Same OpenAI account/project family. Corpus may use STT for source media; TTS is normally unnecessary |
| Optional Polly | `not_admitted` by default | Remains not admitted unless benchmark evidence justifies it |
| Secrets | Existing owner protected-ledger + least-privilege conventions | Reuse custody/rotation approach; never expose identifiers/secrets in GitHub |
| Observability | Existing GitHub/Coolify/VM/provider signals + structured logs/health | No new APM/log/analytics SaaS unless Stage 24 proves it necessary |

The App implementation handoff currently records provider setup as accepted repository/runbook work, **not proof that all live resources are already provisioned**. Later implementation must verify live state before reuse.

## 3. Account and resource reuse order

For every external provider or paid/control-plane dependency:

1. **Use no external service** when deterministic/local/batch work suffices.
2. **Reuse the existing App provider/account/billing relationship.**
3. Reuse an existing resource only when security, rights, auditability, cost attribution and failure isolation remain correct.
4. If isolation is warranted, plan a **separate least-privilege Corpus resource inside the same account**: e.g. database/schema/user, R2 bucket, Auth0 application, API project/key, SES configuration set.
5. Introduce a new vendor/account/subscription only when the stage documents a concrete Corpus-specific blocker, compares reuse fairly, quantifies incremental cash and owner effort, defines an exit, and records the durable decision in an ADR.

“Same account” never means “same credential.” Do not mix App learner data and Corpus source data or grant one product broad access to the other.

## 4. Python is a first-class Corpus option

Stage 03 must compare at least these coherent shapes:

- **Python-first Corpus:** one Python modular monolith/control plane with Python background processing and an internal UI approach that preserves the design; containerized for Coolify; PostgreSQL/R2/provider-account reuse.
- **TypeScript-first Corpus:** reuse App runtime/tooling more directly; add no Python unless a bounded processor demonstrably benefits.
- **Hybrid only if justified:** one primary runtime plus a bounded secondary processor. Hybrid is not the default because two ecosystems increase maintenance.

Select the shape with the lowest **total owner cost**, not the greatest code reuse. Total owner cost includes implementation complexity, parser/OCR/ASR ecosystem quality, testability, package/security maintenance, container size/build time, operational burden, recurring cash, paid model dependence and future exit.

Python is acceptable for the entire Corpus without requiring a special exception if Stage 03 finds it better. The non-negotiable deployment constraint is that the selected runtime can run reproducibly in containers/services managed by the existing Coolify setup and fit the Pangolin/private-ingress boundary.

## 5. Simplicity and cost rules

- Prefer one Corpus primary language/runtime, not a Node+Python split by default.
- Prefer one repository, one relational database technology, one job mechanism, one object-storage provider/account, one deployment control plane and one CI system.
- Prefer batch/offline/on-demand processing over always-on workers when latency is not product-critical.
- Prefer existing VM/container capacity or scheduled worker execution before paying for another always-on service/VM.
- Prefer PostgreSQL queries/materialized projections before Elasticsearch/OpenSearch/vector DB/graph DB/warehouse.
- Prefer content hashes, caching, replay and deterministic parsers before paid AI.
- Prefer local/open-source OCR/ASR/extraction when benchmark quality is sufficient; use Gemini/OpenAI only for bounded benchmark-qualified gaps.
- Treat owner maintenance time as real cost; “free” infrastructure that materially increases patching/recovery burden is not free.
- No new subscription merely for dashboards, feature flags, analytics, queueing, search, cron, secrets or email.
- Every deviation from reuse must state why reuse fails, incremental monthly/variable cost, added operations, security/privacy/rights effect, cheaper fallback and exit path.

## 6. Security and data isolation

- App learner data never enters Corpus.
- Corpus reference-only/prohibited/uncertain source bytes never become App runtime objects merely because both products share an account.
- Use separate database users/databases/schemas, bucket/prefix credentials, API keys/projects, auth clients, environment variables and service identities where least privilege or rights isolation requires them.
- Never reuse a credential solely to save setup effort.
- Never expose provider account IDs, private domains, owner identity/email, VM addresses, keys, tokens, secrets or billing identifiers in prompts/ADRs/examples/logs/GitHub.

## 7. Research/change detection

At every technology/provider-sensitive stage:

1. re-fetch current App implementation handoff/runbook and relevant setup guide;
2. record repository-safe status (`verified`, `owner_pending`, `not_admitted`, replaced, etc.) where available;
3. check current official vendor/runtime docs only for mutable facts that materially affect the decision;
4. do not reopen a provider selection because another provider is fashionable or temporarily discounted;
5. recommend change only when measured Corpus requirements outweigh reuse, simplicity and switching cost.

## 8. Required prompt language

Every Stage 01–28 prompt must include or incorporate:

> **App implementation reuse and no-provisioning rule:** Read `Architecture/00-app-implementation-tooling-and-account-reuse-policy.md` and the current Bestehen / App implementation provider handoff/runbook. Reuse the existing GitHub/Coolify/Pangolin/provider-account ecosystem by default. Prefer no new service, then reuse, then a separate least-privilege Corpus resource inside the same account. A new vendor/account is exceptional and requires measured justification, explicit incremental cost/operations, an ADR and an exit. **The Corpus implementation language is not required to match App: Python is a first-class option and may be selected end-to-end if it is simpler/better, provided the resulting services remain containerized and deployable on the existing Coolify boundary.** This architecture stage must not provision/configure/deploy/create resources/keys, enter dashboards, or make live provider calls.

## 9. Stage output requirement

Every stage touching tooling/providers/hosting/storage/auth/AI/media/security/observability/CI/CD/cost must include:

| Need | Existing App tool/account | Reuse? | Isolation needed | Incremental cost | Decision / reason |
|---|---|---|---|---:|---|

If a new vendor/account is selected, the stage is incomplete until reuse is explicitly rejected with evidence. If Python is selected, it is **not** a vendor/account deviation and needs no exception ADR merely for being Python; Stage 03 must still document why it reduces total complexity/cost.

## 10. What this policy does not decide

This policy does not select the Corpus language, framework, ORM/query layer, job library, OCR/ASR stack or physical resource layout. Stages 03, 05, 11–15 and 20–26 still own those choices. It changes the burden of proof: **reuse infrastructure/accounts, keep the runtime simple, and let the Corpus-specific implementation ecosystem determine whether Python or TypeScript is the better primary language.**
