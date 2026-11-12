# Scoring Rules

Mirror of the Notion page "Scoring Rules". The agent reads this to calculate Priority Score itself, because the Notion connector cannot read formula results. The formula in `notion/priority-score.formula` uses exactly these rules — change both together.

## Formula

`Priority Score = round((Urgency × 0.30 + Importance × 0.25 + Strategic Value × 0.20 + Progress Risk × 0.15 + Neglect × 0.10) × 20)`

Range 20–100. Completed projects score 0.

## Component scores (1–5)

| Component | Weight | 5 | 4 | 3 | 2 | 1 |
|---|---|---|---|---|---|---|
| Deadline urgency (days to deadline) | 30% | ≤ 3 or overdue | 4–7 | 8–14 | 15–30 | > 30 or none |
| Importance | 25% | Critical | High | Medium | Low | Empty |
| Strategic value | 20% | Critical | High | Medium | Low | Empty |
| Progress risk | 15% | < 25% or empty | 25–49% | 50–74% | 75–89% | ≥ 90% |
| Neglect (days since Last Worked On) | 10% | > 14 or never | 8–14 | 4–7 | 2–3 | 0–1 |

## Rules for the agent
- Always calculate from the raw properties using today's date. Never guess a score.
- When explaining a ranking, name the components that drove it.
- The score ranks projects; it does not make decisions. Calendar availability can override it on a given day.
