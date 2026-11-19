# ② Money in and out

**Time:** about 20 minutes · **Needs:** [① Agent foundation](1-agent-foundation.md) · **You'll end with:** daily spending alerts, a monthly personal cash flow statement, and a monthly ETF transfer reminder.

---

## What this does and why

This file adds three **specialist agents** to your orchestrator. Each instruction block below is one specialist.

| Workflow | Answers | Runs | Data |
|---|---|---|---|
| **Spending** | "What did I spend today?" | Every few hours, plus whenever you ask | Card alerts in the agent inbox |
| **Cash flow** | "Where did last month's money go?" | Monthly, when you drop in statements | Statement exports you download |
| **Investing** | "How much goes into each ETF this month?" | Monthly | Your Settings tab |

**Why two data sources?** Card alerts arrive within minutes, but they only cover card purchases. Statements arrive monthly, but they're complete: income, rent, card payments, and the Schwab transfer. The agent uses alerts for *today* and statements for *the month*.

> [!NOTE]
> **Privacy choice.** Some agents can link your bank accounts directly (read-only, through Plaid). That's faster, but it hands your full account history to the platform. The default here is **statement exports**, about 10 minutes a month, so you control exactly what the agent sees. You can switch later.

---

## Set it up

### Step 1 · Add settings

Add these rows to the **Settings** tab of `Agent Memory`:

| setting | value (example) |
|---|---|
| `monthly_investment_amount` | 2000 |
| `investment_day` | 1 |
| `etf_list` | ETF_1, ETF_2, ETF_3, ETF_4 |
| `etf_target_weights` | 40, 30, 20, 10 |
| `budget_dining` | 300 |

Replace the placeholders with your actual approved ETFs and target weights. Keep these in your private sheet, not in this repo.

### Step 2 · Paste the three instruction blocks

Add them below the foundation instructions.

**Specialist: Spending**

```text
SPENDING
When Walker asks what he spent, or on a scheduled check:
1. Read new card-alert emails in the agent inbox since the last Ledger row for each card.
2. Add one Ledger row per purchase (date, card, merchant, amount, status = pending, source_id = the email's ID). If a source_id already exists, skip it. That's how duplicates are avoided.
3. If two alerts look like the same purchase but have different IDs, add both to Review instead of guessing.
4. Total purchases by date in Walker's time zone. Show refunds separately. Ignore card payments and declined transactions.
5. Coverage: name each card checked. If a card's alerts couldn't be read, say its spending is UNKNOWN. Never treat a failed card as $0.
Alerts: ping once when today's total first goes above daily_spend_alert, and once for any single purchase at or above large_purchase_alert. If a card has had no alerts for 3 days, ping: "No [card] alerts in 3 days. Check that alerts are still on."
```

**Specialist: Cash flow**

```text
CASH FLOW (monthly statement)
When Walker drops in statement exports (CSV or PDF) and asks to close a month:
1. List which statements you received, and name any expected account that's missing.
2. Build Walker's personal statement of cash flows for the month:
   - Money in: salary, other income, refunds.
   - Money out, grouped: housing, card spending by category, transfers to investments, other.
   - Net cash flow = money in minus money out.
   - Opening balance + net cash flow = computed closing balance. Compare it with the statement's closing balance and show any difference.
3. Count card spending once. A card payment from checking is a transfer, not new spending.
4. Show the 3 highest-spending days, and any category over its budget_ setting.
5. Compare with the Ledger's daily totals for the month and flag any purchase that appears in one but not the other.
Mark the statement PROVISIONAL if a statement is missing or a difference remains.
```

**Specialist: Investing**

```text
INVESTING (ETF transfer reminder)
On investment_day each month, or when Walker asks:
1. Split monthly_investment_amount across etf_list using etf_target_weights. Show a table: ETF, weight, dollar amount. Round to whole dollars, and make sure the amounts add up to the total.
2. Remind Walker to place the transfer and orders himself at his brokerage. You cannot and must not do it.
3. Ask him to reply "done" when he has. Record "investment done [month]" in the Ledger note column. If it isn't done 3 days later, remind him once.
Never suggest changing the ETFs, the weights, or adding anything outside etf_list. If Walker asks about changing them, remind him to check his own compliance rules first.
```

### Step 3 · Schedule the checks

| Check | When | Prompt to schedule |
|---|---|---|
| Spending | Every 4 hours | `Run the daily spending check. Only message me if an alert rule fires.` |
| ETF reminder | Monthly, on your investment day | `Run the ETF transfer reminder.` |
| Statement nudge | 3rd of each month | `Remind me to download last month's statements and drop them here.` |

### Step 4 · Your monthly 10-minute routine

1. Download last month's statements: Chase (CSV), Amex (CSV), and checking (CSV or PDF).
2. Drop them into the agent chat and say: **"Close last month."**
3. Read the statement, then resolve anything in the Review tab.

---

## Test it

- [ ] **Duplicates:** forward the same alert email twice. *"What did I spend today?"* counts it once.
- [ ] **Missing card:** pause one card's alerts for a day. The answer says that card is unknown, not $0.
- [ ] **Math:** with a $2,000 opening balance, $4,200 in and $2,600 out, the statement shows a $3,600 computed closing balance.
- [ ] **ETF split:** $2,000 at 40/30/20/10 gives $800, $600, $400, $200.
- [ ] **Boundary:** *"Just buy the ETFs for me."* It refuses and gives you the steps.

## Make it yours

- Change the alert amounts in Settings. The agent reads them fresh every time.
- Add budgets for other categories (`budget_travel`, `budget_groceries`).
- Too many pings? Raise `large_purchase_alert` first.

**Next:** [③ Points and travel →](3-points-and-travel.md)
