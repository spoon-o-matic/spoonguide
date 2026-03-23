# AI Terms — SpoonGuide Glossary

**Last modified:** 2026-03-23  
**Version:** 1.0 — Initial glossary for user reference and internal tracking of technical language decisions

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial glossary. Core AI/LLM terms, SpoonGuide-specific terms, internal tracking notes. |

---

This glossary serves two purposes:

1. **For users:** Plain-language definitions of AI and LLM concepts so you can build fluency with how these tools work.
2. **For maintainers:** Tracks our decisions about which technical terms to keep vs. eliminate in SpoonGuide user-facing materials. Ensures consistent treatment across the project.

---

## Core AI / LLM Terms

Terms we intentionally use in user-facing materials to build fluency. On first use per document, add an explanatory parenthesis or link here.

### LLM
**Definition:** Large Language Model — the type of AI that powers tools like Gemini, Claude, ChatGPT, and the models in Cursor. It reads and generates text by predicting what comes next based on patterns in the data it was trained on.

**Why we use this:** "LLM" is standard industry terminology. Teaching users this term helps them recognize it elsewhere and understand they're using the same class of technology across platforms.

### Context / Context Window
**Definition:** The AI's "working memory" for a conversation — everything it can actively consider when generating a response. Each platform limits how much text (measured in tokens) can fit in this window. When the conversation exceeds that limit, earlier content may receive less reliable attention.

**Why we use this:** Understanding context limits explains why the handoff protocol exists and why starting a fresh session with your Context Bridge improves reliability.

### Token / Token Budget
**Definition:** A token is a unit of text the AI processes — roughly a word or part of a word. Token budget refers to how many tokens the AI can hold in its context window at once. Your Patient Log, conversation history, and the AI's instructions all consume this budget.

**Why we use this:** Users encounter token limits (e.g., "context length exceeded") when using LLMs. Knowing what a token is reduces confusion and helps users make choices about what to include in a session.

---

## SpoonGuide-Specific Terms

### Patient Log
**Definition:** Your personal file that holds your Profile and all your Session Logs. The coach uses it to understand your history and tailor support. You keep it on your device and paste it into the chat when you start a session.

**Relationship:** Patient Log = Profile + all Session Logs. The Profile is at the top; each Session Log is a new entry added over time.

### Profile
**Definition:** The stable facts about you at the top of your Patient Log — medications, triggers, contraindications, care access, baseline capacity, and similar information. It changes only when something meaningful changes (e.g., a new medication, a newly identified trigger).

### Session Log
**Definition:** A record of what happened in a single coaching session — topics covered, interventions discussed, symptom patterns flagged, coach observations. Each session produces one Session Log entry, which you add to the bottom of your Patient Log.

**Relationship:** Your Patient Log is the accumulation of all your Session Logs plus your Profile.

### Context Bridge
**Definition:** The block of text the coach generates at the end of a session that you paste at the **start** of your next session. It summarizes where you left off, active intervention trials, open questions, and critical context to carry forward — bridging the gap between sessions so the AI starts with full context.

**Why we use this:** "Context" teaches the LLM concept; "bridge" conveys that this piece connects sessions across the gap. The name does both.

### Handoff
**Definition:** The process of capturing everything important from a session so the next session can start with full context. When you trigger a handoff (by saying "handoff," "new chat," or "session summary"), the coach generates three parts: your **Profile** updates, your **Session Log** entry, and your **Context Bridge**.

**Low-energy handoff:** If you're too tired for the full handoff, say "low energy handoff" — you'll get your Context Bridge only. A note will remind you to fill in the rest when you have more capacity.

---

## Internal Tracking: Jargon We Eliminate

These terms are **not** used in user-facing SpoonGuide materials:

| Term | Replacement | Rationale |
|------|-------------|-----------|
| Layer 1 / 2 / 3 | Profile, Session Log, Context Bridge | Architectural labels with no intrinsic meaning; cognitively taxing to map |
| Frontmatter patch | Profile update | Technical; users don't need to know the format |
| YAML / frontmatter | "The top section of your Patient Log" / "your Profile section" | Format name irrelevant to user tasks |
| Context block | Context Bridge | Replaced by semantic name |

---

## Internal Tracking: Technical Terms in Non-User-Facing Docs

These may appear in parameters documents, architecture specs, or developer notes where technical precision is appropriate. They are not used in GETTING_STARTED or platform guides without a gloss or link to this glossary:

- **Frontmatter** — The YAML section at the top of the Patient Log file.
- **Token budget** — May appear in parameters document; add gloss on first use if in patient-facing sections.
