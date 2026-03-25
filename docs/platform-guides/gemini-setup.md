# SpoonGuide Gemini Setup Guide

**Last modified:** 2026-03-25  
**Version:** 1.1 — Testing notes aligned with parameters v1.4 handoff (two-step, three blocks)

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Restructured. Split into Free setup and Paid setup. Removed universal content (patient log, handoff, session start) — now in [GETTING_STARTED.md](../../GETTING_STARTED.md). Updated model names (Fast, Pro 3.1, Thinking). Gems available on free tier. |
| 1.1 | 2026-03-25 | Developer testing checklist: prose changelog + Profile diff / Session Log / Context Bridge; session start via Patient Log file upload + Context Bridge paste. |

---

This guide covers **Gemini-specific setup** for SpoonGuide. For privacy notice, patient log setup, starting your first session, the handoff protocol, and general troubleshooting, see **[GETTING_STARTED.md](../../GETTING_STARTED.md)**.

---

## Before you start

You will need:

- **A Google account** — any personal Gmail or Google Workspace account
- **The parameters file** — [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md)

Gems are available on the free tier. For the paid path (Pro 3.1, Thinking, higher limits), you need a Google AI subscription (Plus or Pro).

---

## Which model to use

Gemini Apps uses the Gemini 3 family. The models available depend on your plan:

### Fast (free tier)

- Available to all Google accounts at no cost
- General access; no daily prompts limit for Fast
- Less capable for complex system prompts — may miss instructions, apply reasoning patterns less consistently, or produce less careful responses
- **If you use Fast:** apply extra skepticism to the coach's responses and check important claims independently

### Pro 3.1 (paid: Google AI Plus, Pro, or Ultra)

- Better reasoning, better instruction-following, more reliable for a complex system prompt
- Has daily usage limits that vary by plan (e.g., Pro: up to 100 prompts/day; Ultra: 500/day)
- **If you hit your limit mid-session:** Gemini switches to Fast automatically without warning. Responses may suddenly seem less careful or start missing things. Trigger a handoff and start a new session when your Pro limit resets.

### Thinking (paid)

- Faster reasoning model; balances speed and complex problem-solving
- Also has daily limits

**Not sure which you have?** In the Gemini web app, look for the model name in the top right of the chat window.

---

## Free or Paid setup

Gems are generally available to most users, including on the free tier. You can create a persistent Gem with the parameters as a knowledge file without a paid subscription.

1. Go to [gemini.google.com](https://gemini.google.com)
2. On the left sidebar, click **Explore Gems**
3. Click **New Gem**
4. Name it — for example, "SpoonGuide Coach" or "My Chronic Illness Coach"
5. Leave the instructions field empty for now — you'll fill it in step 7
6. In the **Knowledge** section, click **Add files**
7. Upload [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md). Wait for the upload to complete.
8. In the instructions field, paste:

```
You are a chronic illness coach for patients with hEDS, POTS, MCAS, ME/CFS, CCI, Long Covid, and related conditions.

Your full behavioral parameters, clinical knowledge, and session protocols are in the uploaded knowledge file: chronic-illness-coach-parameters.md

Follow all instructions in that file precisely. It governs your identity, governing principles, session protocols, intervention framework, safety escalation, and handoff behavior.

Do not summarize or abbreviate the parameters. Do not deviate from them. If you are uncertain how to handle a situation, refer back to the parameters document.
```

9. Click **Save**

**Note:** If you upload from Google Drive instead of your device, you may need "Keep Activity" turned on and Google Workspace connected to Gemini Apps.

---

## Paid setup (Google AI Plus, Pro, or Ultra)

Same steps as Free setup above. The paid tier gives you:

- Access to **Pro 3.1** and **Thinking** models (better instruction-following for complex parameters)
- Higher daily prompt limits
- Larger context window (up to 1M tokens on Ultra)

The Gem creation process is identical. Your subscription determines which models you can select and your usage limits.

---

## Patient log, sessions, and handoff

After setup, see [GETTING_STARTED.md](../../GETTING_STARTED.md) for:

- Creating your patient log
- Starting your first session
- The handoff protocol
- General troubleshooting

---

## Gemini-specific troubleshooting

### The model switched mid-session

**What it looks like:** Responses suddenly feel less careful, shorter, or less consistent with the parameters.

**Why it happens:** You've hit your Pro or Thinking daily limit. Gemini switches to Fast automatically.

**What to do:** Note where the session was, trigger a handoff, and wait for your limit to reset before continuing.

---

## Testing notes (developer only)

**🧪 Developer Testing Notes — Not for patients**

Use this template for each test session:

```
## Test session — [date]

**Model used:** [ ] Fast  [ ] Pro 3.1  [ ] Thinking
**Session switched mid-conversation:** [ ] Yes  [ ] No

**Parameters compliance observations:**
- Care access check triggered: [ ] Yes  [ ] No  [ ] Not applicable
- Timeline restatement pattern applied correctly: [ ] Yes  [ ] No  [ ] Not tested
- Dose confirmation behavior: [ ] Yes  [ ] No  [ ] Not tested
- Hard refusal list respected: [ ] Yes  [ ] No  [ ] Not tested
- Handoff triggered correctly: [ ] Yes  [ ] No  [ ] Not tested
- Handoff Step A (prose changelog) before Step B (three blocks): [ ] Yes  [ ] No  [ ] Not tested
- Low-energy handoff variant worked: [ ] Yes  [ ] No  [ ] Not tested

**Session start (parameters Section 3.2):**
- Patient Log provided as file upload: [ ] Yes  [ ] No  [ ] Not applicable
- Context Bridge pasted when continuing from prior session: [ ] Yes  [ ] No  [ ] Not applicable

**Handoff output quality:**
- Prose changelog accurate / patient could validate: [ ] Yes  [ ] No  [ ] Not tested
- Profile diff (YAML) accurate; block-style lists only (no flow arrays): [ ] Yes  [ ] No  [ ] Not tested
- Session Log entry accurate; heading format `## YYYY-MM-DD: Session` (no bracket literals): [ ] Yes  [ ] No  [ ] Not tested
- Context Bridge accurate: [ ] Yes  [ ] No  [ ] Not tested

**Cognitive load observations:**
- Session start friction (care access check): 
- Handoff trigger felt natural: [ ] Yes  [ ] No
- Two-step handoff (confirm changelog, then copy blocks) manageable: [ ] Yes  [ ] No
- Low-energy handoff sufficient when tired: [ ] Yes  [ ] No

**Notable failures or unexpected behaviors:**


**Parameter change candidates (bring to design discussion):**


**Overall session notes:**
```
