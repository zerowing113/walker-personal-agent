# Spending (v1)

Answers "what did I spend?" from card-alert emails and the ledger. Card alerts are the fastest signal Walker gets, because they arrive minutes after a purchase, long before the statement does.

## Inputs

| Input | Source | Required |
|---|---|---|
| Card-alert emails for the period | Email reader, filtered by the alert senders in Config | Yes, or pasted alerts in manual mode |
| Read status per card | Your own record of whether each card's read worked | Yes |
| Ledger rows for the period | Ledger tab | Yes, if the spreadsheet capability exists |
| Reporting time zone, daily threshold, currency | Config | Time zone required. Threshold optional |

## Steps

1. For each card in Config, search for alert emails from its sender since the last ledger row for that card (or for the requested period). Record whether each card's search **succeeded**, **succeeded with nothing found**, or **failed**.
2. Parse each alert into a ledger row (`status = pending`). Use the email's message ID as `source_key`. Apply the [ledger rules](ledger-rules.md) to dedupe, match, and append.
3. Summarize purchases by transaction date in Walker's time zone. If a row has no transaction date, put it in Review and report it separately.
4. Count each purchase once. Use the posted row when an alert has been matched to a posting. Exclude declines, voids, and card payments. Show refunds separately.
5. Keep currencies separate unless a reliable posted billing-currency amount exists.

## Output

Return the period, observed gross purchases, purchase count, pending count, the biggest purchases, refunds, and coverage as of the run time.

Apply Walker's threshold to observed gross purchases in the threshold currency. Flag only a strict crossing above it.

> **Example.** "$600 observed in two purchases on Nov 14, both pending, across Chase and Amex. That's $100 above your $500 threshold."

## Coverage language

| Situation | Say |
|---|---|
| All cards read, purchases found | The total, plus "Chase and Amex checked" |
| All cards read, nothing found | "No purchases observed" |
| Some cards failed | The subtotal from the cards that worked, plus "Amex couldn't be read, so its spending is unknown." Do not imply that the combined total stayed under the threshold. |
| A card has had no alerts for longer than its silence limit | "No Chase alerts in 3 days. Check that alerts are still on." |

A threshold on its own does not create a scheduled alert. Pings come from [scheduled-check.md](scheduled-check.md).

## Evals

| Case | Expect |
|---|---|
| One $350 Chase alert received twice, plus a $250 Amex alert | $600 (the duplicate collapsed) |
| Amex read fails | $350, Chase only, with a coverage warning |
| Both reads succeed with zero alerts | "No purchases observed", not "unknown" |
| Two distinct $350 purchases at the same hotel on the same day, with different message IDs | $700. Both kept. |
