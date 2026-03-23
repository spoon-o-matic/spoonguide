# Contributing to SpoonGuide

Welcome. SpoonGuide is a patient community project. Clinical accuracy is as important as code quality—when a change affects what the coaching system says or how it behaves, patient safety is at stake. We appreciate contributions that reflect that responsibility.

## Spec-driven development process

We use a structured flow to keep changes deliberate and well-documented:

1. **RFC (Request for Comments)** — Before building anything non-trivial: what are we proposing and why? RFCs invite feedback and explore the design space. Write an RFC before implementation.

2. **ADR (Architecture Decision Record)** — Once a decision is made, record it. ADRs document what was decided and why. They lock in the rationale for future contributors.

3. **Spec** — For implementations, we produce an exact contract: what are the inputs, outputs, and behavior? The spec is the source of truth.

4. **Tests** — Tests treat the spec as executable. Tests pass when implementation matches spec.

5. **Implementation** — Code follows the spec and tests.

Not every change needs all steps. Small, self-contained decisions may only need an ADR. Large, architectural, or clinical changes need an RFC, then ADR, then spec, then tests, then implementation.

## When to write an RFC vs. an ADR

- **RFC** — Written *before* a decision. Use when proposing new features, changes to coaching parameters or safety language, or changes to the MCP tool surface. RFCs are for exploration and feedback.

- **ADR** — Written *after* a decision. Use when recording why a choice was made. ADRs are for historical record and consistency.

**Which template to use:**

- **Lightweight** — For small, focused decisions or proposals. Examples: adding a new CLI flag, changing a minor API detail, a small UI tweak.
- **Thorough** — For significant architectural, clinical, or safety-impacting decisions. Examples: changing the hard refusal list, redesigning the MCP tool surface, changing the storage model.

See `docs/adr/README.md` and `docs/rfc/README.md` for template details.

## Document audience

SpoonGuide docs serve different audiences — patients, the LLM (system prompt), and developers. When editing documentation, consult [docs/DOC_AUDIENCE.md](docs/DOC_AUDIENCE.md) to ensure you use appropriate language and framing for each document's primary audience.

## Clinical accuracy standards

Any changes to the coaching parameters, hard refusal list, or safety escalation language **require a thorough RFC** with documented clinical rationale. This is not a code style preference—it is a patient safety requirement. Contributors proposing such changes must provide:

- The proposed change and its rationale
- Supporting evidence or references where applicable
- Discussion of risks and mitigations

The maintainers will review these changes with extra care.

## PR process

TODO: PR process, review expectations, and merge criteria will be defined here.

## Local development setup

TODO: Local development setup instructions will be added when the first package ships.

## Code of conduct

By participating in this project, you agree to abide by our [Code of Conduct](CODE_OF_CONDUCT.md).
