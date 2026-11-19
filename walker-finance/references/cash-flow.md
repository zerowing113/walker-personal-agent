# Cash Flow (fallback)

> **When to use this.** If Walker has a read-only bank-link feature on his platform (`bank_link_available = yes` in Config), suggest that first for "where did my money go last month?", because it already reads his linked accounts. Use this module when he provides statement exports, wants a reconciliation against a statement balance, or has no bank link.

## Inputs

| Input | Required |
|---|---|
| Month, reporting currency, and the cash accounts in scope | Yes |
| Posted cash-account exports and opening/closing balance snapshots | Yes, to reconcile each selected cash account |
| Posted card exports, with categories where known | Yes, for the spending view. Report any missing cards. |

## Instructions

Apply the [ledger rules](ledger-rules.md). Produce two views for the requested month.

**Cash movement** uses posted dates and signed amounts from the selected cash accounts.
- Show the opening balance, all inflows, all outflows, the net change, the computed closing balance, and the reported closing balance.
- Count a card payment here when it leaves an included cash account.
- Exclude both sides of transfers that stay inside the scope from total inflows and outflows. Show transfers between included and excluded accounts as boundary transfers. Send ambiguous transfers to Review.
- Reconcile each selected cash account and the total. The difference is the reported closing balance minus the computed closing balance.
- Mark the result **provisional** if a cash export or balance is missing, a relevant classification is unresolved, or a difference remains.

**Spending** uses posted purchase rows grouped by transaction date where available.
- Show refunds separately, and label net spend as net.
- Include direct cash or bank spending where the posted rows support it.
- Exclude card payments and investment transfers.
- Group by category and report the days with the highest gross spending.
- Disclose missing dates, uncategorized rows, currencies, and coverage gaps.
- Keep the reconciliation status and the spending coverage separate.

## Output

Monthly cash and spending tables, the account scope, the reconciliation difference, and named exceptions.

## Evals

| Case | Expect |
|---|---|
| $2,000 opening + $4,200 in − $2,600 out | $3,600 computed closing |
| Reported closing balance of $3,575 | Difference of **−$25**, marked provisional |
