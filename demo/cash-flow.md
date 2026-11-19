# Cash Flow chat demos

Load [Cash Flow](../agents/cash-flow.md) and the [ledger rules](../shared/transaction-ledger.md). All data are fictional. Paste the input block and Walker's messages.

~~~text
Period: October 2026. Currency: USD. Cash scope: Checking only.
Opening checking: 2000. Reported closing checking: 3600.
Checking export: all below posted in October.
10-01, payroll, +4200, income
10-03, rent, -1400, housing expense
10-18, card payment, -900, card payment
10-20, transfer to investment account, -300, boundary transfer
Card exports: all below posted in October; dates are transaction dates.
10-08, Chase, dining, 240, purchase
10-22, Amex, dining, 140, purchase
10-22, Chase, travel, 500, purchase
~~~

**Walker:** Close October. Where did my cash go, and which day had the most spending?

**Agent:** Checking increased $1,600. You received $4,200 and paid out $2,600, including $1,400 for rent, a $900 card payment and a $300 investment transfer. The computed $3,600 close matches your export. Across the supplied cash and card records, October 3 was the largest spending day at $1,400 for rent. October 22 was the largest card-only spending day at $640. Dining totaled $380.

**Walker:** The closing balance should be $3,575. Why doesn't it match?

**Agent:** The corrected balance is $25 below the $3,600 computed close. October remains provisional. Check for an omitted withdrawal, a date boundary issue, or an opening balance correction. The current rows do not identify which occurred.

**Pass checks.** The difference is −$25 after the correction. The card payment is a checking outflow and contributes zero to purchase spending. The investment transfer is shown as a boundary transfer.
