# Chronic Illness Coach — Open-Source Project Roadmap

**Last modified:** 2026-03-23  
**Version:** 0.1 — Working document

| Version | Date | Changes |
|---------|------|---------|
| 0.1 | 2026-03-23 | Initial roadmap. Design principles, Milestones 0–4. Privacy-first, accessibility as user-controlled option. |

*Framing: privacy-first architecture, accessibility as user-controlled option at each milestone*

---

## Design Principles

These apply across the entire roadmap and should live in the repo README.

### Three Co-Equal Governing Principles

**Accessibility.** The system must be usable by patients with disability, fatigue, cognitive load, and limited technical ability. Accessibility is not a future enhancement or a trade-off — it is a requirement at every tier. Where a milestone does not yet fully serve non-technical patients, that gap is named explicitly and closed as a priority.

**Privacy.** Patients have full control over their data at every tier. A fully local, zero-data-leaving-your-machine option exists at every milestone where data is handled. Hosted or cloud options are always opt-in and always disclosed with plain-language explanation of what the trade-off means.

**User autonomy.** Patients make informed decisions about their own trade-offs. The system does not make those calls for them. Where accessibility and privacy conflict and no design solution is available, the system presents the trade-off transparently and clearly, and the patient chooses. This is not a fallback — it is the principle in action, and it is consistent with the patient autonomy framework embedded in the coaching parameters themselves.

These three principles are co-equal. When they appear to conflict, the first response is to find a design solution that honors all three. When that is not possible, the resolution is informed user choice — not a hierarchy.

### Additional Principles

**Open stack.** No proprietary platform dependencies in the core path. Anthropic API is a dependency, but is interchangeable by design (model-agnostic parameters).

**Solo-developer paced.** Milestones are scoped to be shippable by one developer without burning out.

---

## Milestone 0 — Repository Foundation
*Ships before any functional code*

**What a patient can do:** Nothing yet. This milestone is infrastructure for contributors and future users.

### Deliverables

- Repo scaffolding with clear directory structure (see below)
- `README.md` — project purpose, conditions covered, patient audience, privacy philosophy, current tier, roadmap link
- `CONTRIBUTING.md` — contribution guidelines, clinical accuracy standards, how to propose changes to the parameter document
- `LICENSE` — MIT or Apache 2.0; both are standard for open health tools with no proprietary restrictions. Apache 2.0 includes an explicit patent grant, which is worth considering if the project grows.
- `CODE_OF_CONDUCT.md` — essential for a patient community project; Contributor Covenant is a reasonable base
- Parameter document (`chronic-illness-coach-parameters.md`) committed to `/docs` — immediately usable as a copy-paste Gem/Claude Project system prompt even before Milestone 1 ships
- Architecture spec committed to `/docs`
- Roadmap committed to `/docs`

### Decision Points

- **`CLINICAL_REVIEW.md`** — document the evidence basis for hard refusals and tier classifications. Useful for community trust and contributor accountability. Adds maintenance burden. Include or defer?
- **Pre-release parameter review** — the parameter document is substantive and patient-facing. A lightweight review of the hard refusal list and safety escalation language before public release is worth considering given the audience.

### Suggested Repo Structure

```
/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
└── docs/
    ├── chronic-illness-coach-parameters.md
    ├── chronic-illness-coach-architecture-spec.md
    ├── roadmap.md
    └── clinical-decisions.md          # if included
```

### Privacy Posture
Not applicable — no data handling yet.

---

## Milestone 1 — Tier 1.5: Usable Without Any Setup
*Target user: any patient with a Google / Claude / ChatGPT account*

**What a patient can do:** Use the coaching system today, with no installation, using any major LLM platform. Maintain their own log file manually. Get meaningful clinical coaching within the constraints of a single conversation window.

### Deliverables

- Polished, versioned parameter document in `/docs`
- Patient-facing `GETTING_STARTED.md` covering:
  - How to create a Google Gem / Claude Project / GPT using the system prompt
  - How to start and maintain a log file
  - How to use the handoff protocol
  - What this tool can and cannot do (scope and safety disclosure)
- Log file template (`patient-log-template.md`) in `/templates`
- Platform-specific setup guides in `/docs/platform-guides/`:
  - `gemini-setup.md`
  - `claude-setup.md`
  - `chatgpt-setup.md`

