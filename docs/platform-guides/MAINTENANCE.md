# Platform Guides — Maintenance Instructions

**Last modified:** 2026-03-23  
**Purpose:** Instructions for using Cursor to validate and update SpoonGuide platform docs against current platform capabilities.

---

## When to run this

- **Quarterly** — Platforms change plans, models, and features frequently
- **When a user reports outdated info** — e.g., "Gemini setup steps don't match the current UI"
- **Before a release** — Ensure docs reflect what users will see
- **After a platform announcement** — New models, pricing changes, or feature launches

---

## Official sources to check

Fetch current information from these URLs. Do not assume — verify.

| Platform | Pricing & plans | Models & features |
|----------|-----------------|-------------------|
| **Gemini** | [support.google.com/gemini](https://support.google.com/gemini/answer/16275805) | [gemini.google/subscriptions](https://gemini.google/subscriptions) |
| **Claude** | [anthropic.com/pricing](https://www.anthropic.com/pricing) | Same page; check model availability |
| **ChatGPT** | [openai.com/pricing](https://openai.com/pricing) | [help.openai.com](https://help.openai.com) for Custom GPT limits |
| **Cursor** | [cursor.com/pricing](https://www.cursor.com/pricing) | [cursor.com/docs/models](https://www.cursor.com/docs/models) |

**Search tip:** Use the current year (e.g., 2026) when searching for third-party summaries. Platform docs are authoritative; use search to find model names, tier changes, or feature availability if the official pages are unclear.

---

## Step-by-step: Validate and update

### 1. Open Cursor with this repo

Ensure the SpoonGuide repo is your workspace. Open `docs/platform-guides/`.

### 2. Run the validation prompt

Paste the prompt below into a Cursor chat. It instructs the AI to fetch current data and compare it to the guides.

### 3. Review the output

The AI should produce:
- A comparison of what each guide says vs. what the platform currently offers
- A list of changes needed (model names, pricing, steps, limits)
- Suggested edits for each affected guide

### 4. Apply updates

Edit the relevant guide(s). For each change:
- Update the **Last modified** date to today (YYYY-MM-DD)
- Add a row to the **Version table** with the date and a brief description of changes

---

## Copy-paste prompt for Cursor

Use this prompt to run the validation. Adjust the year if needed.

```
I need you to validate and update the SpoonGuide platform guides against the current capabilities of each platform.

**Task:**
1. For each platform (Gemini, Claude, ChatGPT, Cursor), fetch current information from the official sources:
   - Gemini: support.google.com/gemini (limits), gemini.google/subscriptions (plans)
   - Claude: anthropic.com/pricing
   - ChatGPT: openai.com/pricing, help.openai.com for Custom GPTs
   - Cursor: cursor.com/pricing, cursor.com/docs/models

2. Read the current guides in docs/platform-guides/:
   - gemini-setup.md
   - claude-setup.md
   - chatgpt-setup.md
   - cursor-setup.md

3. Compare what each guide says (plans, model names, pricing, setup steps, limits) against what the platforms currently offer.

4. Produce a report:
   - What's outdated or wrong in each guide
   - What needs to be updated (with specific line/section references)
   - Suggested replacement text for each change

5. Apply the updates to the guide files. For each file changed:
   - Update "Last modified" to today's date (YYYY-MM-DD)
   - Add a version table entry with today's date and a brief description of the changes

Do not assume — fetch the current data. Use the current year (2026) in any web searches.
```

---

## What to verify in each guide

### All platforms

- [ ] Plan names and pricing (free vs paid)
- [ ] Model names (e.g., Gemini 3 Flash vs 3.1 Pro; Claude Sonnet vs Opus)
- [ ] Which features require paid vs free
- [ ] Setup steps (UI may have changed)
- [ ] Usage limits (messages/day, context window)

### Platform-specific

- **Gemini:** Gems availability on free tier; Pro/Thinking limits; model fallback behavior
- **Claude:** Projects on free tier; Sonnet vs Opus access
- **ChatGPT:** Custom GPT requirements (Plus only); knowledge file limits
- **Cursor:** Hobby vs Pro; model list and pricing; rules format (.mdc in .cursor/rules/)

---

## Version table format

When updating a guide, add a row like:

```
| 1.1 | 2026-06-15 | Updated Gemini model names to 3.2; corrected Pro daily limit to 120. |
```

Keep descriptions concise but specific enough that a future maintainer understands what changed.
