# SpoonGuide Claude Setup Guide

**Last modified:** 2026-03-23  
**Version:** 1.0 — Initial Claude setup guide with Free/Paid sections

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial guide. Claude Projects free. Free: Sonnet, 200K context. Pro: Opus, more usage. Parameters as knowledge file upload. |

---

This guide covers **Claude-specific setup** for SpoonGuide. For privacy notice, patient log setup, starting your first session, the handoff protocol, and general troubleshooting, see **[GETTING_STARTED.md](../../GETTING_STARTED.md)**.

---

## Before you start

You will need:

- **A Claude account** — sign up at [claude.ai](https://claude.ai)
- **The parameters file** — [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md)

**Claude Projects are free.** You can create a Project with the parameters loaded without a paid subscription. Pro gives you access to Opus (more capable model) and higher usage limits.

---

## Which model to use

### Sonnet (free tier)

- Available on the free tier with Claude Projects
- Strong instruction-following — well-suited for complex system prompts like SpoonGuide
- Message limits: roughly 20–30 per day (varies; resets periodically)
- 200K token context window

### Opus (Pro tier)

- Requires Claude Pro ($17–20/month)
- Most capable model; best for complex reasoning and instruction adherence
- ~5× usage capacity of free tier
- Same 200K context; Pro also includes Claude Code and Cowork

**Recommendation:** Sonnet on the free tier is sufficient for most patients. If you hit daily limits or want the strongest instruction-following, Pro and Opus are the upgrade path.

---

## Free setup

Claude Projects let you create a workspace with persistent context. You can upload the parameters file as a knowledge file and add a short instruction that tells Claude to follow it.

1. Go to [claude.ai](https://claude.ai) and sign in
2. Click **Projects** in the sidebar
3. Click **Create new project**
4. Name it — for example, "SpoonGuide Coach" or "My Chronic Illness Coach"
5. In the project settings, find **Add knowledge** or the file upload area
6. Upload [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md) (supported formats include .md, .txt, .pdf)
7. In **Project instructions** or **Custom instructions**, add:

```
You are a chronic illness coach for patients with hEDS, POTS, MCAS, ME/CFS, CCI, Long Covid, and related conditions.

Your full behavioral parameters, clinical knowledge, and session protocols are in the uploaded knowledge file: chronic-illness-coach-parameters.md

Follow all instructions in that file precisely. It governs your identity, governing principles, session protocols, intervention framework, safety escalation, and handoff behavior.

Do not summarize or abbreviate the parameters. Do not deviate from them. If you are uncertain how to handle a situation, refer back to the parameters document.
```

8. Save the project

**Note:** Claude Projects support file uploads (up to 30MB per file). The parameters document fits within that limit. Context is shared across conversation and files — the 200K token window holds your log, parameters, and chat history together.

---

## Paid setup (Claude Pro)

Same steps as Free setup. Pro adds:

- **Opus** — most capable model for complex instruction-following
- **Higher usage limits** — ~5× more messages per day
- **Claude Code and Cowork** — not required for SpoonGuide, but available

The Project creation process is identical. Your subscription determines which model you can select and your usage capacity.

---

## Patient log, sessions, and handoff

After setup, see [GETTING_STARTED.md](../../GETTING_STARTED.md) for:

- Creating your patient log
- Starting your first session
- The handoff protocol
- General troubleshooting

---

## Claude-specific troubleshooting

### Hitting the daily message limit

**What it looks like:** Claude stops responding or indicates you've reached your limit.

**What to do:** Trigger a handoff to capture session state, then wait for the limit to reset (typically 4–8 hours on free tier). Start a new conversation when ready.

### Context overflow in long sessions

**What it looks like:** Claude seems to lose track of earlier details or contradict itself.

**Why it happens:** The context window (the AI's working memory for the conversation) includes your log, parameters, and conversation. Very long sessions can push older content out of effective attention.

**What to do:** Trigger a handoff and start a fresh session. The handoff compresses important state into your Context Bridge for the next session.

---

## Testing notes (developer only)

**🧪 Developer Testing Notes — Not for patients**

Use this template for each test session:

```
## Test session — [date]

**Model used:** [ ] Sonnet  [ ] Opus
**Plan:** [ ] Free  [ ] Pro

**Parameters compliance observations:**
- Care access check triggered: [ ] Yes  [ ] No  [ ] Not applicable
- Timeline restatement pattern applied correctly: [ ] Yes  [ ] No  [ ] Not tested
- Dose confirmation behavior: [ ] Yes  [ ] No  [ ] Not tested
- Hard refusal list respected: [ ] Yes  [ ] No  [ ] Not tested
- Handoff triggered correctly: [ ] Yes  [ ] No  [ ] Not tested
- Low-energy handoff variant worked: [ ] Yes  [ ] No  [ ] Not tested

**Handoff output quality:**
- Profile accurate: [ ] Yes  [ ] No  [ ] Not tested
- Session Log accurate: [ ] Yes  [ ] No  [ ] Not tested
- Context Bridge accurate: [ ] Yes  [ ] No  [ ] Not tested

**Cognitive load observations:**
- Session start friction (care access check): 
- Handoff trigger felt natural: [ ] Yes  [ ] No
- Three-part handoff manageable at end of session: [ ] Yes  [ ] No
- Low-energy handoff sufficient when tired: [ ] Yes  [ ] No

**Notable failures or unexpected behaviors:**


**Parameter change candidates (bring to design discussion):**


**Overall session notes:**
```
