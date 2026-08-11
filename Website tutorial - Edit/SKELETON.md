# SKELETON — Universal structure for every generated CLAUDE.md

Every project's `CLAUDE.md` is generated from this skeleton, filled with the
chosen template + `PROFILE.md`. The same content is written to `AGENTS.md` so
Codex, Cursor and Gemini CLI read it too.

Nine blocks. Keep each tight — a bloated CLAUDE.md gets ignored.

---

## 1. Context & goal
One paragraph: what this project is, who it's for, what "done" means. Pulled from
`PROJECT.md`. The single must-work thing stated explicitly.

## 2. Role & scope of the lead
The Claude session is the **project lead and orchestrator**, not the sole worker.
Its job: read instructions, make decisions, delegate to the right expertise,
review results, recover from errors, keep the system improving. It does not try
to do everything itself.

## 3. Always do first
Per-template startup actions (e.g. websites: invoke `frontend-design`, start the
local server). Plus: read `PROFILE.md`, this file, `PROJECT.md`, and `LOG.md`
before acting.

## 4. Environment
Paths, exact commands, versions, OS-specific quirks. This is where hardcoded
truths live (server command, screenshot command, tool locations). Windows.

## 5. Capability register (project-local view)
Which skills / plugins / MCPs / repos / agents are installed for this project,
what each is for, and **when NOT to use it**. Grows during the project via
`SETUP.md`. Anything new is proposed to me and installed only after approval.

## 6. Working loop — with a verification gate
Every task follows: attempt → **verify against ground truth** → fix → re-verify →
stop only when a defined stop-condition is met (not after one pass). The
verification method is template-specific (screenshot-compare for web, tests for
tools, a brand-voice checklist for content).

Two rules that always apply here:

**The friction ladder**
- Attempts 1–2: try normally.
- After 2 failures on the same problem: stop guessing, get ground truth (DOM,
  screenshot, console, logs).
- After 3: switch tool/agent; actively search for a skill/MCP/agent for this
  exact problem.
- After 4: escalate to me with what was tried + two concrete options.
- Every firing → `LOG.md` entry.

**The review gate**
- No result from an external agent (Codex, Gemini, a sub-agent) is accepted
  without the lead reviewing it for errors first. Accuracy compounds downward:
  90% per step is 59% over five steps. The gate after every handoff is what keeps
  the system reliable.

## 7. Output defaults
Per-template defaults for what gets produced and where it's saved.

## 8. Hard rules
The non-negotiables — mostly negative rules ("do not X"). These carry the most
weight; they come from real friction, not theory. The autonomy exceptions live
here: **do not** commit, push, deploy, make paid API calls, or overwrite/delete
files without my approval.

## 9. Log & retro protocol
- **During the project:** append to `LOG.md` on every decision, break, and fix —
  date, what broke, what we changed, which rule (if any) it produced.
- **At the end:** I paste the adapted `CLAUDE.md` + `LOG.md` back into the
  meta-project. We run the retro (`lessons/retros/_TEMPLATE.md`), distil lessons,
  and apply the promotion rule (a lesson enters a template only after recurring
  in two projects).

---

## Orchestration & cost model (applies to every project)
- **Claude = lead:** architecture, decisions, review, pushing back on me. Costly,
  so used sparingly.
- **Codex CLI / Gemini CLI = executors:** bulk code, refactors, research. Free
  tiers — be liberal here. Every output passes the review gate.
- **Deterministic Python scripts = everything repeated twice.** No AI, so free
  and reliable.
- **Sub-agents inside Claude: sparingly**, only where isolation genuinely helps
  (e.g. a reviewer that never builds). Each one costs a full context window.
- Lock model-per-role in the sub-agent/agent definition, not in your head.
- `/clear` between unrelated tasks to avoid resending stale history.
