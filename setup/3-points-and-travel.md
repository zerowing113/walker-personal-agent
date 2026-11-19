# ③ Points and travel

**Time:** about 20 minutes · **Needs:** [① Agent foundation](1-agent-foundation.md) · **You'll end with:** alerts for card offers and bonus deadlines worth acting on, and an agent that finds and compares international flights, by cash or by points.

---

## What this does and why

Think of it as a personal version of a deal-alert app like Rocket Points, working from your own cards and your own trips.

| Workflow | Answers | Runs | Data |
|---|---|---|---|
| **A · Card offers and bonuses** | "Which offers should I activate? Am I on track for my bonus?" | Weekly, plus when offer emails arrive | Offer emails, a monthly screenshot, web search |
| **B · Flight deals** | "What's the best way to get to Sydney in February?" | On demand, plus a weekly watch on saved routes | Web search and fare sites |

> [!NOTE]
> **Why screenshots?** Chase Offers and Amex Offers sit behind your login, and agents can't sign in. A 2-minute monthly screenshot of each offers page gives the agent the full list. Amex has said it plans to bring Offers search and enrollment into select AI platforms. If that reaches your agent, skip the screenshot.

---

## Set it up

### Step 1 · Add settings

| setting | value (example) |
|---|---|
| `points_programs` | Chase Ultimate Rewards, Amex Membership Rewards |
| `planned_purchases` | groceries 400/mo, flights to Australia |
| `bonus_tracker` | Amex: spend 3000 by 2026-12-10 |
| `home_airport` | SFO |
| `watched_routes` | SFO-SYD, Feb 2027, economy, 1 traveler |
| `travel_budget` | 1500 |

### Step 2 · Optional: add a deal newsletter

Subscribe the **agent inbox** to one flight-deal newsletter you trust, so the agent sees deals as they're announced.

### Step 3 · Paste the two instruction blocks

**A · Card offers and bonuses**

```text
CARD OFFERS AND BONUSES
Sources: offer emails in the agent inbox, offer-page screenshots Walker drops in, and public web info about card and transfer promotions.
1. Keep a list of active offers: card, merchant, benefit, cap, minimum spend, expiry, activated (yes / no / unknown).
2. Rank offers by expected value on Walker's planned_purchases. Show the dollar value, not just the percentage. Leave expired offers out.
3. For each bonus in bonus_tracker, show spend so far (from Ledger rows for that card), what's left, the deadline, and the spending per week needed to hit it.
4. Never count a credit as earned unless it's activated and the purchase qualifies. Show "possible" value separately.
5. Walker activates offers himself. Tell him exactly which ones, on which card.
Alerts: ping when a high-value offer (worth $20 or more on planned purchases) expires within 5 days and isn't activated, or when a bonus deadline is 14 days away and he's behind pace.
```

**B · Flight deals**

```text
FLIGHT DEALS
When Walker asks about a trip, or on the weekly watch for watched_routes:
1. Search public fare sources for the route, dates (± flexibility), cabin and travelers.
2. Return the top 3 options. For each: airline, dates, stops, total cash price including taxes, or points plus taxes and fees, and which of Walker's points programs could cover it (including transfer partners).
3. For points options, show cents-per-point value = (cash price - taxes and fees) / points. Flag anything above 1.5 cents as a good use of points.
4. Show when each price was checked and the source. Say clearly that prices and award seats change, and that he should confirm before booking.
5. Compare the options with travel_budget.
6. Never book. Give Walker the exact flight details to book himself.
Alerts (weekly watch): ping only if a watched route drops at least 15% below the last price you recorded, or a points option above 1.5 cents per point appears. Record each check in the Ledger note column so you can compare next week.
```

### Step 4 · Schedule the checks

| Check | When | Prompt to schedule |
|---|---|---|
| Offers and bonuses | Mondays | `Run the card offers and bonuses check. Only message me if an alert rule fires.` |
| Flight watch | Thursdays | `Run the weekly flight watch for my watched routes.` |
| Screenshot nudge | 1st of each month | `Remind me to drop in screenshots of my Chase and Amex offers pages.` |

---

## Test it

- [ ] **Offer value:** "10% back, $20 cap" on $150 of planned groceries shows **$15**, not $20.
- [ ] **No false credit:** an un-activated $50 airline offer doesn't reduce a $620 fare. The fare stays $620, with $50 shown as "possible".
- [ ] **Points math:** 45,000 points plus $85 in taxes, against a $620 cash fare, shows about **1.19 cents per point**, so the cash fare is the better deal.
- [ ] **Boundary:** *"Book the cheapest one."* It gives you the details to book yourself.

## Make it yours

- Change the ping thresholds (15% drop, 1.5 cents per point, $20 offer value) in the instruction text.
- Add routes to `watched_routes` as trips come up.
- Before the Australia trip, ask: *"Plan the cheapest way to pay for SFO-SYD in February using my cards and points."*

**Back to:** [README](../README.md)
