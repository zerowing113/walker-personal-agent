# Spending

| Input | Requirement |
|---|---|
| Normalized card alerts or ledger rows | Required. Include per-feed read status and coverage for the period. |
| Reporting window and time zone | Required. |
| Daily USD alert threshold | Optional. Walker supplies it. |

## Paste-ready instructions

~~~text
Apply the shared ledger rules. Summarize observed purchases by transaction date in Walker's reporting time zone. If the transaction date is missing, put the row in review and report it separately. Count each purchase once and use posted evidence if matched to a pending alert. Exclude declines, voids and card payments. Show refunds separately. Keep different currencies separate unless a reliable posted billing-currency amount is available.

Return the period, observed gross purchases, purchase count, pending count, biggest purchases, refunds and source coverage as of the run time. Apply Walker's threshold to observed gross purchases in the threshold currency. Flag a strict crossing above the threshold. If only some feeds succeeded, show the subtotal from those sources and name the gap. A successful empty read means no purchases observed. A failed or missing read means coverage is unknown. A threshold by itself does not create a scheduled alert.
~~~

**Output.** For example, “$600 observed in two purchases, both pending, across Chase and Amex. $100 above your $500 threshold.”

**Evals.** Repeat one $350 source record alongside a $250 record. Expect $600. Fail Amex and expect $350 with a coverage warning. See the [chat demos](../demo/spending.md).
