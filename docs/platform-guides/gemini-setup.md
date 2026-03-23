# SpoonGuide Gemini Setup Guide

This guide walks you through setting up SpoonGuide as a Google Gem. You'll create a custom AI coach that follows SpoonGuide's parameters, upload the coaching instructions as a knowledge file, and learn how to start sessions and use the handoff protocol.

Setup takes about 10–15 minutes if you do it all at once. You can also do it in stages — stop whenever you need to rest and come back later. Your progress is saved.

---

## 1. Before you start

You will need:

- **A Google account** — any personal Gmail or Google Workspace account
- **A Google One subscription with Gemini Advanced** — to use the Pro model (recommended). The free tier gives access to the Fast model, which is less capable for this use case
- **The parameters file** — download it from the SpoonGuide repository: [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md)

---

## 2. Privacy notice

**Please read this before you begin setup.**

SpoonGuide is an AI coaching tool, not a medical provider. It can make mistakes, including confident-sounding mistakes.

Your conversations with the Gem are processed by Google. By default, Gemini Apps keeps your activity for 18 months. Google staff may review it to improve their systems.

You can turn off activity retention in your Google Account settings (Gemini Apps Activity). If you turn it off, Google may still temporarily retain conversations for up to 72 hours.

Your patient log file lives on your own device. SpoonGuide does not collect or store your data.

[Read more about AI risks in health tools before you start →](../ai-safety.md)

---

## 3. Which model to use

### Gemini Pro (recommended)

- Requires a Google One subscription with Gemini Advanced
- Better reasoning, better instruction-following, more reliable for a complex system prompt like this one
- Has daily usage limits. If you hit them mid-session, Gemini will switch to the Fast model automatically without warning. If responses suddenly seem less careful or start missing things, this may be why. Start a new session when your Pro limit resets.

### Gemini Fast (free tier)

- Available to all Google accounts at no cost
- Less capable for this use case — may miss instructions, apply reasoning patterns less consistently, or produce less careful responses
- Still useful for getting familiar with the system before committing to a subscription
- **If you use Fast:** apply extra skepticism to the coach's responses and check important claims independently

**Not sure which you have?** In the Gemini web app, look for the model name in the top right of the chat window.

---

## 4. Creating your Gem

