# Ledger rules

The ledger is a spreadsheet Walker owns, such as Google Sheets, Excel, or a CSV file. It has three tabs:

| Tab | Who writes | Purpose |
|---|---|---|
| **Ledger** | Agent (append only) | One row per source record. The single source of truth for totals. |
| **Review** | Agent adds, Walker resolves | Rows the agent is not sure about. They are excluded from totals until Walker resolves them. |
| **Config** | Walker | His cards, threshold, and ping settings. See [config.md](config.md). |

A blank template is in [../assets/ledger-template.csv](../assets/ledger-template.csv).

## Columns

| Column | Rule |
|---|---|
| `source` and `source_key` | `source` is the feed the row came from (for example `chase-alert-email`, `amex-statement-csv`). `source_key` is a stable ID from that feed, or a stable key built from the imported row. Together they must be unique. |
| `account` | Alias from Config, such as Chase, Amex, or Checking. Never a card or account number. |
| `row_type` | `purchase`, `refund`, `card_payment`, `transfer`, `income`, `fee`, or `unknown`. |
| `amount` and `currency` | Exact decimals. Cash deposits are positive and withdrawals negative. Card purchases and refunds are stored as positive magnitudes, and `row_type` sets the direction. |
| `transaction_date`, `posting_date`, `observed_at` | Keep each one when available. Leave a value blank if it is unknown. Never guess. |
| `status` | `pending` or `posted`. |
| `merchant` | As shown by the source. |
| `linked_key` | The `source_key` of the matching alert or posting, if any. |
| `review_state` | `ok`, `in_review`, or `corrected`. |
| `correction` | Walker's approved fix, written as a note. The original values stay unchanged. |

## Rules

1. **Import each source key once.** Before appending, check whether `source` + `source_key` already exists. Keep separate keys when the evidence shows two different purchases, even if the merchant, date, and amount match.
2. **Match alerts to postings.** Link a pending alert to its posting when there is an explicit reference, or a clear one-to-one match within the same account and currency. Keep both rows, and report using the posted row. If more than one match is plausible, send the rows to Review and report the unresolved amount separately.
3. **Use the right date for each view.** The cash statement uses posted cash rows. The spending view uses transaction dates. Pending alerts appear only in the daily view. Refunds are stored as their own rows.
4. **Separate transfers from spending.** Identify transfers between included cash accounts using both sides where available. Treat transfers across the scope boundary separately from consumption. A checking-to-card payment counts as a checking outflow, while the underlying card purchase counts in spending.
5. **Report coverage.** Every answer says which sources and dates were checked, and marks missing coverage. Re-running an import must leave totals unchanged.
6. **Never delete.** Corrections go in `correction`, and `review_state` becomes `corrected`.
