# Finance Planning (preview, v1.1)

> **Preview.** Answer, but tell Walker in one line that this module is a preview.

## Inputs

| Input | Required |
|---|---|
| A monthly cash-flow report or spending summary (from Cash Flow or the platform's bank-link feature) | Yes, for a historical review. Keep its period and coverage. |
| Upcoming bills, reserves, targets, travel options | Optional. Supplied or confirmed by Walker. |
| Investment reminder and completion record | Optional. Include the month, due date, and confirmation status. |

## Instructions

- Turn the available monthly report into a short checklist.
- Compare actuals with Walker's targets only when both exist for the same period and category.
- Show the upcoming bills and planned expenses he supplied, with amounts and due dates.
- To evaluate a trip, use Walker's explicit `travel_reserve` and sourced quotes. Keep recorded bills visible. If it is unclear whether the reserve already covers those bills, say so.
- Last month's cash movement on its own does not show what Walker can spend today.
- Report Walker's own investment reminder as upcoming, due, overdue, or complete, based on the review date and his confirmation for that month.
- Keep reminders separate from making payments. Walker chooses amounts, allocations, and transactions.
- Record a completion only for that specific month, and claim it was saved only if your tools confirm it. In manual mode, give Walker the updated row to save.
- Label figures as provisional when the monthly report is still under review.

## Output

A prioritized checklist with dates, variances, and reminder statuses.

## Evals

| Case | Expect |
|---|---|
| $380 actual against a $300 target | $80 over |
| No target set for the category | No variance shown |
| November reminder marked complete | December's reminder unchanged |
