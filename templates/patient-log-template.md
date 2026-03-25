# Patient Log Template

**Last modified:** 2026-03-25  
**Version:** 1.4 — Profile: `lifestyle_and_mechanical_treatments`, `vitals_baseline`; aligns with parameters v1.7 Section 6.2

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial template. YAML frontmatter and log entry format from parameters Section 6. Self-use reminder. |
| 1.1 | 2026-03-24 | Pointer to GETTING_STARTED for Markdown-friendly editors and optional LLM-assisted Profile setup. |
| 1.2 | 2026-03-24 | Clarified: you do not need to complete the Profile before the first session; coach onboarding is valid. |
| 1.3 | 2026-03-25 | Log entry heading example: `## YYYY-MM-DD: EntryType`. Session start: upload Patient Log (or paste); see GETTING_STARTED. |
| 1.4 | 2026-03-25 | Profile YAML: `lifestyle_and_mechanical_treatments`, `vitals_baseline` (parameters Phase 4). Optional intervention lifecycle line retained. |

---

This template is for tracking **your own** health. Do not use it to record health information about anyone else.

Copy this file and save it with your initials or ID (e.g., `jd-patient-log.md`). You **do not** need to complete the **Profile** (the section at the top between the `---` lines) before your first session — you may leave it blank and let your configured coach walk through intake in chat (see **Section 4** in the [parameters document](../docs/parameters/chronic-illness-coach-parameters.md)). You can also use an optional LLM-assisted prompt first; see [GETTING_STARTED.md — Set up your Patient Log](../GETTING_STARTED.md#set-up-your-patient-log). At the start of each SpoonGuide session, **upload** this file to your coach if the app supports attachments; otherwise paste the full file. After your first handoff, also paste your **Context Bridge** from the prior session (see [GETTING_STARTED.md — The handoff protocol](../GETTING_STARTED.md#the-handoff-protocol)).

```markdown
patient_id: ""
last_updated: ""

conditions_confirmed: []
conditions_suspected: []

care_access_level: ""

baseline_functional_capacity: ""

known_triggers:
  mcas: []
  pem: []
  pain_instability: []
  other: []

known_contraindications: []

current_medications:
  - name: ""
    dose: ""
    indication: ""
    prescriber_aware: true

current_supplements:
  - name: ""
    dose: ""
    rationale: ""

lifestyle_and_mechanical_treatments:
  - type: ""
    description: ""
    frequency: ""
    status: ""

vitals_baseline:
  bp_systolic: ""
  bp_diastolic: ""
  hr_resting: ""
  last_measured: ""
  notes: ""

home_monitoring:
  devices: []
  metrics_tracked: []
  protocols_in_use: []

caregivers:
  - type: ""
    availability: ""
    familiarity: ""

caregiver_involvement_preference: ""

goals: []

autonomy_acknowledgments: []
---

# Log entries

Add entries below in chronological order. The coach will generate Session Log entries in this format at the end of each session.

Use a real ISO date and one entry-type word. **Do not** put square brackets in the rendered heading. `EntryType` is one of: **Intervention**, **Symptom**, **Observation**, or **Session**.

Examples: `## 2026-01-01: Session` or `## 2026-01-01: Intervention`

## YYYY-MM-DD: EntryType


**State before:** [Baseline at time of entry — functional level, symptoms, confounders like sleep, stress, weather]

**Intervention / Event:** [What was done, taken, or observed]
- Dose / protocol: [if applicable]
- Timing: [time of day, relation to meals, activity]

**Intervention lifecycle status:** (optional — Intervention entries only) proposed | patient-confirmed | outcome-reported | resolved — see **Section 6.3.1** in the [parameters document](../docs/parameters/chronic-illness-coach-parameters.md)

**Rationale:** [Why this intervention; proposed mechanism]

**Confounding factors:** (optional)
- Sleep quality: 
- Stress level: 
- Cycle phase: (if applicable)
- Weather / barometric: 
- Other:

**Outcome:** [What happened — timing of effects, what changed and what didn't]

**Side effects / adverse effects:** (optional)

**Home metrics:** (optional)
- [metric]: [value] at [time]

**Next steps / questions:** (optional)

**Coach flags:** (optional)
```