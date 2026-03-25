# SpoonGuide Cursor Setup Guide

**Last modified:** 2026-03-25  
**Version:** 1.2 — Handoff: two-step flow + three separate outputs; session start with file + Context Bridge

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial guide. Hobby vs Pro. Model trade-offs (Claude, GPT, Gemini). Rule-based and @file parameter loading. Direct log file editing. |
| 1.1 | 2026-03-23 | Replaced Layer 1/2/3 with Profile, Session Log, Context Bridge. Patient Log consistency. |
| 1.2 | 2026-03-25 | Aligned with parameters §10.5: prose changelog → confirm → Profile diff, Session Log entry, Context Bridge. Session start: @ log + Context Bridge. Testing notes updated. |

---

This guide covers **Cursor-specific setup** for SpoonGuide. For privacy notice, patient log setup, starting your first session, the handoff protocol, and general troubleshooting, see **[GETTING_STARTED.md](../../GETTING_STARTED.md)**.

**Who this is for:** Cursor is an advanced option for users comfortable with a code editor. The main benefit: the AI can **read and directly edit your Patient Log** after a handoff—so you merge the **Profile diff** and append the **Session Log entry** without manual copy-paste from the coach output. Your log stays in the workspace. You still **copy the Context Bridge** yourself for the next chat (see [GETTING_STARTED.md](../../GETTING_STARTED.md#the-handoff-protocol)). The coach follows a **two-step** handoff (prose changelog, then—after you confirm—three separate blocks); see **Section 10.5** in the [parameters document](../parameters/chronic-illness-coach-parameters.md).

---

## Before you start

You will need:

- **Cursor** — [cursor.com](https://cursor.com)
- **A clone of the SpoonGuide repo** — so the parameters file and (optionally) your log file live in your workspace
- **The parameters file** — [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md)

---

## Cursor plans: Hobby vs Pro

### Hobby (free)

- No credit card required
- Limited Agent requests and Tab completions
- Viable for light use (a few sessions per month)
- If you hit the limit, you'll need to wait or upgrade

### Pro ($20/month)

- Extended Agent limits; access to frontier models (Claude, GPT, Gemini)
- $20 included API usage per month; pay-as-you-go above that
- Recommended for regular SpoonGuide sessions

**Note:** Cursor uses a credit-based system. Model choice affects how quickly you consume the included $20 — complex models cost more per request.

---

## Which model to use

Cursor supports multiple model providers. Choose in Cursor Settings → Models. All can run SpoonGuide; instruction-following varies.

| Model | Provider | Instruction-following | Cost (typical) | Notes |
|-------|----------|----------------------|----------------|-------|
| Claude 4 Sonnet / 4.5 Sonnet | Anthropic | Strong | Medium | Recommended for complex system prompts |
| Claude 4.6 Opus | Anthropic | Strongest | Higher | Best adherence; may require Max Mode on some plans |
| GPT-5 / GPT-5.4 | OpenAI | Strong | Medium–High | Good reasoning; agentic capabilities |
| Gemini 3 Pro / 3.1 Pro | Google | Good | Medium | Solid; check Cursor's current model list |
| Gemini 3 Flash | Google | Adequate | Lower | Faster, cheaper; less reliable on complex parameters |
| Composer 2 (Cursor) | Cursor | Good for coding | Lower | Optimized for code; coaching use case not primary |

**Recommendation:** Claude Sonnet or Opus for the best balance of instruction adherence and cost. GPT-5 and Gemini Pro are viable alternatives.

---

## Loading the parameters

Two options:

### Option A: Cursor rule (persistent)

Create a rule so the SpoonGuide parameters apply automatically when you're in a coaching session.

1. Create `.cursor/rules/spoonguide-coach.mdc` in your workspace:

```markdown
---
description: SpoonGuide chronic illness coach — follow parameters when user is in a coaching session
alwaysApply: true
---

When the user shares their own Patient Log or asks for chronic illness coaching, you are the SpoonGuide coach.

Your full behavioral parameters, clinical knowledge, and session protocols are in:
docs/parameters/chronic-illness-coach-parameters.md

Read that file and follow it precisely. It governs your identity, governing principles, session protocols, intervention framework, safety escalation, and handoff behavior.

Do not summarize or abbreviate the parameters. Do not deviate from them.
```

2. Cursor will include this rule in relevant conversations. When you paste your log or ask for coaching, the AI should load and follow the parameters.

**Note:** The parameters document is long. If the rule doesn't reliably pull it in, use Option B.

### Option B: @file reference (each session)

In each chat session, reference the parameters file so Cursor loads it:

- Type `@docs/parameters/chronic-illness-coach-parameters.md` (or `@chronic-illness-coach-parameters.md` if Cursor resolves it)
- Or drag the file into the chat

Then attach your Patient Log (e.g. `@my-patient-log.md`) and paste your **Context Bridge** if continuing from a prior session. This ensures the full parameters are in context every time.

---

## Log file workflow (Cursor advantage)

Keep your Patient Log in the workspace — for example, `my-patient-log.md` in the repo root or a `logs/` folder.

**Why this matters:** Cursor can read and write files. The coach emits a **prose changelog** first; after you **confirm** (or correct) it, you get **three** labeled copy blocks: **Profile diff** (YAML), **Session Log entry** (markdown), **Context Bridge** (markdown). You can ask Cursor to:

1. **Merge the Profile diff** into the YAML between the `---` lines at the top of your Patient Log
2. **Append the Session Log entry** to the bottom of the file
3. **Surface the Context Bridge** as text for you to copy—you still paste it at the start of your **next** session yourself

**Example prompt after Step B:** "Merge the Profile diff from the coach into the top of `my-patient-log.md`, append the Session Log entry at the bottom, and show me the Context Bridge block to copy for my next chat."

The AI will edit the file. Review the changes before your next session.

---

## Starting a session

1. Open your Patient Log in the editor (or have it in the workspace)
2. Open a new Cursor chat (Agent or Composer)
3. If using Option B, reference `@chronic-illness-coach-parameters.md`
4. Reference your Patient Log (e.g. `@my-patient-log.md`) and paste your **Context Bridge** if you have one from the last session
5. Use an opening like:

```
Hi — I'm starting a new session. Here's my Patient Log:

[@my-patient-log.md or paste]

[Context Bridge from last session, if any]

I'd like to start by [your focus].
```

---

## Handoff in Cursor

Trigger a handoff by typing `handoff`, `new chat`, or `session summary`.

### With direct file access

**Flow:** The coach first sends a **prose changelog** (Step A). Reply with corrections or **confirmed**. Then it sends **Profile diff**, **Session Log entry**, and **Context Bridge** as **three separate** fenced blocks (Step B).

**Exact prompt to run after Step B:** 

> Merge the Profile diff YAML into the top section of `my-patient-log.md`, append the Session Log markdown entry at the bottom, and print the Context Bridge block so I can copy it for my next session.

(Replace `my-patient-log.md` with your log filename.)

**Expected AI responses:**
- Confirmation of which Profile fields were merged (or a diff summary)
- Confirmation the Session Log entry was appended
- The Context Bridge text for your clipboard

**Verification:** Open your log in the editor and confirm YAML + new entry before your next session.

**Without file access:** Use the workflow in [GETTING_STARTED.md](../../GETTING_STARTED.md#step-by-step-after-handoff).

---

## Cursor-specific troubleshooting

### The AI doesn't follow the parameters

**What it looks like:** Skips care access check, proposes hard-refusal items, or behaves inconsistently.

**Why it happens:** The rule may not have loaded the full parameters file, or the model may not weight it heavily enough.

**What to do:** Use Option B (@file) to explicitly load the parameters each session. Ensure you're on a capable model (Claude Sonnet/Opus preferred).

### Hitting Pro usage limits

**What it looks like:** Cursor indicates you've used your included API credit.

**What to do:** Add on-demand usage in Cursor settings, or wait for the monthly reset. Consider switching to a cheaper model (e.g., Gemini Flash) for lighter sessions.

### File edits are wrong or overwrite something

**What to do:** Review the AI's proposed edits before accepting. Keep your log in version control (git) so you can revert if needed. Ask for a diff before applying.

---

## Testing notes (developer only)

**🧪 Developer Testing Notes — Not for patients**

Use this template for each test session:

```
## Test session — [date]

**Model used:** [ ] Claude  [ ] GPT  [ ] Gemini  [ ] Composer
**Parameter loading:** [ ] Rule  [ ] @file
**Direct log edit used:** [ ] Yes  [ ] No

**Parameters compliance observations:**
- Care access check triggered: [ ] Yes  [ ] No  [ ] Not applicable
- Timeline restatement pattern applied correctly: [ ] Yes  [ ] No  [ ] Not tested
- Dose confirmation behavior: [ ] Yes  [ ] No  [ ] Not tested
- Hard refusal list respected: [ ] Yes  [ ] No  [ ] Not tested
- Handoff triggered correctly: [ ] Yes  [ ] No  [ ] Not tested
- Handoff Step A (prose changelog) before Step B: [ ] Yes  [ ] No  [ ] Not tested
- Low-energy handoff variant worked: [ ] Yes  [ ] No  [ ] Not tested
- Direct file edit (Profile diff + Session Log entry) accurate: [ ] Yes  [ ] No  [ ] Not tested
- Context Bridge surfaced for next session: [ ] Yes  [ ] No  [ ] Not tested

**Cognitive load observations:**
- Rule vs @file — which was more reliable: 
- Direct log edit reduced friction: [ ] Yes  [ ] No

**Notable failures or unexpected behaviors:**


**Overall session notes:**
```
