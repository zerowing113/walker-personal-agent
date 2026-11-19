# Walker's personal finance assistant

**Goal.** Give Walker one place to answer everyday money questions, review the month, and compare travel options.

Today those decisions can involve checking several places for card activity, statements, points, and travel prices. This prototype tests which of those decisions would be easier in one chat. It uses scripted replies and fictional data.

**[Open the interactive prototype](https://zerowing113.github.io/walker-personal-agent/)**

## Problems and proposed solutions

| When Walker wants to… | The problem | What the assistant would do |
|---|---|---|
| Know what he spent today | Card alerts are spread across issuers. A missing feed makes the total incomplete. | **Spending** combines observed purchases, removes duplicates, and shows pending charges, threshold flags, and missing coverage. |
| Understand where last month’s money went | Card purchases, card payments, and transfers can make spending and cash movement hard to reconcile. | **Cash Flow** shows money in and out, reports purchases separately, and flags any difference from the statement balance. |
| Decide how to pay for a trip | Cash fares, points, fees, and card offers are hard to compare on the same basis. | **Rewards & Travel** compares cash and points options, shows fees and when quotes were checked, and flags credits that still need confirmation. |
| Know what to do next | Monthly figures, upcoming bills, and reminders sit apart from the decisions they inform. | **Finance Planning** turns the monthly review into a checklist with upcoming bills, spending variances, and reminders Walker sets. |

## What to decide before building

Start with **Australia trip** to see the workflows together. Then open the scenarios you’d actually use. Step through the replies and try a **what-if** control where available.

1. **Scope.** Which workflows belong together? What would you add or drop?
2. **Behavior.** Which reply would you change? Where should the assistant ask, flag uncertainty, or leave the decision to you?
3. **First build.** Which workflow would you use first, and when?

Use [Your feedback](https://zerowing113.github.io/walker-personal-agent/#feedback) in the demo to copy your answers into a message to Huy. The review will shape what gets built first.

## Architecture

The orchestrator receives a question, calls the relevant modules, and returns one reply. For “Can I afford this flight?”, Rewards & Travel finds the fare and Finance Planning compares it with the money Walker set aside.

~~~mermaid
flowchart TD
    W["Walker's question"] --> O["Orchestrator"]
    O --> S["Spending"]
    O --> C["Cash Flow"]
    O --> R["Rewards and Travel"]
    O --> P["Finance Planning"]
~~~

[Module notes](agents/) · [Scenario notes](demo/) · [Shared ledger proposal](shared/transaction-ledger.md)