### Decision Points

- **Tier 1.5 parameters long-term status** — three options:
  - Maintained indefinitely as the no-install path (lowest barrier, highest accessibility value)
  - Marked deprecated once Milestone 2 ships (reduces maintenance burden)
  - Actively maintained in parallel with tooled tiers (recommended if non-technical patients are a sustained priority)

### Suggested Structure Addition

```
├── templates/
│   └── patient-log-template.md
└── docs/
    └── platform-guides/
        ├── gemini-setup.md
        ├── claude-setup.md
        └── chatgpt-setup.md
```

### Accessibility Note
This is the most accessible tier — zero installation, works with tools patients may already have. It is the right starting point for non-technical patients and should be maintained as a supported path even as later milestones add more capable options.

### Privacy Posture
Patient data never touches project infrastructure. Data goes only to the LLM platform the patient chooses. Patients should be informed in `GETTING_STARTED.md` that their log content is sent to their chosen LLM provider on each session. No project infrastructure involved.

---

## Milestone 2 — Tier 3a: Local MCP Server
*Target user: technically capable patients and developers*

**What a patient can do:** Run the full MCP-backed coaching system locally. Log entries are structured automatically. Context is managed by tools. Handoff is automated. All data stays on their machine.

### Deliverables

- Local MCP server in `/packages/mcp-server` (Node.js)
- Full tool surface from the architecture spec:
  - `structure_statement` — extracts structured YAML from natural language via Haiku internally
  - `append_log_entry` — validates and persists structured entries
  - `get_patient_context` — assembles token-budgeted context window with filters
  - `patch_frontmatter` — applies partial updates to stable patient data
  - `generate_handoff` — produces the three-layer handoff block
  - `get_session_context` — optimized session-start context assembly
  - `get_active_trials` — lightweight call for open intervention trials
  - `get_autonomy_acknowledgments` — timestamped acknowledgment log
  - `log_session_summary` — persists session-level summary entry
- Log storage: local filesystem, `.md` files per the existing schema
- Claude API integration (Sonnet as reasoning model, Haiku inside `structure_statement`)
- Schema validation for `append_log_entry` (Zod recommended for Node.js)
- `structure_statement` prompt v1 with a small evaluation corpus in `/evals`
- Technical setup guide: Node.js install, API key config, MCP connection to Claude

### Spoongrid Integration: Contract Definition

Even though live Spoongrid integration is not built in this milestone, the **data exchange format is defined here**. This creates the integration contract both apps can build toward without requiring Spoongrid to be complete.

Define a `SpoongridDailySnapshot` schema covering:
- Date and entry metadata
- Up to 16 "Ingredient" scores with labels and values (-50 to +50)
- Bucketed grid output (pressures, supports, needs, resources)
- Interventions planned or taken
- Environmental factors noted

This schema lives in `/packages/mcp-server/src/types/spoongrid.ts` and is the canonical contract. The Spoongrid app builds its export toward this shape; the MCP server consumes it.

Also add a `get_spoongrid_context` tool stub that returns an empty result with a clear not-yet-connected message — this keeps the tool surface consistent and makes integration a drop-in at Milestone 3.

### Suggested Structure Addition

```
├── packages/
│   └── mcp-server/
│       ├── src/
│       │   ├── tools/
│       │   ├── storage/
│       │   ├── prompts/
│       │   └── types/
│       │       └── spoongrid.ts      # integration contract
│       ├── evals/
│       └── README.md
```

### Accessibility Gap
This milestone requires Node.js installation, API key configuration, and comfort with a local development environment. It is intentionally scoped to technical users. This gap is a known limitation, not an acceptable end state — Milestone 3a closes it by delivering the full tooled experience to non-technical patients. The gap should be named clearly in the Milestone 2 README so non-technical patients are directed to wait for or use Milestone 1 in the interim.

### Privacy Posture
Maximum. All log data on local filesystem. Only patient statements and log excerpts leave the machine via Anthropic API. Patients informed at setup. Anonymous patient IDs by default per existing schema.

### Decision Gate: Codebase Relationship (Resolve Before Milestone 3)

Before any app scaffolding is written, decide: **monorepo or separate repos?**

