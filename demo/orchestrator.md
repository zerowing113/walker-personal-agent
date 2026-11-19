# Orchestrator chat demos

Load the [Orchestrator](../agents/orchestrator.md), Spending, Rewards and Travel, and the ledger rules. Paste the first input block from [Spending](spending.md) and the fictional offer and date block from [Rewards and Travel](rewards-and-travel.md).

**Walker:** What did I spend yesterday, and which offers expire in the next seven days?

**Agent:** I observed $600 on November 14 across Chase and Amex, both purchases pending. In the next seven days, the Chase grocery offer expires November 20 and the Amex airline offer expires November 21. The airline offer still needs activation and eligibility confirmation.

**Variation.** Start fresh. Provide the Spending inputs and state that both offer feeds failed. Ask the same question.

**Agent:** I observed $600 in purchases on November 14 across Chase and Amex. The offer feeds were unavailable, so I can't verify which offers expire this week.

**Pass checks.** One answer, two workflows, no fabricated empty result for offers. The orchestrator does not send transaction records into the offer lookup.
