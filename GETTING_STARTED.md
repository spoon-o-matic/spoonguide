# SpoonGuide — Getting Started

**Last modified:** 2026-03-25  
**Version:** 1.6 — Profile: lifestyle/mechanical treatments + vitals baseline (parameters §6.2)

## What SpoonGuide is

SpoonGuide helps patients with chronic illness (hEDS, POTS, MCAS, ME/CFS, CCI, Long Covid, and related conditions) manage their care through AI-assisted coaching. You use an LLM platform — Gemini, Claude, ChatGPT, or Cursor — loaded with SpoonGuide's parameters to get a coach that follows evidence-informed guardrails, supports your thinking, and helps you advocate with your care team.

**SpoonGuide is for you to manage your own health.** Use only your own data — do not upload or manage someone else's health information.

**This is not a medical provider.** It can make mistakes, including confident-sounding mistakes. Use it to support your thinking and care team conversations — not to replace them. [→ Learn about AI risks in health tools](docs/ai-safety.md)

**SpoonGuide cannot guarantee your safety and may contain mistakes** SpoonGuide is a toolset intended to help you get more helpful results out of your LLM conversations about your health, but it CANNOT promise you accuracy or safety. Always trust your own judgment and your own decisions made with your doctor more than you trust an LLM. SpoonGuide itself was created with the help of an LLM and may contain mistakes. 