| Option | Pros | Cons |
|---|---|---|
| Monorepo | Shared types and schema in one place; easier to keep Spoongrid data contract in sync; simpler local dev | Couples two apps with different release cadences; contributor scope is larger |
| Separate repos | Independent release cycles; cleaner separation of concerns for open-source contributors | Shared schema must be maintained across two repos or extracted to a shared package; more coordination overhead |
| Separate repos + shared package | Schema lives in a published npm package both repos depend on | Adds a third artifact to maintain; versioning becomes explicit (which may be a feature) |

**Recommendation:** If Spoongrid and the coach are both patient-facing tools you intend to develop in parallel, a monorepo is likely the lower-friction choice. If you expect them to diverge in audience or cadence, separate repos with a shared types package is cleaner long-term.

This decision affects repo structure, CI setup, and how the Spoongrid data contract is maintained. It does not need to be made today — but it must be made before Milestone 3 scaffolding begins.

---

## Milestone 3a — Wraparound App: Manual Spoongrid Integration
*Target user: non-technical patients; Spoongrid users who want to bring their data to the coach*

**What a patient can do:** Use the full MCP-backed coaching system through a simple web interface with no local installation. Export a Spoongrid snapshot and have it automatically inform their coaching session. Choose where their data lives.

### Deliverables

- Lightweight web app in `/packages/app` — minimal UI, chat interface
- Connects to a hosted instance of the MCP server
- **Spoongrid manual integration:** patient exports a daily snapshot from Spoongrid; app ingests it and makes it available to the coach as session context via `get_spoongrid_context`
  - No dependency on Spoongrid's internal architecture
  - Export format follows the `SpoongridDailySnapshot` schema defined in Milestone 2
  - This is the integration path that works regardless of whether a live API exists yet
- **Storage model — two explicit options presented at onboarding:**
  - **Bring-your-own-storage (privacy-first path):** patient authenticates with their own cloud storage (Google Drive, Dropbox, or S3); logs stored there; project server never persists patient data
  - **Hosted storage (accessibility path):** project holds the data, encrypted at rest, with explicit consent and full export/delete capability always available
- Plain-language privacy disclosure at first use — not buried in terms of service
- Patient-facing setup guide for non-technical users

### Privacy Posture
Both options — bring-your-own-storage and hosted storage — are presented at onboarding with plain-language explanation of what each means for data custody. Neither is a default; the patient chooses with full information. This is the co-equal accessibility/privacy/autonomy principle in practice: the system makes both options genuinely usable, discloses the trade-off clearly, and lets the patient decide. The local MCP path from Milestone 2 remains available for patients who want maximum privacy and have the technical capability.

---

## Milestone 3b — Wraparound App: Live Spoongrid Integration
*Dependency: Spoongrid MVP shipped; codebase relationship decided*

**What a patient can do:** Spoongrid data syncs automatically to the coach. No manual export step. Daily Ingredient scores, grid output, and interventions are always available as session context without any patient action.

### Deliverables

- Live sync between Spoongrid and the coach via shared data layer or API
- `get_spoongrid_context` tool fully implemented — returns current snapshot automatically at session start, integrated into `get_session_context`
- Spoongrid data treated as always-available context (equivalent to frontmatter), not a queried resource
- Sync mechanism respects the privacy model: local sync for local-storage users, cloud sync for hosted users

### Architectural note
Because Spoongrid data is always synced rather than queried on demand, the `SpoongridDailySnapshot` schema becomes part of the canonical session context shape — not an optional integration. This is why the schema definition in Milestone 2 matters: it gives both apps a stable contract to build toward independently.

### Privacy Posture
Inherits from Milestone 3a. Sync is local-to-local or cloud-to-cloud depending on the patient's chosen storage model. No new data custody concerns introduced. The automatic sync is designed to improve accessibility — patients with cognitive load or fatigue should not have to remember an export step to get the benefit of their Spoongrid data.

---

## Milestone 4 — Health Data Integration + Pattern Detection
*Target user: all users, delivered as improvements to existing interfaces*

**What a patient can do:** Connect wearables and health platforms. Receive insights grounded in objective biometric data alongside subjective Spoongrid scores. Ask questions like "what triggered my MCAS reactions most often this month" and get answers grounded in their actual data.

### Health Data Integration

**Strategy: target platform aggregators first, not individual devices.**

