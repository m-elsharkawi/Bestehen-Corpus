# Bestehen / Corpus — Architecture Decision Records

This directory contains lightweight durable Architecture Decision Records (ADRs) created by the numbered Corpus architecture stages.

## When to create an ADR

Create an ADR only for a durable decision with meaningful cross-stage consequences, for example:

- primary persistence/storage strategy;
- content-addressing or stable-identity strategy;
- pipeline orchestration model;
- execution-isolation / secure-processing boundary;
- deployment topology;
- Corpus → App publication/contract style;
- operations UI architecture;
- model-provider abstraction / automation gateway;
- benchmark release method.

Do **not** create an ADR for every checklist item. Stage-local decisions belong in the stage Markdown artifact. When a durable decision changes, add a new ADR that supersedes the old one; do not delete or rewrite decision history.

## Numbering

Use sequential names:

`Architecture/adr/ADR-0001-short-title.md`

Before assigning a number, inspect this directory on current `main` and choose the next unused number. Do not create competing ADRs with the same number in parallel.

## ADR template

```markdown
# ADR-NNNN — Short Decision Title

- **Status:** Proposed | Accepted | Superseded | Deprecated
- **Date:** YYYY-MM-DD
- **Owning architecture stage:** Stage XX — Title
- **Supersedes:** ADR-NNNN or None
- **Superseded by:** ADR-NNNN or None

## Context

What durable architecture uncertainty had to be removed? Which product/design constraints and prior architecture decisions govern it?

## Decision

State the chosen architecture decision precisely, including scope and what it does not decide.

## Alternatives Considered

Summarize credible alternatives and why they were not chosen.

## Consequences

Record positive consequences, negative consequences, operational burden, migration/exit implications, and downstream stage impact.

## Product / Design Traceability

List exact shaping/design/architecture source paths that constrain this decision.

## Cost

Record recurring cash, variable processing, human-review/maintenance implications, cheaper fallback, and upgrade trigger where relevant.

## Security / Rights / Privacy

Record trust-boundary, least-privilege, rights/takedown, retention or privacy consequences where relevant.

## Validation

How will the decision be proven: tests, benchmark slices, restore drills, compatibility checks, performance/cost measurements, or other evidence?

## Supersession Notes

If this ADR supersedes or is superseded by another decision, explain the migration/reconciliation required. Historical ADRs remain in the repository.
```

## Index

Stage agents append accepted ADRs here as they are created.

| ADR | Status | Owning stage | Decision | Supersedes |
|---|---|---:|---|---|
| [ADR-0001](ADR-0001-offline-first-reuse-first-operating-model.md) | Accepted | 01 | Offline-first, reuse-first personal-project operating model; minimum operational surface and new-vendor burden of proof | None |

## Workflow rules

- Fetch the current ADR index and target ADR path before writes.
- Use current file/blob SHA for updates.
- Do not run parallel writes against this index.
- Cite the owning stage output and exact product/design constraints.
- Preserve superseded ADRs; update Status/Superseded-by rather than deleting them.
- A checked checklist item that relies on an ADR must link to that ADR from the owning stage output.
