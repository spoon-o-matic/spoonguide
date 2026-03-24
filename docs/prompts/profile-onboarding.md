# Profile onboarding — LLM-assisted setup (optional)

**Last modified:** 2026-03-24  
**Version:** 1.0 — Initial prompt for SpoonGuide Profile (YAML) generation from prose or Q&A

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-24 | Initial document: privacy, safety, usage modes, copy-paste prompt aligned to parameters Section 6.2. |

---

## What this is

This is an **optional** way to create the **Profile** (the structured top section of your Patient Log, between the first pair of `---` lines). You describe your situation in **plain language** or answer the model’s questions; the model outputs **YAML** you can paste into your copy of [patient-log-template.md](../../templates/patient-log-template.md).

SpoonGuide does not run this for you — you choose **which** LLM product to use and **when** to paste health-related text.

---

## Privacy

- **Your words are processed by whichever LLM you use** (Google, Anthropic, OpenAI, etc.). Each product has its own data retention and privacy settings — same class of consideration as coaching sessions. See [GETTING_STARTED.md — Privacy notice](../../GETTING_STARTED.md#privacy-notice).
- **SpoonGuide has no servers** and does not receive your Patient Log unless you choose to share it (for example by pasting into a chat).

---

## Safety and accuracy

- The output is a **draft** for **your** log, not medical advice. **You** are responsible for checking medications, doses, diagnosis wording, contraindications, and anything you will rely on clinically.
- Models can **hallucinate** or mis-format structured text. After pasting, open the file in an editor and fix indentation or typos if needed.

---

## How this relates to your SpoonGuide coach

If you start a session with little or no Profile filled in, the configured coach can gather history **conversationally** (see **Section 4: Patient History Intake Protocol** in [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md)). Use this document when you want:

- **Up-front structure** — a filled Profile **before** your first coached session, or  
- **A standalone helper** — e.g. a generic chat **before** you finish Gem / Project / Custom GPT setup, only to produce Profile YAML.

---

## After the model responds

1. Copy **only** the YAML block (from the opening `---` through the closing `---`, inclusive).
2. Open your saved copy of the template. Replace the **Profile** block: in [patient-log-template.md](../../templates/patient-log-template.md), that is the content **between** the pair of `---` lines that sits **immediately above** `# Log entries` (not the horizontal rule `---` lines near the top of the file after the version table).
3. Leave the `# Log entries` section and everything below it unchanged unless you already have entries.
4. Set `last_updated` to today’s date (`YYYY-MM-DD`) if the model left it blank.

**Template reference:** [patient-log-template.md](../../templates/patient-log-template.md)  
**Full schema and comments:** [chronic-illness-coach-parameters.md — Section 6.2](../parameters/chronic-illness-coach-parameters.md#62-yaml-frontmatter-schema)

---

## Copy-paste prompt (for the LLM)

Copy everything inside the fence below into a **new** chat (any major LLM), **or** paste it into a session with your **already configured** SpoonGuide coach if you want that coach to emit the Profile block in this format.

````
You are helping someone create the Profile section for a SpoonGuide Patient Log. The Profile is YAML frontmatter: a single block starting and ending with a line that contains only ---.

Rules:
1. Either (a) ask short, respectful clarifying questions for anything missing, then produce the YAML, OR (b) if the user already pasted a narrative, infer what you can and use empty strings or empty lists for unknowns. Do not invent clinical facts; if unsure, leave empty.
2. Output exactly ONE YAML document wrapped in --- delimiters (opening --- line, YAML body, closing --- line). No markdown fences, no commentary, no text before or after the block.
3. Match this structure and keys exactly. Use valid YAML: 2-space indentation for nested lists/objects; use [] for empty lists; use "" for empty strings where a string is expected.
4. For current_medications and current_supplements: if none, use empty lists (e.g. current_medications: []). If some exist, use a list of objects with the keys shown. prescriber_aware must be true or false (boolean), not a string.
5. For caregivers: if none, use an empty list []. Otherwise list objects with type, availability, familiarity.
6. conditions_confirmed = clinician-diagnosed; conditions_suspected = not yet confirmed. Keep wording faithful to what the user said; do not upgrade "suspected" to "confirmed."
7. care_access_level: one of specialist | gp-only | limited | none | "" if unknown.
8. caregiver_involvement_preference: one of proactive | on-request | exclude | "" if unknown.
9. autonomy_acknowledgments: usually [] unless the user explicitly describes prior acknowledgments in the requested format.

Schema to produce:

---
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

Now begin: ask the user for a brief narrative about their conditions, care access, meds/supplements, triggers, contraindications, baseline function, home monitoring, caregivers and preferences, and goals — OR invite them to paste whatever they already have. Then output only the YAML block as specified.
````
