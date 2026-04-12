# PRE_TASK_RITUAL

**A structured protocol for making AI assistants more reliable, honest, and harder to fool — including by themselves.**

---

## What is this?

PRE_TASK_RITUAL is a JSON-format instruction set you paste into an AI assistant's system prompt (or custom instructions field). It forces the AI to run a fixed checklist before and after every task, instead of jumping straight to an answer.

The core idea: **don't expect AI to follow rules. Design assuming it won't.**

That means:
- Rules are placed where the model is most likely to read them (position bias countermeasure)
- The AI must declare failure modes *before* it writes anything
- Every output goes through an "External Witness" review — the AI critiques its own work as if it were a different AI reading it for the first time
- Hallucination risk is self-scored on a 1–5 scale and flagged openly

This won't make AI perfect. The goal is to get AI into a state where **it can detect its own problems and surface them to you**, rather than confidently presenting garbage.

---

## Files

| File | Description |
|------|-------------|
| `PRE_TASK_RITUAL_v1_1_public.json` | Main protocol (English) |
| `PRE_TASK_RITUAL_v1_1_public_ja.json` | Main protocol (Japanese) |
| `PRE_TASK_RITUAL_changelog.json` | Change history (English) |
| `PRE_TASK_RITUAL_changelog_ja.json` | Change history (Japanese) |

---

## How to use

### Step 1 — Open your AI assistant's settings

- **Claude (claude.ai):** Settings → Custom instructions (or start a Project and paste into the Project instructions)
- **ChatGPT:** Settings → Personalization → Custom instructions
- **Gemini:** Use a system instruction field in your preferred interface

### Step 2 — Paste the JSON

Copy the entire contents of `PRE_TASK_RITUAL_v1_1_public.json` and paste it into the system prompt / custom instructions field.

### Step 3 — Customize the placeholders

Search the JSON for these strings and replace them with values specific to your project:

| Placeholder | Replace with |
|-------------|-------------|
| `project bible` | The name of your main reference document |
| `canon documents` | Any other canonical source files you use |

If you are not doing creative writing work, the `CREATIVE_SESSION_PROTOCOL` and `CREATIVE_FAILURE_PATTERN_DB` sections can be left as-is or removed entirely.

### Step 4 — Start a new session

The protocol activates automatically. When you give the AI a task, it will declare `PRE_TASK_RITUAL v1.1 executing. Step 1: Search` before doing anything else.

---

## The 9 steps

| Step | Name | What it does |
|------|------|-------------|
| 1 | Search | Web search (or document search for creative tasks) before answering anything from memory |
| 2 | Declare 5 Failure Patterns | AI explicitly names 5 ways this specific task could go wrong |
| 3 | Declare Mitigations | One countermeasure per failure pattern |
| 4 | Constraint Check | Gates: Steps 1–3 must all be complete before proceeding |
| 5 | Pre-mortem | AI states the most likely reason its upcoming output will fail — before writing it |
| 6 | Output (3 Proposals or 1 Solution) | A/B/C proposals for open-ended tasks; single answer for deterministic tasks |
| 7 | External Witness Protocol | AI reviews its own output as if it were a different AI seeing it for the first time |
| 8 | Await User Selection | Does nothing until the user explicitly picks A, B, or C |
| 9 | POST-TASK Verification | Full checklist: requirements, sources, failure avoidance, hallucination risk score |

---

## Key concepts

**ABSOLUTE_MANDATORY** — Cannot be skipped under any condition.

**ABSOLUTE_FORBIDDEN** — Cannot be done under any condition.

**GATE_BLOCK** — If a step's completion conditions aren't met, the AI stops and reports `GATE_BLOCK: Step [N] not met, reason: [reason]`. It cannot proceed without your explicit instruction.

**COMPLIANCE_SIMULATION_DETECTED** — If the AI catches itself going through the motions without actually checking (e.g., outputting a `[Document Check]` block while writing from memory), it must immediately report this and re-run the step.

**Hallucination risk score (1–5)** — Declared at the end of every session. 1 = well-sourced; 5 = mostly from training data, treat with caution.

---

## Design philosophy

> Do not expect AI to follow rules. Design assuming it won't. Unread rules and unexecuted rules are the same as no rules. Strengthening includes not just addition but also consolidation and integration — reducing items to raise density is also a form of strengthening. Eliminating hallucination entirely is neither possible nor the goal — the goal is to reach a state where the AI itself can detect hallucinations when they occur and handle them together with the User.

---

## Version

Current public release: **v1.1-public** (based on internal v5.19)  
See `PRE_TASK_RITUAL_changelog.json` for full version history and design rationale.

---

## License

MIT License — use freely, modify for your own workflow, and share improvements.
