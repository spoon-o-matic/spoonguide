# Request for Comments (RFCs)

RFCs are proposal documents written *before* a decision is made. They invite feedback and explore the design space. In this project, RFCs and ADRs serve different purposes:

- **RFC** — Written before building. Proposes what we might do and why. Invites discussion and alternative ideas.
- **ADR** — Written after deciding. Records what we decided and locks in the rationale.

## When to write an RFC

Write an RFC when:

- **Before building anything non-trivial** — New features, significant refactors, or new subsystems deserve a proposal first.
- **Before changing the coaching parameters or hard refusal list** — Clinical content changes require documented rationale and community input.
- **Before changing the MCP tool surface** — Tool changes affect both the server and any consumers; the contract should be proposed and reviewed first.

Small, focused changes (e.g., a typo fix, a small bug fix with obvious solution) typically do not need an RFC.

## Which template to use

We provide two templates:

- **`000-rfc-template-lightweight.md`** — Use for focused proposals with limited scope. Sections: Title, Date, Status, Problem, Proposal, Alternatives considered, Open questions. Good for targeted changes or additions.

- **`001-rfc-template-thorough.md`** — Use for significant system design, architectural changes, or proposals that affect patient safety. Includes Authors, Summary, Motivation, Detailed design, Drawbacks, Alternatives, Unresolved questions, and Future possibilities. Use when the proposal is substantial enough that someone could implement from the doc.

## Status values

- **Draft** — Work in progress
- **In Review** — Ready for feedback
- **Accepted** — Proposal accepted; implementation can proceed
- **Rejected** — Proposal not accepted
- **Superseded** — Replaced by a newer RFC or ADR
