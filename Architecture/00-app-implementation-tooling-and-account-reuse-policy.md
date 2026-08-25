# Bestehen / Corpus — App Implementation Tooling and Account Reuse Policy

> **Status:** Mandatory architecture-workflow constraint  
> **Scope:** Architecture prompts and architecture decisions only — **not implementation or provisioning**  
> **Owner intent:** Reuse the same tools, provider accounts/billing relationships, infrastructure boundary, and operating practices already selected in the current Bestehen / App implementation whenever they can satisfy Corpus requirements safely. Keep Corpus as simple and cost-efficient as possible.

## 1. Why this policy exists

Bestehen / Corpus and Bestehen / App are separate products, but they are one personal project operated by one owner. The default architecture should therefore **reuse what the App implementation already uses** instead of opening duplicate vendor accounts, subscriptions, control planes, deployment systems, monitoring products, or technology stacks.

This policy is a planning constraint. A Corpus architecture stage may research, compare, recommend, and document how a current App implementation tool/account should be reused. It must **not** provision a resource, create an account/project/tenant/application/key/bucket/database, enter a dashboard, deploy, rotate a credential, make a live provider call, or write production configuration/code.

## 2. Implementation reality is the tooling/account baseline

When deciding tools, providers, deployment/account topology, CI, secrets or operational integrations, read the **current App implementation artifacts**, not only the older App architecture vendor baseline.

At minimum, every technology/provider/account-sensitive Corpus architecture stage must read current versions of:

- `m-elsharkawi/Bestehen-App/Implementation/Personal/02-provider-service-setup/handoff.md`
- `m-elsharkawi/Bestehen-App/docs/setup/personal/README.md`
- the relevant numbered guide under `m-elsharkawi/Bestehen-App/docs/setup/personal/`
- `m-elsharkawi/Bestehen-App/.env.example`
- `m-elsharkawi/Bestehen-App/README.md`
- relevant current `m-elsharkawi/Bestehen-App/Architecture/*.md` for semantic/technical context

If the implementation artifacts and older App architecture disagree about the operational provider/topology, **current accepted implementation reality wins for reuse planning**, unless a Corpus requirement proves that reuse is unsafe or impossible. This does not let App implementation override Corpus product semantics.

The current accepted App implementation setup/runbook establishes this reusable family:

| Concern | Reuse baseline for Corpus architecture | Default planning posture |
|---|---|---|
| Source control / CI | GitHub + GitHub Actions | Same GitHub owner/account/app installation where permissions allow; no second CI SaaS |
| Runtime/deployment control | Existing two-VM **Coolify** boundary | Reuse the same Coolify control/deployment estate before paying for another host/control plane |
| Private ingress/network | **Pangolin** / Newt private ingress and DNS boundary | Reuse the existing owner-only private network/ingress approach; no public admin console by default |
| Runtime | Node.js 24 LTS | Same runtime family and pinned-version discipline unless a parser/media capability has a measured blocker |
| Language | TypeScript | Same language for web/control-plane/domain code by default; introduce another language only for a bounded processor with a concrete ecosystem/quality benefit |
| Package manager / monorepo tooling | pnpm 11 / private workspace conventions | Reuse; no Nx/Turborepo/new package manager without measured need |
| Web UI | Next.js 16 + React | Reuse for the owner operations console unless a simpler implementation can still preserve the design/accessibility contract and materially reduces burden |
| Relational persistence | PostgreSQL 18 + Kysely | Reuse technology; prefer same existing infrastructure/account/host with a **separate Corpus database/schema/user boundary** if capacity/isolation allow, rather than buying another database service |
| Durable jobs | pg-boss on PostgreSQL | Reuse before Redis/managed queue/new broker; separate Corpus queues/tables/credentials logically |
| Object storage | Cloudflare R2, EU jurisdiction, S3-compatible boundary | Same Cloudflare account/billing relationship; prefer separate Corpus bucket or tightly scoped prefix/credential when rights/security isolation requires it; do not open another object-storage vendor by default |
| Identity | Auth0 Public Cloud EU, Passwordless Email OTP | Same Auth0 account/tenant family. Prefer reuse of existing owner identity; use a separate application/client only when callback/audience/blast-radius isolation requires it. If Pangolin owner access alone safely satisfies an internal-only Corpus console, compare that simpler option before adding another Auth0 application |
| Email | Amazon SES, `eu-central-1` | Same AWS account/SES region if email is genuinely required; do not add a second email provider. Corpus should avoid email entirely if the owner workflow does not need it |
| General bounded AI | Gemini Developer API / current App-approved Gemini route | Same Google AI account/billing relationship; reuse project when safe, otherwise separate project/key within the same account only for isolation/metering. No new LLM provider unless benchmarked need proves it |
| STT / TTS | OpenAI current App-approved STT/TTS routes | Same OpenAI account/project family; use separate capability key/project only where least privilege/cost attribution requires. Corpus should use STT only where source-media processing needs it; TTS is normally unnecessary |
| Optional AWS Polly | `not_admitted` by default in App setup | Also not admitted for Corpus unless a later benchmark explicitly justifies it |
| Secrets | Existing owner protected-ledger + least-privilege secret custody conventions | Reuse conventions and provider accounts; never put private identifiers/secrets in architecture artifacts |
| Observability | Structured logs/health plus existing GitHub/Coolify/VM/provider signals; no new APM baseline | Do not add Sentry/Datadog/Grafana Cloud/etc. unless Stage 24 proves the existing signals cannot operate Corpus safely |
| Containers / local dev | Docker/Compose + PostgreSQL, deterministic fake adapters by default | Reuse. Local/CI must not require paid-provider calls |

