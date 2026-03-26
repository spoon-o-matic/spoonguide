# Using AI for Chronic Illness Management: What You Need to Know
v1.0 - March 25, 2025 - Prepared with Claude AI using resources found by and guidance from, and fully reviewed and OK'd, by Michelle C. Funk

*A patient guide to real risks and practical safeguards*

---

## Quick Summary

*Cognitive fatigue is real. If reading the full document isn't possible right now, start here.*

**AI health tools can genuinely help you** — understanding your conditions, preparing for appointments, tracking symptoms, and navigating a system that routinely fails complex patients. This document is not here to tell you not to use them.

**But AI tools have serious, well-documented limitations in medical contexts.** Knowing what they are will help you get more value from AI while protecting yourself from real harms.

The short version:

- **AI makes confident mistakes.** "Hallucination" — generating plausible but false information — is not rare. Research documents rates above 60% in open-ended clinical contexts.
- **AI does not know you.** It cannot access your medical records, current medications, organ function, or individual history. Generic advice can be wrong *for you* even when it's correct in general.
- **AI's knowledge has an expiration date.** Models are trained up to a cutoff and cannot access updated guidelines, new drug approvals, or recent research.
- **AI reflects and can amplify bias** — including bias around disability, race, gender, and socioeconomic status.
- **What you share may not be private.** Entering sensitive health information into public AI tools carries real privacy risks.
- **This tool was built with these limitations in mind** — but it is still an AI, and the same risks apply.

The goal of this document is not to discourage AI use. It is to help you use it *more safely*, with a clear understanding of where it can fail you and what to do about it.

---

## Part 1: What AI Actually Is (and Isn't)

### How large language models work

The AI tools increasingly used for health information — ChatGPT, Gemini, Claude, and others — are called Large Language Models (LLMs). They work by predicting likely sequences of words based on patterns learned from enormous amounts of text.

This is important to understand: **LLMs do not reason the way a clinician reasons.** They do not look up information in a database, verify facts against authoritative sources, or apply a structured clinical decision framework. They generate text that is statistically likely to follow from your input, based on patterns in their training data.

This means they can produce fluent, confident, clinically plausible-sounding output that is factually wrong — sometimes dangerously so. The text *looks* like it was produced by someone who knows what they're talking about. The model has no reliable mechanism for flagging its own uncertainty, and no way to check whether what it said is true.

As Clusmann et al. summarize in their overview of LLMs in medicine: while these models demonstrate substantial medical knowledge and can perform well on standardized licensing exams, they "have the inherent limitation of reproducing existing medical biases and perpetuating inequalities," and "currently do not always provide appropriate detailed summaries or critical appraisals of up-to-date, high-quality, peer-reviewed evidence."[^1]

### The difference between general-purpose and specialized AI

There is an important distinction between:

- **General-purpose LLMs** (public versions of ChatGPT, Gemini, Claude, etc.) — trained on broad data, not validated for clinical use, not connected to current medical databases
- **Specialized or fine-tuned LLMs** — additionally trained on curated medical data for specific clinical tasks, with more rigorous validation

Most AI tools patients encounter — including this chronic illness coach — are general-purpose LLMs, even when given a specific persona or system prompt. As Moëll and Sand Aronsson note, specialized medical LLMs are still emerging and "require careful regulatory oversight and transparent reporting of performance and limitations. Even fine-tuned models are not infallible."[^4]

This matters. The chronic illness coach is a carefully parameterized general-purpose AI. It has been given detailed instructions to behave in specific ways, apply clinical reasoning standards, and explicitly flag uncertainty. But it is still operating on the fundamental architecture of the model underneath it, with all its limitations intact.

---

## Part 2: The Specific Risks

### Hallucination and inaccuracy

Hallucination refers to AI generating information that sounds credible but is simply false — invented medications, fabricated citations, incorrect dosages, treatment claims that have no basis in evidence.

This is not an edge case. A 2025 systematic review of LLMs in chronic disease management found a pooled accuracy rate of 71% across studies — meaning roughly 1 in 3 responses contained inaccurate or incomplete information, even in structured testing conditions.[^3] In open-ended clinical contexts, hallucination rates above 60% have been documented.[^4]