If you ever get concerning results with an LLM using SpoonGuide, or notice something in SpoonGuide materials that seems wrong, please [file an issue](https://github.com/spoon-o-matic/spoonguide/issues) or [submit a PR correction](https://github.com/spoon-o-matic/spoonguide/pulls) on GitHub to help us improve SpoonGuide.
---

## Privacy notice

**Please read this before you begin setup.**

Your conversations are processed by whichever LLM platform you choose (Google, Anthropic, OpenAI, or Cursor's model providers). Each platform has its own data retention and privacy policies.

- **SpoonGuide does not collect or store your data.** This project has no servers that receive your information.
- **Your Patient Log file lives on your device.** You choose when to share it by **uploading** it as a file attachment (or pasting it if upload is not available). It is never uploaded automatically.
- **Platform policies vary.** Check your chosen platform's privacy and activity retention settings. You can often turn off or reduce how long your conversations are stored.

---

## Choose your platform

SpoonGuide runs on **Gemini, Claude, ChatGPT, or Cursor**. The biggest practical differences are whether the platform **keeps your coaching instructions between chats** without you pasting the long parameters file every time, and whether you want a **normal web app** or **Cursor** (a code editor where the AI can **edit your Patient Log file** for you after a handoff). Limits, models, and privacy settings differ by platform and plan — see the [privacy notice](#privacy-notice) above and each setup guide below.

On **Gemini** and **Claude**, free and paid use the **same setup steps**; paying mainly upgrades **model quality** and **usage limits**. **ChatGPT** is different on the free tier: you paste the full parameters document at the start of each new chat unless you use **Plus** and a Custom GPT.

| Platform | Free setup | Paid setup | Consider this if… |
|----------|------------|------------|-------------------|
| [Gemini](docs/platform-guides/gemini-setup.md) | Create a **Gem** and upload the parameters as a **knowledge file** — the coach stays configured between chats. Free tier uses the **Fast** model. | Same Gem workflow; paid (e.g. Google AI Plus/Pro) adds **Pro 3.1** / **Thinking**, higher daily limits, and often a larger context window. | You already use Google, or you want a **persistent coach on the free tier** without pasting the full parameters each session. |
| [Claude](docs/platform-guides/claude-setup.md) | Create a **Project**, upload the parameters as project knowledge, add short project instructions — **persistent** between chats. Free tier uses **Sonnet** with a **daily message cap** (roughly tens of messages; resets periodically). | Same Project workflow; **Pro** adds **Opus** and roughly **more daily usage**. | You want a **strong free persistent setup** (no full-parameter paste each chat) and like Anthropic’s chat experience. |
| [ChatGPT](docs/platform-guides/chatgpt-setup.md) | **Paste the entire parameters document** at the start of **each** new chat (free tier). | **Plus:** build a **Custom GPT** with the parameters as a **knowledge file** — same persistence idea as a Gem or Project. | You already use ChatGPT daily; free is fine to try SpoonGuide, **Plus** removes the repeat paste. |
| [Cursor](docs/platform-guides/cursor-setup.md) | **Hobby** plan (limited monthly usage). Load parameters via a **Cursor rule** and/or **`@` file** reference; **clone the repo** so the parameters path is local. | **Pro:** more usage and access to **frontier models**; same workflow. | You’re comfortable in an editor and want the AI to **apply Profile and Session Log updates to your log file** instead of only copy-pasting. |

**Still unsure?**

- **Least copy-paste on a free tier:** **Gemini** (Gem) or **Claude** (Project) — both keep the parameters loaded in a persistent coach.
- **ChatGPT is home base:** start on **free** (paste each new chat); move to **Plus** if you want a Custom GPT and skip that step.
- **Less manual merging after handoff:** **Cursor** — only if the editor workflow works for you; otherwise use a web platform and merge the Profile diff / Session Log blocks into your Patient Log yourself.

Follow the setup guide for your chosen platform. Each guide covers free and paid in **one document** so you can upgrade without switching files.

---

## Set up your Patient Log

Your **Patient Log** is a personal file where you record your conditions, medications, symptoms, and session summaries. The coach uses it to understand your history and tailor its support. You keep it on your device. When you start a session, **upload** that markdown file to the chat if your app supports file attachments (Gemini, Claude, ChatGPT, and Cursor generally do). If upload is not available, paste the full file text instead.

**Your Patient Log = your Profile + all your Session Logs.** The Profile (at the top) holds your stable information — medications, supplements, triggers, contraindications, and related fields. It can also include **lifestyle and mechanical treatments** (e.g. physical therapy, TENS, tVNS) and a **resting vitals baseline** (blood pressure and heart rate), as defined in the [parameters document](docs/parameters/chronic-illness-coach-parameters.md) (Section 6.2, YAML frontmatter schema). Each Session Log is a record of one coaching session, added over time. The coach helps you update both via **handoff** (Profile diff + Session Log entry).

1. Download the patient log template: [patient-log-template.md](templates/patient-log-template.md)
2. Open it in any text editor (Notes, TextEdit, Notepad, VS Code — anything that saves plain text)
3. Save it with a name you'll recognize — for example: `jd-patient-log.md`
4. **Profile:** The top section between the `---` lines holds your stable information. You **do not** need to manually enter any information here - most users should leave it blank unless very comfortable with writing markdown. You can either generate a profile to start with, or just create your SpoonGuide and have it fill out the profile in "intake". See [Choosing how to fill your Profile](#choosing-how-to-fill-your-profile) for more details.
5. Do not add any Session Log entries yet.

### Choosing how to fill your Profile

You **do not** need a finished Profile before your first session. Having a Patient Log **file** (even with empty fields) still helps: you have a place to merge **Profile** diffs and paste **Session Log** entries after handoffs. 

**1. Coach onboarding — configure the coach, then intake in chat**  
Finish platform setup (Gem / Project / Custom GPT / Cursor), **upload** your Patient Log file **or** paste it **as-is** (empty Profile is fine), and say you want to start with intake. The coach follows **Section 4: Patient History Intake Protocol** in the [parameters document](docs/parameters/chronic-illness-coach-parameters.md).

- **Works well if:** You want the **fewest** steps before talking to the coach, or conversation is easier than editing the structured top section.  
- **Trade-offs:** The first session is **slower** and more Q&A-heavy. You still get Profile material over time — especially via **handoff** — rather than one perfect block before you start.

**2. LLM-assisted — Profile onboarding prompt**  
Use a copy-paste prompt so an LLM turns your narrative or short answers into Profile text you paste into your log. See [Profile onboarding (LLM-assisted)](docs/prompts/profile-onboarding.md).

- **Works well if:** You want a **draft** Profile **before** your first coached session, or you prefer one brain-dump instead of editing structured text.  
- **Trade-offs:** You send health-related text to **whichever** LLM you use (sometimes before your SpoonGuide coach exists). Treat the result as a **draft** — check meds, diagnoses wording, and contraindications; fix indentation if needed.

**3. Manual — edit the Profile in your file**  
If you are comfortable working with markdown and don't find the profile's text confusing, type or paste into the top section yourself (alone or alongside Session Log entries later).

- **Works well if:** You like working directly in the file, or you already have tidy lists (meds, conditions) to copy in.  
- **Trade-offs:** No extra LLM step to **create** the initial Profile structure, but spacing and list shape matter; a Markdown-friendly editor ([below](#picking-an-app-to-edit-your-patient-log)) reduces mistakes.

**How these compare:** Paths **1** and **2** both involve sharing health context with an LLM. Path **1** uses your **configured SpoonGuide coach** (full parameters from the first message). Path **2** is optional when you want a **single structured paste** early, including from a generic chat before setup. Path **3** avoids an LLM for **building** the initial Profile yourself (you still **upload or paste** the Patient Log when you run a session).

### Picking an app to edit your Patient Log

The top section is **structured** (similar to a form in text form). A **Markdown-friendly** editor — syntax highlighting, lists, optional preview — can reduce mistakes and make long Session Log entries easier to read.

**Plain text is still enough.** Notes, TextEdit, Notepad, VS Code, or any editor that saves plain text works fine. The apps below are optional.

If you want a more comfortable experience, including on **phone or tablet**, you might try one of these (SpoonGuide does not endorse any vendor; app names, pricing, and features change — verify before you rely on them):

| App | Mobile / desktop | Notes |
|-----|------------------|--------|
| **Bear** | iOS, macOS | Markdown-focused; **Apple only.** If you use Bear’s sync, your content may be stored on the vendor’s systems. |
| **iA Writer** | iOS, Android, Mac, Windows | Minimal writing workflow; **paid** on some platforms. |
| **Obsidian** | iOS, Android, Mac, Windows, Linux | Local-first option available; **sync** (official or third-party) is a separate choice with its own privacy trade-offs. |
| **Markor** | Android | Free / open source; good option if you want no-cost editing on Android. |
| **1Writer** | iOS | Markdown-oriented editor for iPhone/iPad. |

**Privacy:** If an app **syncs** your notes to the cloud, that can send file contents to that company — a different trade-off from pasting into an LLM, but still **your choice** about what leaves your device. See the [privacy notice](#privacy-notice).

**Accessibility:** Choose an app that works well with **your** assistive technology on **your** devices.

**Your Patient Log stays on your device.** It is never uploaded automatically. You choose when to share it by uploading the file (or pasting) into a session.

---

## Start your first session

1. Open your coach (Gem / Claude Project / Custom GPT / Cursor chat) and start a new conversation.
2. **Upload** your Patient Log markdown file as an attachment. If your app does not support uploads, paste the full contents of the file instead.
3. **After the first session:** also **paste your Context Bridge** from the previous handoff in the same message (or immediately after), so the coach picks up where you left off. Skip this on your very first session.
4. Use an opening message like this, filling in the bracketed parts:

```
Hi — I'm starting a new session. I've attached my Patient Log (markdown file).

[If continuing from a handoff, paste your Context Bridge block here.]

I'd like to start by [tell the coach what you want to focus on — for example: "doing my intake" / "discussing my current symptoms" / "understanding my POTS better"].
```

**What to expect:**
- The coach will ask about care access and caregiver availability at the start of every session. This is part of the protocol.
- If you don't share a log, it will offer a lighter intake instead.
- If you share a log with an **empty or sparse** Profile, expect **onboarding-style questions** the first time — that is normal; you do not need a pre-filled Profile.
- First sessions will feel slower as the coach gathers context. This is normal.

---

## The handoff protocol

### Why it exists

AI models don't retain memory between conversations. As a session grows longer, earlier details receive less reliable attention. The handoff captures everything important so the next session starts with full context.

### How to trigger it

Type one of these words at any point during a session:

- `handoff`
- `new chat`
- `session summary`

### What you'll get (two steps)

The coach uses a **two-step** handoff so you can check what changed **before** copying structured YAML:

1. **Prose changelog** — A short list of Profile (top-of-file) changes: ADD / UPDATE / REMOVE by field. Read it and confirm it is accurate (or ask the coach to fix it).
2. **Three separate copy blocks** — After you confirm, the coach gives you **three** labeled sections, each with its own code fence:
   - **Profile diff** — YAML to **merge manually** into the `---` section at the top of your Patient Log (only what changed; lists use block style with `-` lines, not `["like", "this"]`).
   - **Session Log entry** — Markdown to **append** to the bottom of your Patient Log.
   - **Context Bridge** — Markdown to **copy for your next session**; paste it when you open the next chat **together with uploading** your saved Patient Log file.

You do **not** copy one giant combined block anymore—use each section for its purpose.

### If you're too tired for the full handoff

Say **"low energy handoff"** — you'll get the **Context Bridge** only. A note will remind you to update Profile and Session Log when you have more capacity.

### Step-by-step after handoff

1. Read the prose changelog and confirm (or correct) it with the coach.
2. Copy the **Profile diff** YAML block and merge those changes into the top of your Patient Log file by hand.
3. Copy the **Session Log entry** block and paste it at the bottom of your Patient Log.
4. **Save** your Patient Log file.
5. Copy the **Context Bridge** block to your clipboard (or a scratch note).
6. Start a **new** chat for your next session: **upload** the saved Patient Log file and **paste** the Context Bridge; add a short line about what you want to focus on today.

You can also trigger a handoff proactively before you get tired — the coach may suggest it if the session has been long. You don't have to wait for it to suggest.

---

## If something seems wrong

### The coach ignores part of the parameters

**What it looks like:** The coach skips the care access check, doesn't do the timeline restatement, proposes something on the hard refusal list, or otherwise doesn't behave as described.

**Why it happens:** LLMs don't always follow complex instructions perfectly, especially on free or lighter models. This is a known limitation.

**What to do:** Gently redirect: "Can you check the parameters document and tell me what it says about [topic]?" If it happens consistently, note it and report it in the [repo issues](https://github.com/spoon-o-matic/spoonguide/issues).

### The coach seems to have forgotten something

**What it looks like:** It contradicts something established earlier, misses a contraindication, or seems to be missing context.

**Why it happens:** The AI's context window (its working memory for the conversation) has limits; attention to earlier details degrades in long sessions.

**What to do:** Trigger a handoff and start a fresh session. If you're mid-topic, say "before we continue — quick handoff" and it will start the handoff flow (prose changelog first, then copy blocks after you confirm) so you can create a new chat and continue the conversation.

### The coach says something that seems clinically wrong

**What it looks like:** Information that contradicts what you know about your conditions, a dose that seems off, a claim that surprises you.

**What to do:** Do not act on it without checking. Note it, look it up, and bring it to your care team if relevant. This is one of the core limitations of AI health tools. See [AI risks in health tools](docs/ai-safety.md) for more.

---

## Next steps

- **Platform-specific troubleshooting** — See your platform's setup guide (Gemini, Claude, ChatGPT, or Cursor) for issues like model switching or platform-specific limits.
- **Parameters document** — [chronic-illness-coach-parameters.md](docs/parameters/chronic-illness-coach-parameters.md) — the full system prompt and behavioral specification.
- **AI safety** — [ai-safety.md](docs/ai-safety.md) — risks and limitations of AI in health tools.
- **AI terms glossary** — [ai-glossary.md](docs/ai-glossary.md) — plain-language definitions of LLM, context, tokens, and SpoonGuide terms like Profile, Session Log, and Context Bridge.

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial structure. Universal content: privacy notice, platform comparison, patient log setup, session start, handoff protocol, troubleshooting. |
| 1.1 | 2026-03-23 | Handoff protocol: replaced Layer 1/2/3 with Profile, Session Log, Context Bridge. Added Patient Log framing. Plain-language replacements for YAML/frontmatter. Glossary link. |
| 1.2 | 2026-03-24 | Choose your platform: parallel comparison, correct Gemini free path. |
| 1.3 | 2026-03-24 | Patient Log: optional Markdown-friendly editors (mobile-capable); link to LLM-assisted Profile onboarding prompt. |
| 1.4 | 2026-03-24 | Profile optional before first session; “Choosing how to fill your Profile” (manual vs LLM-assisted vs coach onboarding) with trade-offs; first-session note when Profile is sparse. |
| 1.5 | 2026-03-25 | Session start: upload Patient Log file (paste fallback) + Context Bridge after first session. Handoff: two-step validation, three separate copy blocks (Profile diff, Session Log, Context Bridge). Aligns with parameters v1.4 Phase 1. |
| 1.6 | 2026-03-25 | Patient Log overview: Profile may include lifestyle/mechanical treatments and vitals baseline (parameters §6.2). |
