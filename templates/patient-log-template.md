# Patient Log Template

**Last modified:** 2026-03-24  
**Version:** 1.2 — Profile completion not required before first session; pointer to Profile paths

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial template. YAML frontmatter and log entry format from parameters Section 6. Self-use reminder. |
| 1.1 | 2026-03-24 | Pointer to GETTING_STARTED for Markdown-friendly editors and optional LLM-assisted Profile setup. |
| 1.2 | 2026-03-24 | Clarified: you do not need to complete the Profile before the first session; coach onboarding is valid. |

---

This template is for tracking **your own** health. Do not use it to record health information about anyone else.

Copy this file and save it with your initials or ID (e.g., `jd-patient-log.md`). You **do not** need to complete the **Profile** (the section at the top between the `---` lines) before your first session — you may leave it blank and let your configured coach walk through intake in chat (see **Section 4** in the [parameters document](../docs/parameters/chronic-illness-coach-parameters.md)). You can also use an optional LLM-assisted prompt first; see [GETTING_STARTED.md — Set up your Patient Log](../GETTING_STARTED.md#set-up-your-patient-log).  Paste your Patient Log into the chat at the start of each SpoonGuide session.

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

Anything in brackets is meant to be replaced by the information indicated inside the brackets. that is, `[YYYY-MM-DD] [Entry Type: Intervention | Symptom | Observation | Session]` might be filled out as `2026-01-01: Intervention`

# [YYYY-MM-DD]: [Entry Type: Intervention | Symptom | Observation | Session]


**State before:** [Baseline at time of entry — functional level, symptoms, confounders like sleep, stress, weather]

**Intervention / Event:** [What was done, taken, or observed]
- Dose / protocol: [if applicable]
- Timing: [time of day, relation to meals, activity]

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