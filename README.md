# Walker's personal finance agent

A proof of concept to review with Walker. One chat brings together spending, cash flow, rewards and travel, and monthly planning. The demo uses fictional data and scripted replies.

**[Open the interactive prototype](https://zerowing113.github.io/walker-personal-agent/)**

## Architecture

Walker uses one chat. The orchestrator chooses the modules for each request and combines their results into one reply. A configured schedule can also start a run.

~~~mermaid
flowchart TD
    W["Walker or a scheduled run"] --> O["Orchestrator"]
    O --> S["Spending"]
    O --> C["Cash Flow"]
    O --> R["Rewards &amp; Travel"]
    O --> P["Finance Planning"]
~~~

| Proposed module | Reads | Returns | Scenario notes |
|---|---|---|---|
| [Spending](agents/spending.md) | Purchase alerts and posted records from the [private ledger](shared/transaction-ledger.md) | Observed spending, pending purchases, and threshold flags | [Daily digest](demo/spending.md) |
| [Cash Flow](agents/cash-flow.md) | Posted transactions and balances from the private ledger | Monthly inflows, outflows, and balance reconciliation | [Monthly close](demo/cash-flow.md) |
| [Rewards & Travel](agents/rewards-and-travel.md) | Card offer terms, trip preferences, and fare quotes | Offer deadlines and flight options in cash or points | [Offers and flights](demo/rewards-and-travel.md) |
| [Finance Planning](agents/finance-planning.md) | Walker's goals and bills, plus cash-flow or trip summaries when needed | A monthly checklist and reminders | [Monthly review](demo/finance-planning.md) |

**Example.** Walker asks, ΓÇ£Can I afford this flight?ΓÇ¥ Rewards & Travel finds the fare, Finance Planning compares it with the money Walker set aside, and the orchestrator replies with both the price and the remaining travel budget. [See the full trip walkthrough.](demo/walker-chat.md)
