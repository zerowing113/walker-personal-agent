# Full chat demo · Planning an Australia trip

All inputs and quotes are fictional. Load the [Orchestrator](../agents/orchestrator.md), the four module instructions, and the [ledger rules](../shared/transaction-ledger.md). To replay, paste the input blocks from [Spending](spending.md), [Cash Flow](cash-flow.md), [Rewards and Travel](rewards-and-travel.md), and [Finance Planning](finance-planning.md) into the same chat. Use the original $3,600 reported closing balance. Then send the Walker messages in order.

## 1. Check spending

**Walker:** What did I spend yesterday?

**Agent:** I observed $600 on November 14 across Chase and Amex. There were two pending purchases, $350 for the hotel and $250 for the airline. That's $100 over your $500 threshold.

*Handoff.* The ledger collapses the repeated Chase alert before Spending adds the amounts.

## 2. Review last month

**Walker:** How did October end? Do I have room for another travel expense?

**Agent:** Checking increased $1,600, from $2,000 to $3,600. Inflows were $4,200 and outflows were $2,600. That matches the statement. For this trip, you've entered a separate $650 travel reserve, and your $65 internet bill is due November 18.

*Handoff.* Cash Flow supplies the reconciled summary. Finance Planning uses Walker's travel reserve for the trip decision.

## 3. Compare flights and rewards

**Walker:** Compare the Sydney flights and tell me whether either of my cards helps.

**Agent:** For February 4 in economy, the sample options are $620 cash from Sample Airlines, checked at 6:45 p.m. PT, or 45,000 Sample Miles plus $85 in fees from Sample Miles, checked at 6:50 p.m. PT. The cash option leaves $30. The award option leaves $565 and uses 45,000 points. Your Amex offer could return $50 if activated and the fare is eligible. Budget the full $620 until you confirm both.

*Handoff.* Rewards and Travel receives the trip details, reserve and relevant offer terms.

## 4. Make a monthly checklist

**Walker:** Give me this month's checklist and include my investment reminder.

**Agent:**
- **Trip.** Choose the cash or award fare. If you choose cash, verify the Amex offer before paying.
- **Spending.** Review October dining. You spent $380 against a $300 target.
- **Upcoming bill.** Internet, $65 on November 18.
- **Investment reminder.** Review your planned contribution. Due November 15.

**Walker:** I made the contribution.

**Agent:** Save November's investment reminder as complete. Trip, dining and internet are still open. The December 15 reminder is still upcoming.

*Handoff.* Finance Planning combines the summaries and produces a proposed checklist update for Walker to save.

## Pass checks

- The repeated alert leaves observed spending at $600.
- October's +$1,600 cash change reconciles, with one $900 card payment in cash movement.
- Fare comparison preserves both the 45,000 points and the $85 fees. The cash option remains $620.
- The monthly review flags dining $80 over target. November's reminder is complete only after Walker confirms. December remains upcoming.
