# Master Project Tracker — Notion database schema

Inline database on the page **Personal Project Manager**.

| Property | Type | Values / notes |
|---|---|---|
| Name | Title | Project name |
| Category | Select | University, Career, Coding & Technical, Personal, Business & Creative |
| Status | Status | Idea, Planned (to do) · Active (in progress) · On Hold · Completed |
| Deadline | Date | Optional; date or date-time. Most non-university projects have none. |
| Importance | Select | Critical, High, Medium, Low |
| Strategic Value | Select | Critical, High, Medium, Low |
| Estimated Hours | Number | Total effort estimate |
| Progress | Number (percent) | Stored as a fraction: 0.5 = 50% |
| Last Worked On | Date | Updated by the evening check-in |
| Next Action | Text | The single next step |
| Priority Score | Formula | See `priority-score.formula`; 20–100, Completed = 0 |

## Suggested views
- **Active Projects** — Status = Active, sorted by Priority Score (desc)
- **Upcoming Deadlines** — Deadline within next 14 days
- **Backlog** — Status = Idea or Planned
- **Needs Attention** — Last Worked On more than 7 days ago, or Priority Score > 70
- **Completed** — Status = Completed

## Other content on the Personal Project Manager page
- **This Week** section (below the database) — weekly goals + one checklist per day.
- Child pages: **Scoring Rules**, **PMA Operating Manual**, and **Draft Plan – w/c [date]** pages created by the Sunday task.
