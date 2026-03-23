# SpoonGuide — Getting Started

**Last modified:** 2026-03-23  
**Version:** 1.0 — Initial getting-started guide with platform comparison

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial structure. Universal content: privacy notice, platform comparison, patient log setup, session start, handoff protocol, troubleshooting. |

---

## What SpoonGuide is

SpoonGuide helps patients with chronic illness (hEDS, POTS, MCAS, ME/CFS, CCI, Long Covid, and related conditions) manage their care through AI-assisted coaching. You use an LLM platform — Gemini, Claude, ChatGPT, or Cursor — loaded with SpoonGuide's parameters to get a coach that follows evidence-informed guardrails, supports your thinking, and helps you advocate with your care team.

**This is not a medical provider.** It can make mistakes, including confident-sounding mistakes. Use it to support your thinking and care team conversations — not to replace them. [→ Learn about AI risks in health tools](docs/ai-safety.md)

---

## Privacy notice

**Please read this before you begin setup.**

Your conversations are processed by whichever LLM platform you choose (Google, Anthropic, OpenAI, or Cursor's model providers). Each platform has its own data retention and privacy policies.

- **SpoonGuide does not collect or store your data.** This project has no servers that receive your information.
- **Your patient log file lives on your device.** You choose when to share it by pasting it into the chat. It is never uploaded automatically.
- **Platform policies vary.** Check your chosen platform's privacy and activity retention settings. You can often turn off or reduce how long your conversations are stored.

---

## Choose your platform

Pick one platform below. Each has **free** and **paid** setup options. Both paths work — choose based on your budget and how often you'll use the coach.

| Platform | Free setup | Paid setup | Notes |
|----------|------------|------------|-------|
| [Gemini](docs/platform-guides/gemini-setup.md) | Paste parameters each session; Gems also available on free tier | Google AI Plus/Pro for higher limits, Pro 3.1 model | Beginner-friendly |
| [Claude](docs/platform-guides/claude-setup.md) | Projects free — create a Project with parameters | Pro for Opus, more usage | Strong instruction-following |
| [ChatGPT](docs/platform-guides/chatgpt-setup.md) | Paste parameters each session | Plus for Custom GPTs | Widely familiar interface |
| [Cursor](docs/platform-guides/cursor-setup.md) | Hobby tier (limited usage) | Pro for frontier models | **Advanced** — AI can edit your log file directly |

Follow the setup guide for your chosen platform. The guides walk you through loading SpoonGuide's parameters and creating your coach.

---

## Set up your patient log

Your patient log is a personal file where you record your conditions, medications, symptoms, and session summaries. The coach uses it to understand your history and tailor its support. You keep it on your device and paste it into the chat when you start a session.

1. Download the patient log template: [patient-log-template.md](templates/patient-log-template.md)
2. Open it in any text editor (Notes, TextEdit, Notepad, VS Code — anything that saves plain text)
3. Save it with a name you'll recognize — for example: `jd-patient-log.md`
4. Fill in the YAML frontmatter fields (the section at the top between the `---` lines) with what you know right now. It's okay to leave fields blank and fill them in during your first session.
5. You do not need to add any log body entries yet.

**Your log file stays on your device.** It is never uploaded automatically. You choose when to share it by pasting it into the chat.

---

## Start your first session

1. Open your coach (Gem / Claude Project / Custom GPT / Cursor chat) and start a new conversation.
2. Paste your patient log.
3. Use an opening message like this, filling in the bracketed parts:

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

## The handoff protocol

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
3. **Layer 1:** Find the YAML frontmatter at the top and update the fields shown (only fields that changed need updating)
4. **Layer 2:** Paste the session entry at the bottom of your log body
5. **Layer 3:** Paste this at the start of your next session, before or after your log
6. Start a new conversation for your next session

You can also trigger a handoff proactively before you get tired — the coach may suggest it if the session has been long. You don't have to wait for it to suggest.

---

## If something seems wrong

### The coach ignores part of the parameters

**What it looks like:** The coach skips the care access check, doesn't do the timeline restatement, proposes something on the hard refusal list, or otherwise doesn't behave as described.

**Why it happens:** LLMs don't always follow complex instructions perfectly, especially on free or lighter models. This is a known limitation.

**What to do:** Gently redirect: "Can you check the parameters document and tell me what it says about [topic]?" If it happens consistently, note it and report it in the [repo issues](https://github.com/spoon-o-matic/spoonguide/issues).

### The coach seems to have forgotten something

**What it looks like:** It contradicts something established earlier, misses a contraindication, or seems to be missing context.

**Why it happens:** Context window attention degrades in long sessions.

**What to do:** Trigger a handoff and start a fresh session. If you're mid-topic, say "before we continue — quick handoff" and it will generate the block without derailing the conversation.

### The coach says something that seems clinically wrong

**What it looks like:** Information that contradicts what you know about your conditions, a dose that seems off, a claim that surprises you.

**What to do:** Do not act on it without checking. Note it, look it up, and bring it to your care team if relevant. This is one of the core limitations of AI health tools. See [AI risks in health tools](docs/ai-safety.md) for more.

---

## Next steps

- **Platform-specific troubleshooting** — See your platform's setup guide (Gemini, Claude, ChatGPT, or Cursor) for issues like model switching or platform-specific limits.
- **Parameters document** — [chronic-illness-coach-parameters.md](docs/parameters/chronic-illness-coach-parameters.md) — the full system prompt and behavioral specification.
- **AI safety** — [ai-safety.md](docs/ai-safety.md) — risks and limitations of AI in health tools.