The risks are particularly acute for complex patients. Aydin et al. document that ChatGPT achieved only 16.7% accuracy when making dose adjustments that required accounting for patient-specific variables like renal function and comorbidities.[^2] A separate study found that while GPT-4 was more accurate than its predecessor in assessing medication safety for kidney disease patients, neither version matched the reliability of established drug information resources — and both particularly struggled with supplement safety assessments, often defaulting to "unknown toxicity" classifications due to limited training data.[^2]

For patients with multiple conditions, polypharmacy, and complex interactions — which describes most people using this tool — these accuracy gaps are not theoretical. They are likely to surface.

**What this means in practice:**
- Do not act on specific dosage information, drug interaction warnings, or treatment recommendations from AI without verification against another source or a qualified clinician.
- Be especially cautious with AI advice about supplements, off-label medications, or rare conditions where training data is sparse.
- A confident tone in AI output is not a signal of accuracy. Confident tone is a feature of how these models generate text.

### Knowledge cutoffs and outdated information

LLMs are trained on data up to a specific cutoff date. They cannot access information published after that point — including updated clinical guidelines, new drug approvals, newly identified drug interactions, or emerging research.

For rapidly evolving areas — Long Covid research, emerging ME/CFS treatments, updated POTS management guidelines — this cutoff is clinically significant. An AI may confidently describe the standard of care as it was understood two or three years ago, with no indication that things have changed.

Clusmann et al. note that because LLMs "are currently not dynamically updated, their knowledge is static, which prevents access to the latest scientific progress if used as a primary source of information."[^1]

Some AI tools now include web search capabilities that partially address this — but web search adds its own accuracy risks and does not substitute for access to current, peer-reviewed clinical literature.

**What this means in practice:**
- For anything time-sensitive — current guidelines, recently approved medications, emerging research — treat AI as a starting point, not an endpoint.
- When AI cites a specific guideline or recommendation, check whether that guideline has been updated. The 2021 NICE ME/CFS guidelines represented a significant shift from prior recommendations; an AI trained before that revision would give you dangerously outdated information about GET and exercise therapy.

### The personalization gap

AI health tools do not know you. They cannot access your medical records, your current medication list, your organ function, your allergy history, your genetic profile, or the specific way your conditions present and interact. They respond to what you tell them in the current conversation — which is inevitably incomplete.

This limitation becomes dangerous with complex patients. Aydin et al. describe how ChatGPT's deprescribing recommendations aligned with guidelines for patients without comorbidities, but lost accuracy when accounting for functional impairments and cardiovascular history — at one point recommending deprescribing pain medications without considering older adults' pain management needs.[^2] For patients whose conditions are themselves defined by complex multi-system involvement, this gap is structural.

The chronic illness coach is designed to gather information from your patient log and session context, which partially mitigates this. But even a detailed log cannot substitute for a clinician who has reviewed your full history, examined you, and ordered relevant tests.

**What this means in practice:**
- When sharing information with AI, err toward more detail — your conditions, current medications and doses, known contraindications. The more context you provide, the better calibrated the response can be.
- Treat any AI recommendation as conditional on information you may not have fully provided. Ask yourself: *does this account for my specific situation?*
- Anything involving dosing, interactions, or clinical decisions should be verified with someone who has access to your full picture.

### Bias in AI systems

LLMs are trained on large bodies of text that reflect the biases present in existing medical literature and broader internet content. This means they can reproduce and amplify biases related to race, gender, disability, socioeconomic status, age, and other factors.

In a healthcare context, these biases can manifest as differential quality of advice for different groups, stigmatizing language in responses about certain conditions, or framings of chronic illness that reflect ableist assumptions baked into the training data.

Li et al. found that 23% of responses about mental health and substance use disorders from one major AI model contained stigmatizing phrases.[^3] Clusmann et al. note that LLMs "perpetuate inequalities related to factors such as race, gender, sexual orientation, and socioeconomic status."[^1] A 2025 risk analysis documented "measurable race-linked content distortions across four leading LLMs."[^4]

For patients with conditions that have historically been dismissed, psychologized, or attributed to demographic factors — which includes most of the conditions this tool is designed to support — this is not an abstract concern. AI trained on medical literature that has systematically underserved these patients will reflect that underservice.

The chronic illness coach has been explicitly parameterized to operate from a disability justice framework, to treat patient-reported symptoms as authoritative, and to reject psychologizing framings of physiological conditions. This is a meaningful mitigation. It is not a complete one.

