# Document Audience — SpoonGuide

**Purpose:** Defines which documents are written for which audience. Use this when editing docs to choose appropriate language, technical depth, and framing.

When adding new docs, add them to the appropriate table below.

---

## User-facing (patients)

Plain language. Avoid jargon; when technical terms are needed (LLM, context window, token), add a brief gloss or link to the [AI glossary](ai-glossary.md). Semantic names primary for handoff layers — use "Profile (Layer 1)" not "Layer 1: Profile."

| Document | Notes |
|----------|-------|
| [GETTING_STARTED.md](../GETTING_STARTED.md) | Entry point. Patient log setup, session start, handoff protocol, troubleshooting. |
| [README.md](../README.md) | Project overview, quick links, cautions. Mixed audience (users + contributors). |
| [docs/ai-glossary.md](ai-glossary.md) | AI/LLM terms and SpoonGuide terms. User reference + internal tracking of language decisions. |
| [docs/ai-safety.md](ai-safety.md) | AI risks in health tools. Patient education. |
| [docs/platform-guides/gemini-setup.md](platform-guides/gemini-setup.md) | Platform-specific setup. User-facing portions only; see "Testing notes" exception. |
| [docs/platform-guides/claude-setup.md](platform-guides/claude-setup.md) | Same. |
| [docs/platform-guides/chatgpt-setup.md](platform-guides/chatgpt-setup.md) | Same. |
| [docs/platform-guides/cursor-setup.md](platform-guides/cursor-setup.md) | Same. |
| [templates/patient-log-template.md](../templates/patient-log-template.md) | Patient log template. Patient-facing. |

**Platform guides exception:** Each platform guide has a "Testing notes (developer only)" section at the bottom. That section is developer-facing; use technical language there.

---

## LLM-facing (system prompt / AI instructions)

Loaded as AI system prompt or instructions. Not written for patient reading. Technical precision matters; the AI is the audience.

| Document | Notes |
|----------|-------|
| [docs/parameters/chronic-illness-coach-parameters.md](parameters/chronic-illness-coach-parameters.md) | Full system prompt and behavioral spec. Pasted into Gemini/Claude/ChatGPT/Cursor. Defines handoff output format, session protocols, intervention framework, safety escalation. |

---

## Developer / maintainer-facing

Technical language allowed. Contributors and AI assistants editing implementation or process docs.

| Document | Notes |
|----------|-------|
| [docs/roadmap.md](roadmap.md) | Milestones, deliverables, privacy posture, design principles. |
| [docs/architecture/chronic-illness-coach-architecture-spec.md](architecture/chronic-illness-coach-architecture-spec.md) | Architecture spec (content TBD). |
| [docs/platform-guides/MAINTENANCE.md](platform-guides/MAINTENANCE.md) | Instructions for validating and updating platform guides. |
| [docs/rfc/](rfc/) | Request for Comments. Proposal and design exploration. |
| [docs/adr/](adr/) | Architecture Decision Records. Historical decisions. |
| [CONTRIBUTING.md](../CONTRIBUTING.md) | Contribution process, RFC/ADR flow, clinical accuracy standards. |
| [CODE_OF_CONDUCT.md](../CODE_OF_CONDUCT.md) | Community standards. |
| [LICENSE.md](../LICENSE.md) | License terms. |
| [docs/community-commitment.md](community-commitment.md) | Community and governance. |

---

## Handoff layer naming convention

Across user-facing docs, handoff layers are always referred to as **Semantic Name (Layer N)**:

- **Profile (Layer 1)** — Updates to top of Patient Log
- **Session Log (Layer 2)** — Session record at bottom of Patient Log
- **Context Bridge (Layer 3)** — Paste at start of next session

Use semantic name first. Layer number in parentheses for context. Do not lead with "Layer N:" in explanatory text. In the parameters doc handoff output format, delimiters use the same convention: `--- Profile (Layer 1) ---`, etc.
