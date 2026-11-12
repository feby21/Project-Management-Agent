# Personal Project Manager Agent (PMA)

A no-code AI project manager built on **Claude**, **Notion** and **Google Calendar**. It keeps my projects in one place, ranks what deserves my time, plans work into my calendar, sends me a morning brief, and replans when things overrun — while never touching my fixed commitments without approval.

> Status: v1.2 MVP, in daily use since 12 Nov 2026.

## How it works

```mermaid
flowchart LR
    Me([Me]) -- chat: plan / update / approve --> CP[Claude Project<br/>Personal Project Manager]
    ST[Scheduled tasks<br/>08:44 brief · evening reminder · Sunday review] -- run on schedule --> CP
    CP -- read + write --> N[(Notion<br/>Tracker · This Week · Manual)]
    CP -- read all · write PMA Plan only --> GC[(Google Calendar)]
    ST -- read --> N
    ST -- read --> GC
```

| Component | Role |
|---|---|
| **Claude Project** "Personal Project Manager" | The agent. Custom instructions in [`prompts/project-instructions.md`](prompts/project-instructions.md). |
| **Notion** | Master Project Tracker (database), This Week (goals + daily to-dos), Scoring Rules, **PMA Operating Manual** (the rulebook). |
| **Google Calendar** | University Schedule, Part time Job, TO DOs, Social, Trips and Holiday (read-only) + **PMA Plan** (the only calendar the agent writes to). |
| **Claude scheduled tasks** | Morning brief, evening check-in reminder, Sunday review + draft plan. Prompts in [`prompts/scheduled-tasks/`](prompts/scheduled-tasks/). |

## Daily rhythm

| When | Automatic | My part |
|---|---|---|
| 08:44 daily | Morning brief (read-only) | Read it |
| Evening | Check-in reminder | Send `evening update: …`, approve the replan |
| Sunday 17:38 | Weekly review + Draft Plan page in Notion | Say `approve draft plan` |
| Any time | — | `urgent: …`, `check my calendar`, `plan my week` |

## Repository structure

```
.
├── README.md                       ← you are here
├── CLAUDE.md                       ← guidance for Claude Code working in this repo
├── CHANGELOG.md
├── docs/
│   ├── PRD.md                      ← product requirements (v1.2)
│   ├── operating-manual.md         ← mirror of the Notion "PMA Operating Manual"
│   └── scoring-rules.md            ← Priority Score rules (mirror of Notion page)
├── prompts/
│   ├── project-instructions.md     ← paste into the Claude Project
│   └── scheduled-tasks/
│       ├── morning-brief.md
│       ├── evening-reminder.md
│       └── sunday-review.md
└── notion/
    ├── database-schema.md          ← Master Project Tracker properties + views
    └── priority-score.formula      ← Notion formula for the Priority Score column
```

## Set it up yourself

1. **Notion:** create a page "Personal Project Manager" with an inline database "Master Project Tracker" using [`notion/database-schema.md`](notion/database-schema.md). Add the formula from [`notion/priority-score.formula`](notion/priority-score.formula). Create child pages "Scoring Rules" and "PMA Operating Manual" from the files in `docs/`, and a "This Week" section under the database.
2. **Google Calendar:** create the calendars University Schedule, Part time Job, TO DOs, Social, Trips and Holiday and **PMA Plan**.
3. **Claude:** connect the Notion and Google Calendar connectors. Create a Project "Personal Project Manager" and paste [`prompts/project-instructions.md`](prompts/project-instructions.md) into its instructions.
4. **Scheduled tasks:** create the three tasks with the prompts in [`prompts/scheduled-tasks/`](prompts/scheduled-tasks/) and move them into the project.
5. In the project, say **`plan my week`**.

## Design principles

1. Clarity over complexity — no admin overhead.
2. Action over information — tell me what to do next.
3. Realistic planning — respects lectures, shifts, rest.
4. Human approval over automation — the agent writes only to its own calendar, and only after I approve.
5. One source of truth — rules live in the Notion manual; every chat and scheduled task reads it.
