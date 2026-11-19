# Walker's personal finance agent

Build one agent that answers spending questions, reconciles monthly cash flow, compares card rewards and flights, and prepares a monthly review. Start with fictional data in the chat or agent platform you already have.

**[See the complete Australia-trip conversation](demo/walker-chat.md)** or **[run the first spending demo](demo/spending.md)**.

## Architecture

~~~mermaid
flowchart TD
    W["Walker or a configured schedule"] --> O["Orchestrator"]
    O --> S["Spending"]
    O --> C["Cash Flow"]
    O --> R["Rewards and Travel"]
    O --> P["Finance Planning"]
    I["Dedicated inbox or redacted exports"] --> L["Private transaction ledger"]
    L --> S
    L --> C
    C --> P
    R --> P
    T["Offer terms and fare quotes"] --> R
~~~

Finance Planning receives a cash-flow summary or trip comparison when the request needs it. Rewards and Travel uses card aliases, offer terms, and trip details.

## Quick start

1. Create a fresh chat or agent in Muse, Dot, Duet, or another platform you can access. Copy the **Paste-ready instructions** from [Orchestrator](agents/orchestrator.md) into its instructions or first message.
2. Add the [ledger rules](shared/transaction-ledger.md) and the **Paste-ready instructions** from [Spending](agents/spending.md). If your platform cannot load files, paste those sections into the same chat.
3. Open the [spending demo](demo/spending.md), paste its first input block, and ask the question in the transcript. Check for **$600 observed**, **two pending purchases**, and **$100 above threshold**. Change the threshold to $700 and confirm the flag clears.
4. Add the other three instruction blocks. Replay their demos one at a time, then replay the [full conversation](demo/walker-chat.md). Share only the input blocks and Walker's messages with the agent during an eval. Keep the expected replies for comparison.
5. For everyday use, keep the ledger in a Walker-owned private spreadsheet or equivalent exportable store. Apply reviewed rows and checklist changes there if the platform cannot persist them reliably.

| Instructions | Standalone chat demos |
|---|---|
| [Orchestrator](agents/orchestrator.md) | [Routing and partial results](demo/orchestrator.md) |
| [Spending](agents/spending.md) | [Digest, threshold, and missing feed](demo/spending.md) |
| [Cash Flow](agents/cash-flow.md) | [Monthly close and balance exception](demo/cash-flow.md) |
| [Rewards and Travel](agents/rewards-and-travel.md) | [Offers, welcome bonus, and international flights](demo/rewards-and-travel.md) |
| [Finance Planning](agents/finance-planning.md) | [Monthly review and reminder completion](demo/finance-planning.md) |

## From demo to personal use

- **Session 1 · 30 minutes.** Walker installs the orchestrator, runs the $600 test, changes a threshold, and explains which rows were counted.
- **Session 2 · 30 minutes.** Walker creates a dedicated finance-alert inbox and checks in each issuer's own settings which purchase or offer emails can be delivered there. If an issuer requires the primary address, use narrowly filtered forwarding for eligible alerts or manually paste redacted rows. Keep security, sign-in, and verification messages out. Compare sample alerts with the issuer app, test Cash Flow with redacted exports, and replay an offer or fare example.
- **Virtual follow-up · about one month later.** Review alert coverage, statement differences, and which reminders were useful. Confirm Walker's Australian city and both time zones when choosing the 30-minute slot.

The demo uses manual inputs. Before enabling a live connector, verify that the chosen platform supports read-only access limited to the dedicated inbox. Test the reporting time zone, delivery schedule, and failure reporting with a controlled example before relying on push alerts. If a capability is unavailable, use the on-demand command with redacted inputs. Email alert coverage can vary, so treat digests as observed activity and use posted exports for the monthly close.

## Bank access and privacy

Chase describes authorized access through approved APIs in its [Digital Services Agreement](https://www.chase.com/content/dam/legal-agreements/library/en/dsa_la/versions/dsa_la.pdf) and lists email alerts in its [Account Alerts guide](https://www.chase.com/personal/mobile-online-banking/login-alerts). Amex documents [permissioned data sharing](https://www.americanexpress.com/en-us/company/open-banking/) and [email alert terms](https://online.americanexpress.com/myca/shared/summary/AccountProfile/sdo/html/interstitial_alertsterms.html). [Stripe Financial Connections](https://docs.stripe.com/financial-connections/transactions) documents transaction access for registered integrations. Compatibility with this agent platform and Walker's specific cards is unverified. Use the inbox or redacted exports for this build.

This public repo contains fictional examples. Store real transactions, balances, email content, travel confirmations, credentials, and settings outside GitHub. Walker signs in through the issuer himself, handles card activations and bookings, and makes any investment contributions himself.