**Important:** the App implementation handoff says its provider-service setup is accepted as repository execution but not yet live-service-ready. Corpus architecture must therefore describe reuse as **reuse of the accepted implementation tooling/account plan and existing owner infrastructure**, and must verify current live state when later implementation begins. Do not claim an account/resource is provisioned merely because a runbook exists.

## 3. Account reuse rule

For every external provider or paid/control-plane dependency, the default decision order is:

1. **No external service at all** — deterministic/local/batch processing or existing product data is enough.
2. **Reuse the same existing App tool and owner account/billing relationship.**
3. Inside that same account, reuse an existing resource/project when doing so preserves security, rights, auditability, cost attribution and failure isolation.
4. If resource-level isolation is warranted, create the architecture for a **separate least-privilege Corpus resource inside the same account** (for example database, R2 bucket, Auth0 application, API key/project, SES configuration set) rather than a new vendor/account.
5. Introduce a new vendor/account/subscription only if the stage documents a concrete Corpus-specific blocker, compares the existing App option fairly, quantifies added recurring/operational cost, defines an exit, and records the decision in an ADR.

A recommendation to create a distinct resource later is **not permission to provision it during architecture shaping**.

## 4. Simplicity and cost rules

Every stage prompt must enforce these defaults where relevant:

- Prefer one repository, one primary runtime family, one primary relational database technology, one job mechanism, one object-storage provider/account, one deployment control plane and one CI system.
- Prefer batch/offline/on-demand Corpus processing over always-on workers when latency is not product-critical.
- Prefer scaling an existing VM/container vertically or running a worker only when work exists before paying for a new always-on service.
- Prefer PostgreSQL queries/materialized projections before Elasticsearch/OpenSearch/vector DB/graph DB/warehouse.
- Prefer content hashes, caching, replay and deterministic parsers before paid AI.
- Prefer local/open-source OCR/ASR or deterministic extraction when benchmark quality is sufficient; use Gemini/OpenAI only for bounded benchmark-qualified gaps.
- Share billing/account relationships but isolate credentials/data paths where rights/security require it.
- Treat owner maintenance time as real cost. A nominally free self-hosted component that adds material patching/recovery burden can be more expensive than reusing an existing managed/account capability.
- No new subscription merely for convenience, dashboards, feature flags, analytics, queueing, search, cron, secrets, or email.
- Every deviation from reuse must state: why reuse fails, incremental monthly/variable cost, added owner operations, security/privacy/rights consequence, cheaper fallback, and removal/exit path.

## 5. Security and data-isolation rule

Cost reuse never permits unsafe cross-product coupling.

- Bestehen / App learner data must never enter Corpus.
- Corpus source bytes, including reference-only/prohibited/uncertain material, must not become App runtime objects merely because both products share a Cloudflare/AWS/VM account.
- Use separate database users/databases/schemas, bucket/prefix credentials, API keys, auth clients, environment variables and service identities where least privilege or rights isolation requires them.
- Never reuse a credential just to save setup effort when it would broaden access across App and Corpus.
- Never expose provider account IDs, private domains, owner email, VM addresses, keys, tokens, secrets or billing identifiers in prompts, ADRs, examples, logs or GitHub.
- Architecture artifacts may use symbolic references such as `<existing-owner-cloudflare-account>` or `<corpus-r2-runtime-resource>` only when needed.

## 6. Research and change-detection rule

At the start of every technology/provider-sensitive architecture stage:

1. re-fetch the App implementation handoff/runbook and relevant setup guide;
2. record the current App implementation baseline and whether the needed account/tool is `verified`, `owner_pending`, `not_admitted`, replaced, or otherwise changed if repository-safe evidence exists;
3. check current official vendor docs only for mutable facts that materially affect the decision;
4. do not reopen a provider selection merely because another provider is popular or has a temporary promotion;
5. recommend a change only when measured Corpus requirements outweigh reuse, simplicity and switching cost.

## 7. Prompt language that must appear in every Stage 01–28 prompt

Every executable Corpus architecture prompt must include or incorporate this instruction:

> **App implementation reuse and no-provisioning rule:** Read `Architecture/00-app-implementation-tooling-and-account-reuse-policy.md` and the current Bestehen / App implementation provider handoff/runbook before any tooling/provider/account decision. Default to the same tools, existing owner accounts/billing relationships and current two-VM Coolify/Pangolin operating boundary. Prefer no new service, then reuse, then a separate least-privilege Corpus resource inside the same account. A new vendor/account is exceptional and requires measured justification, explicit incremental cost/operations, an ADR and an exit path. This architecture stage must not provision, configure, deploy, create accounts/resources/keys, enter dashboards, or make live provider calls.

Stages with no technology/provider decision still read this policy so they do not accidentally introduce a future dependency that violates it.

## 8. Architecture-stage output requirement

Every stage that touches tooling, providers, hosting, storage, authentication, AI, media, security, observability, CI/CD or cost must include an **App implementation reuse assessment** table:

| Need | Existing App implementation tool/account | Can Corpus reuse it? | Isolation needed | Incremental recurring/variable cost | Decision / reason |
|---|---|---|---|---:|---|

If the selected answer is a new vendor/account, the stage is incomplete until the alternative using the current App implementation baseline is explicitly shown and rejected with evidence.

## 9. What this policy does not decide

This policy does **not** pre-decide the Corpus physical architecture or authorize implementation. Stages 03, 05, 11–14, 20, 22–26 still own their technical decisions. They may choose a bounded exception when Corpus evidence proves it. The policy changes the default and burden of proof: **reuse and simplicity are the baseline; divergence must earn its cost.**