**What this means in practice:**
- If an AI response feels dismissive, minimizing, or reflects assumptions you recognize from years of being dismissed by the medical system, trust that instinct. Challenge the framing.
- Be particularly watchful when AI discusses your conditions in ways that implicate your psychology, motivation, or effort.
- This tool is designed to push back on dismissive framings — but if something feels wrong, say so.

### Privacy risks

When you share health information with a public AI tool, that information is transmitted to external servers. Depending on the platform and its data practices, it may be stored, used in model training, reviewed for safety purposes, or subject to data breaches.

Moëll and Sand Aronsson report that 133 million US health records were breached in 2023, with most occurring via cloud APIs and vendor platforms.[^4] Even where data is not actively misused, sharing identifying or sensitive health information — genetic findings, mental health history, reproductive health details, specific medications — with an uncontrolled third-party platform has real privacy implications that persist beyond the conversation.

**What this means in practice:**
- You do not need to share your full legal name, date of birth, specific location, or other direct identifiers with an AI health tool. The patient log format for this tool uses patient-chosen anonymous identifiers by default for this reason.
- Be thoughtful about sharing highly sensitive information — particularly genetic test results, mental health history, or reproductive health details — in any AI interface.
- If you are using the Claude interface on claude.ai, Anthropic's privacy policy governs your data. If you are accessing this through another platform, review that platform's data practices separately.
- Understand that even "anonymized" health information can sometimes be re-identified when specific details are combined.

### The risk of AI replacing care that is hard to access

This risk is specific to patients with inadequate access to specialist care — which, for the conditions this tool covers, is almost everyone.

When the alternative is a six-month waitlist, a GP who has never heard of MCAS, or simply going without information, an AI tool may feel like a more reliable resource than the formal care system. In some respects, it is. AI is available immediately, doesn't dismiss you, has broader knowledge of these conditions than many general practitioners, and will engage with complexity.

Moëll and Sand Aronsson acknowledge the value of AI for patients who would otherwise go without information, including anecdotal cases where AI helped patients identify diagnoses that multiple clinicians had missed — one case involving tethered cord syndrome in a child that 17 doctors had failed to diagnose.[^4] The point is not to deny this value. The point is that the same tool that helps you name a condition can also give you incorrect dosing advice with equal confidence, and there may be no human clinician in your care to catch the error.

**What this means in practice:**
- Use this tool to *prepare* for care, not to replace it. It is particularly well-suited for helping you understand your conditions, formulate questions for your care team, evaluate proposed interventions, and identify what specialist care you need to advocate for.
- Where AI and a human clinician disagree, do not default to the AI — even if the AI has been more engaged and more knowledgeable in your experience. Bring the disagreement to your clinician explicitly and ask them to engage with the reasoning.
- The hard refusals and safety escalations built into this tool exist precisely because some decisions require human clinical judgment. They are not there to be talked around.

---

## Part 3: Using AI More Safely

This section draws on the harm reduction framework proposed by Moëll and Sand Aronsson (2025), which applies public health principles of harm reduction — pragmatic risk minimization rather than prohibition — to LLM use in healthcare.[^4] The underlying logic: these tools will be used regardless of warnings, so the most useful response is not to prohibit their use but to make that use as safe as possible.

### Verify before acting

Any AI output that would inform a decision — about a medication, a treatment, a dose, a supplement interaction — should be verified against another source before you act on it.

Useful verification sources include:
- Your prescribing clinician or a pharmacist (especially for drug interactions)
- Official clinical guidelines from credible bodies (NICE, Bateman Horne Center, the EDS Society, IACFS/ME, Dysautonomia International)
- Peer-reviewed literature (PubMed, Google Scholar)
- Established drug information databases (Drugs.com, Micromedex) for medication and supplement questions

For supplement and OTC medication questions specifically, AI has shown particular weakness in the research. Verification is especially important here.

### Use AI to prepare for care, not to replace it

Some of the most effective and lower-risk uses of AI in healthcare involve preparation and translation rather than decision-making:

- *"What questions should I ask my cardiologist about my POTS management?"*
- *"Help me explain my symptom pattern to a GP who may not be familiar with MCAS."*
- *"What does this test result typically mean, and what should I follow up on?"*
- *"What are the current first-line approaches for this symptom cluster?"*
- *"Can you help me draft a letter to my insurer explaining why this treatment is medically necessary?"*

These uses leverage AI's genuine strengths — broad knowledge, accessibility, ability to translate complex concepts into plain language — while keeping clinical decisions in human hands.

