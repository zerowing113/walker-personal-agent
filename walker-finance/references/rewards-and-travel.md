# Rewards & Travel (preview, v1.1)

> **Preview.** Answer, but tell Walker in one line that this module is a preview and he should check the result. Offers and fares change quickly and come from sources this skill cannot verify on its own.

## Inputs

| Input | Required |
|---|---|
| Card offers or welcome bonuses: issuer terms, card alias, benefit, deadline, eligibility, activation status if known, confirmed eligible progress | For offer questions. Planned purchases are optional. |
| Flights: dates or flexibility, airports, cabin, traveler count, cash budget or points programs | For trip questions. Use sourced quotes or quotes Walker supplies. |
| `travel_reserve`, `loyalty_programs` | From Config, when relevant |

## Card offers

- Show the benefit, the required eligible spend, the cap, the card alias, the expiry, and the activation state.
- Rank offers by estimated savings on purchases Walker already plans to make, when the terms allow a comparison.
- Count a credit as applied only when eligibility and activation are confirmed. Show conditional value separately.
- Leave expired offers out of active results.
- **Welcome bonuses:** subtract only confirmed, eligible, posted spend from the requirement, flag uncertain spend, and show the deadline.

## Flights

- Return a short list within Walker's route, dates, cabin, and traveler constraints.
- For each quote, show:
  - route and dates
  - cash total, or points plus taxes and fees
  - the program where relevant
  - the source
  - the time it was checked
- Distinguish verified availability from estimates, missing fees, and stale quotes.
- Compare against `travel_reserve` when it is set, and keep points visible separately.
- Mention relevant card offers, but never reduce the fare by a credit that is not confirmed.

## Boundaries

- Never send ledger rows into a fare or offer search.
- Walker checks final eligibility and availability, activates offers, and books trips himself.

## Evals

| Case | Expect |
|---|---|
| 10% back with a $20 cap, $150 of eligible planned spend | $15 |
| Unconfirmed $50 airline credit on a $620 fare | Budget the full $620 and show the $50 as conditional |
