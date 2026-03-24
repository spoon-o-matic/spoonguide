# SpoonGuide

**Last modified:** 2026-03-24
**Version:** 1.1 — Platform table aligned with GETTING_STARTED comparison

---

An open-source chronic illness coaching tool for patients with hEDS, POTS, MCAS, ME/CFS, CCI, Long Covid, and related conditions.

**CAUTION: Unstable project in active pre-Alpha development**

## What SpoonGuide is

SpoonGuide helps patients with chronic illness (hEDS, POTS, MCAS, ME/CFS, CCI, Long Covid, and related conditions) manage their care through AI-assisted coaching. You use an LLM platform — Gemini, Claude, ChatGPT, or Cursor — loaded with SpoonGuide's parameters to get a coach that follows evidence-informed guardrails, supports your thinking, and helps you advocate with your care team.

**SpoonGuide is for you to manage your own health.** Use only your own data — do not upload or manage someone else's health information.

**This is not a medical provider.** It can make mistakes, including confident-sounding mistakes. Use it to support your thinking and care team conversations — not to replace them. [→ Learn about AI risks in health tools](docs/ai-safety.md)

**SpoonGuide cannot guarantee your safety and may contain mistakes.** SpoonGuide is a toolset intended to help you get more helpful results out of your LLM conversations about your health, but it CANNOT promise you accuracy or safety. Always trust your own judgment and your own decisions made with your doctor more than you trust an LLM. SpoonGuide itself was created with the help of an LLM and may contain mistakes. 

If you ever get concerning results with an LLM using SpoonGuide, or notice something in SpoonGuide materials that seems wrong, please [file an issue](https://github.com/spoon-o-matic/spoonguide/issues) or [submit a PR correction](https://github.com/spoon-o-matic/spoonguide/pulls) on GitHub to help us improve SpoonGuide.

## SpoonGuide is pre-Alpha and unstable. Use with caution.
SpoonGuide is currently in "pre-Alpha", which means that it is in an extremely new, untested, unfinished and unstable state. Any use should be considered as "testing" the project for its effectiveness and stability. All project contents are subject to rapid change and evolution.

 If you are testing SpoonGuide, please treat any conversations with your LLM with even more skepticism than usual, and be willing to submit [issues](https://github.com/spoon-o-matic/spoonguide/issues) to help SpoonGuide reach a stable and tested Alpha status. You can also email experiences and feedback to [michelle@michellefunk.com](mailto:michelle@michellefunk.com). Always include the version number from the [parameters document](docs/parameters/chronic-illness-coach-parameters.md) in any issue.

**SpoonGuide can NEVER guarantee your safety and may contain mistakes.** SpoonGuide is a toolset intended to help you get more helpful results out of your LLM conversations about your health, but it CANNOT promise you accuracy or safety. Always trust your own judgment and your own decisions made with your doctor more than you trust an LLM.

SpoonGuide itself was created with the help of LLMs and may contain mistakes. Never assume that SpoonGuide or an LLM using SpoonGuide knows better than you and your care team.

If you ever get concerning results with an LLM while testing SpoonGuide, or notice something in SpoonGuide materials that seems wrong, please [file an issue](https://github.com/spoon-o-matic/spoonguide/issues) or [submit a PR correction](https://github.com/spoon-o-matic/spoonguide/pulls) on GitHub to help us improve SpoonGuide.

## What you can do today

You can use SpoonGuide today with no installation. Choose an AI platform (Gemini, Claude, ChatGPT, or Cursor), load SpoonGuide's parameters, and get a coach that follows evidence-informed guardrails and helps you track your care. You keep a personal log file on your device and paste it into the chat at the start of each session. Free and paid options are available for every platform.

**[→ Get started](GETTING_STARTED.md)** — Choose your platform, set up your log, and run your first session.

## Governing principles

Three principles govern this project. Where they conflict and no design solution exists, informed user choice leads.

- **Accessibility.** The system must be usable by patients with disability, fatigue, cognitive load, and limited technical ability. Accessibility is a requirement at every tier, not a future enhancement.

- **Privacy.** Patients have full control over their data at every tier. A fully local, zero-data-leaving-your-machine option exists at every milestone where data is handled. Hosted or cloud options are opt-in only, with plain-language explanation of trade-offs.

- **User autonomy.** Patients make informed decisions about their own trade-offs. Where accessibility and privacy conflict and no design solution is available, the system presents the trade-off clearly and the patient chooses.

## Current milestone

**Current milestone: Milestone 1 — Tier 1.5: Usable Without Any Setup**

## Important notice

> **This is not a medical provider.**
>
> SpoonGuide is an AI coaching tool, not a substitute for medical care. It can make mistakes—including confident-sounding mistakes. It may agree with you when it should push back. It may not know enough about your specific conditions to give you accurate information. Use it to support your thinking and your care team conversations—not to replace them.
>
> [→ Learn about AI risks in health tools](docs/ai-safety.md)

**Intended use:** SpoonGuide is for individuals managing their own health while under professional medical supervision. Use only your own data. Do not upload or manage health information about others. 

Do not ever substitute an LLM response for the care of a qualified professional. SpoonGuide is designed to assist you in getting better responses from LLMs that can help you in self-management activities that you are doing already.

We make our best efforts throughout our documentation and instruction to inform you of the risks of using LLMs for anything regarding your personal health. However, we cannot be responsible for your safety -- only you can be responsible for your safety.

As a toolset built with the help of AI tooling, as well as a patient-created community tool, SpoonGuide may contain factual or other errors due to human or technical errors.

Use your own judgment, and please submit [issues](https://github.com/spoon-o-matic/spoonguide/issues) to the SpoonGuide project if you find any problems in our documentation.

## Quick links

- [Getting Started](GETTING_STARTED.md)
- [Roadmap](docs/roadmap.md)
- [Contributing](CONTRIBUTING.md)
- [AI Safety](docs/ai-safety.md)
- [AI Terms Glossary](docs/ai-glossary.md)
- [Community Commitment](docs/community-commitment.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)

## Platform setup guides

| Platform | Guide | Notes |
|----------|-------|-------|
| [Gemini](docs/platform-guides/gemini-setup.md) | Google Gemini | Persistent **Gem** + knowledge file on free or paid; paid improves model and limits |
| [Claude](docs/platform-guides/claude-setup.md) | Anthropic Claude | Persistent **Project** on free (Sonnet, daily cap); Pro adds Opus and more usage |
| [ChatGPT](docs/platform-guides/chatgpt-setup.md) | OpenAI ChatGPT | Free: paste parameters each new chat; Plus: **Custom GPT** with knowledge file |
| [Cursor](docs/platform-guides/cursor-setup.md) | Cursor IDE | Advanced; AI can edit your Patient Log; Hobby or Pro |

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-23 | Initial README. Project overview, governing principles, intended use, platform guide links. |
| 1.1 | 2026-03-24 | Platform notes: persistent Gem/Project, ChatGPT paste vs Custom GPT, Cursor Hobby/Pro. |