### Be a skeptical reader

The fluency and confidence of AI output is not a signal of accuracy. Develop the habit of asking:

- *Is this specific to my situation, or generic advice that might not apply to me?*
- *Does this account for my full medication list and health history?*
- *Is this consistent with what my care team has told me?*
- *Could this information be outdated?*
- *Does this feel like it's dismissing something I know from my own experience?*

Your experience of your own body is valid clinical data. If an AI response contradicts something you have observed consistently about your own health, that contradiction is worth investigating — not automatically resolving in the AI's favour.

### Protect your privacy

- Use an anonymous identifier rather than your full name in patient logs and AI sessions.
- Avoid pasting raw genetic test results, detailed mental health records, or other highly sensitive documents into public AI interfaces.
- Be aware that detailed, specific health information can sometimes be re-identified even without a name attached, particularly if it includes unusual combinations of conditions, medications, and history.
- If you are using this tool via claude.ai, you can review Anthropic's privacy and data use policies at [anthropic.com/legal/privacy](https://www.anthropic.com/legal/privacy).

### Know when AI is not the right tool

There are situations where AI should not be your first or primary resource:

- **Medical emergencies.** Anaphylaxis, cardiac symptoms, suspected myelopathic presentations, or acute mental health crises require immediate human care. Do not consult AI first.
- **Decisions about starting prescription medications.** AI can help you understand a medication and prepare questions for your prescriber, but should not be the basis for starting something new.
- **Interpreting your specific diagnostic test results.** AI can explain what a test measures in general, but interpreting your specific results requires someone with access to your full clinical picture.
- **When you are in a mental health crisis.** If you are experiencing suicidal ideation or feel unsafe, please contact the 988 Suicide and Crisis Lifeline (call or text 988 in the US) or your local emergency services.

---

## Part 4: About This Tool

The chronic illness coach is a general-purpose AI (currently Claude, by Anthropic) configured with a detailed system prompt designed to address many of the failure modes described in this document. Specifically, it is built to:

- Apply **clinical reasoning standards** that explicitly guard against hallucination-adjacent failures: temporal ordering errors, dose-insensitive extrapolation, and post hoc causal attribution from single data points
- Require **dose specificity** before commenting on interactions or expected effect sizes
- Use **calibrated uncertainty language** — distinguishing between "this is consistent with X," "X is the most likely explanation," and "this strongly suggests X"
- Operate from a **disability justice framework** that treats patient-reported symptoms as authoritative and rejects psychologizing framings of physiological conditions
- Follow a **hard refusal list** for interventions with documented harm potential (GET for ME/CFS, DNRS/Gupta, mold detox protocols, and others)
- Apply **safety hard stops** for acute medical emergencies, with immediate escalation language
- Be transparent about its own **epistemic limitations** when asked

These design choices meaningfully reduce some of the risks described in this document. They do not eliminate them. The underlying model still hallucinates, still has a knowledge cutoff, still cannot access your records, and still carries biases from its training data.

Treat this tool as a knowledgeable, carefully designed collaborator — one worth engaging with seriously, and whose outputs are worth verifying before acting on.

The full system prompt for this tool, and the architecture documentation, are available in this repository for anyone who wants to review them.

---

## References

[^1]: Clusmann J, Kolbinger FR, Muti HS, et al. The future landscape of large language models in medicine. *Communications Medicine*. 2023;3:141. https://doi.org/10.1038/s43856-023-00370-1

[^2]: Aydin S, Karabacak M, Vlachos V, Margetis K. Navigating the potential and pitfalls of large language models in patient-centered medication guidance and self-decision support. *Frontiers in Medicine*. 2025;12:1527864. https://doi.org/10.3389/fmed.2025.1527864

[^3]: Li C, Zhao Y, Bai Y, et al. Unveiling the potential of large language models in transforming chronic disease management: mixed methods systematic review. *Journal of Medical Internet Research*. 2025;27:e70535. https://doi.org/10.2196/70535

[^4]: Moëll B, Sand Aronsson F. Harm reduction strategies for thoughtful use of large language models in the medical domain: perspectives for patients and clinicians. *Journal of Medical Internet Research*. 2025;27:e75849. https://doi.org/10.2196/75849

---

*This document is part of the chronic illness coaching tool project. It is intended for patients, and a brief summary with a link to it is included in the tool's session start prompt. It is not a substitute for clinical advice.*

*Last updated: March 2026*
