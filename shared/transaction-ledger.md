# Transaction ledger

Use a private spreadsheet or an exportable store Walker controls. Keep a source record key and a link between alert and posting records for traceability. In manual mode the agent returns proposed rows and Walker reviews and saves them.

| Field | Rule |
|---|---|
| Source and source record key | Use a stable scoped ID from the feed or a stable imported row key. Preserve provenance. |
| Account alias and row type | Examples include Chase, Amex and Checking. Mark purchase, refund, card payment, transfer, income, fee or unknown. |
| Amount and currency | Use exact decimals or integer minor units. Cash deposits are positive and withdrawals negative. Store card purchase and refund magnitudes as positive and use the row type to determine direction. |
| Dates and status | Keep transaction date, posting date, observed time and status where available. Preserve unknown values. |
| Match and review fields | Store the linked record key, confidence or review state, and any approved correction. |

1. Import each scoped source key once. Preserve separate source keys when the evidence shows two different purchases, even if merchant, date and amount match.
2. Match pending alerts to postings using an explicit reference or a clear one-to-one match within the same account and currency. Keep both source references and use the posted row for reporting. If multiple matches are plausible, keep them for review and disclose unresolved amounts separately.
3. Use posted cash rows for the cash statement. Use transaction dates for the spending view. Keep pending alerts in the daily view only. Store refunds independently.
4. Identify transfers between included cash accounts using both sides where available. Treat transfers across the scope boundary separately from consumption. A checking-to-card payment counts as a checking outflow, while the underlying card purchase counts in spending.
5. Report which sources and dates were checked and mark unavailable coverage. Repeated imports should leave totals unchanged.
