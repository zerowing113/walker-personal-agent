# PRD · Walker's personal finance assistant

| | |
|---|---|
| **Owner** | Huy (builder) · Walker (user and approver) |
| **Status** | v1 draft for Walker's review |
| **Last updated** | November 2026 |

> [!TIP]
> **The one-minute version.** An assistant that watches Walker's card-alert emails, keeps one de-duplicated ledger in a spreadsheet he owns, answers "what did I spend?" with honest coverage, and pings him only when something matters. It runs on any assistant that supports the open skills format, and Claude is the primary platform.

---

## 1. Problem

Walker's card activity is spread across issuers. Each card sends its own alerts, has its own app and its own statement date. A simple question like *"what did I spend yesterday?"* takes several apps to answer, and the answer is still wrong in two quiet ways:

- **Double counting.** The same purchase shows up as an alert, then as a pending charge, then as a posting.
- **Silent gaps.** If one card stops sending alerts, its total looks like $0 instead of *unknown*.

## 2. Who it's for and what he needs

| When Walker wants to… | He needs | v1? |
|---|---|---|
| Check what he spent today or yesterday | One total across cards, each purchase counted once, with a note on anything missing | ✅ |
| Know when something needs attention | A ping when it matters, and silence the rest of the time | ✅ |
| Trust the numbers | A ledger he owns and can open, where nothing is ever silently deleted | ✅ |
| See where last month's money went | Cash in and out, reconciled to the statement | Native bank-link feature, with the skill as fallback |
| Decide how to pay for a trip | Cash versus points, fees, and offers compared on the same basis | v1.1 (preview) |
| Know what to do this month | A checklist of bills, variances, and reminders | v1.1 (preview) |

## 3. Goals and non-goals

**Goals**
1. Give an accurate daily spending answer across all of Walker's cards, with coverage stated every time.
2. Send proactive pings that Walker doesn't mute.
3. Keep Walker's data in a spreadsheet he owns, in a format he can export.
4. Work on more than one assistant platform without rewriting the logic.

**Non-goals**
- Moving money, paying, booking, investing, or activating offers. The assistant reads and prepares only.
- Connecting directly to banks. Platforms already offer read-only bank links, so we use those instead of building one.
- A custom app, server, or database. That is a v2 question at the earliest.
- Budgeting advice or investment recommendations.

## 4. Build vs. buy

As of November 2026, the major assistants already provide much of what the original concept planned to build. The rule: **build only what no platform gives Walker.**

| Need | Buy (use the platform) | Build (this skill) |
|---|---|---|
| Linked bank and card balances, monthly cash flow, bills | ✅ Native read-only bank-link features (e.g. [Personal Finance in Claude](https://claude.com/blog/introducing-personal-finance-in-claude)) | Fallback only, from statement exports |
| Real-time spending from card alerts | | ✅ The Spending monitor |
| A ledger that dedupes alerts against postings and states coverage | | ✅ Ledger rules |
| Proactive checks and morning briefs | ✅ Platform schedulers (e.g. [Claude Duet](https://claude.com/blog/claude-duet)) | ✅ Ping rules that decide *what* is worth a message |
| Portable instructions | ✅ The open skills format ([agentskills.io](https://agentskills.io)) | ✅ The `walker-finance` skill |

**Why card alerts instead of bank links for daily spending?** Two reasons. Alerts arrive minutes after a purchase. And on Claude, the proactive agent (Duet) can read email, but Personal Finance isn't available inside it.

## 5. v1 requirements

| ID | Requirement | Priority |
|---|---|---|
| **R1** | Read card-alert emails for every card listed in Config, and record success, empty, or failure for each card. | Must |
| **R2** | Turn each alert into a ledger row with a stable source key. Re-importing must not change totals. | Must |
| **R3** | Answer spending questions for any day or week in Walker's time zone, with coverage stated. | Must |
| **R4** | Never report a failed read as $0. Partial totals name the missing card. | Must |
| **R5** | Append confident rows automatically and send uncertain rows to a Review tab. | Must |
| **R6** | Run a scheduled check that pings for a threshold crossing, a large purchase, a quiet card, or new review items. Stay silent otherwise. | Must |
| **R7** | Fall back to manual mode (pasted alerts in, proposed rows out) when the email or spreadsheet capability is missing. | Must |
| **R8** | Read every setting from Walker's private Config tab. Store no personal data in the skill or the repo. | Must |
| **R9** | Refuse payments, bookings, transfers, and offer activation, and say that Walker does these himself. | Must |
| **R10** | Respect quiet hours, send at most one combined ping per check, and fire each rule at most once a day. | Should |
| **R11** | Add one spending line to the platform's morning brief when one exists. | Could |

## 6. What the assistant may do on its own

| Action | Without asking | Asks first | Never |
|---|:---:|:---:|:---:|
| Read card-alert emails | ✅ | | |
| Read the spreadsheet | ✅ | | |
| Append a confident ledger row | ✅ | | |
| Resolve a possible duplicate | | ✅ via the Review tab | |
| Edit Config | | | ✅ (except `last_check_at`) |
| Delete or overwrite a row | | | ✅ |
| Pay, book, transfer, invest, activate an offer | | | ✅ |

## 7. Success after four weeks

| # | Metric | Target | If it misses |
|---|---|---|---|
| 1 | Posted card totals match statements | To the cent, zero double counts | Fix the ledger rules |
| 2 | Useless pings, as judged by Walker | Fewer than 2 a week | Retune the ping rules and thresholds |
| 3 | Walker stops opening issuer apps just to check spending | Yes, by his own account | Rethink the concept |

## 8. Roadmap

| Release | Scope | Gate to move on |
|---|---|---|
| **v1** | Spending monitor, ledger, scheduled check. Claude as primary platform | Metrics 1 and 2 met for 4 weeks |
| **v1.1** | Rewards & Travel and Finance Planning move from preview to supported | Walker asks for them |
| **v2** | ChatGPT and Gemini adapters tested. Possibly a coded agent with its own scheduler if platform schedulers prove too limited | A platform limit blocks a Must requirement |

## 9. Risks

| Risk | Mitigation |
|---|---|
| A card's alert email format changes, so parsing breaks | The quiet-card ping catches it within `silence_days`, and parsing failures go to Review |
| Alerts are off or partial for a card | SETUP asks Walker to turn on alerts for every purchase. Coverage is reported every time. |
| Too many pings, so Walker mutes them | Hard limits: one combined message, each rule at most once a day, quiet hours |
| Prompt injection through email content | Email is treated as data, and the skill has no ability to pay or move money |
| Platform features change, since several are betas or waitlists | Capability contract plus manual-mode fallback. Only the adapters change. |
| Walker's details leak through the public repo | The repo holds templates and fictional data only. Real config lives in his private sheet. |

## 10. Open questions for Walker

1. Which cards matter, and do they all send purchase alerts by email?
2. What daily amount should trigger a ping?
3. Is he on the Duet waitlist, and is Personal Finance showing in his sidebar yet?
4. After v1, which preview should come first: Rewards & Travel or Finance Planning?

---

**Read next:** [Architecture](architecture.md) · [Setup questionnaire](../SETUP.md) · [Claude setup](../adapters/claude.md)
