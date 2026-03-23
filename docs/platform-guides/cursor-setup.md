# SpoonGuide Cursor Setup Guide

**Last modified:** 2026-03-23  
**Version:** 1.0 — Initial Cursor guide for advanced users

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial guide. Hobby vs Pro. Model trade-offs (Claude, GPT, Gemini). Rule-based and @file parameter loading. Direct log file editing. |
| 1.1 | 2026-03-23 | Replaced Layer 1/2/3 with Profile, Session Log, Context Bridge. Patient Log consistency. |

---

This guide covers **Cursor-specific setup** for SpoonGuide. For privacy notice, patient log setup, starting your first session, the handoff protocol, and general troubleshooting, see **[GETTING_STARTED.md](../../GETTING_STARTED.md)**.

**Who this is for:** Cursor is an advanced option for users comfortable with a code editor. The main benefit: the AI can **read and directly edit your Patient Log**, eliminating the copy-paste handoff step. Your log stays in the workspace; the AI applies Profile (Layer 1) and Session Log (Layer 2) updates for you.

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

Then paste your Patient Log and start the session. This ensures the full parameters are in context every time.

---

## Log file workflow (Cursor advantage)

Keep your Patient Log in the workspace — for example, `my-patient-log.md` in the repo root or a `logs/` folder.

**Why this matters:** Cursor can read and write files. When you trigger a handoff, you can ask the AI to:

1. **Apply Profile (Layer 1)** — Edit the top section of your Patient Log directly
2. **Apply Session Log (Layer 2)** — Append the session entry to the bottom of your log
3. **Provide Context Bridge (Layer 3)** — Give you the block to paste at the start of your next session (you still paste this manually)

**Example prompt after a handoff:** "Apply the Profile (Layer 1) updates and Session Log (Layer 2) entry to my-patient-log.md. Give me my Context Bridge (Layer 3) to paste at the start of my next session."

The AI will edit the file. Review the changes before your next session.

---

## Starting a session

1. Open your Patient Log in the editor (or have it in the workspace)
2. Open a new Cursor chat (Agent or Composer)
3. If using Option B, reference `@chronic-illness-coach-parameters.md`
4. Paste your Patient Log (or type `@my-patient-log.md` if it's in the workspace)
5. Use an opening like:

```
Hi — I'm starting a new session with my Patient Log. Here it is:

[paste or @ your log]

I'd like to start by [your focus].
```

---

## Handoff in Cursor

Trigger a handoff by typing `handoff`, `new chat`, or `session summary`.

### With direct file access

**Exact prompt to run:** After the AI generates the handoff block, say:

> Apply the Profile (Layer 1) updates and Session Log (Layer 2) entry to `my-patient-log.md`. Give me my Context Bridge (Layer 3) to paste at the start of my next session.

(Replace `my-patient-log.md` with your log filename.)

The AI will edit the Profile at the top of your log and append the Session Log entry to the bottom. It will also output your Context Bridge for you to paste at the start of your next chat.

**Expected AI responses:**
- Confirmation that Profile (Layer 1) was updated (or which fields were changed)
- Confirmation that Session Log (Layer 2) entry was appended
- A Context Bridge (Layer 3) copy block for you to paste into your next session

**Verification:** Open your log file in the editor and visually confirm the Profile (Layer 1) changes and the new Session Log (Layer 2) entry at the bottom before starting your next session.

**Without file access:** Use the standard three-step copy-paste from [GETTING_STARTED.md](../../GETTING_STARTED.md).

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
- Low-energy handoff variant worked: [ ] Yes  [ ] No  [ ] Not tested
- Direct file edit (Profile + Session Log, Layers 1–2) accurate: [ ] Yes  [ ] No  [ ] Not tested

**Cognitive load observations:**
- Rule vs @file — which was more reliable: 
- Direct log edit reduced friction: [ ] Yes  [ ] No

**Notable failures or unexpected behaviors:**


**Overall session notes:**
```