Apple HealthKit and Google Health Connect already aggregate data from Garmin, Oura, most wearables, and many CGMs. Targeting these two platforms gets broad device coverage without direct vendor partnerships.

- **Phase 1:** Apple HealthKit + Google Health Connect
- **Phase 2:** Dexcom and Libre CGM integrations (both have HealthKit support on iOS; Android path via Health Connect is less complete and may require direct API)
- **Direct device integrations** (Garmin API, Oura API) only if there are meaningful gaps the platform aggregators don't cover

**New MCP tool: `get_health_context(metrics[], date_range, session_intent)`**

Biometric data is queried on demand, not synced in bulk. The reasoning model calls this tool selectively based on what's clinically relevant to the current session — not everything, every time.

Metrics that meaningfully change clinical reasoning:
- **HRV trend + resting HR** — PEM risk signal; can push back on activity plans with data
- **Sleep stages** — confounder the coach currently has to ask about; available automatically if patient has a wearable
- **Orthostatic HR** — can supplement or replace manual orthostatic vitals series
- **Glucose variability** — relevant context for MCAS and fatigue pattern interpretation
- **Activity and step data** — PEM envelope tracking

Patient controls which metrics are shared with the coach. Granular per-metric consent, not all-or-nothing.

### Pattern Detection

- RAG layer over patient log — vector embeddings of log entries, semantic search via enhanced `get_patient_context`
- Pattern detection tools added to MCP server:
  - `find_patterns(symptom?, trigger?, intervention?, date_range?)`
  - `summarize_trigger_history`
  - `compare_intervention_outcomes`
- Clinical knowledge base as retrieval source (NICE guidelines, Bateman Horne resources, EDS Society criteria) — open-licensed sources only
- Provider report generation: structured summary of log + biometric data formatted for a clinical appointment

### Privacy Posture
Biometric data is queried from patient-controlled sources (HealthKit, Health Connect) with explicit per-metric consent. No biometric data is persisted by project infrastructure beyond what the patient's chosen storage model already holds. Embedding generation for RAG requires sending log content to an embeddings API unless run locally — a local embedding option should be offered for the privacy-first path. This is a meaningful technical challenge and may be staged within Milestone 4.

---

## Milestone 5 — Outcomes + Community
*Long-term; requires community traction and governance framework*

**What a patient can do:** Opt in to contributing anonymized outcome data to a shared research pool. Access aggregated pattern insights from the broader patient community.

### Deliverables

- Opt-in anonymized data contribution with explicit, specific, revocable consent
- Outcome analytics dashboard
- Community pattern insights

### Prerequisites
This milestone should not be built until a clear data governance framework is in place. Depending on how contributed data is used, IRB consideration may be appropriate. This is likely a collaboration milestone — not a solo-developer deliverable.

### Privacy Posture
Opt-in only, with zero data leaving any patient's control without explicit consent. Full data governance framework required before build begins.

---

## Health Data Integration: Phased Approach Summary

| Phase | What's integrated | Mechanic | Dependency |
|---|---|---|---|
| Milestone 2 | Spoongrid (contract only) | Schema definition, tool stub | None |
| Milestone 3a | Spoongrid (manual) | Patient exports snapshot; app ingests | Spoongrid export feature |
| Milestone 3b | Spoongrid (live sync) | Automatic sync at session start | Spoongrid MVP + codebase decision |
| Milestone 4a | HealthKit + Health Connect | On-demand query by session intent | Platform OAuth integration |
| Milestone 4b | CGM (Dexcom, Libre) | Via HealthKit where possible; direct API as fallback | HealthKit phase complete |
| Milestone 5 | Aggregated community data | Opt-in anonymized contribution | Governance framework |

---

## AI Safety Disclosure Framework

### Why This Exists

This tool uses AI to support health coaching. AI can be genuinely useful for this — but it carries real risks that guardrails alone cannot eliminate. Patients deserve to understand those risks clearly, in plain language, before they rely on this tool. This section defines what the disclosure says, where it appears, and how it is delivered across milestones.

This is not a legal disclaimer. It is patient education, written for people with cognitive load, fatigue, and complex health situations — and it must be brief enough to actually be read.

---

### The Tiered Disclosure Structure