1. Go to [gemini.google.com](https://gemini.google.com) <!-- verify link before publishing -->
2. On the left sidebar, click **Explore Gems**
3. Click **New Gem**
4. Name it — for example, "SpoonGuide Coach" or "My Chronic Illness Coach"
5. Leave the instructions field empty for now. You'll fill it in Section 6
6. Do not click Save yet

---

## 5. Adding the parameters as a knowledge file

The parameters document is too long to paste directly into the instructions field. You will upload it as a knowledge file instead.

1. In the Gem editor, find the **Knowledge** section below the instructions field
2. Click **Add files**
3. Upload the `chronic-illness-coach-parameters.md` file from the SpoonGuide repo. If you haven't downloaded it yet, get it here: [chronic-illness-coach-parameters.md](../parameters/chronic-illness-coach-parameters.md)
4. Wait for the upload to complete. You should see the filename appear under Knowledge
5. **Note:** If you upload from Google Drive instead of your device, you will need "Keep Activity" turned on and Google Workspace connected to Gemini Apps

The parameters file contains the full coaching instructions. The Gem reads it as background knowledge for every conversation.

---

## 6. Writing the Gem instructions

The instructions field is a short directive that tells the Gem how to use the knowledge file. Copy and paste this text exactly:

```
You are a chronic illness coach for patients with hEDS, POTS, MCAS, ME/CFS, CCI, Long Covid, and related conditions.

Your full behavioral parameters, clinical knowledge, and session protocols are in the uploaded knowledge file: chronic-illness-coach-parameters.md

Follow all instructions in that file precisely. It governs your identity, governing principles, session protocols, intervention framework, safety escalation, and handoff behavior.

Do not summarize or abbreviate the parameters. Do not deviate from them. If you are uncertain how to handle a situation, refer back to the parameters document.
```

After pasting, click **Save**.

---

## 7. Creating your patient log file

Your patient log is a personal file where you record your conditions, medications, symptoms, and session summaries. The coach uses it to understand your history and tailor its support. You keep it on your device and paste it into the chat when you start a session.

1. Download the patient log template from the repo: [patient-log-template.md](../../templates/patient-log-template.md)
2. Open it in any text editor (Notes, TextEdit, Notepad, VS Code — anything that saves plain text)
3. Save it somewhere easy to find. Consider naming it with your initials, for example: `jd-patient-log.md`
4. Fill in the YAML frontmatter fields (the section at the top between the `---` lines) with what you know right now. It's okay to leave fields blank and fill them in during your first session
5. You do not need to fill in any log body entries yet

**Your log file stays on your device.** It is never uploaded automatically. You choose when to share it with the Gem by pasting it into the chat.

---

## 8. Starting your first session

1. Open your Gem and start a new chat
2. Paste your patient log
3. Copy and use this opening message, filling in the bracketed parts:

```
Hi — I'm starting a new session with my patient log. Here it is:

[paste your full patient log here]

I don't have much history in the log yet. I'd like to start by [tell the coach what you want to focus on — for example: "doing my intake" / "discussing my current symptoms" / "understanding my POTS better"].
```

**What to expect:**

- The coach will ask about care access and caregiver availability at the start of every session. This is part of the protocol.
- If you don't paste a log, it will offer a lighter intake instead.
- First sessions will feel slower as the coach gathers context. This is normal.

---

## 9. Using the handoff protocol

### Why it exists

AI models don't retain memory between conversations. As a session grows longer, earlier details receive less reliable attention. The handoff captures everything important so the next session starts with full context.

### How to trigger it

Type one of these words at any point during a session:

- `handoff`
- `new chat`
- `session summary`

### What you'll get

Three blocks of text:

- **Layer 1:** Updates to paste into your log file's frontmatter section (the YAML at the top)
- **Layer 2:** A session log entry to paste into the body of your log file
- **Layer 3:** A context block to paste at the start of your next session

### If you're too tired for the full handoff

Say **"low energy handoff"** — you'll get Layer 3 only. A note will remind you to fill in the rest when you have more capacity.

### Step-by-step for using the handoff output

1. Copy the entire handoff block
2. Open your patient log file
3. **Layer 1:** Find the YAML frontmatter at the top of your log and update the fields shown (only fields that changed need updating)
4. **Layer 2:** Paste the session entry at the bottom of your log body
5. **Layer 3:** Paste this at the top of your next session, before or after your log
6. Start a new Gem conversation for your next session

You can also trigger a handoff proactively before you get tired — the coach may suggest it if the session has been long. You don't have to wait for it to suggest.

---

## 10. If something seems wrong

### The coach ignores part of the parameters

**What it looks like:** The coach skips the care access check, doesn't do the timeline restatement, proposes something on the hard refusal list, or otherwise doesn't behave as described.

**Why it happens:** Gemini doesn't always follow complex instructions perfectly, especially the Fast model. This is a known limitation.

**What to do:** Gently redirect: "Can you check the parameters document and tell me what it says about [topic]?" If it happens consistently, note it and report it as a testing observation in the [repo issues](https://github.com/YOUR_ORG/spoonguide/issues) <!-- verify link before publishing — update YOUR_ORG with actual org/username -->.

### The coach seems to have forgotten something

**What it looks like:** It contradicts something established earlier, misses a contraindication, or seems to be missing context.

**Why it happens:** Context window attention degrades in long sessions.

**What to do:** Trigger a handoff and start a fresh session. If you're mid-topic, say "before we continue — quick handoff" and it will generate the block without derailing the conversation.

### The model switched mid-session

**What it looks like:** Responses suddenly feel less careful, shorter, or less consistent with the parameters.

**Why it happens:** You've hit your Pro daily limit and Gemini has switched to Fast automatically.

**What to do:** Note where the session was, trigger a handoff, and wait for your Pro limit to reset before continuing.

### The coach says something that seems clinically wrong

**What it looks like:** Information that contradicts what you know about your conditions, a dose that seems off, a claim that surprises you.

**What to do:** Do not act on it without checking. Note it, look it up, and bring it to your care team if relevant. This is one of the core limitations of AI health tools. See [AI risks in health tools](../ai-safety.md) for more.

---

## 11. Testing notes (developer only)

**🧪 Developer Testing Notes — Not for patients**

Use this template for each test session:

```
## Test session — [date]

**Model used:** [ ] Pro  [ ] Fast
**Session switched mid-conversation:** [ ] Yes  [ ] No

**Parameters compliance observations:**
- Care access check triggered: [ ] Yes  [ ] No  [ ] Not applicable
- Timeline restatement pattern applied correctly: [ ] Yes  [ ] No  [ ] Not tested
- Dose confirmation behavior: [ ] Yes  [ ] No  [ ] Not tested
- Hard refusal list respected: [ ] Yes  [ ] No  [ ] Not tested
- Handoff triggered correctly: [ ] Yes  [ ] No  [ ] Not tested
- Low-energy handoff variant worked: [ ] Yes  [ ] No  [ ] Not tested

**Handoff output quality:**
- Layer 1 (frontmatter patch) accurate: [ ] Yes  [ ] No  [ ] Not tested
- Layer 2 (session log entry) accurate: [ ] Yes  [ ] No  [ ] Not tested
- Layer 3 (context block) accurate: [ ] Yes  [ ] No  [ ] Not tested

**Cognitive load observations:**
- Session start friction (care access check): 
- Handoff trigger felt natural: [ ] Yes  [ ] No
- Three-layer handoff manageable at end of session: [ ] Yes  [ ] No
- Low-energy handoff sufficient when tired: [ ] Yes  [ ] No

**Notable failures or unexpected behaviors:**


**Parameter change candidates (bring to design discussion):**


**Overall session notes:**
```
