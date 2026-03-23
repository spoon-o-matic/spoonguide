# SpoonGuide ChatGPT Setup Guide

**Last modified:** 2026-03-23  
**Version:** 1.0 — Initial ChatGPT setup guide with Free/Paid sections

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial guide. Free: paste parameters each session. Plus: Custom GPT with knowledge file. GPT-5.3/GPT-5.4. |

---

This guide covers **ChatGPT-specific setup** for SpoonGuide. For privacy notice, patient log setup, starting your first session, the handoff protocol, and general troubleshooting, see **[GETTING_STARTED.md](../../GETTING_STARTED.md)**.

---

> **⚠️ Privacy warning — read before uploading your health data**
>
> **SpoonGuide is intended for individuals managing their own health data only.** Do not use it to upload or manage anyone else's health information.
>
> Before using SpoonGuide with ChatGPT:
> 1. **Review ChatGPT/OpenAI data usage and retention policies** for your plan tier — these vary by subscription and affect how your inputs are stored and processed.
> 2. **Opt out of data training** in ChatGPT settings where available — check your account settings and disable any options that allow your conversations to be used for model improvement.
> 3. **Consider privacy implications** — avoid uploading your own health data to third-party services if you have concerns; use de-identified or synthetic logs for testing when possible.
> 4. **Consult a privacy professional** if you have questions before using your personal log with ChatGPT or any external AI service.
>
> SpoonGuide is designed to support chronic illness self-management. Ensuring your data handling complies with HIPAA, GDPR, or other applicable requirements, as well as never substituting the advice of an LLM for that of a qualified medical professional, is your sole responsibility.

---

## Before you start

You will need:

- **A ChatGPT account** — sign up at [chat.openai.com](https://chat.openai.com)
- **The parameters file** — [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md)

**Custom GPTs require ChatGPT Plus** ($20/month). On the free tier, you paste the parameters at the start of each session instead.

---

## Which model to use

### Free tier

- **GPT-5.3** (or current free model) with daily usage limits
- Limited messages per day; capacity varies
- Adequate for getting familiar with SpoonGuide; apply extra skepticism to responses

### ChatGPT Plus ($20/month)

- **GPT-5.3** and **GPT-5.4 Thinking** — better reasoning and instruction-following
- **Custom GPTs** — persistent setup so you don't paste parameters every session
- Higher message limits
- Custom GPTs can include knowledge files (upload the parameters document)

### ChatGPT Go ($8/month)

- Budget option; more usage than free, less than Plus
- Does not include Custom GPT creation — use paste workflow if on Go

**Recommendation:** Free tier works for trying SpoonGuide. For regular use, Plus and a Custom GPT reduce friction and improve model access.

---

## Free setup (paste each session)

On the free tier, you paste the parameters and your patient log at the start of each session.

1. Open [chat.openai.com](https://chat.openai.com) and start a new chat
2. Download [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md) and open it in a text editor
3. Copy the **entire** parameters document
4. Paste it as your first message, followed by your patient log and your opening:

```
[Paste the full chronic-illness-coach-parameters.md content here]

---

Hi — I'm starting a new session with my patient log. Here it is:

[paste your patient log here]

I'd like to start by [your focus: e.g. "doing my intake" / "discussing my current symptoms"].
```

**Limitation:** The parameters document is long (~30K tokens). ChatGPT's context window fits it, but you may hit free-tier message limits. If the model truncates or seems to miss parts, consider Plus for a Custom GPT.

---

## Paid setup (Custom GPT with ChatGPT Plus)

A Custom GPT lets you load the parameters once and reuse them for every session.

1. Go to [chat.openai.com](https://chat.openai.com) and ensure you have ChatGPT Plus
2. Click your profile → **My GPTs** → **Create a GPT** (or use [platform.openai.com](https://platform.openai.com) GPT builder)
3. In **Configure**, set the name — e.g., "SpoonGuide Coach"
4. In **Instructions**, add:

```
You are a chronic illness coach for patients with hEDS, POTS, MCAS, ME/CFS, CCI, Long Covid, and related conditions.

Your full behavioral parameters, clinical knowledge, and session protocols are in the uploaded knowledge file: chronic-illness-coach-parameters.md

Follow all instructions in that file precisely. It governs your identity, governing principles, session protocols, intervention framework, safety escalation, and handoff behavior.

Do not summarize or abbreviate the parameters. Do not deviate from them. If you are uncertain how to handle a situation, refer back to the parameters document.
```

5. In **Knowledge** or **Upload files**, upload [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md)
6. Save and publish (for yourself only, or share if you choose)

**Note:** Custom GPTs support up to 10 knowledge files. The parameters document is a single file and fits well.

---

## Patient log, sessions, and handoff

After setup, see [GETTING_STARTED.md](../../GETTING_STARTED.md) for:

- Creating your patient log
- Starting your first session
- The handoff protocol
- General troubleshooting

---

## ChatGPT-specific troubleshooting

### Running out of free-tier messages

**What it looks like:** ChatGPT stops responding or shows a limit message.

**What to do:** Trigger a handoff to capture state, then wait for the daily limit to reset. Consider Plus if you use SpoonGuide regularly.

### Custom GPT not following parameters

**What it looks like:** The coach skips the care access check, proposes something on the hard refusal list, or behaves inconsistently.

**Why it happens:** Custom GPTs can be less deterministic than a raw system prompt. The model may not always weight the knowledge file as heavily as intended.

**What to do:** Gently redirect: "Can you check the parameters document and tell me what it says about [topic]?" Ensure the knowledge file uploaded correctly and that the instructions reference it by filename.

---

## Testing notes (developer only)

**🧪 Developer Testing Notes — Not for patients**

Use this template for each test session:

```
## Test session — [date]

**Model used:** [ ] Free (GPT-5.3)  [ ] Plus (GPT-5.3)  [ ] Plus (GPT-5.4)
**Setup:** [ ] Paste  [ ] Custom GPT

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