**Tier 1 — Always visible, very short**
Appears at every entry point: README, GETTING_STARTED, app onboarding, session start. Three to four plain-language sentences covering the core risk. Includes a "learn more" link to the Tier 2 document. Requires a one-time acknowledgment in the app UI; passive in text-based contexts.

**Tier 2 — Full plain-language explanation**
A standalone document (`/docs/ai-safety.md`) covering each failure mode with a brief plain-language explanation and a concrete example relevant to this patient population. Linked from Tier 1. Written to be readable by someone with brain fog — short paragraphs, plain language, no jargon. Includes links to Tier 3 external resources.

**Tier 3 — External resources**
Links to credible external writing on AI limitations in healthcare for patients who want to go deeper. Curated and reviewed for quality.

---

### Tier 1 Text (canonical — use at all entry points)

> **Before you use this tool, please read this.**
>
> This is an AI coaching tool, not a medical provider. It can make mistakes — including confident-sounding mistakes. It may agree with you when it should push back. It may not know enough about your specific conditions to give you accurate information. Use it to support your thinking and your care team conversations — not to replace them.
>
> [→ Learn about AI risks in health tools (2 min read)](#)

*The link targets `/docs/ai-safety.md`. In the app UI, this is presented before the patient can begin their first session, with a simple "I understand" acknowledgment. It reappears as a brief banner at the start of subsequent sessions until the patient opts to hide it.*

---

### Tier 2 Document Outline (`/docs/ai-safety.md`)

The following covers the full set of known failure modes relevant to this tool and population. This is the author's guide for writing the document — the document itself is written for patients, not developers.

**1. AI can be confidently wrong (hallucination)**
AI generates responses that sound authoritative even when the information is incorrect or invented. This is not rare — it is a documented, ongoing limitation of all current AI systems. In a health context, a confident wrong answer about a medication, a symptom, or a research finding can cause real harm.

*What this means for you:* If something the coach says surprises you or seems off, check it. The coach is a starting point, not an endpoint.

*External resource:* ECRI 2025 Health Technology Hazards report — AI hallucination in healthcare (ecri.org)

**2. AI may agree with you when it should push back (sycophancy)**
AI systems are trained in ways that make them tend to agree with users, validate their beliefs, and avoid conflict — even when the user's belief is incorrect or risky. Research has shown that LLMs exhibit a tendency to comply with illogical requests that generate false information, even when they have the knowledge to identify the request as illogical. This tool has explicit guardrails designed to counter this — but those guardrails are imperfect. The FDA's Digital Health Advisory Committee has identified sycophancy as a significant concern for generative AI health tools, noting that without human oversight to identify errors, AI devices could adversely affect patients.

*What this means for you:* If the coach seems to be telling you what you want to hear, be skeptical. Push back. Ask it to steelman the opposite view.

*External resource:* "When helpfulness backfires" — npj Digital Medicine (nature.com)

**3. AI may anchor on your framing rather than challenge it**
If you present a hypothesis about what's causing your symptoms, the AI tends to reason from that hypothesis rather than independently evaluate it. This is a known reasoning failure — sometimes called anchoring — and it can lead to false confirmation of incorrect beliefs.

*What this means for you:* Try framing questions as open questions ("what could be causing X?") rather than closed ones ("is X causing my symptoms?"). Ask the coach explicitly to generate alternative explanations.

**4. AI has less reliable knowledge about conditions like yours**
These conditions — hEDS, POTS, MCAS, ME/CFS, Long Covid, and related diagnoses — are underrepresented in medical research and, by extension, in the data AI systems are trained on. AI models are only as good as the data they are trained on, and if training data underrepresents certain groups, the results will not be equitable. The medical literature AI was trained on also reflects decades of dismissal, misdiagnosis, and bias toward these conditions. The coach is explicitly designed to counter this — but it cannot fully overcome it.

*What this means for you:* Be especially critical of AI responses about rare presentations, experimental treatments, or anything that sounds like it might be minimizing your experience.

**5. AI can lose track of things in long conversations**
As a conversation grows longer, earlier information — a contraindication you mentioned, a decision you made, a warning you acknowledged — receives less reliable attention from the AI. This is why the handoff protocol exists. It is not a complete fix.

*What this means for you:* Use the handoff feature. If the coach seems to have forgotten something important, flag it and start a fresh session.

**6. AI is not a clinical relationship**
The coach does not know you over time the way a clinician does. It does not carry memory between sessions unless you provide your log. It cannot observe you physically, order tests, or take responsibility for your care. It is a tool to support your thinking — not a substitute for a clinical relationship.

*What this means for you:* Keep working toward adequate care, even when that's hard. Use this tool to help you advocate for yourself, not to replace advocacy.

**7. AI guardrails are imperfect and evolving**
This tool has explicit safeguards designed to counter the above failure modes. Those safeguards improve with each version. They do not make the tool safe in an absolute sense — they make it safer than it would be without them. The field of AI safety in healthcare is active and evolving, and our understanding of these risks is still developing.

*External resources:*
- AHRQ PSNet: "Artificial Intelligence and Patient Safety: Promise and Challenges" (psnet.ahrq.gov)
- WHO Europe report on AI in health systems (who.int)
- CDC: "Ethical and Equitable Implementation of AI in Public Health and Medicine" (cdc.gov)

---

### Disclosure Delivery by Milestone

| Milestone | Where it appears | Acknowledgment required? | Recurrence |
|---|---|---|---|
| 0 | README callout (Tier 1 text) | No | Always visible |
| 1 | GETTING_STARTED.md (Tier 1 + link to Tier 2) | No | Always visible |
| 1 | Platform setup guides (brief note per guide) | No | Always visible |
| 2 | Local MCP README (Tier 1 + link) | No | Always visible |
| 3a+ | App onboarding (Tier 1, full screen) | Yes — one-time acknowledgment | Banner at session start until dismissed |
| 3a+ | App session start (Tier 1, brief banner) | No | Until patient opts to hide |
| All | `/docs/ai-safety.md` (Tier 2, always linked) | No | Always available |

---

### Writing Guidelines for `ai-safety.md`

The document is written for patients with brain fog, fatigue, and high cognitive load. These are not rhetorical constraints — they are the actual reading conditions.

- Maximum 3 sentences per paragraph
- Plain language throughout — no technical jargon without immediate plain-language translation
- Each failure mode gets: one-sentence plain summary, one concrete example relevant to this population, one "what this means for you" takeaway
- No legalese, no passive voice, no buried caveats
- Total document target: under 600 words
- External links open in new tab, are labeled clearly, and are reviewed for accessibility before inclusion

---

### Maintenance

The disclosure document should be reviewed whenever:
- A new AI failure mode is documented in peer-reviewed literature that is relevant to this population
- The underlying model changes significantly
- New guardrails are added or removed from the coaching parameters
- A patient or contributor reports an experience consistent with an undisclosed risk

Version and date the document. Log significant changes in the repo changelog.

---

## Out of Scope

These are explicit non-goals for this project. They should be stated clearly in the README.

- Diagnosis — the system does not diagnose
- Prescription — the system does not prescribe or recommend unprescribed medications
- EHR / FHIR integration — possible future collaboration, not a solo build
- Insurance or billing interaction of any kind
- Regulatory approval as a medical device (SaMD) — the system is a coaching and logging tool, not a diagnostic or therapeutic device; this framing must be consistent across all docs and disclosures

---

## Open Decisions Log

| Decision | Options | Gate | Stakes |
|---|---|---|---|
| License | MIT vs Apache 2.0 | Milestone 0 | Apache has explicit patent grant — relevant if project grows |
| Pre-release clinical review | Ship as-is vs. lightweight review pass | Milestone 0 | Patient safety; community trust |
| `CLINICAL_REVIEW.md` | Include vs. defer | Milestone 0 | Contributor accountability; community trust |
| Tier 1.5 parameters long-term | Maintained / deprecated / parallel | Milestone 1 | Accessibility value for non-technical patients vs. maintenance burden — accessibility principle favors maintaining |
| Milestone 3 storage model | Bring-your-own vs. hosted vs. both | Milestone 3a | Infrastructure burden; accessibility; legal exposure; both options required to honor co-equal principles |
| Codebase relationship | Monorepo vs. separate repos vs. shared package | End of Milestone 2 | Schema maintenance; contributor scope; release coupling |

---

*End of roadmap — v0.1*
*Next: resolve Milestone 0 decision points, then begin repo scaffolding*
