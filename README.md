# Walker's personal finance assistant

**Goal.** Give Walker one place to answer everyday money questions, review the month, and compare travel options.

Today those decisions can involve checking several places for card activity, statements, points, and travel prices. This prototype tests which of those decisions would be easier in one chat. It uses scripted replies and fictional data.

**[Open the interactive prototype](https://zerowing113.github.io/walker-personal-agent/)**

## Architecture

Walker sends a message from the chat. A backend orchestrator asks a language model (LLM) to interpret it and select a module. The backend validates and runs the module’s tool calls. The tools read the relevant data and use code for calculations such as deduplication, totals, and balance checks. The LLM turns the results into a reply, and the chat displays it.

~~~mermaid
flowchart TD
    F["Front end · chat"] <-->|Question and reply| O["Backend · orchestrator"]
    O <-->|Intent and wording| L["LLM"]
    O <-->|Tool calls and results| T["Spending · Cash Flow · Rewards and Travel · Finance Planning"]
    T <-->|Read and calculate| D["Ledger · statements · offers · fare quotes · planning settings"]
~~~

The [interactive prototype](https://zerowing113.github.io/walker-personal-agent/) simulates this flow with fictional data. Open **Sample requests and results** beside a reply to see what the planned backend would pass between components.

[Module notes](agents/) · [Scenario notes](demo/) · [Shared ledger proposal](shared/transaction-ledger.md)

## Problems and proposed solutions

| When Walker wants to… | The problem | What the assistant would do |
|---|---|---|
| Know what he spent today | Card alerts are spread across issuers. A missing feed makes the total incomplete. | **Spending** combines observed purchases, removes duplicates, and shows pending charges, threshold flags, and missing coverage. |
| Understand where last month’s money went | Card purchases, card payments, and transfers can make spending and cash movement hard to reconcile. | **Cash Flow** shows money in and out, reports purchases separately, and flags any difference from the statement balance. |
| Decide how to pay for a trip | Cash fares, points, fees, and card offers are hard to compare on the same basis. | **Rewards & Travel** compares cash and points options, shows fees and when quotes were checked, and flags credits that still need confirmation. |
| Know what to do next | Monthly figures, upcoming bills, and reminders sit apart from the decisions they inform. | **Finance Planning** turns the monthly review into a checklist with upcoming bills, spending variances, and reminders Walker sets. |
