# Architecture Decision Records (ADRs)

This project uses Architecture Decision Records to document significant technical and design decisions. ADRs are written *after* a decision is made—they record what was decided and why, so future contributors understand the rationale and context.

## When to write an ADR

Write an ADR when you:

- Make an architectural choice that affects the system's structure or behavior
- Choose a technology, pattern, or approach that future changes should align with
- Resolve a trade-off that could plausibly be revisited

Small, self-contained decisions (e.g., a minor refactor, a dependency version bump) typically do not need an ADR.

## Which template to use

We provide two templates:

- **`000-adr-template-lightweight.md`** — Use for small, self-contained decisions. Sections: Title, Date, Status, Context, Decision, Consequences. Sufficient when the decision is straightforward and the impact is limited.

- **`001-adr-template-thorough.md`** — Use for significant architectural or clinical decisions. Includes Authors, Problem statement, Decision drivers, Options considered, Rationale, and Links. Use this when the decision affects patient safety, system architecture, or long-term maintainability.

## Status values

- **Proposed** — Under discussion, not yet decided
- **Accepted** — Decision made and in effect
- **Deprecated** — No longer applicable
- **Superseded by [link]** — Replaced by a newer ADR
