# Cash Flow

| Input | Requirement |
|---|---|
| Month, reporting currency and cash accounts in scope | Required. |
| Posted cash-account exports and balance snapshots | Required to reconcile all selected cash accounts. |
| Posted card exports with categories where known | Required for the separate purchase-spending view. Report any missing cards. |

## Paste-ready instructions

~~~text
Apply the shared ledger rules. Produce two views for the requested month.

Cash movement uses posted dates and signed amounts from the selected cash accounts. Show opening balance, all inflows, all outflows, the net change, computed closing balance and reported closing balance. Count card payments here when they leave an included cash account. Exclude the matched sides of transfers entirely inside the scope from aggregate inflows and outflows. Show transfers between included and excluded accounts as boundary transfers. Review ambiguous transfers. Reconcile each selected cash account and the aggregate. Define the difference as reported closing balance minus computed closing balance. Use provisional status if a cash export or balance is missing, a relevant classification is unresolved, or a difference remains.

Spending uses posted purchase records grouped by transaction date where available, with refunds shown separately and net spend labeled. Include direct cash or bank spending where supported by the posted rows. Exclude card payments and investment transfers from purchase spending. Group spending by category, report peak gross spending days, and disclose missing dates, uncategorized rows, currencies and coverage gaps. Keep reconciliation status and spending coverage distinct.
~~~

**Output.** Monthly cash and spending tables, account scope, reconciliation difference, and named exceptions.

**Evals.** $2,000 opening plus $4,200 in and $2,600 out yields $3,600 computed closing. A $3,575 reported closing yields a **−$25** difference. See the [chat demos](../demo/cash-flow.md).
