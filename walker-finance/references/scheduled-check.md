# Scheduled check (v1)

This is what runs when a scheduler starts the skill without Walker asking, for example every few hours or as part of a morning brief. The goal is **few, useful pings**. If Walker starts ignoring them, the agent has failed.

## Steps

1. Run the [Spending](spending.md) import for every card since its last ledger row.
2. Evaluate the ping rules below against the ledger and Config.
3. If no rule fires, send nothing. A silent run is a successful run.
4. If one or more rules fire, send **one** message that combines them.
5. Record the run time in Config (`last_check_at`) if the spreadsheet capability allows it.

## Ping rules

| Rule | Fires when | Message |
|---|---|---|
| **Threshold crossed** | Today's observed gross purchases first go above `daily_threshold` | "$612 spent today, above your $500 threshold. Biggest purchase: $350 at Sample Hotel." |
| **Large purchase** | A single new purchase is at or above `large_purchase_amount` | "$900 at Sample Store on Chase, pending." |
| **Card gone quiet** | A card in Config has had no alerts for more than `silence_days` | "No Amex alerts for 3 days. Check that Amex alerts are still on." |
| **Review waiting** | The Review tab has gained new rows since the last ping | "2 transactions need your review." |

- Fire each rule **at most once per day per card** (threshold: once per day in total).
- Respect `quiet_hours` from Config. Hold pings until quiet hours end.
- If the platform sends a daily brief (for example a morning summary), put **one spending line** in the brief instead of sending a separate ping. Rules still fire normally for urgent items (large purchase, threshold).

## Never in a scheduled run

- Do not ask Walker questions. Note what is missing and carry on.
- Do not run preview modules unless Walker turned them on in Config.
- Do not send transaction details anywhere except to Walker.
