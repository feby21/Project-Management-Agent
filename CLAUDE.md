# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this repo is
Documentation and prompt source for a **no-code** personal project manager agent. There is no application code. The "runtime" is a Claude Project + Claude scheduled tasks, using the Notion and Google Calendar connectors. This repo is the version-controlled source for its prompts, rules and requirements.

## Sources of truth
- **Live rules:** the Notion page "PMA Operating Manual". `docs/operating-manual.md` is a mirror of it. If the user says the manual changed in Notion, update the mirror to match — never the other way round without saying so.
- **Requirements:** `docs/PRD.md`.
- **Prompts:** `prompts/project-instructions.md` and `prompts/scheduled-tasks/*.md` are pasted verbatim into Claude. Keep each prompt self-contained: scheduled tasks start fresh sessions with no memory.

## Rules when editing
1. **Keep everything consistent.** A rule change (e.g. working hours) usually touches: `docs/operating-manual.md`, `docs/PRD.md` (planning rules + change log), `CHANGELOG.md`, and sometimes `prompts/project-instructions.md`. Check all of them.
2. **Never weaken the safety rules:** the agent writes only to the PMA Plan calendar, needs explicit approval before any calendar or This Week change, and scheduled tasks are read-only (the Sunday task may create one Draft Plan page only).
3. **Priority Score:** `notion/priority-score.formula` and `docs/scoring-rules.md` must describe exactly the same calculation.
4. **No secrets or personal identifiers:** no emails, calendar IDs, Notion page IDs, API keys or meeting links.
5. British English. Short sentences. Markdown only.
6. Add a dated line to `CHANGELOG.md` for every behavioural change.

## Common tasks
- *"Change my working hours to X"* → update manual section 4, PRD planning rules + change log, project instructions `<planning_rules>`, CHANGELOG.
- *"Add a workflow"* → manual section 6 (next letter), PRD features table, trigger phrase in project instructions, CHANGELOG.
- *"Update a scheduled task"* → edit its file in `prompts/scheduled-tasks/`; remind the user to paste it into the task in Claude.
